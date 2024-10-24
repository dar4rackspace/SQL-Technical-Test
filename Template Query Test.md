
## Queries:

1. **Write a query to show the order number where the order_date took place in 2020.**
   - Looking for candidates to use: SELECT, Filter, BETWEEN, YEAR()
   - Ask about DATE functions
   - Filters: BETWEEN, YEAR
   - ```sql
     SELECT number
     FROM orders
     WHERE order_date BETWEEN '1995-01-01' AND '1996-01-01'
     WHERE YEAR(order_date) = 2020
     ```

2. **Write a query to show the order number with the highest amount**
   - Looking for GROUP BY, Can be solved with ORDER BY, Maybe even RANK
   - Top 1, MAX, GROUP BY
   - ```sql
     SELECT TOP 1 number, MAX(amount) as Highest_amount
     FROM orders
     GROUP BY number
     ```

3. **Write a query that will give me all of the salesperson names and customer names that have had order(s) where the customer name starts with an “s”**
   - Looking for their ability to understand the data, do correct joins and a where clause, wild card
   - ```sql
     SELECT s.name AS sales_person_name, c.name AS customer_name
     FROM salesperson s
     INNER JOIN orders o ON s.id = o.salesperson_id
     INNER JOIN customer c ON o.cust_id = c.id
     WHERE c.name like 's%'
     ```

4. **Write a query that will give me the total amount of sales made by each salesperson, please show results sorted by highest to lowest**
   - Looking for their ability to apply an aggregate function and group by, JOIN
   - ```sql
     SELECT s.name, SUM(o.amount) as total_amount
     FROM salesperson s
     INNER JOIN orders o ON s.id = o.salesperson_id
     GROUP BY s.name
     ORDER BY 2 DESC
     ```
   - What about salespersons who don’t have any orders? Would they show up? What is the amount? How do we get them to show up? FULL or LEFT JOIN to find orphaned records

5. **Write a query that ranks the order by**

6. **Write a query that will give me all of the salesperson names that have had 2 or more orders**
   - Looking for their ability to apply the HAVING function with GROUP BY
   - ```sql
     SELECT s.name, COUNT(o.number)
     FROM salesperson s
     INNER JOIN orders o ON s.id = o.salesperson_id
     HAVING COUNT(o.number) >= 2
     ```

7. **Write a query that ranks salesperson names by the total amount for each of their orders**
   - Could use sub query, could use CTE
   - Ask about tied RANKS, what happens
   - ```sql
     SELECT saleperson_name, RANK() OVER (PARTITION BY saleperson_name ORDER BY total_order_amont DESC) as rank
     FROM (
       SELECT S.name, SUM(o.amount) AS total_order_amont
       FROM salesperson s
       INNER JOIN orders o ON o.salesperson_id = s.id
       GROUP BY s.name
     ) m
     ```

8. **Write a query that does a cumulative sum of each salespersons' orders over time**
   - ```sql
     SUM(Amount) OVER(PARTITION BY salesperson_id ORDER BY order_date RANGE UNBOUNDED PRECEDING)
     ```

9. **Write a query that will give me all of the salesperson names that have not had any orders with Samsonic**
   - This is trickier than it seems as a “not equals” in the where clause does not work. Most use a subquery to solve this. If the candidate does it correctly, I ask them why changing the where from equals to not equals would not work
   - ```sql
     WHERE c.name != Samsonic doesn’t work because we are just removing samsonic rows.
     Proper way is a LEFT JOIN orders o ON o.salesperson_id = s.id AND customer_id = 4 —samsonic
     WHERE o.number IS NULL
     ```
   - Sub Query works as well

10. **Write a Query that shows the salesperson name and their manager name**
    - Notice there is a Manager ID column in the salesperson table. The Manager is related to the salesperons.id column. Can you show me the salesperson(s) where the sales person has no one reporting to them (example: individual contributor)
    - Self LEFT JOIN
    - ```sql
      SELECT s.name
      FROM salesperson m
      LEFT JOIN salesperson s ON m.id = s.manager_id
      WHERE m.id IS NULL
      ```
