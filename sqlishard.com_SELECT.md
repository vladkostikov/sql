### [SELECT Exercises](http://www.sqlishard.com/Exercise#/exercises/SELECT)

#### S1.0 - SELECT
Try using the SELECT statement to retrieve rows from the Customers table.\
`SELECT * FROM Customers;`

#### S1.1 - SELECT Columns
Try editing your query to retrieve only the Id and FirstName columns.\
`SELECT Id, FirstName FROM Customers;`

#### S1.2 - SELECT Columns
Last time we SELECTed the Id and FirstName columns,
let's SELECT them in the reverse order now (SELECT FirstName, Id ...)\
`SELECT FirstName, Id FROM Customers;`

#### S2.0 - WHERE
A numeric condition to filter on id's that are equal to 5 would
look like: id = 5. Let's SELECT all columns (*) FROM the Customers table
using that example condition.\
`SELECT * FROM Customers WHERE id = 5;`

#### S2.1 - WHERE conditions
Let's select all columns (*) from Orders that have an OrderTotal
BETWEEN 100 and 200.\
`SELECT * FROM Orders WHERE OrderTotal BETWEEN 100 AND 200;`

#### S2.2 - WHERE conditions
Let's select all columns (*) from Orders where the DeliveryTime is
less than June 20th, 2013.\
`SELECT * FROM Orders WHERE DeliveryTime < '2013-06-20';`

#### S2.3 - LIKE
Let's select all columns (*) from Customers whose
LastName starts with the letter A.\
`SELECT * FROM Customers WHERE LastName LIKE 'A%';`

#### S2.4 - OR
Let's select all columns (*) from Customers where their FirstName
starts with A or their Id is less than 10.\
`SELECT * FROM Customers WHERE FirstName LIKE 'A%' OR Id < 10;`

#### S2.5 - AND
Let's select all columns (*) from Orders where their OrderTotal
is greater than 100 AND their OrderTime is greater than October 12th, 2012.\
`SELECT * FROM Orders WHERE OrderTotal > 100 AND OrderTime > '2012-10-12';`

#### S2.6 - Complex AND/OR
Let's select all columns (*) from Orders where their OrderTotal
is greater than 300 plus all records where the OrderTotal is greater than 200
and the OrderTime is after November 15th, 2012.\
`SELECT * FROM Orders WHERE OrderTotal > 300 OR  OrderTotal > 200
AND OrderTime > '2012-11-15';`

#### S3.0 - ORDER BY
Let's SELECT all columns (*) from Orders and ORDER BY their OrderTotal.\
`SELECT * FROM Orders ORDER BY OrderTotal;`

#### S3.1 - ORDER BY DESC
SELECT all columns (*) from Orders again, but this time
ORDER BY their DeliveryTime in descending order\
`SELECT * FROM Orders ORDER BY DeliveryTime DESC;`

#### S3.2 - More ORDER BY
Let's SELECT everyone (*) from the Customers and sort them by LastName
and FirstName to see this in practice. Customers with matching last names
will be sub-sorted by their first names.\
`SELECT * FROM Customers ORDER BY LastName,  FirstName;`

#### S1.0 to 3.2 - Recap
Let's put it all together. Let's select all columns from the Orders table where
the OrderTime is earlier than 2013-02-01 and the DeliveryTime is later than
2013-01-31 and then finally order those records by the OrderTotal descending.\
`SELECT * FROM Orders WHERE OrderTime < '2013-02-01' AND
DeliveryTime > '2013-01-31' ORDER BY OrderTotal DESC;`

#### S4.0 - Qualified Columns
Using the example query above, create a query for the Customers.Id column
where the Id is less than 5. Use the two part Table.Column method whereever
you access the Id column.\
`SELECT Customers.Id FROM Customers WHERE Customers.Id < 5;`

#### S4.1 - Table Aliases
In this example I have used "C" as an alias for the Customers table.
Starting with a similar query, retrieve all columns (*) from Customers where
the Id is less than 10, and use an alias of CUST for the Customers table.\
`SELECT * FROM Customers CUST WHERE CUST.Id < 10;`

#### S4.2 - Column Aliasing
Try selecting the Id column from the Orders table, but alias it as "OrderId"
and only include rows where the OrderTotal is less than 50.\
`SELECT Id AS OrderId FROM Orders WHERE OrderTotal < 50;`

#### S5.0 - INNER JOIN
Try using the INNER JOIN syntax to SELECT all columns from the Customers
and Orders tables where the CustomerId column in Orders matches the Id column
in Customers. Since both tables have an Id column, you will need to qualify the
Customers id in the WHERE clause with either the table name or a table alias.\
`SELECT * FROM Customers INNER JOIN Orders ON Customers.Id = Orders.CustomerId;`

#### S5.1 - JOIN w/ WHERE
Try using the INNER JOIN syntax to SELECT all columns from the Customers and
Orders tables using the ON statement above and a WHERE statement to limit
the results to rows with an OrderTotal greater than 200.\
`SELECT * FROM Customers C INNER JOIN Orders O ON O.CustomerId = C.Id
WHERE OrderTotal > 200;`
