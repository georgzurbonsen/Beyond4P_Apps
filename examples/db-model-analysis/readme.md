
## Datbase model comparison

Fileman (File Manager) is a hierachical filestore, which stores data in numbered fields (FieldNumber) within numbered files (FileNumber).

__Objective:__ Compare fields in commmon between the Fileman datastore and the clinical data warehouse (CDW).

```text

database source files / worksheets / columns to analyze:

A:
excel:      db-source / fileman_db
worksheet:  FileManFields (90587)
columns:    FileNumber
            FieldNumber

B:
excel:      db-source/ cdw_db
worksheet:  CDW View Columns (18649)
columns:    SourceFileNumber
            SourceFieldNumber

Compare A vs B:
A. [FileNumber + FieldNumber] in FileManFields workbook in fileman_db
B. [SourceFileNumber+SourceFieldNumber] in CDW View Columns workbook in cdw_db

```

Task:
1. Create new excel file called 'fileman_cdw_map' that contains a copy of the 'FileManFields (90587)' worksheet.  
2. Add a new column to 'fileman_cdw_map'  with the heading 'cdw match'.   
3. Compare all [FileNumber + FieldNumber] pairs in fileman_db vs cdw_db
4. Add 'Y' to the 'cdw match' column there is an exact match of the FieldNumber+FileNumber; otherwise it should be blank.

Optional: all rows that are marked with 'Y' should be highlighted in yellow


