
## FIGURE 4.4

First normal form at last!

![](img/1e45673ab6eca9d20e67635ff5b9b318_136_0.png)

The table in Figure 4.4 contains the same data as shown in Figure 4.2 and Figure 4.3. The new arrangement, however, makes it much easier to work with the data. For example, queries are easily constructed to return the total number of a particular book ordered by customers or to determine which titles have been ordered by a particular bookstore.

> Tip
> Your tables should always be in first normal form. Make sure each cell of the table contains a single value, don’t mix values within a cell, and don’t have repeating groups (as you saw in Figure 4.3).

The table design optimization is not complete at this point, however. Much remains to be done with the BookOrders data and the other tables in this application. In particular, the table shown in Figure 4.4 contains redundant information. The book titles are repeated each time customers order the same book, and the order number and order date are repeated for all the rows for an order.

A subtler issue is the fact that the OrderID can no longer be used as the table’s primary key. Because the OrderID is duplicated for each book title in an order, it can’t be used to identify individual records in the table. Instead, the OrderID field is now a key field for the table and can be used to locate all the records relevant to a particular order. The next step of optimization corrects this situation.

## Second normal form

A more efficient design results from splitting the data in tblBookOrders into multiple tables to achieve second normal form (2NF). The second rule of normalization states the following:

Data not directly dependent on the table's primary key is moved into another table.

This rule means that a table should contain data that represents a single entity. Because we're gradually turning one unnormalized table into normalized data, tblBookOrders3 doesn't have a primary key. We'll ignore that fact for the time being and think of each row in a table as an entity. All the data in that row that isn't an integral part of the entity is moved to a different table. In tblBookOrders3, neither the Customer field nor the Title field is integral to the order and should be moved to a different table.

### Identifying entities

But aren't customers integral to an order? Yes, they are. However, the data that's stored in tblBookOrders3 in the Customer field is the customer's name. If the customer were to change names, it would not fundamentally change the order. Similarly, while the book is integral to the order, the book's title is not.

To remedy this situation, we need separate tables for customers and books. First, create a new table named tblBookstores, as shown in Figure 4.5.

To create tblBookstores follow these steps:

- 1. Click Table Design on the Create tab of the Ribbon.
- 2. Add an AutoNumber field named BookstoreID.
- 3. Click Primary Key on the Table Tools Design tab of the Ribbon.
- 4. Add a Short Text field named StoreName.
- 5. Set the Field Size of StoreName to 50.
- 6. Save the table as tblBookstores.

You can imagine that we want to store some more information about customers, such as their mailing addresses and phone numbers. For now, we're getting our data into 2NF by moving data that isn't integral to an order to its own table.

Next create a table for books by following these steps:

- 1. Click Table Design on the Create tab of the Ribbon.
- 2. Add an AutoNumber field named BookID.
- 3. Click Primary Key on the Table Tools Design tab of the Ribbon.
- 4. Add a Short Text field named BookTitle.
- 5. Save the table as tblBooks.

## FIGURE 4.5

Moving customer data to its own table.

![](img/1e45673ab6eca9d20e67635ff5b9b318_138_0.png)

The customer and the book are still integral to the order (just not the name and title), and we need a way to relate the tables to each other. While the customer may change names, the customer can't change the BookstoreID because we created it and we control it. Similarly, the publisher may change the book's title but not the BookID. The primary keys of tblBookstores and tblBooks are reliable pointers to the objects they identify, regardless of what other information may change.

Figure 4.6 shows our three tables, but instead of a customer name and a book title, tblBookOrders4 now contains the primary key of its related record in both tblBookstores and tblBooks. When the primary key of one table is used as a field in another table, it's called a foreign key.

Before we split out the customer data to its own table, if Uptown Books changed its name to Uptown Books and Periodicals, we would have to identify all the rows in tblBookOrders3 that had a customer of Uptown Books and change the field's value for each row identified.

Overlooking an instance of the customer's name during this process is called an update anomaly and results in records that are inconsistent with the other records in the database. From the database's perspective, Uptown Books and Uptown Books and Periodicals are two completely different organizations, even if we know that they're the same store. A query to retrieve all the orders placed by Uptown Books and Periodicals will miss any records that still have Uptown Books in the Customer field because of the update anomaly.

## FIGURE 4.6

The first step in making our table 2NF.

![](img/1e45673ab6eca9d20e67635ff5b9b318_139_0.png)

Another advantage of removing the customer name from the orders table is that the name now exists in only one location in the database. If Uptown Books changes its name to Uptown Books and Periodicals, we now only have to change its entry in the tblBookstores table. This single change is reflected throughout the database, including all forms and reports that use the customer name information.

Identifying separate entities and putting their data into separate tables is a great first step to achieving second normal form. But we’re not quite done. Our orders table still doesn’t have a unique field that we can use as the primary key. The OrderID field has repeating values that provide a clue that there is more work to be done to achieve 2NF.

### Less obvious entities

Customers and books are physical objects that are easy to identify as separate entities. The next step is a little more abstract. Our orders table, now called tblBookOrders4, still contains information about two separate, but related, entities. The order is one entity, and the order details (the individual lines on the order) are entities all their own.

## Chapter 4: Understanding Table Relationships

The first three records of tblBookOrders4, shown in Figure 4.6, contain the same OrderID, OrderDate, and BookStoreID. These three fields are characteristics of the order as a whole, not of each individual line on the order. The Quantity and BookID fields contain different values in those three first records. Quantity and BookID are characteristics of a particular line on the order.

> **TIP**
> 
> Values that repeat in multiple records, like OrderID in tblBookOrders4 shown in Figure 4.6, are an indication that your data is not yet in second normal form. Some data, like foreign keys, is meant to repeat. Other data, like dates and quantities, repeats naturally and is not indicative of a problem.

The last step to get our order data into second normal form is to put the information integral to the order as a whole into a separate table from the information for each line on the order. Create a new table named tblBookOrderDetails with the fields BookOrderDetailID, Quantity, and BookID. BookOrderDetailID is an AutoNumber field that will serve as the primary key, and BookID is a foreign key field that we use to relate the two tables. Figure 4.7 shows our new orders table, tblBookOrders5, and our new details table, tblBookOrderDetails.

The OrderID field in tblBookOrders5 was deleted and a new AutoNumber field named OrderID was created. Now that we have a unique field in the orders table, we can set OrderID as the primary key. All the data in each record of tblBookOrders5 directly relates to an order entity. Or, in 2NF language, all the data is directly dependent on the primary key.

The OrderID field in tblBookOrderDetails is a foreign key that is used to relate the two tables together. Figure 4.7 shows that the first three records in tblBookOrderDetails show an OrderID of 1 that maps to the first record of tblBookOrders5.

All the fields in tblBookOrderDetails are directly dependent on the primary key BookOrderDetailID. The quantity from the first record, 10, relates directly to the line item on the order. It only relates to the order as a whole indirectly, just as the quantities from the next two records, 5 and 7, do. That indirect relationship is created by including the OrderID foreign key in the record.

The original table, tblBookOrders1, contained data about several different entities in each record. Through a series of steps, we split the data into four tables—tblBookOrders5, tblBookOrderDetails, tblBookStores, and tblBooks—each of which contains data about one entity. Our data is finally in the second normal form.

Breaking a table into individual tables, each of which describes some aspect of the data, is called decomposition. Decomposition is a very important part of the normalization process. Even though the tables appear smaller than the original table (refer to Figure 4.2), the data contained within the tables is the same as before.
