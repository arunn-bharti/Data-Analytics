CREATE DATABASE flipcart_db;

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

  
ALTER SEQUENCE products_product_id_seq
RESTART WITH 1001;

INSERT INTO products (name, sku_code, price , stock_quantity, is_available, category)
VALUES
('Wireless Mouse', 'WM123456', 699.99, 50, 'yes', 'Electronics'),
('Bluetooth Speaker', 'BS234567', 1499.00, 30, 'yes', 'Electronics'),
('Laptop Stand', 'LS345678', 799.50, 20, 'yes', 'Accessories'),
('USB-C Hub', 'UC456789', 1299.99, 15, 'yes', 'Accessories'),
('Notebook', 'NB567890', 99.99, 100, 'yes', 'Stationery'),
('Pen Set', 'PS678901', 199.00, 200, 'no', 'Stationery'),
('Coffee Mug', 'CM789012', 299.00, 75, 'yes', 'Home & Kitchen'),
('LED Desk Lamp', 'DL890123', 899.00, 00, 'no', 'Home & Kitchen'),
('Yoga Mat', 'YM901234', 499.00, 25, 'yes', 'Fitness'),
('Water Bottle', 'WB012345', 349.00, 60, 'yes', 'Fitness');


select * from products;



Test 1 Basics :

#1) display name and price of all table.

select name, price from products;


#2) Show all products where the category is 'Electronics'.

select * from products
where category='Electronics';


#3) Group products by category. Show each category once.

select category from products
group by category;


#4) Show categories that have more than 1 product.

select category, COUNT(*) from products
group by category
having COUNT(*)>1;


#5) Show all products sorted by price in ascending order.

select * from products
order by  price asc;


#6) Show only the first 3 products from the table.

select * from products
limit 3;


#7) Show product name as "Item_Name" and price as "Item_Price".

select name as item_name, price as item_price from products;


#8) Show all the unique categories from the products table

SELECT DISTINCT category FROM products;




#Test 2 : clauses n aggregation 


#1) Display the name and price of the cheapest product in the entire table.

select name, price from products
where price=(select min(price) from products);


#2) Find the average price of products that belong to the 'Home & Kitchen' or 'Fitness' category.

select round(avg(price),2) from products 
where category in ('Fitness','Home & Kitchen');


#3) Show product names and stock quantity where: the product is available, stock is more than 50, and price is not equal to ₹299.

select name,stock_quantity from products
where is_available='yes' and stock_quantity>50 and not price=299;


#4) Find the most expensive product in each category (name and price).

select category,max(price) as max_price from products
group by category;


#5) Show all unique categories in uppercase, sorted in descending order.

select distinct upper(category) as new_cat from products
order by new_cat desc;


#6) Display products where price between 500-1500.

select * from products
where price between 500 and 1500;





/* String Functions */
(String indexing starts from 1)


select lower(sku_code) as lower_sku from products;

select upper(sku_code) as upper_sku from products;

select length(sku_code) as length_of_sku from products;


select substring(sku_code,3,8) from products;

select left(sku_code,2) from products;

select right(sku_code,6) from products;


select concat(name,' ',category) from products;

select concat_ws(' ',name,category,price) from products;


select trim('   hey arun');

select replace(sku_code,left(sku_code,2),'GG') from products;
