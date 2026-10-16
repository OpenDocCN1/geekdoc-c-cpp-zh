
Applying a set of rules to the database structure and content can ensure the integrity of data resources. These rules consist of table and column constraints, and will be discussed in detail in Chapter 5, “Creating, Populating, and Deleting Tables.”

## Referential Integrity

Referential integrity refers to the way in which database tables handle update and delete requests. Database tables frequently have a primary key where one or more columns have a unique value by which rows in a table can be identified and selected. Other tables may have one or more columns called a foreign key that are used to connect to some other table through its value. Database designers frequently apply rules to database tables to control what happens when a primary key value changes and its effect on one or more foreign key values in other tables. These referential integrity rules apply restrictions on the data that may be updated or deleted in tables.

Referential integrity ensures that rows in one table have corresponding rows in another table. This prevents lost linkages between data elements in one table and those of another enabling the integrity of data to always be maintained. Using the 3NF tables defined earlier, a foreign key called CUSTNUM can be defined in the PURCHASES table that corresponds to the primary key CUSTNUM column in the CUSTOMERS table. Users are referred to Chapter 5, “Creating, Populating, and Deleting Tables” for more details on assigning referential integrity constraints.

## Database Tables Used in This Book

This section describes a database or library of tables that is used by an imaginary computer hardware and software wholesaler. The library consists of six tables: Customers, Inventory, Invoice, Manufacturers, Products, and Purchases. The examples used throughout this book are based on this library (database) of tables and are described and displayed below. An alphabetical description of each table used throughout this book appears below.

## CUSTOMERS Table

The CUSTOMERS table contains customers that have purchased computer hardware and software products from a manufacturer. Each customer is uniquely identified with a customer number. A description of each column in the Customers table follows.

### Table 1.7: Description of Columns in the Customers Table

| Column | Description |
|---|---|
| CUSTNUM | Unique number identifying the customer. |
| CUSTNAME | Name of customer. |
| CUSTCITY | City where customer is located. |

## INVENTORY Table

The INVENTORY table contains customer inventory information consisting of computer hardware and software products. The Inventory table contains no historical data. As inventories are replenished, the old quantity is overwritten with the new quantity. A description of each column in the Inventory table follows.

### Table 1.8: Description of Columns in the Inventory Table

| Column | Description |
|---|---|
| PRODNUM | Unique number identifying product. |
| MANUNUM | Unique number identifying the manufacturer. |
| INVENQTY | Number of units of product in stock. |
| ORDDATE | Date product was last ordered. |
| INVENCST | Cost of inventory in customer’s stock room. |

## INVOICE Table

The INVOICE table contains information about customers who purchased products. Each invoice is uniquely identified with an invoice number. A description of each column in the Invoice table follows.

### Table 1.9: Description of Columns in the Invoice Table

| Column | Description |
|---|---|
| INVNUM | Unique number identifying the invoice. |
| MANUNUM | Unique number identifying the manufacturer. |
| CUSTNUM | Customer number. |
| PRODNUM | Product number. |
| INVQTY | Number of units sold. |
| INVPRICE | Unit price. |

## MANUFACTURERS Table

The MANUFACTURERS table contains companies who make computer hardware and software products. Two companies cannot have the same name. No historical data is kept in this table. If a company is sold or stops making computer hardware or software, then the manufacturer is dropped from the table. In the event that a manufacturer has an address change, the old address is overwritten with the new address. A description of each column in the Manufacturers table follows.

### Table 1.10: Description of Columns in the Manufacturers Table

| Column | Description |
|---|---|
| MANUNUM | Unique number identifying the manufacturer. |
| MANUNAME | Name of manufacturer. |
| MANUCITY | City where manufacturer is located. |
| MANUSTAT | State where manufacturer is located. |

## PRODUCTS Table

The PRODUCTS table contains computer hardware and software products offered for sale by the manufacturer. Each product is uniquely identified with a product number. A description of each column in the Products table follows.

### Table 1.11: Description of Columns in the Products Table

