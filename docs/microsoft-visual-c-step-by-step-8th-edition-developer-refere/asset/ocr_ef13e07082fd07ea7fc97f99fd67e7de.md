to write to add data access capabilities to an app. This is where you will start, but first you need to set up the AdventureWorks database, which contains the details of Adventure Works customers.

# Note

There is not sufficient space in this book to go into great detail on how to use the Entity Framework, and the exercises in this section walk you through only the most essential steps to get started. If you want more information, look at “Entity Framework” on the Microsoft website at http://msdn.microsoft.com/data/aa937723.

To make the scenario more realistic, the exercises in this chapter show you how to create the database in the cloud by using Microsoft Azure SQL Database and how to deploy the web service to Azure. This architecture is common to many commercial apps, including ecommerce applications, mobile banking services, and even video streaming systems.

# Note

The exercises require that you have an Azure account and subscription. If you don’t already have an Azure account, you can sign up for a free trial account at https://azure.microsoft.com/pricing/free-trial/. Additionally, Azure requires that you have a valid Microsoft account with which it can associate your Azure account. You can sign up for a Microsoft account at https://signup.live.com/.

# Create an Azure SQL Database server and install the AdventureWorks sample database

+   1. Using a web browser, connect to the Azure portal at https://portal.azure.com. Sign in using your Microsoft account.
+   2. In the toolbar on the left of the portal, click New.
+   3. On the Create page, click Data + Storage, and then click SQL Database.
+   4. In the SQL Database pane, perform the following tasks:
+      a. In the Name box, type AdventureWorks.
+      b. Click Server, and then click Create A New Server. In the New Server pane, type a unique name for your server. (Use your company name or even your own name—I used csharpstepbystep. If the name you enter has been used by someone else, you will be alerted, in which case enter