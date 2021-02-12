This challenge uses the W3Schools SQL playground

__Question 1: Which customers are from the UK?__ 

SELECT * \
FROM Customers \
WHERE Country = 'UK';

__Question 2: What is the name of the customer who has the most orders?__

WITH num_orders_cust AS ( \
  SELECT Customers.*, Orders.OrderID \
  FROM Customers \
  LEFT JOIN Orders \
  ON Customers.CustomerID = Orders.CustomerID) \
SELECT CustomerName, CustomerID, count(OrderID) \
  FROM num_orders_cust \
  GROUP BY CustomerID \
  ORDER BY count(OrderID) DESC \
  LIMIT 10;

__Ernst Handel__ has the most orders

__Question 3: Which supplier has the highest average product price?__

WITH supp_prods AS (\
  SELECT Suppliers.SupplierName,Products.* \
  FROM Suppliers \
  LEFT JOIN Products \
  ON Suppliers.SupplierID = Products.SupplierID) \
SELECT SupplierName, sum(Price)/count(ProductID) AS av_price \
  FROM supp_prods \
  GROUP BY SupplierName \
  ORDER BY av_price DESC \
  LIMIT 10;

__Aux joyeux ecclésiastiques__ has the highest average product price at 140.75

__Question 4: How many different countries are all the customers from? (Hint: consider DISTINCT.) 

SELECT COUNT(DISTINCT(Country))\
FROM Customers;

__21__ countries are represented

__Question 5: What category appears in the most orders?__ 

WITH prod_cats AS (\
  SELECT Products.ProductID,Products.CategoryID,OrderDetails.ProductID \
  FROM Products \
  LEFT JOIN OrderDetails \
  ON Products.ProductID = OrderDetails.ProductID) \
SELECT CategoryID, count(CategoryID) \
  FROM prod_cats \
  GROUP BY CategoryID \
  ORDER BY 2 Desc \
  Limit 10;

__CategoryID 4__ appears in the most orders

__Question 6: What was the total cost for each order?__ 

WITH orders_val AS (\
  SELECT OrderDetails.*,Products.Price\
  FROM OrderDetails LEFT JOIN Products\
  ON OrderDetails.ProductID = Products.ProductID)\
SELECT OrderID, Quantity*Price AS Total_amount\
 FROM orders_val\
 GROUP BY OrderID\
 ORDER BY Total_amount DESC\
 LIMIT 10;

__Question 7: Which employee made the most sales (by total price)?__ 

WITH orders_val AS (\
  SELECT OrderDetails.,Products.Price \
  FROM OrderDetails \
  LEFT JOIN Products \
  ON OrderDetails.ProductID = Products.ProductID) \
SELECT sum(orders_val.Quantity * orders_val.Price) AS total_val\
FROM orders_val LEFT JOIN Orders ON orders_val.OrderID = Orders.OrderID \
GROUP BY EmployeeID \
ORDER BY total_val DESC;

__EmployeeID 4__ made the most sales

__Question 8: Which employees have BS degrees?__

SELECT * \
FROM Employees \
WHERE Notes LIKE '%BS%';

__Employee ID 3 and 5__ have a BS degree

__Question 9: Which supplier of three or more products has the highest average product price?__

WITH supp_prices AS (\
  SELECT SupplierID, COUNT(ProductID) AS product_count, AVG(Price) AS average_price \
  FROM Products GROUP BY SupplierID) \
SELECT * \
  FROM supp_prices \
  WHERE product_count >= 3 \
  ORDER BY average_price DESC;

__Supplier ID 4__ has highest average product price
