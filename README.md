### SQL CLEANING
This is a project on data cleaning by using SQL. There is a database in the file name* club_member_info.csv *. And there are some tasks request me using SQL to work with data.
##### Task 1

- Get the 10 first rows from the table club_member_info using SQL console:
```sql
SELECT *
FROM club_member_info
LIMIT 10;
```
- And here is the result:


|full_name|age|martial_status|email|phone|full_address|job_title|membership_date|
|---------|---|--------------|-----|-----|------------|---------|---------------|
|addie lush|40|married|alush0@shutterfly.com|254-389-8708|3226 Eastlawn Pass,Temple,Texas|Assistant Professor|7/31/2013|
|      ROCK CRADICK|46|married|rcradick1@newsvine.com|910-566-2007|4 Harbort Avenue,Fayetteville,North Carolina|Programmer III|5/27/2018|
|Sydel Sharvell|46|divorced|ssharvell2@amazon.co.jp|702-187-8715|4 School Place,Las Vegas,Nevada|Budget/Accounting Analyst I|10/6/2017|
|Constantin de la cruz|35||co3@bloglines.com|402-688-7162|6 Monument Crossing,Omaha,Nebraska|Desktop Support Technician|10/20/2015|
|  Gaylor Redhole|38|married|gredhole4@japanpost.jp|917-394-6001|88 Cherokee Pass,New York City,New York|Legal Assistant|5/29/2019|
|Wanda del mar       |44|single|wkunzel5@slideshare.net|937-467-6942|10864 Buhler Plaza,Hamilton,Ohio|Human Resources Assistant IV|3/24/2015|
|Joann Kenealy|41|married|jkenealy6@bloomberg.com|513-726-9885|733 Hagan Parkway,Cincinnati,Ohio|Accountant IV|4/17/2013|
|   Joete Cudiff|51|divorced|jcudiff7@ycombinator.com|616-617-0965|975 Dwight Plaza,Grand Rapids,Michigan|Research Nurse|11/16/2014|
|mendie alexandrescu|46|single|malexandrescu8@state.gov|504-918-4753|34 Delladonna Terrace,New Orleans,Louisiana|Systems Administrator III|3/12/1921|
| fey kloss|52|married|fkloss9@godaddy.com|808-177-0318|8976 Jackson Park,Honolulu,Hawaii|Chemical Engineer|11/5/2014|
##### Task 2
- Make a copy of the table, named it club_member_info_cleaned: 
Right click on the table name -> Choose the "Generate SQL" option -> Choose the "DDL" option;
Copy the SQL code that is generated for you;
```sql
CREATE TABLE club_member_info_cleaned (
	full_name VARCHAR(50),
	age INTEGER,
	martial_status VARCHAR(50),
	email VARCHAR(50),
	phone VARCHAR(50),
	full_address VARCHAR(50),
	job_title VARCHAR(50),
	membership_date VARCHAR(50)
```
Put this code to SQL console, change the table name to "club_member_info_cleaned" and run it.
New copied table is a blank table. Then copy all values from original table to new one using INSERT INTO SELECT statement:
```sql
INSERT INTO club_member_info_cleaned
SELECT *
FROM club_member_info;
```
Then refresh to get data updated.

##### Task 3 - CLEAN THE DATA
- Inconsistent letter case and leading and trailing whitespaces:
```sql
SELECT trim(lower(full_name)) AS fullname, age, martial_status, email, phone, full_address, job_title, membership_date
FROM club_member_info_cleaned;
```
Then refresh to get data updated.
- Age out of realistic range: 
  Find the median age of the members:
```sql
SELECT median(age)
FROM club_member_info_cleaned;
```
  And we found the median age is 41.
  Then we will replace the age out of realistic range (>100) with the median age (41)
```sql
UPDATE club_member_info_cleaned
SET age = (SELECT median(age)
		   FROM club_member_info_cleaned
		   )
WHERE age > 100
;
```
Then refresh to get data updated.

###End
