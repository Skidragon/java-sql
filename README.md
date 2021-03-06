# Introduction

Working with SQL

# Instructions

Surf to [SQL Try Editor at W3Schools.com](https://www.w3schools.com/Sql/tryit.asp?filename=trysql_select_top)  
Answer the following data queries. Keep track of the SQL you write by pasting it into this document under its appropriate header below. You will be submitting that through the regular fork, change, pull process.

### **Clicking the `Restore Database` button in the page will repopulate the database with the original data and discard all changes you have made**.

### find all customers that live in London. Returns 6 records.

```
SELECT *
FROM customers
WHERE country = "London"
```

### find all customers with postal code 1010. Returns 3 customers.

```
SELECT *
FROM customers
WHERE postalcode = 1010
```

### find the phone number for the supplier with the id 11. Should be (010) 9984510.

```
SELECT phone
FROM suppliers
WHERE supplierid = 11
```

### list orders descending by the order date. The order with date 1997-02-12 should be at the top.

```
SELECT *
FROM Orders
ORDER BY OrderDate DESC
```

### find all suppliers who have names longer than 20 characters. You can use `length(SupplierName)` to get the length of the name. Returns 11 records.

```
SELECT *
FROM Suppliers
WHERE length(SupplierName) > 20
```

### find all customers that include the word "market" in the name. Should return 4 records.

```
SELECT *
FROM Customers
WHERE CustomerName LIKE "%market%"
```

### add a customer record for _"The Shire"_, the contact name is _"Bilbo Baggins"_ the address is _"1 Hobbit-Hole"_ in _"Bag End"_, postal code _"111"_ and the country is _"Middle Earth"_.

```
INSERT INTO customers(CustomerName, ContactName, Address, PostalCode, Country)
VALUES ("The Shire", "Bilbo Baggins", "1 Hobbit-Hole in Bag End", "111", "Middle Earth")
```

### update _Bilbo Baggins_ record so that the postal code changes to _"11122"_.

```
UPDATE customers
SET postalcode = "11122"
WHERE ContactName = "Bilbo Baggins"
```

### list orders grouped by customer showing the number of orders per customer. _Rattlesnake Canyon Grocery_ should have 7 orders.

```
SELECT c.customername as CustomerName, COUNT(o.customerid) as TotalOrders
FROM customers as c
INNER JOIN orders as o
ON c.customerid = o.customerid
GROUP BY c.customername
```

### list customers names and the number of orders per customer. Sort the list by number of orders in descending order. _Ernst Handel_ should be at the top with 10 orders followed by _QUICK-Stop_, _Rattlesnake Canyon Grocery_ and _Wartian Herkku_ with 7 orders each.

```
SELECT c.customername as CustomerName, COUNT(o.customerid) as TotalOrders
FROM customers as c
INNER JOIN orders as o
ON c.customerid = o.customerid
GROUP BY c.customername
ORDER BY COUNT(o.customerid) DESC
```

### list orders grouped by customer's city showing number of orders per city. Returns 58 Records with _Aachen_ showing 2 orders and _Albuquerque_ showing 7 orders.

```
SELECT c.city as City, COUNT(o.customerid) as TotalOrders
FROM customers as c
INNER JOIN orders as o
ON c.customerid = o.customerid
GROUP BY c.city
```

### delete all customers that have no orders. Should delete 17 (or 18 if you haven't deleted the record added) records.

```
DELETE FROM Customers
WHERE CustomerID NOT IN (SELECT CustomerID FROM Orders)
```

## Create Database and Table

### Keep track of the code you write and paste at the end of this document

- use [`SQLite Studio`](https://sqlitestudio.pl/index.rvt) to create a database, name it `budget.sqlite3`.
- add an `accounts` table with the following _schema_:

  - `id`, numeric value with no decimal places that should autoincrement.
  - `name`, string, add whatever is necessary to make searching by name faster.
  - `budget` numeric value.

- constraints
  - the `id` should be the primary key for the table.
  - account `name` should be unique.
  - account `budget` is required.
