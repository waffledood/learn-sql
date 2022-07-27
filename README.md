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

## Logical Operators 

### LIKE, ILIKE
The LIKE logical operator is used to match on similar values, not exact values (think of it like regular expression).
The ILIKE logical opereator is similar to LIKE, except it ignores case.
Note:
- when using either `LIKE` or `ILIKE`, the column name must be quoted in double quotation marks `"`

```sql
SELECT
*
FROM inventory_records
WHERE "item_name" LIKE '%chocolate%';
```

```sql
SELECT
*
FROM inventory_records
WHERE "item_name" ILIKE '%Coca Cola%';
```

### IN
The IN logical operator is used to match from a pool of values.

```sql
SELECT
*
FROM inventory_records
WHERE item_name IN ('butter', 'candy', 'bread');
```

### BETWEEN
The BETWEEN logical operator is used to match from a range of values.
Note:
- BETWEEN operator is always coupled with the AND operator 
- the bounds for BETWEEN is inclusive (meaning `BETWEEN 10 AND 20` is equals to `>= 10 AND <= 20`) 

```sql
SELECT
*
FROM inventory_records
WHERE item_quantity BETWEEN 10 AND 20;
```

### IS NULL
The IS NULL operator is used to check for columns with null values. Accordingly, the user may wish to filter for null or non-null values.

```sql
SELECT
*
FROM inventory_records
WHERE item_name IS NULL;
```

```sql
SELECT
*
FROM inventory_records
WHERE item_name IS NOT NULL;
```

### AND
The AND operator is used to filter for rows that meet both conditional statements.

```sql
SELECT
*
FROM inventory_records
WHERE item_quantity >= 10 AND item_name IS NOT NULL;
```

