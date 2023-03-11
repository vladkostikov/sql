### [AGGREGATE Exercises](http://www.sqlishard.com/Exercise#/exercises/AGGREGATE)

#### A1.0 - COUNT
Try writing a statement to count the records in Orders.
```sql
SELECT COUNT(*) FROM Orders;
```

#### A1.1 - SUM
Trying using a WHERE statement and the SUM function to return the OrderTotal
for orders placed after 1/1/2013 (hint: OrderTime).
```sql
SELECT SUM(OrderTotal) FROM Orders WHERE OrderTime > '2013-01-01';
```

#### A1.2 - GROUP BY
Try altering the query to return a Year and SUM of OrderTotal for each year.
```sql
SELECT Year(OrderTime) AS OrderYear,
  SUM(OrderTotal) AS TotalOfOrderTotal
FROM Orders
GROUP BY Year(OrderTime);
```

#### A1.3 - More GROUP BY
Now we have monthly order totals and they're in order by year and month.
Can you extend this to include grouping by Year, Month, and Day?
```sql
SELECT Year(OrderTime) AS OrderYear,
  Month(OrderTime) AS OrderMonth,
  Day(OrderTime) AS OrderDay,
  SUM(OrderTotal) AS OrderTotal
FROM Orders
GROUP BY Year(OrderTime), Month(OrderTime), Day(OrderTime)
ORDER BY Year(OrderTime), Month(OrderTime), Day(OrderTime);
```

#### A1.4 - MIN/MAX
Can you find the largest OrderTotal for each year?
```sql
SELECT Year(OrderTime) AS OrderYear,
  MAX(OrderTotal) AS LargestOrderTotal
FROM Orders
GROUP BY Year(OrderTime);
```

#### A1.5 - AVG/STDEV
Using the AVG function, can you calculate the average OrderTotal for each year?
```sql
SELECT Year(OrderTime) AS OrderYear,
  AVG(OrderTotal) AS AverageOrderTotal
FROM Orders
GROUP BY Year(OrderTime);
```

#### A2.0 - HAVING
This query will count how many orders each customer has placed, then filter
only for customers with more than 5. Try to alter this query to find
big spenders whose total OrderTotal is more than $1000.
```sql
SELECT CustomerId,
  SUM(OrderTotal) AS Total
FROM Orders
GROUP BY CustomerId
HAVING SUM(OrderTotal) > 1000;
```

#### A2.2 - ORDER BY
Can you change this query to find the 10 customers
that have spent the most using ORDER BY and SUM()?
```sql
SELECT TOP 10 CustomerId,
  SUM(OrderTotal) AS Total
FROM Orders
GROUP BY CustomerId
ORDER BY SUM(OrderTotal) DESC;
```

#### A2.3 - INNER JOIN
Using your previous query from 2.2 (top 10 customers that have spent the most),
can you expand it to return CustomerId, the total, and FirstName and LastName?
```sql
SELECT TOP 10 CustomerId,
  SUM(OrderTotal) AS Total,
  FirstName,
  LastName
FROM Orders O
  INNER JOIN Customers C ON C.Id = O.CustomerId
GROUP BY CustomerId, FirstName, LastName
ORDER BY SUM(OrderTotal) DESC;
```

#### A2.4 - LEFT JOIN
Can you use a LEFT JOIN to return LastName and SUM() of OrderTotal for all
customers, ORDERed from smalledt to largest SUM?
```sql
SELECT LastName, SUM(OrderTotal) AS Total
FROM Customers C
  LEFT JOIN Orders O ON C.Id = O.CustomerId
GROUP BY LastName
ORDER BY SUM(OrderTotal)
```

#### A3.0 - Putting it all together
Find the 10 customers who have had the longest delivery time,
MAX(DateDiff(minute,OrderTime,DeliveryTime)) and return their FirstName,
LastName, Order Id, and that elapsed delivery time in minutes.
```sql
SELECT TOP 10 O.Id,
  MAX(DateDiff(minute,OrderTime,DeliveryTime)) AS DeliveryTimeMinutes,
  FirstName,
  LastName
FROM Orders O
  INNER JOIN Customers C ON C.Id = O.CustomerId
GROUP BY O.Id, FirstName, LastName
ORDER BY DeliveryTimeMinutes DESC
```

#### A3.1 - Conditional Tricks
In the first CASE we return OrderTotal if the record is a saturday, or 0 if it
is not. Switch these to SUM instead of AVG and return 1 instead of OrderTotal,
this will give us a count of Saturday vs non-Saturday orders.
```sql
SELECT SUM(
  CASE WHEN DATEPART(weekday,OrderTime) = 1 THEN 1 ELSE NULL END) AS Saturdays,
  SUM(CASE WHEN DATEPART(weekday,OrderTime) = 1 THEN NULL ELSE 1 END) AS TheRest
FROM Orders
```

#### A3.2 - Conditional Tricks #2
Try using a GROUP BY to Count Orders on Saturdays vs not-saturdays
like this example.
```sql
SELECT COUNT(*) AS Orders,
  CASE WHEN DATEPART(weekday,OrderTime) = 1 THEN 'Saturday' ELSE 'Not Saturday' END AS Weekday
FROM Orders
GROUP BY CASE WHEN DATEPART(weekday,OrderTime) = 1 THEN 'Saturday' ELSE 'Not Saturday' END
```
