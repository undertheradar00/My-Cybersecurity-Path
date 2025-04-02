# Programming Assignment 6: Balanced Living Database Setup

## Overview

This repository contains the solution for **Programming Assignment 6** of my web development course. The goal of this assignment was to create a MySQL database for the Balanced Living web application, which is an e-commerce platform with blogging and user registration features. The database includes tables for products, customers, orders, and user registrations, with appropriate constraints and initial data for the `Product` table.

This assignment builds on previous work:
- **Programming Assignment 1**: Created `checkout.html` (to be used later for populating customer and order data).
- **Programming Assignment 2**: Defined the initial website structure and product details.
- **Programming Assignment 3**: Implemented a shopping cart system.
- **Programming Assignment 4**: Added a slide show to the homepage.
- **Programming Assignment 5**: Added a blog system using PHP and a flat file (`blog.txt`).

In this assignment, I created a SQL script (`create_db.sql`) to set up the database schema, define constraints, and populate the `Product` table with initial data.

## Project Structure

The repository contains the following file:

- **`create_db.sql`**: The main SQL script that:
  - Drops existing tables (if any) in the correct order.
  - Creates the `Product`, `Customer`, `Orders1`, and `Registration` tables.
  - Adds primary key, foreign key, and `NOT NULL` constraints.
  - Inserts 8 product rows into the `Product` table.

### Database Schema

#### Product Table
- **Purpose**: Stores information about e-books available for purchase.
- **Columns**:
  - `item_no NUMERIC(4) NOT NULL`: Catalog number (primary key).
  - `ebook_name VARCHAR(30) NOT NULL`: Name of the e-book.
  - `description VARCHAR(200) NOT NULL`: Description of the e-book.
  - `image VARCHAR(30) NOT NULL`: Image file name for the e-book.
  - `price NUMERIC(9,2) NOT NULL`: Price of the e-book.
  - `inventory NUMERIC NOT NULL`: Number of items in stock (set to 5 for all products).
- **Initial Data**: 8 products are inserted (e.g., "Wheat Belly", "Exercise Cure", "What to Expect").

#### Customer Table
- **Purpose**: Stores customer information (to be populated by `checkout.html` in a future assignment).
- **Columns**:
  - `cc_no NUMERIC(16)`: Credit card number (primary key).
  - `exp_mo NUMERIC(2) NOT NULL`: Expiration month.
  - `exp_yr NUMERIC(4) NOT NULL`: Expiration year.
  - `name_first VARCHAR(20) NOT NULL`: First name.
  - `name_last VARCHAR(20) NOT NULL`: Last name.
  - `email VARCHAR(20) NOT NULL`: Email address.
  - `address1 VARCHAR(50) NOT NULL`: Primary address.
  - `address2 VARCHAR(50)`: Secondary address (nullable).
  - `city VARCHAR(20) NOT NULL`: City.
  - `state VARCHAR(2) NOT NULL`: State (2-letter code).
  - `zip NUMERIC(5) NOT NULL`: ZIP code.
  - `country VARCHAR(20)`: Country (nullable).
  - `phone VARCHAR(15) NOT NULL`: Phone number.
  - `fax VARCHAR(15) NOT NULL`: Fax number.
  - `mail_list NUMERIC(1)`: 1 = on mailing list, 0 = off (nullable).
- **Initial Data**: None (as per assignment requirements).

#### Orders1 Table
- **Purpose**: Relationship table between `Product` and `Customer`, storing order details.
- **Columns**:
  - `item_no NUMERIC(4) NOT NULL`: References `Product.item_no`.
  - `cc_no NUMERIC(16) NOT NULL`: References `Customer.cc_no`.
  - `quantity NUMERIC NOT NULL`: Quantity purchased.
  - `date_sold DATE NOT NULL`: Date of the order.
- **Primary Key**: Composite key `(item_no, cc_no, date_sold)` to allow the same customer to buy the same item on different dates.
- **Initial Data**: None (as per assignment requirements).

#### Registration Table
- **Purpose**: Stores user registration data for newsletters and email alerts (to be populated in Programming Assignment 8).
- **Columns**:
  - `username VARCHAR(16)`: Username (primary key).
  - `password VARBINARY(16) NOT NULL`: Password (binary for potential hashing).
- **Initial Data**: None (as per assignment requirements).

## Setup Instructions

### Prerequisites
- **XAMPP**: You need XAMPP installed to run MySQL. Download it from [apachefriends.org](https://www.apachefriends.org/).
- **MySQL**: Ensure MySQL is running via XAMPP.
- **phpMyAdmin**: Used to execute the SQL script (accessible at `http://localhost/phpmyadmin`).

### Steps to Run
1. **Start XAMPP**:
   - Open the XAMPP Control Panel.
   - Start the MySQL module (Apache is not required for this assignment).

2. **Create the Database**:
   - Open phpMyAdmin in your browser: `http://localhost/phpmyadmin`.
   - Click "New" on the left sidebar.
   - Name the database `balanced_living` and click "Create."

3. **Execute the Script**:
   - In phpMyAdmin, select the `balanced_living` database.
   - Go to the "SQL" tab.
   - Copy the contents of `create_db.sql` and paste them into the SQL query box.
   - Click "Go" to execute the script.
   - Alternatively, use the MySQL command line:
     ```bash
     mysql -u root -p balanced_living < path/to/create_db.sql
     ```
     (The default MySQL root password in XAMPP is empty unless you’ve set one.)

4. **Verify the Setup**:
   - In phpMyAdmin, confirm the following:
     - Tables `Product`, `Customer`, `Orders1`, and `Registration` are created.
     - `Product` has 8 rows (e.g., "Wheat Belly", "Exercise Cure").
     - `Customer`, `Orders1`, and `Registration` are empty (0 rows).
   - Test constraints:
     - Try inserting a row into `Customer` with a null `email`—it should fail.
     - Try inserting a duplicate `item_no` into `Product`—it should fail.

## Usage
This script sets up the database for the Balanced Living web application. Future assignments will:
- Populate the `Customer` and `Orders1` tables using `checkout.html`.
- Populate the `Registration` table using a registration form (Programming Assignment 8).

To integrate this database with the web application:
1. Update your PHP scripts (e.g., `process.php`, `blog.php`) to connect to the `balanced_living` database.
2. Modify `checkout.html` to insert customer and order data into the `Customer` and `Orders1` tables.

## Notes
- **Duplicate Products**: The `Product` table has two entries for "Soul Healing" (`item_no` 4 and 5). This might be a mistake, but I’ve kept it as specified. If needed, you can update one of them to a different product.
- **Future Integration**: This database will be used in upcoming assignments to store customer orders and user registrations, replacing the flat-file storage used in Programming Assignment 5 (`blog.txt`).

## Contributing
This is a student project, but feel free to fork the repository and submit pull requests if you have suggestions or improvements!

## License
This project is for educational purposes and is not licensed for commercial use.
