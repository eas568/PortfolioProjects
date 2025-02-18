/*
Cleaning data by updating and/or converting values 
Below is an example of the format after commenting out the code changes 
*/

--Description of what the code does below
/*
--code
--code
*/
----------------------------------------------------------

--IMPORT Data using SQL Server Import and Export Wizard

--This code below is used to getting the data types for all columns in a table
/*
SELECT COLUMN_NAME, DATA_TYPE
FROM INFORMATION_SCHEMA.COLUMNS
WHERE TABLE_NAME = 'houseprices';
*/
-----------------------------------------------------------

--Creates a backup table before changes
/*
SELECT * INTO houseprices_backup
--FROM houseprices;
*/
----------------------------------------------------------

--Row 1 Header from F1 to DateTime format to Date 
/*
--ALTER TABLE houseprices
--ALTER COLUMN F1 DATE;
*/
----------------------------------------------------------

--Renaming Column Header from F1 to Dates
/*
--EXEC sp_rename 'houseprices.F1', 'Dates', 'COLUMN';
*/
----------------------------------------------------------

--Copying data from old table to the new one
/*
INSERT INTO houseprices2 (Dates, Alabama, Alaska, Arizona, Arkansas, California, Colorado, Connecticut, Delaware, [the District of Columbia], Florida, Georgia, Hawaii, Idaho, Illinois, Indiana, Iowa, Kansas, Kentucky, Louisiana, Maine, Maryland, Massachusetts, Michigan, Minnesota, Mississippi, Missouri, Montana, Nebraska, Nevada, [New Hampshire], [New Jersey], [New Mexico], [New York], [North Carolina], [North Dakota], Ohio, Oklahoma, Oregon, Pennsylvania, [Rhode Island], [South Carolina], [South Dakota], Tennessee, Texas, Utah, Vermont, Virginia, Washington, [West Virginia], Wisconsin, Wyoming)
SELECT Dates, Alabama, Alaska, Arizona, Arkansas, California, Colorado, Connecticut, Delaware, [the District of Columbia], Florida, Georgia, Hawaii, Idaho, Illinois, Indiana, Iowa, Kansas, Kentucky, Louisiana, Maine, Maryland, Massachusetts, Michigan, Minnesota, Mississippi, Missouri, Montana, Nebraska, Nevada, [New Hampshire], [New Jersey], [New Mexico], [New York], [North Carolina], [North Dakota], Ohio, Oklahoma, Oregon, Pennsylvania, [Rhode Island], [South Carolina], [South Dakota], Tennessee, Texas, Utah, Vermont, Virginia, Washington, [West Virginia], Wisconsin, Wyoming
FROM houseprices;
*/
------------------------------------------------------------

--Drop old table after copied successfully
/*
DROP TABLE houseprices;
*/
-------------------------------------------------------------

--Rename new table to old table name
/*
EXEC sp_rename 'houseprices2', 'houseprices';
*/
--------------------------------------------------------------

