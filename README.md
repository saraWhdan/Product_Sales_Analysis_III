
## Product Sales Analysis III

LeetCode Link: [Product Sales Analysis III](https://leetcode.com/problems/product-sales-analysis-iii/description/?envType=study-plan-v2&envId=top-sql-50)


SQL Query using join:

```sql
SELECT s.product_id, s.year AS first_year, s.quantity, s.price
FROM Sales s 
INNER JOIN (
    SELECT product_id, MIN(year) AS first_year
    FROM Sales
    GROUP BY product_id
) first_year_sales ON s.product_id = first_year_sales.product_id AND s.year = first_year_sales.first_year;
```
### illustration
في البدايه انا عملت Subquery عشان احسب الminimum year (اول سنه) لكل Product
```sql
SELECT product_id, MIN(year) AS first_year
FROM Sales
GROUP BY product_id
```
كده انا عنديtable فيه ال product_id  واول سنه اتعمل فيها


ال table ده انا عملتله join مع Sales table بحيث اقدر اوصل للمطلوب 



## SQL Query using Rank() function:
```sql
select  product_id
  , first_year
  ,quantity
  ,price from(
  select product_id
  ,year first_year
  ,quantity
  ,price
  ,rank()over( PARTITION BY  product_id order by year ) year_rank
  from sales  
)t where year_rank=1
```


الطريقه الثانيه هي طريقه استخدام ال RANK() window function
-  اولا استخدمت `PARTITION BY` عشان اقسم ال sales ل partions
- بعد كده رتبتهم بالسنه
- واخيرا عملت condition بحيث ارجع اول سنه لكل product
 ## تقدروا تقرو على ال Rank() function اكثر من هنا: 
 https://www.sqlservertutorial.net/sql-server-window-functions/sql-server-rank-function/ 



