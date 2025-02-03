# File Operations

### Change All File Extensions in a Folder (Windows Command Line)
```cmd
for /R %x in (*.txt) do ren "%x" *.renamed
```
This command recursively changes all `.txt` file extensions to `.renamed`, starting from the current directory. `%x` is the variable holding the matched file names.

[Source](https://stackoverflow.com/questions/9885241/changing-all-files-extensions-in-a-folder-with-one-command-on-windows)

---

# SQL Operations

## Column Operations

### Rename a Column
```sql
EXEC sp_rename 'AuditPreviousYearBranch.BranchId', 'BranchName', 'COLUMN';
```

### Delete a Column
```sql
ALTER TABLE AuditDpInvestigationDetails
DROP COLUMN ColumnName;
```

### Change Column Data Type or Modify Properties
```sql
ALTER TABLE TableName
ALTER COLUMN ColumnName NewDataType;
```

### Add a New Column
```sql
ALTER TABLE TableName
ADD NewColumnName DataType;
```

### Add a New Column with Default Value
```sql
ALTER TABLE AuditWorkList
ADD TestingConclusion NVARCHAR(50) DEFAULT '0';
```

### Add Multiple Columns with Default Values
```sql
ALTER TABLE Table
ADD 
    ColumnName1 DATETIME DEFAULT '0',
    ColumnName2 DATETIME DEFAULT '0',
    ColumnName3 NVARCHAR(50) DEFAULT '0';
```

### Change a Column Name (Alternative Method)
```sql
ALTER TABLE tableName
DROP COLUMN columnName;
ALTER TABLE tableName
ADD ColumnName DataType;
```

## Data Manipulation

### Update Column Values
```sql
UPDATE TableName
SET ColumnName = 99;
```

### Copy a Table Structure and Data
```sql
SELECT 
      columnName,
      columnName1,
      columnName2
INTO AuditSpecialInvestigationReportDetails -- New table name
FROM [dbo].[AuditSpecialInvestigationReport]; -- Source table
```

## String Operations

### Remove Leading and Trailing Spaces from a Column
```sql
UPDATE dbo.hrEmpayroll
SET employeeName = LTRIM(RTRIM(employee));
