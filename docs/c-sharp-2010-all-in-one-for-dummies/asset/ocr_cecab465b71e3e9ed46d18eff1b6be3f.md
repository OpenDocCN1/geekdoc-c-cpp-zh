relationship between the form controls and the Data namespace, it often seems like the data lives right inside the controls, especially when you're dealing with Windows Forms.

In the following sections, you deal primarily with the visual tools, which are as much a part of the C# experience as the code. First, I go over connecting to data sources, and then I show you how to write a quick application using one of those connections. Finally, I go over a little of the code side.

To make all this work, you need to have some kind of schema set up in your database. It can be a local project of your own creation or a sample schema. The next section tells you how.

# Setting up a sample database schema

To get started, direct your browser to www.microsoft.com/sqlserver/2005/en/us/express-starter-schemas.aspx. If this URL doesn't work, search the Web for SQL Server 2008 sample schema and find the nearest Microsoft link. It should get you there.

This page offers two sample listings — sample applications and sample schemas. The sample applications are full-blown applications that show complete end-to-end implementation of data-driven software built using .NET. Some are in C#, some are in Visual Basic. The sample schemas are databases only and are designed for database administrators to practice getting experience in handling the system.

Any of the sample schemas will work. If you want exactly the same one as I use in the examples here, choose the Asset Management schema. Other options may be a better fit for the work you're doing. They include

+   - Assets Maintenance
+   - Contact Management
+   - Customers and Orders
+   - Document Management
+   - e-Commerce
+   - Helpdesk
+   - Issue Tracking Software
+   - Retail Inventory Control
+   - Not for Profits
+   - Product Catalogs