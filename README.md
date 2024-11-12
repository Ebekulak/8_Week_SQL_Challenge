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

After the SQL query, the cleaned and transformed customer_orders table has become as follows.

<img width="1058" alt="image" src="https://user-images.githubusercontent.com/81607668/129472551-fe3d90a0-1e8b-4f32-a2a7-2ecd3ac469ef.png">

### Table: runner_orders
````sql
UPDATE pizza_runner.runner_orders
	SET distance = REPLACE(distance,'km','');
	
UPDATE pizza_runner.runner_orders
	SET duration = LEFT(duration,2);
	
UPDATE pizza_runner.runner_orders
	SET cancellation = NULL
	WHERE cancellation = ''
````
After the SQL query, the cleaned and transformed runner_orders table has become as follows.
<img width="1058" alt="image" src="https://user-images.githubusercontent.com/81607668/129472551-fe3d90a0-1e8b-4f32-a2a7-2ecd3ac469ef.png">
