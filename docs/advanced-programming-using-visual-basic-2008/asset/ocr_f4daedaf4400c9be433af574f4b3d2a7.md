# Writing Reports

Writing and printing reports is an extremely important topic for most business applications. Visual Studio offers several options for reporting applications, which are not available in Visual Basic Express Edition. The New Project dialog box includes a Reporting option, which contains templates for a Crystal Reports application and a Microsoft Reports application. Reporting templates are also available for Web applications.

By far, the most popular reporting tool for Visual Studio applications is the report designer called Crystal Reports, which is owned by Business Objects, a SAP company. The Crystal Report Gallery contains wizards to guide you in creating standard reports, forms, and even mailing labels, or you can use an existing report or generate a new one. You can display a report from a Windows Form or a Web Form.

Visual Studio 2008 (Professional Edition and above) includes Crystal Reports 2008 Basic. Note that Business Objects sells a version of Crystal Reports with more features than the one included in Visual Studio. As of this writing, the newest version is Crystal Reports 2008, which is compatible with VS 2008.

# Creating and Displaying a Crystal Reports

In this section, you will learn to create a Crystal Reports report template and display the report from a Windows application. Crystal Reports can connect to several types of data, including SQL Server, Access, Excel, and many others, including an ADO.NET DataSet, which can be based on many different types of objects, including business objects and collections.

# Creating a Grouped Report—Step-by-Step

This exercise walks you through the steps for creating a Crystal Report template in a Windows Form application. Figure 9.1 shows the completed report, which is based on the products and categories tables of the Northwind SQL Server database.

# Create the Project

+   STEP 1: Create a new Windows Forms application project called Ch09-DatasetSBS.
+   STEP 2: Rename the form to ReportForm.
+   STEP 3: Change the form's Text property to "Northwind Product Report"
+   STEP 4: Add Northwind Database as a new data source, selecting the products and categories tables. Save all.

# Begin the Report

+   STEP 1: In the Solution Explorer, right-click on the project name and select Add / New Item from the context menu. Select the Crystal Report template from the Reporting category.
+   STEP 2: Type the name "Products.rpt" and click on the Add button (Figure 9.2).
+   Note: The first time that you create a Crystal Report template, you must accept its license agreement.