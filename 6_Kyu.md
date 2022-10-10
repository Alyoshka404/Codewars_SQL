# SQL Coding Challenges (6 Kyu) <img align="right" src="https://media.tenor.com/t5INDy2mrzMAAAAi/capoo-bugcat.gif" height="100"/>
<br>

## SQL Basics: Simple HAVING


**DESCRIPTION:**

For this challenge you need to create a simple HAVING statement, you want to count how many people have the same age and return the groups with 10 or more people who have that age.

**people table schema**
* id
* name
* age

**return table schema**
* age
* total_people

<br>
<details><summary>My Solution</summary> <br>
  
>```SQL
>-- Create your SELECT statement here
>
>SELECT  age, COUNT(name) AS total_people
>
>FROM people
>
>GROUP BY  age
>
>HAVING COUNT(name) >= 10
>```
</details>

---
<br>



  ## SQL Basics: Top 10 customers by total payments amount

**DESCRIPTION:**

**Overview**

For this kata we will be using the DVD Rental database.

You are working for a company that wants to reward its top 10 customers with a free gift. You have been asked to generate a simple report that returns the top 10 customers by total amount spent ordered from highest to lowest. Total number of payments has also been requested.

The query should output the following columns:

* customer_id [int4]
* email [varchar]
* payments_count [int]
* total_amount [float]

and has the following requirements:

* only returns the 10 top customers, ordered by total amount spent from highest to lowest

**Database Schema**
<p>
  <a href="https://www.codewars.com/kata/580d08b5c049aef8f900007c" target="_blank"> <img src="https://cdn.icon-icons.com/icons2/2530/PNG/512/codewars_button_icon_151901.png" alt="c" height="50" /> </a> <br>
 
 
<br>
<details><summary>My Solution</summary> <br>
  
>```SQL
>-- Replace with your query (in pure SQL)
>
>SELECT customer.customer_id, customer.email, SUM(payment.amount)::FLOAT AS total_amount, COUNT(customer.*) AS payments_count
>
>FROM customer
>    LEFT join payment ON customer.customer_id = payment.customer_id
>
>GROUP BY customer.customer_id, customer.email
>
>ORDER BY SUM(payment.amount) DESC
>
>LIMIT 10
>```
</details>

---
<br>
  
  
## SQL Basics: Simple EXISTS


**DESCRIPTION:**

For this challenge you need to create a SELECT statement that will contain data about departments that had a sale with a price over 98.00 dollars. This SELECT statement will have to use an EXISTS to achieve the task.  
  
  
**departments table schema**
  
* id
* name

**sales table schema**
  
* id
* department_id (department foreign key)
* name
* price
* card_name
* card_number
* transaction_date
  
**resultant table schema**
  
* id
* name
  

  
<br>
<details><summary>My Solution</summary> <br>
  
>```SQL
>-- Create your SELECT statement here
>
>SELECT id, name
>
>FROM departments
>
>WHERE EXISTS (SELECT *
>              FROM sales
>              WHERE sales.department_id = departments.id
>                    and price > 98.00)
>```
</details>

---
<br>
  
  
  
## SQL Basics: Simple JOIN and RANK

**DESCRIPTION:**

 For this challenge you need to create a simple SELECT statement that will return all columns from the ```people``` table, and join to the ```sales``` table so that you can return the COUNT of all sales and RANK each person by their sale_count. 
  
  
**people table schema**
* id
* name
* age

**sales table schema**
* id
* people_id
* sale
* price

You should return all people fields as well as the sale count as "sale_count" and the rank as "sale_rank".
  
<br>
<details><summary>My Solution</summary> <br>
  
>```SQL
>-- Create your SELECT statement here
>SELECT  people.id, people.name, COUNT(sales.sale) AS sale_count,
>        RANK() OVER (PARTITION BY people.id ORDER BY people.id DESC) AS sale_rank
>
>FROM people 
>     JOIN sales ON people.id = sales.people_id
>      
>GROUP BY people.id
>```
</details>

<img align="right" src="https://media.tenor.com/lNFv9X-PgR0AAAAi/capoo-bugcat.gif" height="100"/>  
  
---
<br>
  
  
  
## SQL Basics - Monsters using CASE

**DESCRIPTION:**

You have access to two tables named top_half and bottom_half, as follows:

