# Adding a LINQ to SQL Class

The next step is to add a LINQ to SQL class. When working with LINQ to SQL, one of the big advantages you will find is that Visual Studio 2010 does an outstanding job of making it as easy as possible. Visual Studio provides an object-relational mapping designer, called the O/R Designer, which allows you to visually design the object to database mapping.

To start this task, right-click your solution and select Add New Item from the provided menu. From the items in the Add New Item dialog box, you will find LINQ to SQL Classes as an option. This is presented in Figure 56-2.

![](bbox=[0.15, 0.37, 0.8, 0.7])

FIGURE 56-2

Because this example is using the Northwind database, name the file Northwind.dbml. Click the Add button, and you will see that this operation creates a couple of files for you. Figure 56-3 presents the Solution Explorer after adding the Northwind.dbml file.

A number of things were added to your project with this action. The Northwind.dbml file was added and it contains two components. Because the LINQ to SQL class that was added works with LINQ, the following references were also added on your behalf: System.Core, System.Data.DataSetExtensions, System.Data.Linq, and System.Xml.Linq.

# Introducing the O/R Designer

Another big addition to the IDE that appeared when you added the LINQ to SQL class to your project (the Northwind.dbml file), was a visual

![](bbox=[0.7, 0.65, 0.9, 0.9])

FIGURE 56-3