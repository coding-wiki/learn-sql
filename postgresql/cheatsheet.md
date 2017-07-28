# PostgreSQL Cheatsheet


### SELECT
```sql
SELECT * FROM table_name;
SELECT id FROM table_name;
SELECT id, random_row FROM table_name;

SELECT * FROM table_name WHERE random_row = 5;

SELECT * FROM table_name WHERE id IN (1,2);

SELECT name, 
	CASE WHEN (percentage > 50) THEN
		'large'
	ELSE
		'small'
	END AS size
	FROM table_name; 

-- Where table_name is the name of the SQL table
```