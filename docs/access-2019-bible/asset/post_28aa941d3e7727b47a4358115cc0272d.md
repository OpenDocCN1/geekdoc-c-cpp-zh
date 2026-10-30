
of the real value you're tracking along with a sequence number (such as A001, A002, A003, B001, B002, and so on). The method may rely on a random set of letters and numbers for the field content (as long as each field has a unique value) or a complicated calculation based on information from several fields in the table.

However, there is no reason why the primary key value has to be meaningful to the application. A primary key exists in a table solely to ensure uniqueness for each row and to provide an anchor for table relationships. Many Access developers routinely use AutoNumber fields as primary keys simply because they meet all the requirements of a primary key without contributing to an application's complexity.

In fact, meaningful primary keys can cause confusion as the data in the table changes. For example, if the primary key for a table of employee information is the first letter of the employee's last name plus a sequential number, then Jane Doe might have an EmployeeID of D001. If Jane were to get married and change her last name, her EmployeeID would no longer be consistent with the data in her record. Her EmployeeID may still be unique, but it may also cause confusion if someone were to rely on that data.

Table 4.1 lists the Collectible Mini Cars tables and describes one possible plan for deriving the primary key values in each table. As this table shows, it doesn't take a great deal of work (or even much imagination) to derive a plan for key values. Any rudimentary scheme with a good sequence number always works. Access automatically tells you when you try to enter a duplicate key value. To avoid duplication, you can simply add the value of 1 to the sequence number.

## TABLE 4.1 Deriving the Primary Key

| Table | Possible Derivation of Primary Key Value |
|---|---|
| tblCustomers | Companies: AutoNumber field assigned by Access |
| tblSales | Invoice Number: AutoNumber field |
| tblSalesLineItems | Invoice Number (from Sales) and an AutoNumber field |
| tblProducts | Product Number, entered by the person putting in a new product |
| tblSalesPayments | Invoice Number (from Sales) and an AutoNumber field |
| tblSalesperson | Sales Person ID: AutoNumber field |
| tblCategories | Category of Items: Entered by the person putting in a new record |

Even though it isn't difficult to use logic (implemented, perhaps, though VBA code) to generate unique values for a primary key field, by far the simplest and easiest approach is to use AutoNumber fields for the primary keys in your tables. The special characteristics of the AutoNumber field (automatic generation, uniqueness, the fact that it can't be changed, and so on) make it the ideal candidate for primary keys. Furthermore, an AutoNumber value is nothing more than a 4-byte integer value, making it very fast and easy for the database engine to manage. For all these reasons, the Collectible Mini Cars exclusively uses AutoNumber fields as primary keys in its tables.

> NOTE
> AutoNumber fields are guaranteed to be unique, but they are not guaranteed to be sequential. There are a number of reasons why gaps in AutoNumbers can be introduced, such as deleting records, and you should never rely on AutoNumbers being sequential.

You may be thinking that all these sequence numbers make it hard to look up information in your tables. Just remember that, in most cases, you never look up information by an ID field. Generally, you look up information according to the purpose of the table. In tblCustomers, for example, you would look up information by customer name—last name, first name, or both. Even when the same name appears in multiple records, you can look at other fields in the table (zip code, phone number) to find the correct customer. Unless you just happen to know the customer ID number, you’ll probably never use it in a search for information.

## Looking at the benefits of a primary key

Have you ever placed an order with a company for the first time and then decided the next day to increase your order? When you call the people at the order desk, they may ask you for your customer number. You tell them that you don’t know your customer number. Next, they ask you for some other information—generally, your zip code and last name. Then, as they narrow down the list of customers, they ask your address. Once they’ve located you in their database, they can tell you your customer number. Some businesses use phone numbers or e-mail addresses as starting points when searching for customer records.

> Primary and foreign keys are discussed in Chapter 1, but because these concepts are so important in database applications, they’re covered again in this chapter.

Database systems usually have more than one table, and the tables are related in some manner. For example, in the Collectible Mini Cars database, tblCustomers and tblSales are related to each other through the CustomerID field. Because each customer is one person or organization, you only need one record in tblCustomers.

Each customer can make many purchases, however, which means you need to set up a second table to hold information about each sale—tblSales. Again, each invoice is one sale (on a specific day at a specific time). CustomerID is used to relate the customer to the sales.

A foreign key in the child table (the CustomerID field in the tblSales table) is related to the primary key in the parent table (CustomerID in tblCustomers).

Besides being a common link field between tables, the primary key field in an Access database table has the following advantages:

- Primary key fields are always indexed, greatly speeding up queries, searches, and sorts that involve the primary key field.
- Access forces you to enter a value (or automatically provides a value, in the case of AutoNumber fields) every time you add a record to the table. You're guaranteed that your database tables conform to the rules of referential integrity.
- As you add new records to a table, Access checks for duplicate primary key values and prevents duplicate entries, thus maintaining data integrity.
- By default, Access displays your data in primary key order.

> TIP
> An index is a special internal file that is created to put the records in a table in some specific order. For example, the primary key field in tblCustomers is an index that puts the records in order by CustomerID field. Using an indexed table, Access uses the index to quickly find records within the table.

## Designating a primary key

From the preceding sections, you're aware that choosing a table's primary key is an important step toward bulletproofing a database's design. When properly implemented, primary keys help stabilize and protect the data stored in your Access databases. As you read the following sections, keep in mind that the cardinal rule governing primary keys is that the values assigned to the primary key field within a table must be unique. Furthermore, the ideal primary key is stable.

## Single-field versus composite primary keys

Sometimes, when an ideal primary key doesn't exist within a table as a single value, you may be able to combine fields to create a composite primary key. For example, it's unlikely that a first name or last name alone is enough to serve as a primary key, but by combining first and last names with birth dates, you may be able to come up with a unique combination of values to serve as the primary key. As you'll see in the "Creating relationships and enforcing referential integrity" section later in this chapter, Access makes it very easy to combine fields as composite primary keys.

There are several practical considerations when using composite keys:

- None of the fields in a composite key can be null.
- Sometimes building a composite key from data naturally occurring within the table can be difficult. Sometimes records within a table differ by one or two fields, even when many other fields may be duplicated within the table.
- Each of the fields can be duplicated within the table, but the combination of composite key fields cannot be duplicated.
