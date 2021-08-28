
## Datbase model comparison: Meta-program

Fileman (File Manager) is a hierachical filestore, which stored data in  (numbered) fields 'FieldNumber' within (numbered) files 'FileNumber'.

__Objective:__ Compare fields in commmon between the Fileman datastore and a subset of Fileman called the clinical data warehouse (CDW).

```text
Source files / worksheets / columns to analyze:

A:
excel:      fileman_db
worksheet:  FileManFields (90587)
columns:    FileNumber
            FieldNumber

B:
excel:      cdw_db
worksheet:  CDW View Columns (18649)
columns:    SourceFileNumber
            SourceFieldNumber

Compare A vs B:
A. [FileNumber + FieldNumber] in FileManFields workbook in fileman_db
B. [SourceFileNumber+SourceFieldNumber] in CDW View Columns workbook in cdw_db

```

Task:
1. Create new excel file called 'fileman_cdw_map' that contains a copy of the 'FileManFields (90587)' worksheet.  
2. Add a new column to 'fileman_cdw_map'  with the heading 'cdw'.   
3. Compare File+Fields defined in fileman_db vs cdw_db
4. Add 'Y' to the 'cdw' column there is an exact match of the FieldNumber+FileNumber; otherwise it should be blank.

Optional: all rows that are marked with 'Y' should be highlighted in yellow


