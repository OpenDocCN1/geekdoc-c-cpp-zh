# 23.4.2 Passing Dataset through Web Services

Web Services provide efficient data delivery mechanism for using disconnected dataset.
Below is the process description of how to dataset is passed via Web Services

# Step 1 : To create data.

There are three database tables in SQL Server :

+   1. An Affiliate table, which has information about all the affiliates in the program
+   2. A Customer table, which keeps track of the customers who have made purchases, including a foreign key relationship with the Affiliate who referred this customer to the site.
+   3. A Purchase table, which has the details about each purchase a particular customer has made on the site.

The Web site owner can integrate the data from this Web service into his existing customer management application, his accounting application, or into his Web site in whatever way has been chosen.

# Step 2 : Writing web service and passing data

+   1. Create a new Visual Basic.NET Web Service project and rename the "service1.asmx" file to "AffiliateManagement.asmx".
+   
+   2. In the Server Explorer, create a Data Connection to the database in which the tables are created, then navigate to the Purchase table, and drag-and-drop the table onto the Web service Designer Surface. This creates a SQL Connection and a SQL Data Adapter on the Web service's Designer Surface.
+   
+   3. Select the SQL Data Adapter and select the "Configure Data Adapter..." link at the bottom of the Properties window. This opens the "Data Adapter Configuration Wizard."
+   
+   4. Use the Query Builder to create a SELECT statement that grabs all of the purchase information from the Purchase table and some customer information, (ESPECIALLY the affiliate_id) from the Customer table. The SELECT statement looks like this,
+   
+   ```sql
+   SELECT purchase.purchase_id, purchase.purchase_date, purchase.purchase_amount,
+   purchase.customer_id, purchase.commission_due, purchase.commission_paid_date,
+   customer.customer_name, customer.customer_email, customer.customer_id
+   FROM purchase
+   INNER JOIN customer ON purchase.customer_id = customer.customer_id WHERE
+   (customer.affiliate_id = @affiliate)
+   ```