**top_half schema**
* id
* heads
* arms

**bottom_half schema**
* id
* legs
* tails

  
You must return a table with the format as follows:
  
  
**output schema**
* id
* heads
* legs
* arms
* tails
* species
  
  
The IDs on the tables match to make a full monster. For heads, arms, legs and tails you need to draw in the data from each table.

For the species, if the monster has more heads than arms, more tails than legs, or both, it is a 'BEAST' else it is a 'WEIRDO'. This needs to be captured in the species column.

All rows should be returned (10).

Tests require the use of CASE. Order by species.

Please use pure SQL, only testing is done in Ruby.  
  
  

<br>
<details><summary>My Solution</summary> <br>
  
>```SQL
>/*  SQL  */
>WITH new_table AS (SELECT *
>                   FROM top_half 
>                        JOIN bottom_half 
>                        ON top_half.id = bottom_half.id)
>
>SELECT *,
>        CASE WHEN (heads > arms) OR (tails > legs)
>        THEN 'BEAST'
>        ELSE 'WEIRDO'
>        END AS species
>
>FROM new_table
>
>ORDER BY species
>```
</details>

---
<br>
  
  
  
## SQL Basics: Simple UNION ALL

**DESCRIPTION:**

  For this challenge you need to create a UNION statement, there are two tables ```ussales``` and ```eusales``` the parent company tracks each sale at its respective location in each table, you must all filter the sale price so it only returns rows with a sale greater than ```50.00```. You have been tasked with combining that data for future analysis. Order by location (US before EU), then by id.
  
  
  
**(us/eu)sales table schema**
* id
* name
* price
* card_name
* card_number
* transaction_date

**resultant table schema**
* location (EU for eusales and US for ussales)
* id
* name
* price (greater than 50.00)
* card_name
* card_number
* transaction_date
  
<br>
<details><summary>My Solution</summary> <br>
  
>```SQL
>-- Create your SELECT statement here
>WITH union_tab AS (SELECT *, 
>                          'US' AS location
>                   FROM ussales
>
>                   UNION ALL
>
>                   SELECT *,
>                          'EU' AS location
>                   FROM eusales )
>
>
>SELECT id, location, *
>
>FROM union_tab
>
>WHERE price >= 50.00
>
>ORDER BY location DESC, id
>```
</details>

---
<br>
  
  
  
## SQL Basics: Simple table totaling.

**DESCRIPTION:**

For this challenge you need to create a simple query to display each unique clan with their total points and ranked by their total points.  
  
**people table schema**
* name
* points
* clan

 You should then return a table that resembles below 
  
**select on**
* rank
* clan
* total_points
* total_people


