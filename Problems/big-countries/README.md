# Big Countries
---

## Problem Statement

We are given the following table:

| Column Name | Type    | Description                                      |
|-------------|---------|--------------------------------------------------|
| name        | varchar | Primary key; unique name of the country           |
| continent   | varchar | Continent where the country is located           |
| area        | int     | Area of the country in square kilometers         |
| population  | int     | Population of the country                        |
| gdp         | bigint  | GDP of the country                               |

Each row represents information about a country.  

A **country is considered big if**:
- Its area is **at least 3,000,000 km²**, OR  
- Its population is **at least 25,000,000**.  

We need to return the `name`, `population`, and `area` of the **big countries**.
---

## Example

### Input
```
World table:
+-------------+-----------+---------+------------+--------------+
| name        | continent | area    | population | gdp          |
+-------------+-----------+---------+------------+--------------+
| Afghanistan | Asia      | 652230  | 25500100   | 20343000000  |
| Albania     | Europe    | 28748   | 2831741    | 12960000000  |
| Algeria     | Africa    | 2381741 | 37100000   | 188681000000 |
| Andorra     | Europe    | 468     | 78115      | 3712000000   |
| Angola      | Africa    | 1246700 | 20609294   | 100990000000 |
+-------------+-----------+---------+------------+--------------+
```

### Output
```
+-------------+------------+---------+
| name        | population | area    |
+-------------+------------+---------+
| Afghanistan | 25500100   | 652230  |
| Algeria     | 37100000   | 2381741 |
+-------------+------------+---------+
```
---

## Usage
You can run this query in your preferred SQL environment after creating and populating the `World` table.
