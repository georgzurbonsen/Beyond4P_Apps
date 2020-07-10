#!/usr/local/bin/Beyond4P

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

The sheet loaded looks like this one:

![Worldbank Table](images/Worldbank_Table.jpg)

* Move table headers with the content below to top row, deleting the unnecessary rows above the years
* Write header name 'country' to top lef of the table (was blank before)
* Delete all colums containing quarterly growth (header names contain 'Q', as well asblank headers)
* Delete rows with no countries specified
* Delete 'e' and 'f' in years column

```text
echo( "         Lift headers, remove quarterly data, add missing header ... ");


table lift header row		( worldbank, "2016" );		// Move table headers to top row (delete the above).  One header is "2016".
[worldbank:0,0] 		= country;			// Add missing header name to table 'worldbank', row 0, column 0
	
// Delete all columns with quarterly data and blank columns (blank behind comma)
table delete columns 		( worldbank, [ worldbank: :'*Q*,', 0 ] );	
	
// Delete current and next row as well (total: 2 rows) if the country column is blank)
table delete selected rows	( worldbank, [country] == '', 2 );		
	
// Delete the 'e' and 'f' behind the years which were used to indicated them as 'expected' or 'forecasted' figures.
for all table selected columns	( worldbank, ('20*'), 0, col nr[] )
    {
	[ col nr[] ] = WBK Y + literal([ col nr[] ]) - e - f; 
	// Example: 'WBK Y2016', with suffix 'e' or 'f' stripped of if existing.
	// Note: Since table context (table name and row number) are known, only column needs to be specified.
    }

table save( worldbank, test wbk 2.csv );	// Save intermediate file

```

The loop **for all table selected columns** is a smart one which loops through all headers beginning with '20' which are years.
The 2nd parameter (0) refers to the row number in the table to check these columns.  The 3rd parameters is an output parameter
to the variable 'col nr[]' which contains the iteratd column numbers.

Inside the loop, the context of the current table (i.e. table name and row number known) allows simplified partial table references
where only the column name or number needs to be specified to read- or write-access a particular cell.  Example: '[col nr[]]' to 
access column number as specified in the variable 'col nr[]'.

At this moment, the worldbank data looks like this:

![Worldbank Table](images/Worldbank_Preprocessed.jpg)


## Prepare and clean IMF Data

The sheet loaded looks like this one:

![IMF Table](images/IMF_Table.jpg)

* As a first step, let's delete all columns except the first the columns labeled 'country', 'year' and the last one. Beyond4P supports negative indexing on columns (also supported on variable array index values, etc.).
* Rename the last column header to 'GDP growth'.
* Delete all rows where the contents below the header 'GDP growth' contain points (and not numeric data).

```text
// Keep 1st two and the last column, forget all other.
table keep columns 		( imf, { country, year, -1 } ); 
table rename column headers	( imf, -1, GDP growth );
table delete selected rows	( imf, [GDP growth] = '.' );

```
In contrast to the Worldbank table which lists years in the columns and country names in the row, the IMF table lists both
year, country names and data in a simple table consisting of 3 columns.  Lets pivot this table so it contains 1 row per
country name and the years distributed horizontally as additional headers.

![IMF Table](images/IMF_Intermediate.jpg)

Before starting with the pivot, let's convert years to 'IMF Y2019', 'IMF Y2020', etc. so the formulation is similar as
for the worldbank done before, like 'WBK Y2019'.  Also round the GDP growth numbers to steps of 0.1 so they look a bit nicer.

The pivot from vertical to horizontal consists of just 2 Beyond4P statements:
* Spread the GDP growth data across years horizontally.  For every different year, a new column with the year will be added.  As of now, the number of rows is still the same.
* Consolidate the table to 1 row per country.  During the consolidateion process, delete the columns 'year' and 'GDP growth' on the left, and sum up the values beyond the column 'GDP growth' which are the tabulated years.


