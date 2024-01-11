# Step 2: Database Design and Setup

Ensure that XAMPP has been installed on your machine before proceeding, and design the MySQL database for our Flask application.


```
## Entity-Relationship Diagram (ERD) - Text Representation

### Entities
1. **Products**
   - `product_id` (PK)
   - `name`
   - `unit`
   - `price_per_unit`
   - `image_url`

2. **Orders**
   - `order_id` (PK)
   - `total_price`
   - `date_time`
   - `customer_contact`

3. **Order Items**
   - `order_item_id` (PK)
   - `order_id` (FK to Orders)
   - `product_id` (FK to Products)
   - `quantity`
   - `price`

### Relationships
- **Products to Order Items**
  - One (Product) to Many (Order Items)
  - A single product can appear in multiple order items.

- **Orders to Order Items**
  - One (Order) to Many (Order Items)
  - A single order can include multiple order items.

### ERD Diagram

```plaintext
+--------------------------------+      +--------------------------------+
|            Products            |      |           Order Items          |
+--------------------------------+      +--------------------------------+
| product_id (PK)                |1    | product_id (FK to Products)    |M
| name                           |<-----| order_id (FK to Orders)        |
| unit                           |      | order_item_id (PK)             |
| price_per_unit                 |      | quantity                       |
| image_url                      |      | price                          |
+--------------------------------+      +--------------------------------+
                                             |
                                             |1
                                             |
                                             v
                                     +-------------------------+
                                     |          Orders         |
                                     +-------------------------+
                                     | order_id (PK)           |M
                                     | total_price             |
                                     | date_time               |
                                     | customer_contact        |
                                     +-------------------------+


```
[🎥 **Watch the Database design and Setup Part 1 Here**](http://tinyurl.com/bdswtt8n)

This format includes a clear definition of the relationships between the entities, highlighting the one-to-many nature of the connections between `Products` and `Order Items`, and `Orders` and `Order Items`.
## 2.1 Designing the SQL Schema
We will define the schema for our database, which includes creating the database and tables for products, orders, and order items.

[🎥 **Watch the Database design and Setup Part 2 Method # 1 Here**](http://tinyurl.com/4vnr4xe2)


[🎥 **Watch the Database design and Setup Part 3 Method # 2 Here**](http://tinyurl.com/563yme7w)
### SQL Schema Creation:

```sql
CREATE DATABASE yourname_kiosk;

USE yourname_kiosk;

CREATE TABLE products (
    product_id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    unit VARCHAR(50),
    price_per_unit DECIMAL(10, 2),
    image_url VARCHAR(255)
);

CREATE TABLE orders (
    order_id INT AUTO_INCREMENT PRIMARY KEY,
    total_price DECIMAL(10, 2),
    date_time DATETIME DEFAULT CURRENT_TIMESTAMP,
    customer_contact VARCHAR(255)
);

CREATE TABLE order_items (
    order_item_id INT AUTO_INCREMENT PRIMARY KEY,
    order_id INT,
    product_id INT,
    quantity DECIMAL(10, 2),
    price DECIMAL(10, 2),
    FOREIGN KEY (order_id) REFERENCES orders(order_id),
    FOREIGN KEY (product_id) REFERENCES products(product_id)
);

INSERT INTO `products` (`product_id`, `name`, `unit`, `price_per_unit`, `image_url`) VALUES
(1, 'Cucumber', 'kg', 3.00, 'images/cucumber.jpg'),
(2, 'Carrot', 'pc', 4.00, 'images/potato.jpg');
```

## 2.2 Starting MySQL Database with XAMPP
Since XAMPP is already installed, we just need to start the MySQL server.

1. **Start MySQL Server**:
   - Open the XAMPP Control Panel.
   - Click 'Start' next to MySQL to run the MySQL server.

2. **Access phpMyAdmin**:
   - Open a web browser and navigate to `http://localhost/phpmyadmin`.

## 2.3 Creating Tables in the Database
Let's use phpMyAdmin to create the database and tables.

1. **Open phpMyAdmin**:
   - Go to the SQL tab.

2. **Run the SQL Schema**:
   - Copy and paste the SQL schema provided above into the SQL tab.
   - Execute the script to create the `yourname_kiosk` database and its tables.

[🎥 **Watch the Database design and Setup Part 4 How to Insert Records **](http://tinyurl.com/269uvr7y)
