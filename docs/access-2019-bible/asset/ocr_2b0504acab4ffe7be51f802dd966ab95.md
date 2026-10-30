# FIGURE 3.15

Creating a composite primary key.

![](bbox=[0.2, 0.22, 0.8, 0.6])

Furthermore, when using composite keys, maintaining relationships between tables becomes more complicated because the fields comprising the primary key must be duplicated in all the tables containing related data. Using composite keys simply adds to the complexity of the database without adding stability, integrity, or other desirable features.

# Indexing Access Tables

Data is rarely, if ever, entered into tables in a meaningful order. Usually, records are added to tables in random order (with the exception of time-ordered data). For example, a busy order-entry system will gather information on a number of different customer orders in a single day. Most often, this data will be used to report orders for a single customer for billing purposes or for extracting order quantities for inventory management. The records in the Orders table, however, are in chronological order, which is not necessarily helpful when preparing reports detailing customer orders. In that case, you'd rather have data entered in customer ID order.

To further illustrate this concept, consider the Rolodex card file many people used to use to store names, addresses, and phone numbers. Assume for a moment that the cards in the file were fixed in place. You could add new cards, but only to the end of the card file. This