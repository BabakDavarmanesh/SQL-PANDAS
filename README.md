# SQL + Pandas Solutions

This repository contains a curated collection of **classic data problems** solved using both **SQL** and **Pandas**.  
The goal is to demonstrate practical problem-solving skills in multiple tools commonly used for data analysis and engineering.

---

## 📂 Structure

Each problem has its own folder inside [`problems/`](./problems), with:

- **README.md** → problem description, schema, and sample data  
- **solution_postgres.sql** → PostgreSQL solution  
- **solution_sqlserver.sql** → SQL Server solution (if syntax differs)  
- **solution_pandas.ipynb / .py** → Pandas implementation  
- **sample.csv** → small dataset for quick testing
---
📘 Example Problem: Big Countries

Task:
Return the name, population, and area for all countries where:

area >= 3,000,000, OR

population >= 25,000,000

SQL (PostgreSQL):
SELECT name, population, area
FROM World
WHERE area >= 3000000 OR population >= 25000000;
Pandas:
mask = (df["area"] >= 3_000_000) | (df["population"] >= 25_000_000)
df.loc[mask, ["name", "population", "area"]]
---
## 📑 Table of Contents
- [Big Countries](problems/big-countries)  
- [Department Highest Salary](problems/department-highest-salary)  
- [Rank Scores](problems/rank-scores) 
## 📑 Table of Contents
- [Big Countries](problems/big-countries)  
- [Department Highest Salary](problems/department-highest-salary)  
- [Rank Scores](problems/rank-scores) 
