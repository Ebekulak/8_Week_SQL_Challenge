# 8_Week_SQL_Challenge
# Case Study #1 - Danny’s Diner
# What is the total amount each customer spent at the restaurant?
SELECT 
	s.customer_id,
	SUM(m.price) as total_spent
FROM dannys_diner.sales AS s
LEFT JOIN dannys_diner.menu as m
ON m.product_id = s.product_id
GROUP BY 1
ORDER BY 2 desc;

