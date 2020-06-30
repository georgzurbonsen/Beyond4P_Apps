# IMF Example

This Beyond4P example downloads GDP growth reports from two different sources (IMF and World Bank), converts to true Excel format (.xlsx), aligns the tables, and compares the growth figures.

Written by Georg zur Bonsen, 21. Jan 2021

### Set path and settings files; start stopwatch; begin program code

```text
#!/usr/local/bin/Beyond4P

runtime settings [verbose]=quiet;  	// turn off notifications
include ( Office Library );		// include MS Office compatibility
include ( Support Library );		// include other support libraries
watch start;				// start stopwatch timing
{					// begin of program code section
echo( "This application demonstrates how to retrieve and analyze economics data from different online sources.", new line );

```


## Define Spreadsheets

Note: Variables are defined using brackets "[]", with or without subscripts
	
```text
gdp growth worldbank[] = "GDP Growth Worldbank.xlsx";	//assign spreadsheet to variable
gdp growth imf      [] = "GDP Growth IMF.xlsx";		//assign spreadsheet to variable
```

## Download GDP growth data and load into Worldbank and IMF data objects

```text

echo( "Step 1 - Download the GDP growth data from Worldbank and IMF", new line );

file download overwrite	( 
	"http://pubdocs.worldbank.org/en/872421555426273916/Global-Economic-Prospects-June-2019-GDP-growth-data.xlsx", 
	gdp growth worldbank[] );
	
file download overwrite	( 
	"https://www.imf.org/external/pubs/ft/weo/data/WEOhistorical.xlsx", 
	gdp growth imf[] );
```

## Load subset of spreadsheet files into  into Excel spreadsheets

```text
echo( "Step 2 - Load downloaded excel files" );
echo( "Note: The IMF file is a huge one (> 7 MB compressed).  Allow a few minutes.", new line );

table load excel file	( worldbank, gdp growth worldbank[], Statistical Appendix );
table load excel file	( imf      , gdp growth imf      [], ngdp_rpch );
```

## Prepare and clean Worldbank data

```text
	echo( "Step 3 - Prepare Worldbank data:", new line );
	echo( "         Lift headers, remove quarterly data, add missing header ... ");

	// Move table headers to top row (delete the above).  One header is "2016".
	table lift header row		( worldbank, "2016" );				
	
	// Header name missing
	[worldbank:0,0] 		= country;					
	
	// Delete all columns with quarterly data and blank columns (blankbehind comma)
	table delete columns 		( worldbank, [ worldbank: :'*Q*,', 0 ] );	
	
	// Delete blank row plus description row at the bottom
	table delete selected rows	( worldbank, [country] == '', 2 );		
	
	// Delete the 'e' and 'f' behind the years.
	for all table selected columns	( worldbank, ('20*'), 0, col nr[], col[] )
	{
		[ col nr[] ] = WBK Y + literal([ col nr[] ]) - e - f; // Note: Since table context (table name and row number) are known, only column needs to be specified.
	}
```

## Precondition IMF Data

```text
	echo( "Step 4 - Precondition IMF data", new line );
	echo( "Cleaning up a big an messy table! ... ");

	// Keep 1st two and the last column, forget all other.
	table keep columns 		( imf, { country, year, -1 } ); 
	
	table rename column headers	( imf, -1, GDP growth );
	table delete selected rows	( imf, [GDP growth] = '.' );

	// The years are still listed vertically.  
	// Move them across columns by doing a simple pivot. Round the numbers for clarity
	table process			( imf, [year] = IMF Y + literal([year]); [GDP growth] = round([GDP growth], 0.1 ) ); 
	table spread 			( imf, GDP growth, [year] );
	table consolidate		( imf, country, { year, GDP growth } + [ imf : '>GDP growth'.., 0 ], { delete, delete, sum } );

	table save( imf,       test imf 2.csv );	// Save intermediate files
	table save( worldbank, test wbk 2.csv );
```

## Merge and align IMF and World Bank data into single table

```text
	echo( "Step 5 - Now merge and align IMF and worldbank data into same table", new line );

	// Capitalize all headers and remove superscript numbers
	table process			( imf, 		[country] = ![country] - '1'-'2'-'3'-'4'-'5'-'6'-'7'-'8'-'9'-'0'-',' );
	table process			( worldbank, 	[country] = ![country] - '1'-'2'-'3'-'4'-'5'-'6'-'7'-'8'-'9'-'0'-',' );

	table merge extend columns	( imf, worldbank, country );
	table rename			( worldbank, combined );
	table sort rows			( combined, country );
```

## Compare IMF and World Bank GDP figures

```text
	echo( "Step 6 - Compare the IMF and Worldbank GDP figures", new line );

	years [imf]			= [ combined ::'IMF*', 0 ] -^ 'IMF ';  // Here you see how to use member (child) variables
	years [worldbank]		= [ combined ::'WBK*', 0 ] -^ 'WBK ';  // and parameter sets as contents
	years [both]			= years[imf] & years[worldbank];       // Intersection of the two sets  (logical AND)

	echo				( "Years in IMF       listing : ", years [imf]       );
	echo				( "Years in Worldbank listing : ", years [worldbank] );
	echo				( "Years in both      listings: ", years [both] );

	table insert columns		( combined, "Delta " +^ years[both] );

	for all parameters( years[both], year[] ) // Compare line by line
	{
		table process selected rows( combined,  (["IMF " + year[]] <> '') & (["WBK " + year[]] <> ''), 
							 ["Delta " + year[]] = ["IMF " + year[]] - ["WBK " + year[]] );
	}

	echo (new line, "processing took ", watch stop()/1000, " seconds."  );
	echo ("Everything completed.  Open Result.csv" );

	table save			( combined, Result.csv );

}

```
