#!/usr/local/bin/b4p

# Merge two spreadsheets using translation table

Merging of two clubs using a translation table which harmonizes header names and arranges the columns in a perferred order.

include ( Style Library ); 	// Include this library if you want to use the 'table style ...' functions.

## Load files

```code
table load excel file		( translation table, Translation Table.xlsx );
table lift header row		( translation table, Common Headers );
old club file names[]		= [translation table: :'*Membership List*',0];

for all parameters( old club file names[], file[] )
{
table load excel file		    ( club, file[] );
```


## Harmonize header names

```b4p
table process columns		    ( club, 0, [.] = [translation table:file[],[.], Common Headers] );
```

## Replace diverse position names by simplified main position names

```b4p
table lookup smart ignore case	    ( club, Positions, Positions, translation table, Position, Main Position );

table delete all unnamed columns    ( club );

table merge extend columns	    ( club, new club, { Last Name, First Name },
{ Goals, Since, City, Skill Level, Positions, Supporters, Specific Functions },
{ sum,   min abc,       append once }, ", " ); // 'append once' applies to all further headers
}

table sort rows			( new club, { Skill Level, Last Name,  First Name });
table keep columns			( new club, [translation table:Common Headers,..] - {''} ); // Without blank ones
```


### Before saving to Excel fie, do some formatting.

```b4p
table style theme		( new club, Zebra );
table style auto width	( new club );
table process selected rows ( new club, ([Skill Level] = '*Questionable*'),
table style cells	    ( new club, Skill Level, row(), single, text color, red ) );

table save excel file	( new club, New Club, New Soccer Club Membership List.xlsx );

echo ("New soccer club has ", table length( new club ), " members. Enjoy playing.");
```
