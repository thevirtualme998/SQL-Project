# SQL-Project

## Problem Overview
Monday Coffee, an online coffee retailer operating since January 2023, aimed to strategically expand its business by opening physical coffee shops in India. To make informed decisions, they needed a data-driven approach to identify the top three cities with the highest market potential for new store locations.
This involved analyzing existing sales data, customer demographics, and city-specific factors like population and estimated rent
## My Approach
My primary task was to analyze the provided sales data, customer information, and city demographics to identify the most promising cities for new coffee shop openings. 
This required answering several key business questions related to consumer behavior, sales performance, and market potential, and ultimately providing data-backed recommendations for the top three cities

## Key Analytical Questions
Q.1 Coffee Consumers Count
-- How many people in each city are estimated to consume coffee, given that 25% of the population does?

SELECT 
	city_name,
	ROUND(
	(population * 0.25)/1000000, 
	2) as coffee_consumers_in_millions,
	city_rank
FROM city
ORDER BY 2 DESC;

Q.2 Total Revenue from Coffee Sales
-- What is the total revenue generated from coffee sales across all cities in the last quarter of 2023?

SELECT 
	ci.city_name,
	SUM(s.total) as total_revenue
FROM sales as s
JOIN customers as c
ON s.customer_id = c.customer_id
JOIN city as ci
ON ci.city_id = c.city_id
WHERE 
	YEAR(s.sale_date)  = 2023
	AND
	QUARTER(s.sale_date) = 4
GROUP BY 1
ORDER BY 2 DESC;
