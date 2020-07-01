# IMF Example

This Beyond4P example downloads GDP growth data reports from two different sources (IMF and World Bank), converts to Excel format (.xlsx), cleans and aligns the tables, and compares the growth figures.

Written by Georg zur Bonsen, 21. Jan 2021

### Initialization
* Set program path (Shebang statement for startinng on UNIX/LINUX/MACOS systems)
* Include two library files with functions written in Beyond4P, including ability to load Microsoft Excel files
* Start stopwatch (to do a performance measurement)
* Begin program code

The first statement (runtime settings[verbose]) is an assigment of the literal 'quiet' to the existing system variable called 'runtine settings' with tree-like member variable 'verbose'.
'watch start' is a procedure call.  No parentheses are needed if a procedure is called without parameters passed along.

You may recognize that Beyond4P allows multiple words and special symbols for variable names, function names, table names, etc. 



```text
#!/usr/local/bin/Beyond4P

runtime settings [verbose]=quiet;  	// turn off notifications
include ( Office Library );		// include MS Office compatibility
include ( Support Library );		// include other support libraries
watch start;				// start stopwatch timing
{					// begin of program code section
```


## Define Spreadsheets

The following two statements are assignments to two new variables which are created during the assignment.
Note that simple variables must be delimited with '[]', which is a bit outlandisch compared to other languages, but very beneficial
because you can also access variables indireectly.  Example: a[] = b; a[][] = 1; // The 2nd statement assigns 1 to variable b[].

In the example below, two file names are assigned.  If a variable contains multiple words and no quotation marks around, then
spaces before the begin and after the the full names are ignored, i.e. the 2nd assigment assigns to variable **gdp growth imf[]**.
	
```text
gdp growth worldbank[] = "GDP Growth Worldbank.xlsx";	//assign spreadsheet to variable
gdp growth imf      [] = "GDP Growth IMF.xlsx";		//assign spreadsheet to variable
```

## Download GDP growth data and store in dataset file

The following two procedure calls perform downloads of two Excel files from the Internet and store the data into the files specified in the two
abeforementioned variables.

```text
file download overwrite	( 
	"http://pubdocs.worldbank.org/en/872421555426273916/Global-Economic-Prospects-June-2019-GDP-growth-data.xlsx", 
	gdp growth worldbank[] );
	
file download overwrite	( 
	"https://www.imf.org/external/pubs/ft/weo/data/WEOhistorical.xlsx", 
	gdp growth imf[] );
```

## Load specific sheet from imported dataset into Excel file

The following two procedure calls contain three parameters:  The 1st one is the name of the table which will be created (or initialized if alredy
existing).  The 2nd parameter contains the Excel file name.  The 3rd parameter is the actual sheet name to use in the Excel workbook file.  
You may use quotation marks, but must not if the contents contain no special characters and only one space between the words.


```text
echo( "Note: The IMF file is a huge one (> 7 MB compressed).  Allow a few minutes.", new line );

table load excel file	( worldbank, gdp growth worldbank[], Statistical Appendix );
table load excel file	( imf      , gdp growth imf      [], ngdp_rpch );
```

## Prepare and clean up the Worldbank data

The sheet loaded looks like this one (but without the formatting)

![Worldbank Table](images/Worldbank_Table.jpg.jpg)


* Move table headers with the content below to top row, deleting the unnecessary stuff above.
* Write header name 'country' to top lef of the table (was blank before)
* Delete blank columns
* Delete blank rows
* Delete 'e' and 'f' in years column

```text
echo( "         Lift headers, remove quarterly data, add missing header ... ");


table lift header row		( worldbank, "2016" );		// Move table headers to top row (delete the above).  One header is "2016".
[worldbank:0,0] 		= country;			// Add missing header name to table 'worldbank', row 0, column 0
	
// Delete all columns with quarterly data and blank columns (blank behind comma)
table delete columns 		( worldbank, [ worldbank: :'*Q*,', 0 ] );	
	
// Delete blank row plus description row at the bottom
table delete selected rows	( worldbank, [country] == '', 2 );		
	
// Delete the 'e' and 'f' behind the years.
for all table selected columns	( worldbank, ('20*'), 0, col nr[], col[] )
	{
	[ col nr[] ] = WBK Y + literal([ col nr[] ]) - e - f; 
	// Note: Since table context (table name and row number) are known, only column needs to be specified.
	}
```

## Prepare and clean IMF Data

```text
// Keep 1st two and the last column, forget all other.
table keep columns 		( imf, { country, year, -1 } ); 
	
table rename column headers	( imf, -1, GDP growth );
table delete selected rows	( imf, [GDP growth] = '.' );

// The years are still listed vertically.  
// Move them across columns by doing a simple pivot. Round the numbers for clarity
table process		( imf, [year] = IMF Y + literal([year]); [GDP growth] = round([GDP growth], 0.1 ) ); 
table spread 		( imf, GDP growth, [year] );
table consolidate	( imf, country, { year, GDP growth } + [ imf : '>GDP growth'.., 0 ], { delete, delete, sum } );

table save( imf,       test imf 2.csv );	// Save intermediate files
table save( worldbank, test wbk 2.csv );
```

## Merge and align IMF and World Bank data into single table

```text
// Capitalize all headers and remove superscript numbers
table process	( imf, 		[country] = ![country] - '1'-'2'-'3'-'4'-'5'-'6'-'7'-'8'-'9'-'0'-',' );
table process	( worldbank, 	[country] = ![country] - '1'-'2'-'3'-'4'-'5'-'6'-'7'-'8'-'9'-'0'-',' );

table merge extend columns	( imf, worldbank, country );
table rename			( worldbank, combined );
table sort rows			( combined, country );
```

## Compare IMF and World Bank GDP figures

```text
years [imf]			= [ combined ::'IMF*', 0 ] -^ 'IMF ';  // Here you see how to use member (child) variables
years [worldbank]		= [ combined ::'WBK*', 0 ] -^ 'WBK ';  // and parameter sets as contents
years [both]			= years[imf] & years[worldbank];       // Intersection of the two sets  (logical AND)

echo				( "Years in IMF       listing : ", years [imf]       );
echo				( "Years in Worldbank listing : ", years [worldbank] );
echo				( "Years in both      listings: ", years [both] );

table insert columns		( combined, "Delta " +^ years[both] );

for all parameters( years[both], year[] ) // Compare line by line
	{
	table process selected rows( combined,  
		(["IMF " + year[]] <> '') & (["WBK " + year[]] <> ''), 
			["Delta " + year[]] = ["IMF " + year[]] - ["WBK " + year[]] );
	}
```

## Save results in spreadsheet
```text
echo (new line, "processing took ", watch stop()/1000, " seconds."  );
echo ("Everything completed.  Open Result.csv" );

table save			( combined, Result.csv );

// End of program
}

```
