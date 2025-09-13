E-commerce Store Database Management System
Overview
A comprehensive relational database system designed for an e-commerce platform, built with MySQL. This database supports all core e-commerce operations including customer management, product catalog, order processing, inventory management, and payment processing.

Database Schema Design
Entity-Relationship Diagram
text
CUSTOMERS ──────┬───────────────────────────────────────────────────────────────────
                │
                ├── ADDRESSES (One-to-Many)
                │
                ├── ORDERS (One-to-Many) ────┬── ORDER_ITEMS (One-to-Many)
                │                            │
                │                            └── PAYMENTS (One-to-One)
                │
                ├── WISHLISTS (One-to-Many) ──── WISHLIST_ITEMS (Many-to-Many)
                │
                └── SHOPPING_CARTS (One-to-One) ─── CART_ITEMS (One-to-Many)

PRODUCTS ───────┬───────────────────────────────────────────────────────────────────
                │
                ├── PRODUCT_IMAGES (One-to-Many)
                │
                ├── PRODUCT_REVIEWS (One-to-Many)
                │
                ├── ORDER_ITEMS (One-to-Many)
                │
                ├── WISHLIST_ITEMS (Many-to-Many)
                │
                ├── CART_ITEMS (One-to-Many)
                │
                ├── PRODUCT_SUPPLIERS (Many-to-Many) ─── SUPPLIERS
                │
                └── INVENTORY_TRANSACTIONS (One-to-Many)

CATEGORIES ─────┬───────────────────────────────────────────────────────────────────
                │
                ├── PRODUCTS (One-to-Many)
                │
                └── (Self-Referential) PARENT_CATEGORY

COUPONS ────────┼───────────────────────────────────────────────────────────────────
                │
                └── ORDER_COUPONS (Many-to-Many) ─── ORDERS

SHIPPING_METHODS (Lookup Table)
Visual Schema Representation
text
+-------------+     +-------------+     +---------------+
|  CUSTOMERS  |     |  CATEGORIES |     | SHIPPING_METHODS |
+-------------+     +-------------+     +---------------+
| customer_id |1    | category_id |1    | shipping_method_id |
| first_name  |     | name        |     | method_name    |
| last_name   |     | description |     | cost           |
| email       |     | parent_id   |∞    +---------------+
| ...         |     +-------------+
+-------------+          1
    1|                   |
     |                   ∞
     ∞             +-----------+
+-----------+    1 | PRODUCTS |1
| ADDRESSES |∞-----+-----------+
+-----------+      | product_id|
| address_id|      | name      |
| customer_id|     | price     |
| type       |     | category_id|
| ...        |     | ...       |
+-----------+      +-----------+
                        1
                        |
                        ∞
+-------------+     +-----------------+     +-------------+
|   ORDERS    |1    |   ORDER_ITEMS   |∞----|  PAYMENTS   |
+-------------+     +-----------------+     +-------------+
| order_id    |     | order_item_id   |     | payment_id  |
| customer_id |     | order_id        |     | order_id    |
| status      |     | product_id      |     | amount      |
| ...         |     | quantity        |     | ...         |
+-------------+     | ...             |     +-------------+
     1|             +-----------------+
      |                   ∞
      |                   |1
      |             +-----------+
      |             | COUPONS   |
      |             +-----------+
      |             | coupon_id |
      |             | code      |
      |             | ...       |
      |             +-----------+
      |                  1
      |                  |
      ∞                  ∞
+-----------------+     +---------------+
| ORDER_COUPONS   |     | WISHLIST_ITEMS|∞----+-----------+
+-----------------+     +---------------+     | WISHLISTS |
| order_id        |     | wishlist_id   |     +-----------+
| coupon_id       |     | product_id    |     | wishlist_id|
| discount_amount |     | ...           |     | customer_id|
+-----------------+     +---------------+     | ...       |
                        ∞                 1  +-----------+
                        |1                  1|
+-------------+     +-----------+            |
|  SUPPLIERS  |     | INVENTORY |            |
+-------------+     | TRANSACTIONS|          |
| supplier_id |     +-----------+            |
| name        |     | trans_id  |            |
| ...         |     | product_id|            |
+-------------+     | type      |            |
     1|             | ...       |            |
      |             +-----------+            |
      ∞                 1|                   |
