# 🍕 Case Study #2 - Pizza Runner

## 🍝 Solution - A. Pizza Metrics

### 1. How many pizzas were ordered?

````sql
How many pizzas were ordered?
SELECT 
COUNT (pizza_id)
FROM pizza_runner.customer_orders;
````
#### Answer

![order_count](https://github.com/Ebekulak/images/blob/main/Ekran%20g%C3%B6r%C3%BCnt%C3%BCs%C3%BC%202024-11-13%20224911.png)

### 2. How many unique customer orders were made?

````sql
SELECT 
COUNT (DISTINCT(order_id)) AS unique_orders_count
FROM pizza_runner.customer_orders;
````
![order_count](https://github.com/Ebekulak/images/blob/main/Ekran%20g%C3%B6r%C3%BCnt%C3%BCs%C3%BC%202024-11-13%20235349.png?raw=true)

### 3. How many successful orders were delivered by each runner?

````sql
SELECT
 	runner_id,
  COUNT (DISTINCT order_id) AS succesful_order_count
FROM pizza_runner.runner_orders
WHERE cancellation ISNULL
 GROUP BY 1
 ORDER BY 1;
````
![image](https://github.com/user-attachments/assets/0d0d67ce-6f2c-4d67-9443-53982706046d)