| Column | Description |
|---|---|
| PRODNUM | Unique number identifying the product. |
| PRODNAME | Name of product. |
| MANUNUM | Unique number identifying the manufacturer. |
| PRODTYPE | Type of product. |
| PRODCOST | Cost of product. |

## PURCHASES Table

The PURCHASES table contains computer hardware and software products purchased by customers. Each product is uniquely identified with a product number. A description of each column in the Purchases table follows.

### Table 1.12: Description of Columns in the Purchases Table

| Column | Description |
|---|---|
| CUSTNUM | Unique number identifying the customer. |
| ITEM | Name of product. |
| UNITS | Number of items purchased by customer. |
| UNITCOST | Cost of product. |

## Table Contents

An alphabetical list of tables, variables, and attributes for each table is displayed below.

### Output 1.1: Customers CONTENTS Output

| # | Variable | Type | Len | Label |
|---|---|---|---|---|
| 3 | custcity | Char | 20 | Customer's Home City |
| 2 | custname | Char | 25 | Customer Name |
| 1 | custnum | Num | 3 | Customer Number |

### Output 1.2: Inventory CONTENTS Output

| # | Variable | Type | Len | Format | Informat | Label |
|---|---|---|---|---|---|---|
| 4 | invencst | Num | 6 | DOLLAR10.2 |  | Inventory Cost |
| 2 | invnqty | Num | 3 |  |  | Inventory Quantity |
| 5 | manunum | Num | 3 |  |  | Manufacturer Number |
| 3 | orddate | Num | 4 | MMDDYY10. | MMDDYY10. | Date Inventory Last Ordered |
| 1 | prodnum | Num | 3 |  |  | Product Number |

### Output 1.3: Invoice CONTENTS Output

| # | Variable | Type | Len | Format | Label |
|---|---|---|---|---|---|
| 3 | custnum | Num | 3 |  | Customer Number |
| 1 | invnum | Num | 3 |  | Invoice Number |
| 5 | invprice | Num | 5 | DOLLAR12.2 | Invoice Unit Price |
| 4 | invqty | Num | 3 |  | Invoice Quantity - Units Sold |
| 2 | manunum | Num | 3 |  | Manufacturer Number |
| 6 | prodnum | Num | 3 |  | Product Number |

### Output 1.4: Manufacturers CONTENTS Output

| # | Variable | Type | Len | Label |
|---|---|---|---|---|
| 3 | manucity | Char | 20 | Manufacturer City |
| 2 | manuname | Char | 25 | Manufacturer Name |
| 1 | manunum | Num | 3 | Manufacturer Number |
| 4 | manustat | Char | 2 | Manufacturer State |

### Output 1.5: Products CONTENTS Output

| # | Variable | Type | Len | Format | Label |
|---|---|---|---|---|---|
| 3 | manunum | Num | 3 |  | Manufacturer Number |
| 5 | prodcost | Num | 5 | DOLLAR9.2 | Product Cost |
| 2 | prodname | Char | 25 |  | Product Name |
| 1 | prodnum | Num | 3 |  | Product Number |
| 4 | prodtype | Char | 15 |  | Product Type |

### Output 1.6: Purchases CONTENTS Output

| # | Variable | Type | Len | Format | Label |
|---|---|---|---|---|---|
| 1 | custnum | Num | 4 |  | Custnum |
| 2 | prodnum | Num | 3 |  | Prodnum |
| 4 | unitcost | Num | 4 | DOLLAR12.2 | Unitcost |
| 3 | units | Num | 3 |  | Units |

## The Database Structure

The logical relationship between each table, and the columns common to each, appear below.

Figure 1.2. Logical Database Structure

![](img/9d3e4d8fa063e50a0c9985e34cf9d6e8_36_0.png)

## Sample Database Tables

The following tables: Customers, Inventory, Manufacturers, Products, Invoice, and Purchases represent a relational database that will be illustrated in the examples in this book. These tables are small enough to follow easily, but complex enough to illustrate the power of SQL. The data contained in each table appears below.
