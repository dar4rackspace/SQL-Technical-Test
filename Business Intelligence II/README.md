# Instruccions

1. **Write a query to show the order number where the order_date took place in 2020.**

2. **How would you get the order amount by day of the week** (BigQuery docs: [date functions](https://cloud.google.com/bigquery/docs/reference/standard-sql/date_functions))?

3. **Write a query to show the order number with the highest order amount.**

4. **Write a query that will give me all of the salesperson names and customer names that have had order(s) where the customer name starts with an “s.”**

5. **Write a query that will give me the total amount of sales made by each salesperson; please show results sorted by highest to lowest.**

6. **Write a query that will give me all of the salesperson names that have had 2 or more orders.**

7. **Write a query that will give me all of the salesperson names that have not had any orders with Samsonic.**

8. **Write a query that ranks salesperson names by the total amount for each of their orders.**


# Tables

## ERD

```mermaid

erDiagram
    SALESPERSON {
        int id PK
        string name
        int age
        float salary
        int manager_id
    }
    
    CUSTOMER {
        int id PK
        string name
        string city
        string industry_type
    }
    
    ORDERS {
        int number PK
        date order_date
        int cust_id FK
        int salesperson_id FK
        float amount
    }

```

## Data Preview

### Salesperson 

| id | name          | age | salary  | manager_id |
|----|---------------|-----|---------|------------|
| 1  | Alice Smith   | 30  | 60000   | 3          |
| 2  | Bob Johnson    | 45  | 75000   | 3          |
| 3  | Carol White   | 38  | 80000   | NULL       |
| 4  | David Brown   | 28  | 55000   | 3          |
| 5  | Eva Green     | 35  | 72000   | 2          |

### Customer Table

| id | name          | city       | industry type   |
|----|---------------|------------|------------------|
| 1  | Global Corp   | New York   | Technology        |
| 2  | Eco Solutions  | San Francisco | Environmental     |
| 3  | Foodie Co.    | Chicago    | Food & Beverage   |
| 4  | FinTech Inc.  | Boston     | Finance           |
| 5  | HealthPlus    | Seattle    | Healthcare        |

### Orders Table

| number | order_date | cust_id | salesperson_id | amount  |
|--------|------------|---------|----------------|---------|
| 101    | 2024-01-15 | 1       | 1              | 15000   |
| 102    | 2024-02-20 | 2       | 2              | 20000   |
| 103    | 2024-03-05 | 3       | 1              | 10000   |
| 104    | 2024-03-15 | 4       | 3              | 25000   |
| 105    | 2024-04-01 | 5       | 5              | 30000   |

