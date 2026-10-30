# FIGURE 4.5

Moving customer data to its own table.

![](bbox=[0.18, 0.21, 0.78, 0.58])

The customer and the book are still integral to the order (just not the name and title), and we need a way to relate the tables to each other. While the customer may change names, the customer can't change the BookstoreID because we created it and we control it. Similarly, the publisher may change the book's title but not the BookID. The primary keys of tblBookstores and tblBooks are reliable pointers to the objects they identify, regardless of what other information may change.

Figure 4.6 shows our three tables, but instead of a customer name and a book title, tblBookOrders4 now contains the primary key of its related record in both tblBookstores and tblBooks. When the primary key of one table is used as a field in another table, it's called a foreign key.

Before we split out the customer data to its own table, if Uptown Books changed its name to Uptown Books and Periodicals, we would have to identify all the rows in tblBookOrders3 that had a customer of Uptown Books and change the field's value for each row identified.

Overlooking an instance of the customer's name during this process is called an update anomaly and results in records that are inconsistent with the other records in the database. From the database's perspective, Uptown Books and Uptown Books and Periodicals are two completely different organizations, even if we know that they're the same store. A query to retrieve all the orders placed by Uptown Books and Periodicals will miss any records that still have Uptown Books in the Customer field because of the update anomaly.