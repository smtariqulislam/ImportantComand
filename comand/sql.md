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
SET employeeName = LTRIM(RTRIM(employeeName));
```




## While Loop

### 
``` sql

IF NOT EXISTS (SELECT * FROM sys.columns 
               WHERE object_id = OBJECT_ID('FixTicket') AND name = 'TicketCode')
BEGIN
    ALTER TABLE FixTicket
    ADD TicketCode NVARCHAR(50) NOT NULL DEFAULT 'T000000';
END
GO

--- Update existing records with sequential ticket codes
DECLARE @i INT = 1;
DECLARE @totalRows INT;

-- Get the total number of rows to update
SELECT @totalRows = COUNT(*) FROM FixTicket;

-- Update each row with sequential ticket numbers
WHILE @i <= @totalRows
BEGIN
    UPDATE TOP (1) FixTicket
    SET TicketCode = 'T' + RIGHT('000000' + CAST(@i AS VARCHAR(6)), 6)
    WHERE TicketCode = 'T000000' OR TicketCode IS NULL;
    
    SET @i = @i + 1;
END
```




## 001: UPDATE 

### Less Date
```sql
UPDATE FixTicket
SET CloseDate = '1980-12-31 00:00:00.000'
WHERE CloseDate < '1980-12-31 00:00:00.000';
```





## Most Important SP(For Role add)

### 001
```sql

update  AspNetUsers set Role='User' where UserName='254790151959'

DECLARE @Id NVARCHAR(50);
SELECT @Id = Id 
FROM AspNetUsers 
WHERE EmployeeId = '7387C777-84BA-4689-991D-03D6459EB681';
```



## Most Important SP(For Role add)

### 001
```sql

select * from HrEmployee where EmployeeId='E56624F2-7ADF-4D06-A9E2-48CC9CB56260'
select Id ,role from AspNetUsers where EmployeeId='E56624F2-7ADF-4D06-A9E2-48CC9CB56260'
select * from AspNetRoles where Id='5b62788e-cafd-4a9c-9437-993fb550972a'
select * from AspNetUserRoles where UserId='9855eef9-a3c1-4b65-8838-4a39f4831ead'

INSERT INTO AspNetUserRoles ([UserId], [RoleId])
SELECT Id, '5b62788e-cafd-4a9c-9437-993fb550972a'
FROM AspNetUsers 
WHERE EmployeeId ='C870CD4B-92A8-40F7-9326-BC4A2FA61E4C';

--select 
update
--select * from
AspNetUsers set Role='Úser'  where EmployeeId='C870CD4B-92A8-40F7-9326-BC4A2FA61E4C'

```
### 002
```sql

-- Step 1: Declare variable
DECLARE @RowCount INT

-- Step 2: Check the row count
SELECT @RowCount = COUNT(*) FROM OpsERMFTemplate

-- Step 3: If row count is exactly 189, proceed
IF @RowCount = 189
BEGIN
    -- Step 4: Add a new column named RiskId if it doesn't exist
    IF NOT EXISTS (
        SELECT * 
        FROM INFORMATION_SCHEMA.COLUMNS 
        WHERE TABLE_NAME = 'OpsERMFTemplate' 
        AND COLUMN_NAME = 'RiskId'
    )
    BEGIN
        ALTER TABLE OpsERMFTemplate ADD RiskId INT
    END

    -- Step 5: Update the new column with values 1 to 189
    ;WITH NumberedRows AS (
        SELECT 
            *, 
            ROW_NUMBER() OVER (ORDER BY (SELECT NULL)) AS RowNum
        FROM OpsERMFTemplate
    )
    UPDATE NumberedRows
    SET RiskId = RowNum
END
ELSE
BEGIN
    PRINT 'Warning: Table does not contain exactly 189 rows (' + CAST(@RowCount AS VARCHAR) + ' rows found)'
END
```



## Case SQL 

### 001
```sql

	Attachment=CASE
						WHEN (@Attachment<>'') THEN @Attachment
						ELSE Attachment
						END
```




## Practical prolem  Sql I face

### ticket

#### employeeName and employeeId
```UPDATE FixDeskDb.dbo.FixTicket
SET CreatedBy = a.FullName

--select * 
FROM FixDeskDb.dbo.FixTicket
INNER JOIN UmTanzaniaDb.dbo.AspNetUsers a 
    ON FixDeskDb.dbo.FixTicket.CreatedBy = a.Id;
```
#### Branch

```Update FixDeskDb.dbo.FixTicket set BranchName=yy.bName
--Select * 
from (

Select sub.tid,main.Id,main.EmployeeName,main.BranchName bName from (

Select a.Id,e.EmployeeId,e.EmployeeName,b.BranchName from UmTanzaniaDb.dbo.AdBranch b
inner join UmTanzaniaDb.dbo.HrEmployee e on b.BranchId=e.BranchId
inner join UmTanzaniaDb.dbo.AspNetUsers a on e.EmployeeId=a.EmployeeId
--where a.id='b478a51f-b35c-45a1-8bc8-594321cae16e'
)main
inner join 
(
Select TicketId tid, CreatedId cid ,CreatedBy cby,BranchName from FixDeskDb.dbo.FixTicket ft 
) sub on main.Id=sub.cid
) yy
where TicketId=yy.tid
```






