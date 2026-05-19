# SQL Practice Notes

---

# Create Database

```sql
CREATE DATABASE flipcart_db;
```

---

# Create Products Table

```sql
CREATE TABLE products(
  product_id BIGSERIAL PRIMARY KEY,
  name VARCHAR(100) NOT NULL,
  sku_code VARCHAR(8) UNIQUE NOT NULL CHECK (sku_code ~ '^[A-Z0-9]{8}$'),
  price NUMERIC(10,2) CHECK (price > 0),
  stock_quantity INT DEFAULT 0 CHECK (stock_quantity >= 0),
  is_available VARCHAR CHECK(is_available IN ('yes','no')),
  category TEXT NOT NULL,
  adden_on DATE DEFAULT CURRENT_DATE,
  last_update TIMESTAMP DEFAULT NOW()
);
```

---

# Restart Sequence

```sql
ALTER SEQUENCE products_product_id_seq
RESTART WITH 1001;
```

---

# Insert Data

```sql
INSERT INTO products (name, sku_code, price , stock_quantity, is_available, category)
VALUES
('Wireless Mouse', 'WM123456', 699.99, 50, 'yes', 'Electronics'),
('Bluetooth Speaker', 'BS234567', 1499.00, 30, 'yes', 'Electronics');
```

---

# View All Products

```sql
SELECT * FROM products;
```

---

# Test 1 : Basics

## Display name and price

```sql
SELECT name, price FROM products;
```

## Electronics Products

```sql
SELECT * FROM products
WHERE category='Electronics';
```

## Group By Category

```sql
SELECT category FROM products
GROUP BY category;
```

## Categories Having More Than 1 Product

```sql
SELECT category, COUNT(*)
FROM products
GROUP BY category
HAVING COUNT(*) > 1;
```

## Sort By Price Ascending

```sql
SELECT * FROM products
ORDER BY price ASC;
```

## First 3 Products

```sql
SELECT * FROM products
LIMIT 3;
```

## Column Aliases

```sql
SELECT name AS item_name,
price AS item_price
FROM products;
```

## Unique Categories

```sql
SELECT DISTINCT category
FROM products;
```

---

# Test 2 : Clauses and Aggregation

## Cheapest Product

```sql
SELECT name, price
FROM products
WHERE price = (
    SELECT MIN(price)
    FROM products
);
```

## Average Price

```sql
SELECT ROUND(AVG(price),2)
FROM products
WHERE category IN ('Fitness','Home & Kitchen');
```

## Available Products With Conditions

```sql
SELECT name, stock_quantity
FROM products
WHERE is_available='yes'
AND stock_quantity > 50
AND NOT price = 299;
```

## Most Expensive Product By Category

```sql
SELECT category,
MAX(price) AS max_price
FROM products
GROUP BY category;
```

## Uppercase Categories

```sql
SELECT DISTINCT UPPER(category) AS new_cat
FROM products
ORDER BY new_cat DESC;
```

## Price Between 500 and 1500

```sql
SELECT *
FROM products
WHERE price BETWEEN 500 AND 1500;
```

---

# String Functions

## Lowercase SKU

```sql
SELECT LOWER(sku_code)
FROM products;
```

## Uppercase SKU

```sql
SELECT UPPER(sku_code)
FROM products;
```

## Length of SKU

```sql
SELECT LENGTH(sku_code)
FROM products;
```

## Substring

```sql
SELECT SUBSTRING(sku_code,3,8)
FROM products;
```

## LEFT Function

```sql
SELECT LEFT(sku_code,2)
FROM products;
```

## RIGHT Function

```sql
SELECT RIGHT(sku_code,6)
FROM products;
```

## CONCAT

```sql
SELECT CONCAT(name,' ',category)
FROM products;
```

## CONCAT_WS

```sql
SELECT CONCAT_WS(' ',name,category,price)
FROM products;
```

## TRIM

```sql
SELECT TRIM('   hey arun');
```

## REPLACE

```sql
SELECT REPLACE(sku_code,LEFT(sku_code,2),'GG')
FROM products;
```

---

# ALTER Commands

## Create Database

```sql
CREATE DATABASE DB1_Alt;
```

## Create Table

```sql
CREATE TABLE workers(
name VARCHAR(50) PRIMARY KEY,
age BIGINT
);
```

## Add Column

```sql
ALTER TABLE workers
ADD COLUMN mobile BIGINT;
```

## Insert Values

```sql
INSERT INTO workers(name,age,mobile)
VALUES('Arun',20,8000450949),
('Dev',23,7498754438);
```

## Rename Column

```sql
ALTER TABLE workers
RENAME COLUMN mobile TO phone;
```

## Change Data Type

```sql
ALTER TABLE workers
ALTER COLUMN phone TYPE VARCHAR(10);
```

## Set Default

```sql
ALTER TABLE workers
ALTER COLUMN age SET DEFAULT 18;
```

## Drop Default

```sql
ALTER TABLE workers
ALTER COLUMN age DROP DEFAULT;
```

## Add Constraint

```sql
ALTER TABLE workers
ADD CONSTRAINT chech_age CHECK(age>=0);
```

## Drop Constraint

```sql
ALTER TABLE workers
DROP CONSTRAINT chech_age;
```

## Drop Column

```sql
ALTER TABLE workers
DROP COLUMN phone;
```

## Rename Table

```sql
ALTER TABLE workers
RENAME TO worker;
```

## View Table

```sql
SELECT * FROM worker;
```

---

# CASE Statements

## Temporary Column Using CASE

```sql
SELECT 
    name,
    is_available,
    CASE 
        WHEN is_available = 'yes' THEN 'In stock'
        ELSE 'Out of stock'
    END AS availability_status
FROM products;
```

---

## Stock Label Classification

```sql
SELECT 
    name,
    stock_quantity,
    CASE 
        WHEN stock_quantity >= 100 THEN 'High stock'
        WHEN stock_quantity BETWEEN 50 AND 100 THEN 'Medium stock'
        ELSE 'Low stock'
    END AS label
FROM products;
```

---

# Permanent Column Using ALTER + UPDATE

## Add New Column

```sql
ALTER TABLE products
ADD COLUMN price_tag TEXT;
```

## Update Column Values Using CASE

```sql
UPDATE products
SET price_tag =
CASE 
    WHEN price >= 1000 THEN 'expensive'
    WHEN price BETWEEN 500 AND 1000 THEN 'average'
    ELSE 'cheap'
END;
```