--"Truncate" to two decimal places without rounding
/*
UPDATE houseprices
SET
	Alabama = ROUND(Alabama, 2),
	Alaska = ROUND(Alaska, 2),
	Arizona = ROUND(Arizona, 2),
	Arkansas = ROUND(Arkansas, 2),
	California = ROUND(California, 2),
	Colorado = ROUND(Colorado, 2),
	Connecticut = ROUND(Connecticut, 2),
	Delaware = ROUND(Delaware, 2),
	[the District of Columbia] = ROUND([the District of Columbia], 2),
	Florida = ROUND(Florida, 2),
	Georgia = ROUND(Georgia, 2),
	Hawaii = ROUND(Hawaii, 2),
	Idaho = ROUND(Idaho, 2),
	Illinois = ROUND(Illinois, 2),
	Indiana = ROUND(Indiana, 2),
	Iowa = ROUND(Iowa, 2),
	Kansas = ROUND(Kansas, 2),
	Kentucky = ROUND(Kentucky, 2),
	Louisiana = ROUND(Louisiana, 2),
	Maine = ROUND(Maine, 2),
	Maryland = ROUND(Maryland, 2),
	Massachusetts = ROUND(Massachusetts, 2),
	Michigan = ROUND(Michigan, 2),
	Minnesota = ROUND(Minnesota, 2),
	Mississippi = ROUND(Mississippi, 2),
	Missouri = ROUND(Missouri, 2),
	Montana = ROUND(Montana, 2),
	Nebraska = ROUND(Nebraska, 2),
	Nevada = ROUND(Nevada, 2),
	[New Hampshire] = ROUND([New Hampshire], 2),
	[New Jersey] = ROUND([New Jersey], 2),
	[New Mexico] = ROUND([New Mexico], 2),
	[New York] = ROUND([New York], 2),
	[North Carolina] = ROUND([North Carolina], 2),
	[North Dakota] = ROUND([North Dakota], 2),
	Ohio = ROUND(Ohio, 2),
	Oklahoma = ROUND(Oklahoma, 2),
	Oregon = ROUND(Oregon, 2),
	Pennsylvania = ROUND(Pennsylvania, 2),
	[Rhode Island] = ROUND([Rhode Island], 2),
	[South Carolina] = ROUND([South Carolina], 2),
	[South Dakota] = ROUND([South Dakota], 2),
	Tennessee = ROUND(Tennessee, 2),
	Texas = ROUND(Texas, 2),
	Utah = ROUND(Utah, 2),
	Vermont = ROUND(Vermont, 2),
	Virginia = ROUND(Virginia, 2),
	Washington = ROUND(Washington, 2),
	[West Virginia] = ROUND([West Virginia], 2),
	Wisconsin = ROUND(Wisconsin, 2),
	Wyoming = ROUND(Wyoming, 2)
*/
----------------------------------------------------------------------

--Checking for NULLS in the whole table
/*
DECLARE @sql nvarchar(max) = '';
SELECT @sql += '
    SELECT ''' + c.name + ''' as ColumnName,
           COUNT(*) as TotalRows,
           SUM(CASE WHEN ' + QUOTENAME(c.name) + ' IS NULL THEN 1 ELSE 0 END) as NullCount,
           CAST(SUM(CASE WHEN ' + QUOTENAME(c.name) + ' IS NULL THEN 1 ELSE 0 END) AS float) * 100 / COUNT(*) as NullPercentage
    FROM houseprices'
FROM sys.columns c
WHERE c.object_id = OBJECT_ID('houseprices');

EXEC sp_executesql @sql;
*/
---------------------------------------------------------------------

--Replacing NULLs to 0 for the whole table besides column 1
/*
DECLARE @sql nvarchar(max) = '',
        @houseprices sysname = 'houseprices';

SELECT @sql += '
    UPDATE ' + QUOTENAME(OBJECT_SCHEMA_NAME(c.object_id)) + '.' + QUOTENAME(@houseprices) + '
    SET ' + QUOTENAME(c.name) + ' = COALESCE(CAST(' + QUOTENAME(c.name) + ' AS float), 0)
'
FROM sys.columns c
WHERE c.object_id = OBJECT_ID(@houseprices)
AND c.column_id > 1;  -- Skip first column

EXEC sp_executesql @sql;
*/
------------------------------------------------------------------------

--Identifying duplicate rows
/*
SELECT *
FROM houseprices
WHERE DATES LIKE '2000-01%';
*/
------------------------------------------------------------------------

--Deleting Duplicate Rows
/*
WITH CTE AS (
    SELECT 
        *, 
        ROW_NUMBER() OVER (PARTITION BY Alabama, Alaska, Arizona, Arkansas, California, Colorado, Connecticut, Delaware, [the District of Columbia], Florida, Georgia, Hawaii, Idaho, Illinois, Indiana, Iowa, 
										Kansas, Kentucky, Louisiana, Maine, Maryland, Massachusetts, Michigan, Minnesota, Mississippi, Missouri, Montana, Nebraska, Nevada, 
										[New Hampshire], [New Jersey], [New Mexico], [New York], [North Carolina], [North Dakota], Ohio, Oklahoma, Oregon, Pennsylvania, [Rhode Island], 
										[South Carolina], [South Dakota], Tennessee, Texas, Utah, Vermont, Virginia, Washington, [West Virginia], Wisconsin, Wyoming
                           ORDER BY (SELECT NULL)) AS RowNum
    FROM houseprices
)
DELETE FROM CTE
WHERE RowNum > 1;
*/
------------------------------------------------------------------------------

--Sort Data by Month
/*
SELECT *
FROM houseprices
ORDER BY YEAR(DATES), MONTH(DATES);
*/


--EXPORT Data using SQL Server Import and Export Wizard

