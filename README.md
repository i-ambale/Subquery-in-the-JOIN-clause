# 🌍 SQL Subqueries in the JOIN Clause – United Nations Geographic Data
This project demonstrates how to use subqueries in the JOIN clause in SQL to perform regional land analysis using a table called `Geographic_location` from a MySQL database named `united_nations`.

## 📘 Learning Objectives
In this notebook or project, you will learn how to:

- Understand and apply subqueries in the JOIN clause

- Join a main table with an aggregated subquery based on a shared column

- Calculate each country’s land area as a percentage of its sub-region's total land area

- Use best practices for SQL readability and performance

## 🗂️ Overview
We aim to determine the percentage of land that each country contributes to its respective sub-region, using a dataset from the `Geographic_location` table.

For example, if a sub-region has 10,000 sq.km total land area, and a country in that sub-region has 1,000 sq.km of land, it occupies 10% of the sub-region.

To achieve this efficiently:

- We compute the total land area for each sub-region once using a subquery.

- We then join this result back to the original Geographic_location table.

- Finally, we calculate each country’s share as a percentage.

## 🧩 SQL Query Example
sql
Copy
Edit
```
SELECT 
    g.Country_name,
    (g.Land_area / l.TotalLandArea) * 100 AS Pct_of_region_land,
    g.Sub_region
FROM 
    Geographic_location g
JOIN
    (
        SELECT 
            Sub_region,
            SUM(Land_area) AS TotalLandArea
        FROM 
            Geographic_location
        GROUP BY 
            Sub_region
    ) AS l
ON 
    g.Sub_region = l.Sub_region
ORDER BY 
    g.Sub_region, Pct_of_region_land DESC;
```
## 💾 Database Setup
This project uses a local MySQL database named united_nations. Ensure:

- MySQL Server is running on your machine.

- You’ve created the `Geographic_location` table with relevant fields like `Country_name`, `Sub_region`, and `Land_area`.

- You're connected to the correct database using MySQL Workbench or a Jupyter notebook with MySQL connectivity.

| ⚠️ Google Colab does not support local MySQL database connections, so run this notebook on your local machine for best results.

## 🛠️ Requirements
- MySQL Server

- MySQL Workbench or Jupyter Notebook with MySQL connector (e.g., `mysql-connector-python`)

- `united_nations` database and `Geographic_location` table

## 📚 Related Topics
- SQL Aggregation (SUM, GROUP BY)

- SQL Joins

- Subqueries (non-correlated)

- Data analysis using SQL

## 🧑‍💻 Author
**Ibrahim Ambale**  

[GitHub Profile](https://github.com/i-ambale)
