# learn-sql
A personal repository to collate my learnings for SQL!

# Basic SQL Commands 

## SELECT
The `SELECT` command allows users to specify which columns from the table they wish to query in the results.

```sql
SELECT * FROM inventory_records;
```

The above SQL statement selects all columns (`*` operator) from the `inventory_records` table.

```sql
SELECT item_name, item_type FROM inventory_records;
```

The above SQL statement selects 2 columns (`item_name`, `item_type`) from the `invetory_records` table.


