#  Case Study #2 Pizza Runner

<img src="https://user-images.githubusercontent.com/81607668/127271856-3c0d5b4a-baab-472c-9e24-3c1e3c3359b2.png" alt="Image" width="500" height="520">

## Business Task
Danny is expanding his new Pizza Empire and at the same time, he wants to Uberize it, so Pizza Runner was launched!

Danny started by recruiting “runners” to deliver fresh pizza from Pizza Runner Headquarters (otherwise known as Danny’s house) and also maxed out his credit card to pay freelance developers to build a mobile app to accept orders from customers. 
##  Data Cleaning & Transformation
### Table: customer_orders
Looking at the `customer_orders` table below, The exclusions and extras columns will need to be cleaned up before using them
<img width="1063" alt="image" src="https://user-images.githubusercontent.com/81607668/129472388-86e60221-7107-4751-983f-4ab9d9ce75f0.png">

````sql
UPDATE pizza_runner.customer_orders
SET exclusions = NULL
WHERE exclusions = 'null';

UPDATE pizza_runner.customer_orders
SET extras = NULL
WHERE extras = 'null';

-- Step 2: Convert empty strings to NULLs
UPDATE pizza_runner.customer_orders
SET exclusions = NULL
WHERE exclusions = '';

UPDATE pizza_runner.customer_orders
SET extras = NULL
WHERE extras = '';

-- Step 3: Remove spaces around commas in lists
UPDATE pizza_runner.customer_orders
SET exclusions = TRIM(BOTH ' ' FROM REPLACE(exclusions, ', ', ','))
WHERE exclusions IS NOT NULL;

UPDATE pizza_runner.customer_orders
SET extras = TRIM(BOTH ' ' FROM REPLACE(extras, ', ', ','))
WHERE extras IS NOT NULL;
`````

After the SQL query, the cleaned and transformed table has become as follows.

![customers_users_image]([https://C:\Users\nurte\Pictures\Screenshots\Ekran görüntüsü 2024-11-11 234535.png](https://github.com/Ebekulak/8_Week_SQL_Challenge/blob/Case-Study-%232---Pizza-Runner/Ekran%20g%C3%B6r%C3%BCnt%C3%BCs%C3%BC%202024-11-11%20234535.png))
