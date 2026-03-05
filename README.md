# Project: nv-Product

This project is a variation of the nv-webblog68 project, extended with a new model: **Product**.

## New Model: Product

### Schema
- **name**: STRING\n- **description**: TEXT\n- **price**: FLOAT\n- **stock**: INTEGER\n- **image**: STRING

## New Controller
A dedicated controller `ProductController` has been added to handle CRUD operations for `Product`.

## New Routes
The following routes have been added to `server/src/routes.js`:

- **GET** `/products` - Get all products
- **POST** `/product` - Create a new product
- **GET** `/product/:productId` - Get a product by ID
- **PUT** `/product/:productId` - Update a product
- **DELETE** `/product/:productId` - Delete a product

## Usage
Follow standard setup instructions for Client and Server.
