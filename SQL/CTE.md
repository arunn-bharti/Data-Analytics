

## CTE (Common Table Expression)

A CTE is a temporary result set that can be referenced inside another query.

Syntax:

```sql
WITH cte_name AS (
    query
)
SELECT *
FROM cte_name;
```


## Example : Join Using CTE

```sql
WITH cte1 AS (
    SELECT *
    FROM products p
    JOIN orders o
    ON o.product_id = p.product_id
)

SELECT order_id, price
FROM cte1;
```

---


## Why Use CTE?

- Makes queries cleaner
- Improves readability
- Helps break complex queries into parts
- Useful in recursive queries
- Easier debugging than nested subqueries