+-----------------+      |                   |
| PRODUCT_SUPPLIERS|     |                   |
+-----------------+      |                   |
| product_id      |      |                   |
| supplier_id     |      |                   |
| ...             |      |                   |
+-----------------+      |                   |
            ∞            |                   |
            |1           |                   |
            |            |                   |
      +-----------+      |                   |
      | CART_ITEMS|∞-----+                   |
      +-----------+      |                   |
      | cart_item_id|    |                   |
      | cart_id     |    |                   |
      | product_id  |    |                   |
      | ...         |    |                   |
      +-----------+      |                   |
           1|           |                   |
            |           |                   |
            ∞           |                   |
      +-------------+   |                   |
      | SHOPPING_CARTS| |                   |
      +-------------+   |                   |
      | cart_id     |   |                   |
      | customer_id |1  |                   |
      | ...         |---|-------------------|
      +-------------+   |                   |
           1|           |                   |
            |           |                   |
            |1          |                   |
      +-------------+   |                   |
      | PRODUCT_IMAGES| |                   |
      +-------------+   |                   |
      | image_id    |   |                   |
      | product_id  |∞--+                   |
      | ...         |                       |
      +-------------+                       |
                 1|                         |
                  |                         |
                  ∞                         |
            +----------------+              |
            | PRODUCT_REVIEWS|∞-------------+
            +----------------+
            | review_id      |
            | product_id     |
            | customer_id    |
            | ...            |
            +----------------+
Key Features
Complete Entity Structure: 18 tables covering all e-commerce operations

Relationship Types: One-to-One, One-to-Many, and Many-to-Many relationships

Data Integrity: Comprehensive constraints (PK, FK, UNIQUE, NOT NULL, CHECK)

Performance Optimization: Proper indexing on frequently queried columns

Scalability: Designed to handle large volumes of data and transactions

Tables Included
Customers - User account information

Addresses - Customer address details (billing/shipping)

Categories - Product categorization with hierarchical support

Products - Product catalog with inventory tracking

Product_Images - Product visual assets

Product_Reviews - Customer ratings and reviews

Orders - Customer order records

Order_Items - Individual items within orders

Payments - Payment transaction records

Shipping_Methods - Available delivery options

Coupons - Discount and promotion codes

Order_Coupons - Coupon application to orders

Wishlists - Customer wishlist collections

Wishlist_Items - Products in wishlists

Shopping_Carts - Active customer carts

Cart_Items - Products in shopping carts

Suppliers - Product suppliers/vendors

Product_Suppliers - Supplier-product relationships

Inventory_Transactions - Stock movement tracking

Installation
Ensure MySQL Server is installed and running

Execute the provided SQL file:

bash
mysql -u [username] -p < ecommerce_store.sql
The database ecommerce_store will be created with all tables and relationships

Usage Examples
Basic Queries
sql
-- Find all products in a specific category
SELECT * FROM products WHERE category_id = 1;

-- Get customer order history
SELECT * FROM orders WHERE customer_id = 123 ORDER BY order_date DESC;

-- Check product inventory
SELECT product_name, stock_quantity FROM products WHERE stock_quantity < 10;

-- Calculate total sales
SELECT SUM(total_amount) AS total_sales FROM orders WHERE status = 'delivered';
Constraints Implemented
Primary Keys: All tables have auto-increment primary keys

Foreign Keys: All relationships are enforced with foreign key constraints

Unique Constraints: Email addresses, SKUs, coupon codes, etc.

Check Constraints: Price validation, quantity validation, rating ranges

Not Null: Required fields are properly constrained

Relationships
One-to-One: Customer to Shopping Cart

One-to-Many: Customer to Orders, Category to Products, Product to Images

Many-to-Many: Orders to Coupons, Products to Suppliers, Wishlists to Products

Performance Features
Indexes on frequently searched columns (email, product names, categories)

Proper data types for efficient storage and retrieval

Generated columns for calculated values (e.g., order item subtotals)

Future Enhancements
Stored procedures for common operations

Views for simplified reporting

Triggers for automated inventory updates

Partitioning for large-scale data

