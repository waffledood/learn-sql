# learn-sql
A personal repository to collate my learnings for SQL!

# Basic SQL Commands 

## SELECT
The `SELECT` command allows users to specify which columns from the table they wish to query in the results.

```sql
SELECT
*
FROM inventory_records;
```

The above SQL statement selects all columns (`*` operator) from the `inventory_records` table.

```sql
SELECT
item_name, item_type
FROM inventory_records;
```

The above SQL statement selects 2 columns (`item_name`, `item_type`) from the `invetory_records` table.

## LIMIT 
The `LIMIT` command allows users to limit the number of rows (integer value) queried in the results. This might be particularly useful in cases where the size of the table is huge.

```sql
SELECT
*
FROM inventory_records
LIMIT 100;
```

The above SQL statement returns a query with 100 rows of data.

## WHERE 
The `WHERE` command allows users to specify conditional statements for the queries.

```sql
SELECT
*
FROM inventory_records
WHERE item_quantity >= 10;
```

## Comparison Operators 
The comparison operators used in SQL are: 
- `>`   greater than
- `<`   less than
- `>=`  greater than or equal to
- `<=`  less than or equal to
- `=`   equal to
- `!=`  not equal to
