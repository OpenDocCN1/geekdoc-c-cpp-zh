# The tables that make up the Halloween database

![](bbox=[0.15, 0.095, 0.84, 0.4])

# Description

+   - The Categories table contains a row for each product category. Its primary key is CategoryID, a 10-character code that identifies each category.
+   - The Products table contains a row for each product. Its primary key is ProductID, a 10-character code that identifies each product. CategoryID is a foreign key that relates each product to a row in the Categories table.
+   - The States table contains a row for each state. Its primary key is StateCode, a 2-character code that identifies each state.
+   - The Customers table contains a row for each customer. Its primary key is Email, which identifies each customer by his or her email address. State is a foreign key that relates each customer to a row in the States table.
+   - The Invoices table contains a row for each invoice. Its primary key is InvoiceNumber, an identity column that’s generated automatically when a new invoice is created. CustEmail is a foreign key that relates each invoice to a row in the Customers table.
+   - The LineItems table contains one row for each line item of each invoice. Its primary key is a combination of InvoiceNumber and ProductID. InvoiceNumber is a foreign key that relates each line item to an invoice, and ProductID is a foreign key that relates each line item to a product.
+   - The relationships between the tables in this diagram appear as links, where the endpoints indicate the type of relationship. A key indicates the “one” side of a relationship, and the infinity symbol (∞) indicates the “many” side.