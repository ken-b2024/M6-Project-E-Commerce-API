# E-Commerce API

This is a Flask-based REST API designed to manage an e-commerce system. It allows users to manage products, orders, customer accounts, and user details. The app uses SQLAlchemy for database interaction, Marshmallow for serialization, and MySQL as the backend database.

## Features
User Management: Create, update, delete, and view user information.
Customer Account Management: Create, update, delete, and view customer accounts associated with users.
Product Management: Add, update, delete, and view products in the system.
Order Management: Place, view, and cancel orders. Calculate the total price based on the products selected.
Stock Management: Manage the stock quantity of products in the system.
Installation
Prerequisites
Python 3.x
MySQL Database
Install the required Python packages:
bash
Copy code
pip install Flask Flask-SQLAlchemy Flask-Marshmallow marshmallow mysql-connector
Database Setup
Create MySQL Database: Create a MySQL database named e_test_db (or modify the SQLALCHEMY_DATABASE_URI to point to your existing database).
Create Tables: The tables will be automatically created when the app is run. Ensure your MySQL server is running.
Configuration
Database Connection: Modify the connection string in the app to reflect your MySQL credentials and database name:
python
Copy code
app.config['SQLALCHEMY_DATABASE_URI'] = 'mysql+mysqlconnector://root:MySQL1sLif3!@localhost/e_test_db'
Running the App
To run the app, simply execute the following command:

bash
Copy code
python app.py
This will start the Flask development server on http://127.0.0.1:5000/.

## API Endpoints
### 1. User Management
GET /users: Fetch all users.
POST /user: Create a new user.
Body:
json
Copy code
{
  "name": "John Doe",
  "email": "johndoe@example.com",
  "phone": "1234567890"
}
PUT /users/<int:id>: Update user details.
DELETE /users/<int:id>: Delete a user.
### 2. Customer Account Management
GET /users: Fetch all customer accounts.
POST /accounts: Create a new customer account for a user.
Body:
json
Copy code
{
  "username": "johndoe123",
  "password": "mypassword",
  "user_id": 1
}
PUT /users/<int:user_id>: Update customer account details.
DELETE /users/<int:user_id>: Delete a customer account.
### 3. Product Management
POST /products: Add a new product.
Body:
json
Copy code
{
  "name": "Laptop",
  "price": 999.99,
  "quantity": 10
}
GET /products/<int:id>: Fetch product details by ID.
PUT /products/<int:id>: Update product details.
DELETE /products/<int:id>: Delete a product.
PUT /products/<int:id>/stock: Update product stock quantity.
### 4. Order Management
POST /orders: Place a new order.
Body:
json
Copy code
{
  "date": "2024-12-18",
  "user_id": 1,
  "total_price": 1999.98
}
GET /orders/<int:id>: Retrieve an order by ID.
DELETE /orders/<int:id>: Cancel an order.
Database Models
User
id: Primary key, integer
name: User's name, string
email: User's email address, string
phone: User's phone number, string
orders: One-to-many relationship with the Order model
CustomerAccount
id: Primary key, integer
username: Unique username, string
password: Account password, string
user_id: Foreign key linking to the User model
Product
id: Primary key, integer
name: Product name, string
price: Product price, float
quantity: Product quantity in stock, integer
orders: Many-to-many relationship with the Order model through order_product
Order
id: Primary key, integer
date: Date of the order, string
user_id: Foreign key linking to the User model
total_price: Total price of the order, float
order_products: One-to-one relationship with the Order_Product table
Order_Product (Association Table)
order_id: Foreign key linking to the Order model
product_id: Foreign key linking to the Product model
Error Handling
Validation Errors: If the input data is invalid or missing required fields, the API will return a 400 status code with a detailed error message.



This is a simple and flexible API to handle user, product, account, and order management for an e-commerce platform. You can extend this application further with more advanced features like payment processing, inventory management, etc.