The query must rank each clan by their total_points, you must return each unqiue clan and if there is no clan name (i.e. it's an empty string) you must replace it with ```[no clan specified]```, you must sum the total_points for each clan and the total_people within that clan.

##Note The data is loaded from the live leaderboard, this means values will change but also could cause the kata to time out retreiving the information.  
  
  
<br>
<details><summary>My Solution</summary> <br>
  
>```SQL
>-- Create your SELECT statement here
>
>SELECT RANK() OVER(ORDER BY SUM (points) DESC) AS rank,
>
>       CASE WHEN   clan = ''
>       THEN '[no clan specified]'
>       ELSE clan
>       END AS clan ,
>
>       SUM (points) AS total_points, 
>       COUNT(name) AS total_people
>
>FROM people 
>
>GROUP BY clan
>```
</details>

---
<br>
  
  
  
 ## SQL Basics: Simple IN


**DESCRIPTION:**

 For this challenge you need to create a SELECT statement, this SELECT statement will use an IN to check whether a department has had a sale with a price over 98.00 dollars. 
  
  
**departments table schema**
* id
* name
  
**sales table schema**
* id
* department_id (department foreign key)
* name
* price
* card_name
* card_number
* transaction_date
  
**resultant table schema**
* id
* name
  
<br>
<details><summary>My Solution</summary> <br>
  
>```SQL
>SELECT id, name
>FROM departments
>WHERE id IN (SELECT department_id FROM sales 
>                WHERE (price) > 98.00);
>```
</details>

  
<img align="right" src="https://media.tenor.com/F7YIQb521dgAAAAi/tkthao219-capoo.gif" height="100"/>  
  
---
<br>
  
  
  
## SQL Bug Fixing: Fix the QUERY - Totaling

**DESCRIPTION:**

Oh no! Timmys been moved into the database divison of his software company but as we know Timmy loves making mistakes. Help Timmy keep his job by fixing his query...

Timmy works for a statistical analysis company and has been given a task of totaling the number of sales on a given day grouped by each department name and then each day.

**Resultant table:**
* day (type: date) {group by} [order by asc]
* department (type: text) {group by} [In a real world situation it is bad practice to name a column after a table]
* sale_count (type: int)
  
**Tables and relationship below:**

<img src="https://i.imgur.com/kBkwsbi.png" />
  
  
<br>
<details><summary>My Solution</summary> <br>
  
>```SQL
>SELECT transaction_date::date AS day , 
>        department.name AS department, 
>        COUNT(product_id) AS sale_count
>
>FROM sale
>      JOIN department 
>      ON sale.department_id = department.id
>      
>GROUP BY day, department
>
>ORDER BY day
>```
</details>

---
<br>
  
## Conditional Count

**DESCRIPTION:**

 Given a ```payment``` table, which is a part of DVD Rental Sample Database, with the following schema 

Column       | Type                        | Modifiers
-------------| ----------------------------| ----------
payment_id   | integer                     | not null 
customer_id  | smallint                    | not null
staff_id     | smallint                    | not null
rental_id    | integer                     | not null
amount       | numeric(5,2)                | not null
payment_date | timestamp without time zone | not null  
  
 produce a result set for the report that shows a side-by-side comparison of the number and total amounts of payments made in Mike's and Jon's stores broken down by months.

The resulting data set should be ordered by ```month``` using natural order (Jan, Feb, Mar, etc.).

Note: *You don't need to worry about the year component. Months are never repeated because the sample data set contains payment information only for one year.*

The desired output for the report 
  
 month | total_count | total_amount | mike_count | mike_amount | jon_count | jon_amount
-------|-------------|--------------|------------|-------------|-----------|------------
2      |             |              |            |             |           |           
5      |             |              |            |             |           |           
... 
  
 
* ```month``` - number of the month (1 - January, 2 - February, etc.)
* ```total_count``` - total number of payments
* ```total_amount``` - total payment amount
* ```mike_count``` - total number of payments accepted by Mike (```staff_id = 1```)
* ```mike_amount``` - total amount of payments accepted by Mike (```staff_id = 1```)
* ```jon_count``` - total number of payments accepted by Jon (```staff_id = 2```)
* ```jon_amount``` - total amount of payments accepted by Jon (```staff_id = 2```)
  
  
<br>
<details><summary>My Solution</summary> <br>
  
>```SQL
>SELECT EXTRACT (MONTH FROM payment_date) AS month, 
>       COUNT(payment_id) AS total_count ,
>       SUM (amount) AS total_amount,
>       COUNT(CASE WHEN staff_id = 1
>       THEN payment_id
>       END) AS mike_count ,
>       SUM (CASE WHEN staff_id = 1
>       THEN amount
>       END) AS mike_amount ,
>       COUNT(CASE WHEN staff_id = 2
>       THEN payment_id
>       END) AS jon_count ,
>       SUM(CASE WHEN staff_id = 2
>       THEN amount
>       END) AS jon_amount  
>
>FROM payment
>
>GROUP BY month
>
>ORDER BY month
>```
</details>

---
<br>
  
  
  
## SQL Basics: Simple NULL handling

**DESCRIPTION:**

For this challenge you need to create a SELECT statement, this select statement must have NULL handling, using COALESCE and NULLIF.

If no ``` name```  is specified you must replace with ``` [product name not found]``` 

If no ``` card_name```  is specified you must replace with ``` [card name not found]``` 

If no ``` price```  is specified you must throw away the record, you must also filter the dataset by prices greater than 50.

**eusales table schema**
* id
* name
* price
* card_name
* card_number
* transaction_date
  
**resultant table schema**
* id
* name
* price (greater than 50.00)
* card_name
* card_number
* transaction_date


<br>
<details><summary>My Solution</summary> <br>
  
>```SQL
>-- Create your SELECT statement here
>
>SELECT *,
>        COALESCE (NULLIF (name, ''), '[product name not found]') AS name ,
>        -- COALESCE (NULLIF (price, ''), ) AS price ,
>        COALESCE (NULLIF (card_name, ''), '[card name not found]') AS card_name
>
>FROM eusales 
>
>WHERE price IS NOT NULL
>      AND price > 50
>```
</details>
  
  
---
<br>
 
  
## SQL Bug Fixing: Fix the JOIN

**DESCRIPTION:**
  
  Oh no! Timmys been moved into the database divison of his software company but as we know Timmy loves making mistakes. Help Timmy keep his job by fixing his query...

Timmy works for a statistical analysis company and has been given a task of calculating the highest average salary for a given job, the sample is compiled of 100 applicants each with a job and a salary. Timmy must display each unique job, the total average salary, the total people and the total salary and order by highest average salary. Timmy has some bugs in his query, help Timmy fix his query so he can keep his job!

**people table schema**
* id
* name
  
**job table schema**
* id
* people_id
* job_title
* salary
  
**resultant table schema**
* job_title (unique)
* average_salary (float, 2 dp)
* total_people (int)
* total_salary (float, 2 dp)


  
<br>
<details><summary>My Solution</summary> <br>
  
>```SQL
>SELECT job_title,
>       COUNT(name) AS total_people,
>       ROUND(AVG (salary)::numeric,2)::FLOAT AS average_salary,
>       ROUND(SUM (salary)::numeric,2)::FLOAT AS total_salary 
>
>FROM people 
>     JOIN job  ON people.id = job.people_id
>     
>GROUP BY job_title
>
>ORDER BY average_salary DESC
>```
</details>

  
<img align="right" src="https://media.tenor.com/o4CBDPGRXNEAAAAi/capoo-blue-cat.gif" height="100"/>  
  
---
<br>
  
  
## SQL Basics: Simple WITH


**DESCRIPTION:**

For this challenge you need to create a SELECT statement, this SELECT statement will use an IN to check whether a department has had a sale with a price over 90.00 dollars BUT the sql MUST use the WITH statement which will be used to select all columns from ``` sales```  where the price is greater than 90.00, you must call this sub-query ``` special_sales``` .

**departments table schema**
* id
* name
  
**sales table schema**
* id
* department_id (department foreign key)
* name
* price
* card_name
* card_number
* transaction_date
  
**resultant table schema**
* id
* name

  
<br>
<details><summary>My Solution</summary> <br>
  
>```SQL
>-- Create your SELECT statement here
>WITH special_sales AS (SELECT *
>                       FROM departments 
>                          --JOIN sales ON departments.id = sales.department_id    
>                       WHERE id IN (SELECT department_id 
>                                    FROM sales
>                                    WHERE price >= 90 ))
>  
>SELECT *
>
>FROM special_sales
>```
</details>

---
<br>
  
  
## SQL Basics: Simple FULL TEXT SEARCH

**DESCRIPTION:**
  
 
For this challenge you need to create a simple SELECT statement. Your task is to create a query and do a FULL TEXT SEARCH. You must search the ``` product```  table on the field ``` name```  for the word ``` Awesome```  and return each row with the given word. Your query MUST contain ``` to_tsvector```  and ``` to_tsquery```  PostgreSQL functions.

**Tables and relationship below:**

<img src="https://i.imgur.com/kBkwsbi.png" />
  
  
<br>
<details><summary>My Solution</summary> <br>
  
>```SQL
>-- Create your SELECT statement here
>SELECT * FROM product 
>WHERE to_tsvector(name) @@ to_tsquery('Awesome');
>```
</details>
  
  
---
<br>
  
  
## Calculating Batting Average

**DESCRIPTION:**

In baseball, the batting average is a simple and most common way to measure a hitter's performace. Batting average is calculated by taking all the players ```hits``` and dividing it by their number of ```at_bats```, and it is usually displayed as a 3 digit decimal (i.e. 0.300).

Given a ```yankees``` table with the following schema,

-```player_id``` STRING

-```player_name``` STRING

-```primary_position``` STRING

-```games``` INTEGER

-```at_bats``` INTEGER

-```hits``` INTEGER

return a table with ```player_name```, ```games```, and ```batting_average```.

We want ```batting_average``` to be rounded to the nearest thousandth, since that is how baseball fans are used to seeing it. Format it as text and make sure it has 3 digits to the right of the decimal (pad with zeroes if neccesary).

Next, order our resulting table by ```batting_average```, with the highest average in the first row.

Finally, since ```batting_average``` is a rate statistic, a small number of ```at_bats``` can change the average dramatically. To correct for this, exclude any player who doesn't have at least 100 at bats.

Expected Output Table

-```player_name``` STRING

-```games``` INTEGER

-```batting_average``` STRING
 
  
<br>
<details><summary>My Solution</summary> <br>
  
>```SQL
>/* Your Query Here */
>WITH new_table AS (SELECT *, 
>                          (ROUND((hits::FLOAT/at_bats::FLOAT)::NUMERIC , 3)::FLOAT)::text AS batting_average
>                    FROM yankees
>                    WHERE at_bats >= 100 )
>
>SELECT player_name , games , 
>        CASE WHEN LENGTH(batting_average) <5
>             THEN batting_average || '0'
>             ELSE batting_average
>             END AS batting_average
>
>FROM new_table
>
>ORDER BY batting_average DESC
>```
</details><br>


<details><summary>Favorite solution</summary><br>

>```SQL
>SELECT
>  player_name,
>  games,
>  round(hits::numeric / at_bats, 3)::text as batting_average
>FROM yankees
>WHERE at_bats >= 100
>ORDER BY batting_average DESC;
>```

></details>

---
<br>
  
  
  
 ## SQL: Regex AlphaNumeric Split


**DESCRIPTION:**

You are given a table named repositories, format as below:

**repositories table schema**
* project
* commits
* contributors
* address
  
The table shows project names of major cryptocurrencies, their numbers of commits and contributors and also a random donation address ( not linked in any way :) ).

