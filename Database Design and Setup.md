# Step 2: Database Design and Setup

Now that XAMPP is installed, we'll proceed to set up and design the MySQL database for our Flask application.

## 2.1 Designing the SQL Schema
We will define the schema for our database, which includes creating the database and tables for products, orders, and order items.

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

