# SQL Joins

## Create Database

```sql
create database joins_practice;
```

## Create Customer Table

```sql
create table customer(
    customer_id bigserial primary key,
    customer_name varchar(50) 
);
```

## Create Orders Table

```sql
create table orders(
    order_id bigserial primary key,
    product_name varchar(50),
    price bigint,
    customer_id bigint references customer(customer_id)
);
```

## Insert Data into Customer Table

```sql
insert into customer (customer_name)
values ('Arun'),('Rahul'),('Krish'),('Dev');
```

## Insert Data into Orders Table

```sql
insert into orders (product_name,price,customer_id)
values
('TV',40000,2),
('Phone',20000,1),
('Washing Machine',60000,3),
('Laptop',50000,1),
('Fridge',70000,2);
```

## INNER JOIN

```sql
select c.customer_name, o.product_name, o.price 
from customer c 
inner join orders o 
on c.customer_id = o.customer_id;
```

## LEFT JOIN

```sql
select c.customer_name, o.product_name, o.price 
from customer c 
left join orders o 
on c.customer_id = o.customer_id;
```

## RIGHT JOIN

```sql
select c.customer_name, o.product_name, o.price 
from customer c 
right join orders o 
on c.customer_id = o.customer_id;
```

## CROSS JOIN

```sql
select c.customer_name, o.product_name, o.price 
from customer c 
cross join orders o;
```

## Display Customer Table

```sql
select * from customer;
```

## Display Orders Table

```sql
select * from orders;
```