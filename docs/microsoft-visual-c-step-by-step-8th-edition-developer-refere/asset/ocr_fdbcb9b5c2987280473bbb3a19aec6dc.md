The preceding exercise shows the performance improvement you can attain by making a small change to a LINQ query. However, keep in mind that you will see results such as this only if the calculations performed by the query take some time. I cheated a little by spinning the processor. Without this overhead, the parallel version of the query is actually slower than the serial version. In the next exercise, you will see a LINQ query that joins two arrays in memory. This time, the exercise uses more realistic data volumes, so there is no need to slow down the query artificially.

# Parallelize a LINQ query that joins two collections

1. In Solution Explorer, open the Data.cs file in the Code and Text Editor window and locate the CustomersInMemory class.

This class contains a public string array called Customers. Each string in the Customers array holds the data for a single customer, with the fields separated by commas; this format is typical of data that an application might read in from a text file that uses comma-separated fields. The first field contains the customer ID, the second field contains the name of the company that the customer represents, and the remaining fields hold the address, city, country or region, and postal code.

2. Find the OrdersInMemory class.

This class is similar to the CustomersInMemory class except that it contains a string array called Orders. The first field in each string is the order number, the second field is the customer ID, and the third field is the date that the order was placed.

3. Find the OrderInfo class. This class contains four fields: the customer ID, company name, order ID, and order date for an order. You will use a LINQ query to populate a collection of OrderInfo objects from the data in the Customers and Orders arrays.

4. Display the Program.cs file in the Code and Text Editor window and locate the Test2 method in the Program class.

In this method, you will create a LINQ query that joins the Customers and Orders arrays by using the customer ID to return a list of customers and the orders that each customer has placed. The query will store each row of the result in an OrderInfo object.

5. In the try block in this method, after the first TO DO comment, add the code shown next in bold:

Click here to view code image

```
// TO DO: Create a LINQ query that retrieves customers and orders
from arrays
// Store each row returned in an OrderInfo object
var orderInfoQuery = from c in CustomersInMemory.Customers
```