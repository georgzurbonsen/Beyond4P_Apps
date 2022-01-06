Function Library Guide

    → User Guide
    → Language Guide
    Table of Contents
    1 Function Library
    2 Control Flow Functions
        2.1 Branches
            2.1.1 if, unless
            2.1.2 else
            2.1.3 once
            2.1.4 switch, check
            2.1.5 case
            2.1.6 break, continue
        2.2 Loops
            2.2.1 do
            2.2.2 for
            2.2.3 while, until
            2.2.4 for all parameters
            2.2.5 for all variables
        2.3 User-Defined Procedures and Functions
            2.3.1 define procedure / function
            2.3.2 define additional procedure / function
            2.3.3 Parameter Types in User-Defined Functions
            2.3.4 return
            2.3.5 function / user function existing
            2.3.6 delete user function
        2.4 Launch other B4P programs
            2.4.1 start
            2.4.2 include
            2.4.3 get long options
        2.5 Exception Functions
            2.5.1 pause
            2.5.2 stop
            2.5.3 interactive
            2.5.4 exit
            2.5.5 end
            2.5.6 abort
            2.5.7 throw
            2.5.8 catch, catch if
            2.5.9 exception
            2.5.10 null - Function
        2.6 Comparison and Selection Functions
            2.6.1 select, pick
            2.6.2 select if, pick if
            2.6.3 select ifs, pick ifs
            2.6.4 select/pick if existing ...
            2.6.5 select / pick by value
            2.6.6 compare select / pick
        2.7 Code Execution Functions
            2.7.1 call
            2.7.2 deep, deepr
            2.7.3 exec
            2.7.4 calc
            2.7.5 compare
            2.7.6 assign
    3 Console I/O Functions
        3.1 Text Input / Output
            3.1.1 echo, print ...
            3.1.2 print bar
            3.1.3 format, format print
            3.1.4 compose ...
            3.1.5 input
            3.1.6 input quick ...
            3.1.7 getch ...
            3.1.8 clipboard
        3.2 Console Special Effects
            3.2.1 cls
    clear
            3.2.2 cursor
            3.2.3 text / background color
            3.2.4 console
            3.2.5 blinking
            3.2.6 boldface
            3.2.7 reverse
            3.2.8 underscore
    reset console
        3.3 Inspection and Debugging
            3.3.1 prompt
            3.3.2 inspect
            3.3.3 list variables ...
    4 Type Conversion and Formatting
        4.1 literal, quoted literal, softquoted literal
            4.1.1 Literal to Literal Formatting
            4.1.2 Void to Literal Formatting
            4.1.3 Numeral to Literal Formatting
            4.1.4 Date to Literal Formatting
            4.1.5 Parameter Set to Literal Formatting
            4.1.6 Boolean to Literal Formatting
            4.1.7 Smart Formatting
        4.2 numeral
        4.3 clean (if) numeral
        4.4 smart (if) numeral
        4.5 date, pure date, date time
        4.6 time, pure time
        4.7 Date and Time Detection Rules
        4.8 boolean
        4.9 parameter set
        4.10 best type
        4.11 join ...
        4.12 type, type detailed
        4.13 hash signature
        4.14 excel column
        4.15 excel coordinates
        4.16 excel validate sheet name
    5 Mathematics and Statistics
        5.1 Basic Math Functions
            5.1.1 is numeric / integer - Functions
            5.1.2 even, odd, whole
            5.1.3 zebra
            5.1.4 abs - Absolute Value
            5.1.5 round, round up / down
            5.1.6 mod - Modulo function
            5.1.7 random - Random Integers
            5.1.8 hex to decimal
            5.1.9 distribute amount
        5.2 Transcendental Functions
            5.2.1 sqrt - Square Root
            5.2.2 pow - Power Function
            5.2.3 Exponential Functions
            5.2.4 Logarithmic Functions
            5.2.5 Trigonometric Functions
            5.2.6 Hyperbolic Functions
        5.3 Series Functions
            5.3.1 Arithmetic and Boolean Series Functions
            5.3.2 min, max Functions
            5.3.3 min, max Functions on Literals
            5.3.4 min, max Functions on Numerals
            5.3.5 count Functions
        5.4 Matrix Functions
            5.4.1 mmul, mmdiv - Multiplication and Division
            5.4.2 minv - Matrix Inversion
            5.4.3 mdet - Matrix Determinant
            5.4.4 linear - Solve Linear Equations
            5.4.5 horizontal
            5.4.6 vertical
            5.4.7 flat
            5.4.8 diagonal
            5.4.9 transpose
        5.5 Statistics Functions
            5.5.1 Basic Statistics Functions
            5.5.2 quantile ...
            5.5.3 covariance, correlation
            5.5.4 gini Coefficient Functions
            5.5.5 Linear and Exponential Regression
            5.5.6 Interpolation Functions
                5.5.6.1 Interpolation Examples Visualized
        5.6 Conditional Combination Functions
        5.7 Finance and Business Functions
            5.7.1 cagr - Compond Annual Growth Rate
            5.7.2 irr - Internal Rate of Return
            5.7.3 tv - Terminal Value
            5.7.4 discount - Discount Values
            5.7.5 distribute - Value Distribution over Timeline
    6 String Functions
        6.1 String Search and Extraction Functions
            6.1.1 find ... (string function)
            6.1.2 replace, replace all
            6.1.3 substitute, substitute all
            6.1.4 length ... (string function)
            6.1.5 width
            6.1.6 height
            6.1.7 left ... (string function)
            6.1.8 right ... (string function)
            6.1.9 middle ... (string function)
            6.1.10 outside ... (string function)
            6.1.11 trim ... (string function)
            6.1.12 clean
            6.1.13 tokenize
            6.1.14 get differences
            6.1.15 locate differences
        6.2 Character Encoding and Decoding
            6.2.1 chr
            6.2.2 code
            6.2.3 decode entities
            6.2.4 encode entities
        6.3 Miscellaneous String Functions
            6.3.1 replicate ... (string function)
            6.3.2 random string, random letters
            6.3.3 describe
            6.3.4 abbreviate name
    7 Date and Time Functions
        7.1 Date Functions
            7.1.1 date inside, time inside
            7.1.2 year, quarter, month, day
            7.1.3 day of year
            7.1.4 serial date
            7.1.5 weekday
            7.1.6 week
            7.1.7 fq - Fiscal Quarter
            7.1.8 fy - Fiscal Year
            7.1.9 reschedule
        7.2 Time and Stopwatch Functions
            7.2.1 hour, minute, second
            7.2.2 Stopwatch Functions
        7.3 Sleep and Wait Functions
            7.3.1 sleep, sleep countdown
            7.3.2 sleep until, sleep until countdown
            7.3.3 wait until, wait until countdown
            7.3.4 wait, wait countdown
    8 Parameter Set Functions
        8.1 Set Search and Extraction Functions
            8.1.1 length ... (parameter set function)
            8.1.2 find ... (parameter set function)
            8.1.3 left ... (parameter set function)
            8.1.4 right ... (parameter set function)
            8.1.5 middle ... (parameter set function)
            8.1.6 outside ... (parameter set function)
            8.1.7 trim ... (parameter set function)
            8.1.8 count elements ...
            8.1.9 subset ...
            8.1.10 filter ...
    9 Table Functions
        9.1 Loading and Saving Tables
            9.1.1 table load ...
                9.1.1.1 Loading HTML files
                9.1.1.2 Loading XML files
                9.1.1.3 Loading JSON files
            9.1.2 table save ...
                9.1.2.1 Saving JSON files
            9.1.3 excel list sheets
            9.1.4 table load excel file
            9.1.5 table save excel file
        9.2 Console I/O with Tables
            9.2.1 table list
            9.2.2 table menu ...
        9.3 Creating, Writing, Reading, Deleting
            9.3.1 Creating and Building up Tables
                9.3.1.1 table create ...
                9.3.1.2 table initialize
                9.3.1.3 table configure
                9.3.1.4 forget memorized table columns
            9.3.2 Writing Tables
                9.3.2.1 table append ...
                9.3.2.2 table append blank rows
                9.3.2.3 table add / write row
                9.3.2.4 table (write or) add missing row
                9.3.2.5 table write column selected rows
            9.3.3 Reading Tables
                9.3.3.1 table read row
                9.3.3.2 table read column selected rows
            9.3.4 Deleting Tables
                9.3.4.1 table clear ...
                9.3.4.2 table delete ...
        9.4 Accessing Table Information
            9.4.1 list tables
            9.4.2 table existing
            9.4.3 table length
            9.4.4 table row width
            9.4.5 table min/max width
            9.4.6 row
            9.4.7 col
        9.5 Searching and Exploring Tables
            9.5.1 Search Functions
                9.5.1.1 table search ...
                9.5.1.2 table search row
                9.5.1.3 table find row
                9.5.1.4 table selected rows
                9.5.1.5 table selected columns/headers ...
                9.5.1.6 table search header row
            9.5.2 Explore, Filter, Extract Sub-Tables
                9.5.2.1 table explore
                9.5.2.2 table filter ...
                9.5.2.3 table extract ...
        9.6 Control Flow Functions for Tables
            9.6.1 with table
            9.6.2 for all table rows
            9.6.3 for all table selected rows
            9.6.4 for all table columns
            9.6.5 for all table selected columns
            9.6.6 for all current table columns
            9.6.7 for all current table selected columns
        9.7 Processing Tables
            9.7.1 Checking and Processing Headers
                9.7.1.1 table check header
                9.7.1.2 table column number
                9.7.1.3 table check headers ...
                9.7.1.4 table rename ... headers
                9.7.1.5 table correct headers ...
                9.7.1.6 table lift ...
            9.7.2 Processing Table Columns
                9.7.2.1 table insert (missing) columns
                9.7.2.2 table copy columns ...
                9.7.2.3 table duplicate columns ...
                9.7.2.4 table sort columns
                9.7.2.5 table rearrange ... columns
                9.7.2.6 table keep ... columns
                9.7.2.7 table delete columns
                9.7.2.8 table delete remaining columns
                9.7.2.9 table delete blank/empty/unnamed columns
            9.7.3 Processing Table Rows
                9.7.3.1 table insert rows
                9.7.3.2 table insert ... selected rows
                9.7.3.3 table delete rows
                9.7.3.4 table delete remaining rows
                9.7.3.5 table delete selected rows
                9.7.3.6 table keep selected rows
                9.7.3.7 table delete blank rows
                9.7.3.8 table check row
                9.7.3.9 table move rows
                9.7.3.10 table move selected rows
                9.7.3.11 table rearrange selected rows
                9.7.3.12 table sort (selected) rows
                9.7.3.13 table rank (selected) rows
            9.7.4 Processing Table Contents
                9.7.4.1 table process (all) (selected rows)
                9.7.4.2 table process selected rows fast
                9.7.4.3 table process (selected) columns
                9.7.4.4 table process cells (selected rows)
                9.7.4.5 table process cells in columns (selected rows)
                    9.7.4.5.1 Addt'l Info on fast rows processing
                9.7.4.6 table manipulate (selected rows)
                9.7.4.7 table fill vertically ...
                9.7.4.8 table fill horizontally ...
                9.7.4.9 table substitute vertically ...
                9.7.4.10 table substitute horizontally ...
                9.7.4.11 table delete cells selected rows
                9.7.4.12 table delete cells selected columns
                9.7.4.13 table format numbers
                9.7.4.14 table clean
                9.7.4.15 table fit
            9.7.5 Pivoting and Conosolidating Tables
                9.7.5.1 table transpose
                9.7.5.2 table serialize ...
                9.7.5.3 table spread ...
                9.7.5.4 table spread given headers ...
                9.7.5.5 table consolidate ...
                9.7.5.6 table distribute ...
            9.7.6 Copying, Renaming and Splitting Tables
                9.7.6.1 table rename
                9.7.6.2 table copy table
                9.7.6.3 table copy/split table selected rows
                9.7.6.4 table copy table columns ...
                9.7.6.5 table split table columns ...
        9.8 Multi-Table Integration
            9.8.1 Comparing and Validating Tables
                9.8.1.1 table compare ...
                    9.8.1.1.1 Table Comparison Strategy
                    9.8.1.1.2 Table Comparison Reports
                    9.8.1.1.3 Change Indication Function
                9.8.1.2 table validate
                    9.8.1.2.1 table validate - Row and Group Results
                    9.8.1.2.2 table validate - Examples
                9.8.1.3 table check duplicates ...
            9.8.2 Looking up Other Tables
                9.8.2.1 table lookup ...
                9.8.2.2 table lookup once ...
                9.8.2.3 table lookup fast ...
                9.8.2.4 table lookup smart ...
                9.8.2.5 table lookup smart once ...
                9.8.2.6 table lookup with rules ...
                9.8.2.7 table lookup with rules once ...
                9.8.2.8 table integrate ...
                9.8.2.9 table integrate once ...
                9.8.2.10 table integrate fast ...
                9.8.2.11 table integrate smart ...
                9.8.2.12 table integrate smart once ...
                9.8.2.13 table integrate with rules ...
                9.8.2.14 table integrate with rules once ...
                9.8.2.15 table expand ...
                9.8.2.16 table expand fast ...
                9.8.2.17 table expand smart ...
                9.8.2.18 table expand fast smart ...
                9.8.2.19 table expand with rules ...
                9.8.2.20 table expand with rules once ...
                9.8.2.21 table expand fast with rules ...
                9.8.2.22 table expand fast with rules once ...
                9.8.2.23 table digest ...
                9.8.2.24 table digest smart ...
                9.8.2.25 table digest with rules ...
                9.8.2.26 table digest with rules once ...
                9.8.2.27 Table Integration Operation Identifiers
                9.8.2.28 table describe ...
            9.8.3 Combining Multiple Tables
                9.8.3.1 table merge ...
                9.8.3.2 table overlay/subtract ...
                9.8.3.3 table intersect ...
                9.8.3.4 table subtract ...
                9.8.3.5 table exclude ...
                9.8.3.6 table multiply ...
                9.8.3.7 table divide ...
                9.8.3.8 table arrange ...
        9.9 Formatting and Styling Tables
            9.9.1 Defining User Specific Colors
                9.9.1.1 Color Palettes
                9.9.1.2 add color
                9.9.1.3 rgb
                9.9.1.4 darken color
                9.9.1.5 lighten color
                9.9.1.6 weaken color
                9.9.1.7 lighten colors
                9.9.1.8 darken colors
                9.9.1.9 weaken colors
            9.9.2 Styling Functions
                9.9.2.1 table style table
                9.9.2.2 table style rows
                9.9.2.3 table style columns
                9.9.2.4 table style cells
                9.9.2.5 Generic Formatting Attributes
                9.9.2.6 Formatting Coverages and Precedences
                9.9.2.7 table style auto width
                9.9.2.8 table style themes (beta)
            9.9.3 Finishing up formatting
                9.9.3.1 translate style attributes ...
                9.9.3.2 table style reset
    10 Variables Functions
        10.1 Basic Variables Functions
            10.1.1 existing (and valid)
            10.1.2 copy
            10.1.3 identify
            10.1.4 scope
            10.1.5 name
            10.1.6 exchange
            10.1.7 protect ...
            10.1.8 delete ...
            10.1.9 global
            10.1.10 local
            10.1.11 regional
        10.2 Arrays and Structures
            10.2.1 dim / redim
            10.2.2 dim / redim protect
            10.2.3 array, array protect
            10.2.4 structure, structure protect
            10.2.5 member count
            10.2.6 structure to array ...
            10.2.7 array to structure ...
            10.2.8 set, set names
        10.3 Loading and Saving Variables
            10.3.1 variable load ...
            10.3.2 json to variable ...
            10.3.3 variable save ...
            10.3.4 variable to json ...
        10.4 Variable References Functions
            10.4.1 release
            10.4.2 release all
        10.5 Resident Attributes Functions
            10.5.1 attribute ...
    11 Directory and File System Functions
        11.1 Basic Directory and File Functions
            11.1.1 directory existing, file existing
            11.1.2 read access ..., write access ...
            11.1.3 working directory
            11.1.4 starting directory
            11.1.5 directory size
            11.1.6 file size
            11.1.7 disk space ...
        11.2 Listing and Searching Directories and Files
            11.2.1 directory listing ...
            11.2.2 advanced directory listing ...
            11.2.3 search files ...
            11.2.4 choose recent file
            11.2.5 count files ...
            11.2.6 resolve path/directory/file name
            11.2.7 office document properties
        11.3 Manipulating Directories and Files
            11.3.1 directory create ...
            11.3.2 directory create temp
            11.3.3 file delete ...
            11.3.4 file delete multiple/recursive ...
            11.3.5 directory delete ...
            11.3.6 directory delete multiple/recursive ...
            11.3.7 file rename ...
            11.3.8 directory rename ...
            11.3.9 file copy ...
            11.3.10 file copy mulitple/recursive ...
            11.3.11 file create link ...
            11.3.12 file download ...
        11.4 File Compression and Decompression
            11.4.1 zip compress
            11.4.2 zip extract files
            11.4.3 zip extract all
    12 System Functions
        12.1 Executing System Commands
            12.1.1 system
            12.1.2 quote path
        12.2 set locale
        12.3 Registry Access Functions
        12.4 Licensing and Privileges
            12.4.1 global / script privileges
            12.4.2 license provide identification
            12.4.3 license apply key
    13 Help and Support Functions
        13.1 help
        13.2 help ... / docs
        13.3 openweb
        13.4 docs search
        13.5 view
        13.6 view reset
        13.7 list / explain functions
        13.8 dump functions
    14 Cross-Functional Info
        14.1 Sorting and Ranking Options
        14.2 Consolidation Actions
    15 Index
