use project_1;

-- 1. Retrieve the total number of orders placed

select count(distinct `order_id`) AS total_orders
from orders;

-- 2. Calculate the total revenue generated from pizza sales.

select 
round(sum(order_details.quantity*pizzas.price),2)
AS total_revenue
from order_details 
join pizzas
on pizzas.pizza_id=order_details.pizza_id;

-- 3. Identify the highest-priced pizza.

SELECT
    pizza_types.name AS pizza_name,
    pizzas.size,
    pizzas.price
FROM pizzas
JOIN pizza_types
    ON pizzas.pizza_type_id = pizza_types.pizza_type_id
ORDER BY pizzas.price DESC
LIMIT 1;


-- 4. Identify the most common pizza size ordered

SELECT
    pizzas.size,
    COUNT(*) AS order_count
FROM order_details
JOIN pizzas
    ON order_details.pizza_id = pizzas.pizza_id
GROUP BY pizzas.size
ORDER BY order_count DESC
LIMIT 1;



-- 5. List the top 5 most ordered pizza types along with their quantities.

SELECT
    pt.name AS pizza_name,
    SUM(od.quantity) AS total_quantity
FROM order_details AS od
JOIN pizzas AS p ON p.pizza_id = od.pizza_id
JOIN pizza_types AS pt ON pt.pizza_type_id = p.pizza_type_id
GROUP BY pt.name
ORDER BY total_quantity DESC
LIMIT 5;


-- 6. Join the necessary tables to find the total quantity of each pizza category ordered.

SELECT
    pt.category,
    SUM(od.quantity) AS total_quantity
FROM order_details AS od
JOIN pizzas AS p ON p.pizza_id = od.pizza_id
JOIN pizza_types AS pt ON pt.pizza_type_id = p.pizza_type_id
GROUP BY pt.category
ORDER BY total_quantity DESC;


-- 7. Determine the distribution of orders by hour of the day.

SELECT
    HOUR(time) AS order_hour,
    COUNT(order_id) AS total_orders
FROM orders
GROUP BY order_hour
ORDER BY order_hour;


-- 8. Join relevant tables to find the category-wise distribution of pizzas.

SELECT
    pt.category,
    COUNT(od.order_details_id) AS pizza_order_lines
FROM order_details AS od
JOIN pizzas AS p ON p.pizza_id = od.pizza_id
JOIN pizza_types AS pt ON pt.pizza_type_id = p.pizza_type_id
GROUP BY pt.category
ORDER BY pizza_order_lines DESC;



-- 9. Group the orders by date and calculate the average number of pizzas  ordered per day

SELECT
    ROUND(AVG(daily_total), 2) AS average_pizzas_per_day
FROM (
    SELECT
        o.date,
        SUM(od.quantity) AS daily_total
    FROM orders AS o
    JOIN order_details AS od ON od.order_id = o.order_id
    GROUP BY o.date
) AS daily_orders;


-- 10.Determine the top 3 most ordered pizza types based on revenue.

SELECT
    pt.name AS pizza_name,
    ROUND(SUM(od.quantity * p.price), 2) AS total_revenue
FROM order_details AS od
JOIN pizzas AS p ON p.pizza_id = od.pizza_id
JOIN pizza_types AS pt ON pt.pizza_type_id = p.pizza_type_id
GROUP BY pt.name
ORDER BY total_revenue DESC
LIMIT 3;






