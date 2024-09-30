# E-commerce Sales Analysis

## Project Overview
This project demonstrates an analysis of an e-commerce company’s sales data using PostgreSQL. The data includes information about customers, products, and orders. Several SQL queries were used to extract insights about sales performance and customer behavior.

## Database Structure
- `customers`: Stores customer details.
- `products`: Stores product details.
- `orders`: Stores order details.
- `order_details`: Stores information about the items in each order.

## SQL Queries
The following queries were executed to analyze the data:
- Total Sales

SELECT 
	SUM(total_price) AS total_sales
		FROM order_details;


- Top 5 Customers by Total Purchase

SELECT c.first_name, c.last_name, SUM(od.total_price) AS total_spent
	FROM customers c
		JOIN orders o ON c.customer_id = o.customer_id
		JOIN order_details od ON o.order_id = od.order_id
			GROUP BY c.customer_id
				ORDER BY total_spent DESC
					LIMIT 5;


- Most Popular Products by Quantity Sold

SELECT p.product_name, SUM(od.quantity) AS total_sold
	FROM products p
		JOIN order_details od ON p.product_id = od.product_id
		GROUP BY p.product_name
		ORDER BY total_sold DESC;


- Sales by Category
SELECT p.category, SUM(od.total_price) AS total_sales
	FROM products p
		JOIN order_details od ON p.product_id = od.product_id
		GROUP BY p.category
		ORDER BY total_sales DESC;

  
- Customer Purchase Frequency
SELECT c.first_name, c.last_name, COUNT(o.order_id) AS total_orders
	FROM customers c
		JOIN orders o ON c.customer_id = o.customer_id
		GROUP BY c.customer_id
		ORDER BY total_orders DESC;
