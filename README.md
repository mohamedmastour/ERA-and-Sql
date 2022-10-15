# ERA-and-Sql
#1-Find the names of the top 10 employees who sold the most number of orders, and order them in descending order showing the highest first#

SELECT employees.FirstName AS Employee_FirstName, employees.lastname AS Employee_LastName,
count(orders.orderID) AS Number_of_orders FROM [Orders]INNER 
JOIN [employees] on[Orders].employeeID= [employees].employeeID 
GROUP BY employees.employeeid 
ORDER BY count(orders.orderid) desc LIMIT 10



#2-Find the names of the 10 employees who sold the highest quantity of sales, in “Beverages” Category, and order them in descending order showing the highest first#

SELECT Employee_FirstName, Employee_LastName, count (Quantity) Total_Quantity 
FROM
(SELECT employees.FirstName AS Employee_FirstName, employees.lastname AS Employee_LastName, orders.orderID, orderdetails.Quantity
FROM [Orders]  
INNER JOIN [employees] ON [Orders].employeeID= [employees].employeeID 
INNER JOIN [orderdetails] ON [Orders].orderID= [orderdetails].orderID  
INNER JOIN [products] on [products].productID= [orderdetails].ProductID  
INNER JOIN [categories] on [categories].categoryID= [products].categoryID 
WHERE [categories].CategoryName= 'Beverages')
GROUP BY Employee_FirstName, Employee_LastName 
ORDER BY Total_quantity desc
