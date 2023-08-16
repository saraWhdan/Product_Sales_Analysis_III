
## Product Sales Analysis III

LeetCode Link: [Product Sales Analysis III](https://leetcode.com/problems/product-sales-analysis-iii/description/?envType=study-plan-v2&envId=top-sql-50)


SQL Query:

```sql
SELECT s.product_id, s.year AS first_year, s.quantity, s.price
FROM Sales s 
INNER JOIN (
    SELECT product_id, MIN(year) AS first_year
    FROM Sales
    GROUP BY product_id
) first_year_sales ON s.product_id = first_year_sales.product_id AND s.year = first_year_sales.first_year;
```
# illustration
في البدايه انا عملت Subquery عشان احسب الminimum year (اول سنه) لكل Product
```sql
SELECT product_id, MIN(year) AS first_year
FROM Sales
GROUP BY product_id
```
كده انا عنديtable فيه ال product_id  واول سنه اتعمل فيها


ال table ده انا عملتله join مع Sales table بحيث اقدر اوصل للمطلوب 