```text
// The years are still listed vertically.  
// Move them across columns by doing a simple pivot. Round the numbers for clarity
table process		( imf, [year] = IMF Y + literal([year]); [GDP growth] = round([GDP growth], 0.1 ) ); 
table spread 		( imf, GDP growth, [year] );
table consolidate	( imf, country, { year, GDP growth } + [ imf : '>GDP growth'.., 0 ], { delete, delete, sum } );

table save( imf,       test imf 2.csv );	// Save intermediate file

```

The IMF table looks as illustrated below:

![IMF Table](images/IMF_Preprocessed.jpg)

## Clean up country names

Some country names have left-overs digits and commas at the end because the original files contained
references to footnotes which are just distracting.  The 'table process' procedures take two parameters:
The 1st one is the table name, the 2nd one contains 1 or more statements.  The statements specified here are
called up for every table row.  Only the column names or column numbers need to be specified to reference
cells in the current table and row, e.g. the 'country' column. 

The embedded statemetns are assignments.  First take the value from the column 'country', capitalize it with the
unary exclamation operator (!), then _subtract_ all redundant digits and commas and finally write the
string back into the country column.

```text
// Capitalize all headers and remove superscript numbers
table process	( imf, 		[country] = ![country] - '1'-'2'-'3'-'4'-'5'-'6'-'7'-'8'-'9'-'0'-',' );
table process	( worldbank, 	[country] = ![country] - '1'-'2'-'3'-'4'-'5'-'6'-'7'-'8'-'9'-'0'-',' );
```

## Merge and align IMF and World Bank data into single table

* Merge table 'imf' into the table 'worldbank' with algining on country names.  This single statement puts the IMF and Worldbank
  years on the same rows where both tables contain the same country name.
* Rename the 'worldbank' table to 'combined'
* Sort by country in alphabetic order (sorting function supports lots of nice sorting options)

```text
table merge extend columns	( imf, worldbank, country );
table rename			( worldbank, combined );
table sort rows			( combined, country );
```

The table looks as follows:
![Combined Table](images/Combined_Table.jpg)

## Prepare to Compare IMF and World Bank GDP figures

* Pick the IMF years as 'Y2019', without the 'IMF ' prefix and store them into the variable 'years[imf]'
* Pick the Worldbank years as 'Y2019', without the 'IMF ' prefix and store them into the variable 'years[imf]'
* Both variables contain years in form of parameter sets containing literals.
* The 3rd statement does the intersection of the two parameter sets, containing years found in both IMF and Worldbank tables.

```text
years [imf]			= [ combined ::'IMF*', 0 ] -^ 'IMF ';  // Here you see how to use member (child) variables
years [worldbank]		= [ combined ::'WBK*', 0 ] -^ 'WBK ';  // and parameter sets as contents
years [both]			= years[imf] & years[worldbank];       // Intersection of the two sets  (logical AND)

echo				( "Years in IMF       listing : ", years [imf]       );
echo				( "Years in Worldbank listing : ", years [worldbank] );
echo				( "Years in both      listings: ", years [both] );

```
## Compare IMF and World Bank GDP figures

* Create a bunch of additional columns named 'Delta ' followed by the common years.
* Do the followign steps for every common year:
* Process all table row where both IMF values and Worldbank values are available
* If they are, then calculate the delta and write the value into the corresponding column justcreated before.

```text

table insert columns		( combined, "Delta " +^ years[both] );

for all parameters( years[both], year[] ) // Compare line by line
	{
	table process selected rows( combined,  
		(["IMF " + year[]] <> '') & (["WBK " + year[]] <> ''), 
			["Delta " + year[]] = ["IMF " + year[]] - ["WBK " + year[]] );
	}
```

## Save results in spreadsheet

It's _kinderleicht_. Stop th e watch and save the results.

```text
echo (new line, "processing took ", watch stop()/1000, " seconds."  );
echo ("Everything completed.  Open Result.csv" );

table save			( combined, Result.csv );

// End of program
}

```

The results should like this:

![Result](images/Result_Table.jpg)