Your job is to split out the letters and numbers from the address provided, and return a table in the following format:

**output table schema**
* project
* letters
* numbers
  
Case should be maintained.


<br>
<details><summary>My Solution</summary> <br>
  
>```SQL
>/*  SQL  */
>SELECT
>project,
>REGEXP_REPLACE(address, '\d','','g') AS letters,
>REGEXP_REPLACE(address,'\D','','g') AS numbers
>FROM repositories
>```
</details>
  
---
<br>
  
  
## SQL Basics: Simple PIVOTING data WITHOUT CROSSTAB

**DESCRIPTION:**

DESCRIPTION:
  
This kata is inspired by SQL Basics: Simple PIVOTING data by matt c.

You need to build a pivot table WITHOUT using CROSSTAB function. Having two tables ``` products```  and ``` details```  you need to select a pivot table of products with counts of details occurrences (possible details values are ``` ['good', 'ok', 'bad']``` .

Results should be ordered by product's ``` name``` .

Model schema for the kata is:

  
<img src="https://i.imgur.com/81Ww3YH.png" />

  
your query should return table with next columns

* name
* good
* ok
* bad
  
Compare your table to the expected table to view the expected results.
  
  
<br>
<details><summary>My Solution</summary> <br>
  
>```SQL
>-- add your query here!
>  
>SELECT 
>      name, 
>      SUM(CASE WHEN detail = 'good' THEN 1 ELSE 0 END) AS good,
>      SUM(CASE WHEN detail = 'ok' THEN 1 ELSE 0 END) AS ok,
>      SUM(CASE WHEN detail = 'bad' THEN 1 ELSE 0 END) AS bad
>
>FROM products 
>     JOIN details ON products.id = details.product_id
>GROUP BY  name
>ORDER by name
>```
</details>

  
<img align="right" src="https://media.tenor.com/DdnFqjAGkxAAAAAi/bugcat-capoo.gif" height="100"/>  
  
---
<br>
  
  
  
## SQL Basics: Create a FUNCTION (DATES)

**DESCRIPTION:**

For this challenge you need to create a basic Age Calculator function which calculates the age in years on the age field of the peoples table.

The function should be called ```agecalculator```, it needs to take 1 date and calculate the age in years according to the date ```NOW``` and must return an integer.

You may query the people table while testing but the query must only contain the function on your final submit.

**people table schema**
*id
*name
*age
  
  
<br>
<details><summary>My Solution</summary> <br>
  
>```SQL
>-- Create your FUNCTION statement here
>
>CREATE FUNCTION agecalculator(date_var date) RETURNS integer AS $$
>
>SELECT CAST(date_part('year',AGE(NOW(), date_var)) AS int) AS age;
>
>$$  LANGUAGE sql;
>```
</details><br>


<details><summary>Favorite solution</summary><br>

>```SQL
>CREATE FUNCTION agecalculator(date) RETURNS integer
>AS $$ SELECT EXTRACT(YEAR FROM AGE($1))::int $$
>LANGUAGE SQL;
>```

></details>

---
<br>
  
  
  
## SELECT prime numbers

**DESCRIPTION:**

Write a SELECT query which will return all prime numbers smaller than 100 in ascending order.

Your query should return one column named ```prime```.

  
<br>
<details><summary>My Solution</summary> <br>
  
>```SQL
>-- your code here
>SELECT t1.a AS prime
>  
>FROM generate_series(2, 100) AS t1(a)
>  
>WHERE NOT EXISTS (SELECT t2.a
>                  FROM generate_series(2, t1.a-1) AS t2(a)
>                  WHERE t1.a % t2.a = 0); 
>```
</details>

---
<br>
  
  
## Subqueries master

**DESCRIPTION:**

 The objective of this Kata is to show that you are proficient at string manipulation (and perhaps that you can use extensively subqueries).

You will use people table but will focus solely on the ```name``` column

 name                       |
----------------------------|
Greyson Tate Lebsack Jr.    |
Elmore Clementina O'Conner  |

  
 you will be provided with a full name and you have to return the name in columns as follows. 
 
  

name           | first_lastname                  | second_lastname
---------------| ----------------------------| ----------
Greyson Tate   | Lebsack                     | Jr.
Elmore         | Clementina                  | O'Conner

  
Note: Don't forget to remove spaces around names in your result. Note: Due to multicultural context, if full name has more than 3 words, consider first 2 as name  
  
  
<br>
<details><summary>My Solution 1</summary> <br>
  
>```SQL
>WITH new_table AS (SELECT name,
>                          --SPLIT_PART (name, ' ', '1')  AS name ,
>                          REVERSE(SPLIT_PART (REVERSE(name), ' ', '2')) AS first_lastname ,
>                          REVERSE(SPLIT_PART (REVERSE(name), ' ', '1')) AS second_lastname
>                   FROM people)
>  
>SELECT REGEXP_REPLACE(name , (' ' || first_lastname || ' ' || second_lastname), '') AS name, 
>       first_lastname, second_lastname
>
>FROM new_table
>```
</details><br>


<details><summary>My Solution 2</summary><br>

>```SQL
>WITH new_table as (
>      SELECT STRING_TO_ARRAY(name, ' ') AS name,
>            ARRAY_LENGTH(STRING_TO_ARRAY(name, ' '), 1) AS len
>      FROM people)
>
>SELECT 
>        ARRAY_TO_STRING(name[1:(len)-2], ' ') as name,
>        name[(len)-1] as first_lastname,
>        name[(len)] as second_lastname
>FROM new_table 
>```

></details>

---
<br>
  
  
  
## Analyzing the sales by product and date

**DESCRIPTION:**

  
**Task**
Given the information about sales in a store, calculate the total revenue for each day, month, year, and product.

**Notes**
* The ```sales``` table stores only the dates for which any data has been recorded - the information about individual sales (what was sold, and when) is stored in the ```sales_details``` table instead
* The ```sales_details``` table stores totals per product per date
* Order the result by the ```product_name```, ```year```, ```month```, ```day``` columns
* We're interested only in the product-specific data, so you shouldn't return the total revenue from all sales
  

**Input tables**  
  

|    Table      |   Column   |  Type   |
|---------------|------------|---------|
| products      | id         | int     |
|               | name       | text    |
|               | price      | numeric |
|---------------|------------|---------|
| sales         | id         | int     |
|               | date       | date    |
|---------------|------------|---------|
| sales_details | id         | int     |
|               | sale_id    | int     |
|               | product_id | int     |
|               | count      | int     |
 
  
**Output table**  
  
|    Column    |  Type   |
|--------------|---------|
| product_name | text    |
| year         | int     |
| month        | int     |
| day          | int     |
| total        | numeric |  
  
  
  
**Example output**  
  
 product_name | year | month | day | total
--------------|------|-------|-----|------
 milk         | 2019 | 01    | 01  | 200
 milk         | 2019 | 01    | 02  | 190
 milk         | 2019 | 01    |     | 390
 milk         | 2019 | 02    | 01  | 240
 milk         | 2019 | 02    |     | 240
 milk         | 2019 |       |     | 630
 milk         |      |       |     | 630 
  
  
  
  
  
  
<br>
<details><summary>My Solution</summary> <br>
  
>```SQL
>WITH new_table AS (
>       SELECT 
>       name AS product_name, 
>       EXTRACT (year FROM date) AS year,
>       EXTRACT (MONTH FROM date) AS month,
>       EXTRACT (DAY FROM date) AS day,
>       SUM(price*count) AS total
>
>       FROM sales_details
>            LEFT JOIN sales ON sales_details.sale_id = sales.id
>            LEFT JOIN products ON sales_details.product_id = products.id
>     
>--GROUP BY name, year, month, day
>--GROUP BY name, rollup(year), rollup(month), rollup(day)
>       GROUP BY product_name, rollup(year, month, day)
>       ORDER BY product_name , year , month , day )
>       
>SELECT *
>
>FROM new_table
>```
</details><br>


<details><summary>Favorite solution</summary><br>

>```SQL
>select
>  name as product_name,
>  extract(year from date)::int as year,
>  extract(month from date)::int as month,
>  extract(day from date)::int as day,
>  sum(price * count) as total
>from sales_details sd
>join sales s on sd.sale_id = s.id
>join products p on sd.product_id = p.id
>group by name, rollup(year, month, day)
>order by product_name, year, month, day
>```

></details>

  
 <img align="right" src="https://media.tenor.com/8oRk0EBWv1AAAAAi/bugcat-capoo.gif" height="100"/> 
  
---
<br>
  
  
## Present JSON data the SQL way

**DESCRIPTION:**

**Task**
Given the database where users are stored in JSON format, fetch the records splitting the data into separate columns.

**Notes**
* The ```private``` field determines whether the user's email address should be publicly visible
* If the profile is private, ```email_address``` should equal ```"Hidden"```
* The users may have multiple email addresses
* If no email addresses are provided, ```email_address``` should equal ```"None"```
* If there're multiple email addresses, the first one should be shown
* The ```date_of_birth``` is in the ```yyyy-mm-dd``` format
* The ```age``` fields represents the user's age in years
* Order the result by the ```first_name```, and ```last_name``` columns
  

**Input table**  
  

| Table | Column | Type |
|-------|--------|------|
| users | id     | int  |
|       | data   | json |
 
  
**JSON object format**  
  
|     Field       |       Type       |
|-----------------|------------------|
| first_name      | string           |
| last_name       | string           |
| date_of_birth   | string           |
| email_addresses | array of strings |
| private         | boolean          |
  
  
  
**Output table**  
  
|    Column     | Type |
|---------------|------|
| first_name    | text |
| last_name     | text |
| age           | int  |
| email_address | text |
  
  
<br>
<details><summary>My Solution</summary> <br>
  
>```SQL
>SELECT --* ,
>       data ->> 'first_name' as first_name ,
>       data ->> 'last_name' as last_name ,
>       EXTRACT (YEAR FROM AGE(CURRENT_DATE, CAST(data ->> 'date_of_birth' AS DATE))) as age ,
>       
>       CASE WHEN (CAST (data ->> 'private' AS BOOLEAN)) = TRUE
>            THEN 'Hidden'
>            WHEN (data #>> '{email_addresses, 0}') IS NULL
>            THEN 'None'
>            ELSE data #>> '{email_addresses, 0}'
>            --ELSE CONCAT_WS(', ', data #>> '{email_addresses, 0}', data #>> '{email_addresses, 1}' )
>            END AS email_address 
>     --  data #>> '{email_addresses, 0}'  as email_addresses,
>       
>     --  CAST (data ->> 'private' AS BOOLEAN) as private
>       
>
>FROM users
>
>ORDER BY first_name, last_name
>```
</details><br>


<details><summary>Favorite solution 1</summary><br>

>```SQL
>select 
>  data->>'first_name' as first_name,
>  data->>'last_name' as last_name,
>  extract(year from age(now(), (data->>'date_of_birth')::date))::integer as age,
>  case
>    when data->>'private' = 'true' then 'Hidden'
>    when data->>'private' = 'false' and data#>>'{email_addresses, 0}' is null then 'None'
>    else data#>>'{email_addresses, 0}'
>  end as email_address
>from users
>order by first_name, last_name
>```

></details><br>
  
  
 <details><summary>Favorite solution 2</summary><br>

>```SQL
>CREATE TYPE data_t AS  (
>  first_name         name,
>  last_name          name,
>  date_of_birth      date,
>  email_addresses    jsonb, -- text[]
>  private            boolean
>);
>
>SELECT first_name,  last_name,
>  EXTRACT(YEAR from age(date_of_birth))::int as age,
>  CASE
>    WHEN private THEN 'Hidden'
>    ELSE coalesce(email_addresses->>0, 'None')
>  END as email_address
>
>FROM users, json_populate_record(null::data_t, users.data)
>ORDER BY first_name, last_name
>```

></details>

---
<br>
  
  

## Present XML data the SQL way

**DESCRIPTION:**

**Task**
Given the database where all the users' data is stored in one huge XML string, fetch it as separate rows and columns.

**Notes**
* The ```private``` field determines whether the user's email address should be publicly visible
* If the profile is private, ```email_address``` should equal ```"Hidden"```
* The users may have multiple email addresses
* If no email addresses are provided, ```email_address``` should equal ```"None"```
* If there're multiple email addresses, the first one should be shown
* The ```date_of_birth``` is in the ```yyyy-mm-dd``` format
* The ```age``` fields represents the user's age in years
* Order the result by the ```first_name```, and ```last_name``` columns
  

**Input table**  
  

| Table | Column | Type |
|-------|--------|------|
| users | id     | int  |
|       | data   | xml  |
 
  
**XML format**  
  
```
<data>
    <user>
        <first_name>...</first_name>
        <last_name>...</last_name>
        <date_of_birth>...</date_of_birth>
        <private>...</private>
        <email_addresses>
            <address>...</address>
            <address>...</address>
            ...
            <address>...</address>
        </email_addresses>
    </user>
    <user>...</user>
    ...
    <user>...</user>
</data>
```
  
**Output table**  
  
|    Column     | Type |
|---------------|------|
| first_name    | text |
| last_name     | text |
| age           | int  |
| email_address | text |  
  
 
<br>
<details><summary>My Solution</summary> <br>
  
>```SQL
>select
>  (xpath('/user/first_name/text()', data))[1]::text as first_name,
>  (xpath('/user/last_name/text()', data))[1]::text as last_name,
>  EXTRACT (YEAR FROM AGE(((xpath('/user/date_of_birth/text()', data))[1]::text)::date))::int as age,
>  case
>    when (xpath('/user/private/text()', data))[1]::text = 'true' then 'Hidden'
>    when not xpath_exists('/user/email_addresses/address', data) then 'None'
>    else (xpath('/user/email_addresses/address/text()', data))[1]
>  end as email_address
>from unnest(xpath('/data/user', (select data from users limit 1))) as data
>order by first_name, last_name;
>```
</details><br>


<details><summary>Favorite solution</summary><br>

>```SQL
>SELECT 
>first_name, 
>last_name, 
>DATE_PART('year', AGE(date_of_birth))::integer as age,
>CASE
>    WHEN private = true THEN 'Hidden'
>    WHEN email IS NULL THEN 'None'
>    ELSE email
>END as email_address
>FROM users x,
>   XMLTABLE('/data/user'
>     PASSING x.data
>     COLUMNS 
>       first_name     VARCHAR(50)   PATH 'first_name',
>       last_name      VARCHAR(50)   PATH 'last_name',
>       date_of_birth  DATE          PATH 'date_of_birth',
>       private        BOOLEAN       PATH 'private',
>       email          TEXT          PATH 'email_addresses/address[1]'
>     ) xt
>order by first_name, last_name;
>```

></details>

  
  <img align="right" src="https://media.tenor.com/Z-4mle3_GgwAAAAi/bugcat-capoo.gif" height="100"/>
  
---
<br>

  
  
  
  ## <title of the challenge>

**DESCRIPTION:**

**people table schema**
* id
* name
* age

**return table schema**
* age
* total_people

  
```SQL

```

  
```SQL

``` 

  
  
<br>
<details><summary>My Solution</summary> <br>
  
>```SQL

>```
</details><br>


<details><summary>Favorite solution</summary><br>

>```SQL

>```

></details>

---
<br>
  


