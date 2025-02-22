# E-Commerce Database Management Project

## 📌 Project Overview
As a part of our **Database Management Systems (DBMS)** course, I developed this **E-Commerce Database Management Project (DBMD)**. This project contains both **theoretical concepts** and **SQL implementation** to efficiently manage an e-commerce platform.

## 📂 Contents
- [Project Description](#project-description)
- [Basic Structure](#basic-structure)
  - Functional Requirements
  - Relational Database Schema
- [Implementation](#implementation)
  - Creating Tables
  - Inserting Data
- [Pre-requisites](#pre-requisites)

---

## 📖 Project Description
This **E-Commerce Database Management Project (DBMD)** is designed to streamline and optimize various aspects of an **online shopping platform**. The database supports **customer information, product inventory, orders, reviews, payments**, and more.



![Screenshot 2025-02-22 at 19 12 56](https://github.com/user-attachments/assets/dcf41bff-8037-4918-b540-e6bd4fd91526)





## 🛠️ Pre-requisites
To run this project, you need:
- **MySQL Database Server**

---

## 🚀 Create Schema (Database) in MySQL
```sql
CREATE SCHEMA e_commerce;
```

---

## 📋 Create Tables
### Customer Table
```sql
CREATE TABLE e_commerce.customer (
  customer_id INT PRIMARY KEY,
  FirstName VARCHAR(50),
  MiddleName VARCHAR(50),
  LastName VARCHAR(50),
  Email VARCHAR(100),
  DateOfBirth DATE,
  phone INT,
  age INT NULL
);
```

### Category Table
```sql
CREATE TABLE e_commerce.category (
  category_id INT PRIMARY KEY,
  category_name VARCHAR(255),
  Description VARCHAR(255)
);
```

### Seller Table
```sql
CREATE TABLE e_commerce.seller (
  seller_id INT PRIMARY KEY,
  seller_name VARCHAR(255),
  seller_phone INT,
  total_sales FLOAT
);
```

### Address Table
```sql
CREATE TABLE e_commerce.address (
  address_id INT PRIMARY KEY,
  apart_no INT,
  apart_name VARCHAR(255),
  streetname VARCHAR(255),
  state VARCHAR(255),
  city VARCHAR(255),
  pincode INT,
  customer_id INT,
  FOREIGN KEY (customer_id) REFERENCES customer(customer_id) ON DELETE CASCADE ON UPDATE NO ACTION
);
```

### Product Table
```sql
CREATE TABLE e_commerce.product (
  product_id INT PRIMARY KEY,
  product_name VARCHAR(50),
  MRP FLOAT,
  stock BOOL,
  brand VARCHAR(255),
  category_id INT,
  seller_id INT,
  FOREIGN KEY (category_id) REFERENCES category(category_id) ON DELETE SET NULL ON UPDATE NO ACTION,
  FOREIGN KEY (seller_id) REFERENCES seller(seller_id) ON DELETE SET NULL ON UPDATE NO ACTION
);
```

### Cart Table
```sql
CREATE TABLE e_commerce.cart (
  cart_id INT PRIMARY KEY,
  grandtotal FLOAT,
  itemtotal INT,
  customer_id INT,
  FOREIGN KEY (customer_id) REFERENCES customer(customer_id) ON DELETE SET NULL ON UPDATE NO ACTION,
  product_id INT,
  FOREIGN KEY (product_id) REFERENCES product(product_id) ON DELETE SET NULL ON UPDATE NO ACTION
);
```

### Review Table
```sql
CREATE TABLE e_commerce.review (
  review_id INT PRIMARY KEY,
  description VARCHAR(255),
  rating ENUM('1','2','3','4','5'),
  customer_id INT,
  FOREIGN KEY (customer_id) REFERENCES customer(customer_id) ON DELETE SET NULL ON UPDATE NO ACTION,
  product_id INT,
  FOREIGN KEY (product_id) REFERENCES product(product_id) ON DELETE SET NULL ON UPDATE NO ACTION
);
```

### Order Table
```sql
CREATE TABLE e_commerce.order_table (
  order_id INT PRIMARY KEY,
  order_date DATETIME,
  order_amount FLOAT,
  order_status ENUM('delivery','not delivery'),
  shipping_date DATETIME,
  customer_id INT,
  FOREIGN KEY (customer_id) REFERENCES customer(customer_id) ON DELETE SET NULL ON UPDATE NO ACTION,
  cart_id INT,
  FOREIGN KEY (cart_id) REFERENCES cart(cart_id) ON DELETE SET NULL ON UPDATE NO ACTION
);
```

### OrderItem Table
```sql
CREATE TABLE e_commerce.orderitem (
  order_id INT,
  product_id INT,
  FOREIGN KEY (order_id) REFERENCES order_table(order_id) ON DELETE SET NULL ON UPDATE NO ACTION,
  FOREIGN KEY (product_id) REFERENCES product(product_id) ON DELETE SET NULL ON UPDATE NO ACTION,
  MRP FLOAT,
  quantity INT
);
```

### Payment Table
```sql
CREATE TABLE e_commerce.payment (
  paymentMode ENUM('online','offline'),
  dateofpayment DATETIME,
  order_id INT,
  FOREIGN KEY (order_id) REFERENCES order_table(order_id) ON DELETE SET NULL ON UPDATE NO ACTION,
  customer_id INT,
  FOREIGN KEY (customer_id) REFERENCES customer(customer_id) ON DELETE SET NULL ON UPDATE NO ACTION
);
```

---

## 📥 Insert Data
### Insert into Customer Table
```sql
INSERT INTO e_commerce.customer VALUES (1, 'Merab', 'The Machine', 'Dvalishvili', 'merat.dvalishvili@gmail.com', '2004-09-06', 2147483647, 0);
INSERT INTO e_commerce.customer VALUES (2, 'Ilia', 'El Matador', 'Topuria', 'Topuria.ilia@gmail.com', '2004-05-23', 2147483647, 0);
INSERT INTO e_commerce.customer VALUES (3, 'Khabib', 'The Eagle', 'Nurmagomedov', 'khabib.nurmagomedov@gmail.com', '2004-05-02', 2147483647, 0);
```

### Insert into Category Table
```sql
INSERT INTO e_commerce.category VALUES (1, 'Mobiles & Computers', 'All major brands of phones, tablets, PCs, and desktops');
INSERT INTO e_commerce.category VALUES (2, 'TV & Appliances & Electronics', 'Smart TVs, OLEDs, Mixers, and more');
INSERT INTO e_commerce.category VALUES (3, 'Men’s Fashion', 'T-shirts, jeans, shirts, etc.');
INSERT INTO e_commerce.category VALUES (4, 'Women’s Fashion', 'Dresses, kurtis, T-shirts, jeans, etc.');
```

### Category Table
```sql
INSERT INTO e_commerce.category VALUES (1,'Mobiles & Computer','all the brands are there like phone, tablets, PC, Desktop');
INSERT INTO e_commerce.category VALUES (2,'TV & Appliances & Electronics','all the brands are there like tv smart, tv oled, mixer and many more');
INSERT INTO e_commerce.category VALUES (3,'Men`s Fashion','all the brands are there like t-Shirts, jeans, shirts, etc');
INSERT INTO e_commerce.category VALUES (4,'Women`s Fashion','all the brands are there like shorts, one piece, kurti, t-shirt, jeans, etc');
```

### Seller Table
```sql
INSERT INTO e_commerce.seller VALUES (1,'Magamed Imamguliev','1295874636',12000.75);
INSERT INTO e_commerce.seller VALUES (2,'Vazir Imamguliev','786542355',3800.20);
INSERT INTO e_commerce.seller VALUES (4, 'Gulbeniz Imamguliev','746545456',8529.23);
```

### Address Table
```sql
INSERT INTO e_commerce.address VALUES (1,'108','Dirsi Complex','Shota Nadirashvili Street','Kvemo Qartli','Tbilisi','400066',1);
INSERT INTO e_commerce.address VALUES (2,'214','Orbi City','Shota Rustaveli Street','Ajara','Batumi','400801',2);
INSERT INTO e_commerce.address VALUES (3,'52','Barcelo Tbilisi','Baratashvili Street','Kvemo Qartli','Tbilisi','400526',3);
```

### Product Table
```sql
INSERT INTO e_commerce.product VALUES(1,'pen drive',250,52,'hp',2,1);
INSERT INTO e_commerce.product VALUES(2,'monitor',25000,30,'dell',1,3);
INSERT INTO e_commerce.product VALUES(3,'keyboard',765,69,'lenovo',2,2);
INSERT INTO e_commerce.product VALUES(4,'i phone 15',75000,10,'Apple',1,2);
INSERT INTO e_commerce.product VALUES(5,'Mens t-shirts',350,22,'H&M',3,1);
INSERT INTO e_commerce.product VALUES(6,'mens kurta',766,32,'ZARA',3,3);
INSERT INTO e_commerce.product VALUES(7,'women shorts',360,52,'pantaloons',4,2);
INSERT INTO e_commerce.product VALUES(8,'women jeans',699,65,'zudio',4,1);
INSERT INTO e_commerce.product VALUES(9,'mouse',299,65,'lenovo',2,3);
INSERT INTO e_commerce.product VALUES(10,'desktop',25000,10,'dell',1,2);
```

### Cart Table
```sql
INSERT INTO e_commerce.cart VALUES (1,75000,1,1,4);
INSERT INTO e_commerce.cart VALUES (2,1050,3,2,5);
INSERT INTO e_commerce.cart VALUES (3,598,2,3,9);
INSERT INTO e_commerce.cart VALUES (4,2160,6,2,7);
INSERT INTO e_commerce.cart VALUES (5,250,1,1,1);
INSERT INTO e_commerce.cart VALUES (6,3830,6,3,6);
```

### Order Table
```sql
INSERT INTO e_commerce.order_table VALUES (1,'2023-12-06 10:12:20',75000,'delivery','2023-12-09 09:25:02',1,1);
INSERT INTO e_commerce.order_table VALUES (2,'2023-12-07 20:23:20',1050,'delivery','2023-12-12 05:29:02',2,2);
INSERT INTO e_commerce.order_table VALUES (3,'2023-12-08 18:12:20',598,'delivery','2023-12-23 09:26:02',3,3);
INSERT INTO e_commerce.order_table VALUES (4,'2023-12-10 15:45:20',2160,'delivery','2023-12-15 11:26:02',2,4);
INSERT INTO e_commerce.order_table VALUES (5,'2023-12-10 15:45:20',250,'delivery','2023-12-15 11:26:02',1,5);
INSERT INTO e_commerce.order_table VALUES (6,'2023-12-21 16:23:20',3830,'delivery','2023-12-29 11:35:09',3,6);
```

### Order Item Table
```sql
INSERT INTO e_commerce.orderitem VALUES (7500,1,1,4);
INSERT INTO e_commerce.orderitem VALUES (1050,3,2,5);
INSERT INTO e_commerce.orderitem VALUES (299,2,3,9);
INSERT INTO e_commerce.orderitem VALUES (360,6,4,7);
INSERT INTO e_commerce.orderitem VALUES (250,1,5,1);
INSERT INTO e_commerce.orderitem VALUES (766,6,6,6);
```

### Payment Table
```sql
INSERT INTO e_commerce.payment VALUES ('online','2023-12-06 10:12:56',1,1,1);
INSERT INTO e_commerce.payment VALUES ('online','2023-12-07 20:23:20',2,2,2);
INSERT INTO e_commerce.payment VALUES ('online','2023-12-08 18:12:20',3,3,3);
INSERT INTO e_commerce.payment VALUES ('online','2023-12-10 15:45:20',4,2,4);
INSERT INTO e_commerce.payment VALUES ('online','2023-12-10 15:45:20',5,1,5);
INSERT INTO e_commerce.payment VALUES ('online','2023-12-21 16:23:20',6,3,6);
```

### Review Table
```sql
INSERT INTO e_commerce.review VALUES (1,'i phone 15 is amazing.','5',1,4);
INSERT INTO e_commerce.review VALUES (2,'wow t-shirts, good in quality.','3',2,5);
INSERT INTO e_commerce.review VALUES (3,'best mouse in the world.','4',3,9);
INSERT INTO e_commerce.review VALUES (4,'very comfortable in size and quality.','4',2,7);
INSERT INTO e_commerce.review VALUES (5,'the size is 128mb pendrive, speed is good.','5',1,1);
INSERT INTO e_commerce.review VALUES (6,'size of kurta and quality is good','2',3,6);
```

## 🚀 Run the Project
1. Open MySQL and create the database using:
   ```sh
   ./mysql -u root -p
   CREATE SCHEMA e_commerce;
   ```
2. Copy and execute the SQL scripts for tables and data insertion.
3. Run queries to test the database functionalities.

---

## 💡 Future Improvements
- Implement stored procedures for optimized queries.
- Add triggers for automatic updates.
- Integrate a front-end for user interaction.

---

## 👨‍💻 Author
- **Magamed Imamguliev**  

Feel free to contribute or suggest improvements!

---
