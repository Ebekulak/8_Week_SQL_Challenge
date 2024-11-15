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

### 4. How many of each type of pizza was delivered?

````sql
SELECT 
	pn.pizza_name,	
	COUNT(co.pizza_id)
FROM pizza_runner.customer_orders AS co
JOIN pizza_runner.runner_orders  AS ro 
	ON ro.order_id = co.order_id
JOIN pizza_runner.pizza_names AS pn 
	ON pn.pizza_id = co.pizza_id
WHERE ro.cancellation ISNULL
GROUP BY 1;
````
![image](https://github.com/user-attachments/assets/87fc488f-d3c2-4d8b-9a5f-493eddcaeaa1)

### 5. How many Vegetarian and Meatlovers were ordered by each customer?

````sql
SELECT  
	co.customer_id,
	pn.pizza_name,	
	COUNT(co.pizza_id) AS ordered_pizza_count
FROM pizza_runner.customer_orders AS co
JOIN pizza_runner.pizza_names AS pn 
	ON pn.pizza_id = co.pizza_id
GROUP BY 1,2
ORDER BY co.customer_id;
````
![image](https://github.com/user-attachments/assets/d14b8b69-a2f5-42b4-81eb-1468fd8065d2)

### 6. What was the maximum number of pizzas delivered in a single order?

````sql
SELECT 
	co.order_id,
	COUNT (co.pizza_id) AS pizza_per_order
FROM pizza_runner.customer_orders AS co
JOIN pizza_runner.runner_orders  AS ro 
	ON ro.order_id = co.order_id
JOIN pizza_runner.pizza_names AS pn 
	ON pn.pizza_id = co.pizza_id
WHERE ro.cancellation ISNULL
GROUP BY 1
ORDER BY 2 DESC
LIMIT 1;
````
![image](https://github.com/user-attachments/assets/7db7ebec-af84-42f9-b951-6b94177caefc)

### 7. For each customer, how many delivered pizzas had at least 1 change and how many had no changes?

````sql
SELECT 
	co.customer_id,
	SUM (
		CASE WHEN co.exclusions ISNULL AND co.extras ISNULL	THEN 1
		ELSE 0
		END
		) AS no_change,	
	SUM (
		CASE WHEN co.exclusions IS NOT NULL OR co.extras IS NOT NULL
		THEN 1
		ELSE 0
		END
		) AS at_least_1_change
FROM pizza_runner.customer_orders AS co
JOIN pizza_runner.runner_orders  AS ro 
	ON ro.order_id = co.order_id
JOIN pizza_runner.pizza_names AS pn 
	ON pn.pizza_id = co.pizza_id
WHERE ro.cancellation ISNULL
GROUP BY co.customer_id
ORDER BY co.customer_id;
````
![image](https://github.com/user-attachments/assets/3a9fc73b-6b33-404e-a154-d2f78db3173f)






