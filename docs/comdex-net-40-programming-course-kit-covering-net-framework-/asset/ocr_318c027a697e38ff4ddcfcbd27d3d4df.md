In Listing 7.18, we declare three arrays, where two of them are of **String** type, **names** and **position**, and one is of the **Integer** type, **years**.. Then, we use the **Zip** operator to combine the **names** array values to the **position** array and assign it into **q**. After that, we again use the **Zip** operator to combine **q** and **years** values. Finally, we use the **For Each** loop and add the result into **ListBox1**.

+   10. *Press* the **F5** key to run the application.
+   11. *Click* the **Display** button to generate a combine output, as shown in Fig.VB-7.27:

![](bbox=[0.434, 0.237, 0.589, 0.356])

This is an example of the Zip operator where we can combine the collections and display them jointly.

This is all about the standard query operators used in LINQ. Let's now learn how these operators can be used in ADO.NET.

# ## Implementing LINQ to ADO.NET

LINQ to ADO.NET helps you to query on any ADO.NET object using LINQ programming model. It consists of the following three technologies:

+   - **LINQ to DataSet:** Represents a set of extensions to the standard ADO.NET DataSet programming model. It allows the **DataSet**, **DataTable**, and **DataRow** objects to be a natural target for a LINQ query expression. Moreover, LINQ to DataSet provides richer and optimized querying over datasets.
+   - **LINQ to SQL:** Allows you to interact with a relational database by removing the ADO.NET data types by the use of entity classes. It means that you can directly interact with database rather using ADO.NET objects. LINQ to SQL enables you to query directly the SQL Server database schemas.
+   - **LINQ to Entities:** Allows you to write queries for the Entity Framework conceptual model, which enables users to visually design models and map databases, tables, and views by using Visual Studio 2010 and .NET Framework 4.0.

Let’s now discuss the two important technologies in detail.

# ### LINQ to DataSet

A dataset is an in-memory representation of data that acts as the core of a wide variety of data-based applications. After data is loaded into a dataset, you often need to perform additional queries on the data. These addition queries are generally executed by using the LINQ to DataSet technology.

LINQ to DataSet provides an easier and faster way to query data cached in a DataSet object as compared to traditional methods of querying the data. LINQ to DataSet simplifies the process of querying by enabling you to write queries in the programming language itself. The query operators allow you to perform LINQ queries on the dataset. To begin querying a dataset by using LINQ to DataSet, you need to confirm whether your dataset is filled with data or not because you cannot get any output or result-set from an empty dataset.

Perform the following steps to implement LINQ to DataSet in a Console application:

+   1. *Start* Visual Studio 2010.
+   2. *Select* File→New→Project from the menu bar. The **New Project** dialog box opens.