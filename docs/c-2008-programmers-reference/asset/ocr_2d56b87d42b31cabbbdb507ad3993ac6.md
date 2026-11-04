# Chapter 14: Language Integrated Query (LINQ)

Figure 14-19 shows the relationships among these four tables.

![](bbox=[0.23, 0.2, 0.88, 0.68])

Figure 14-19

Now save the `DataClasses1.dbml` file, and Visual Studio 2008 will create the relevant classes to represent the tables and relationships that you just modeled. For every LINQ to SQL file you added to your solution, a DataContext class is generated. You can view this using the Class Viewer (View → Class View; see Figure 14-20). In this case, the name of the DataContext class is `DataClasses1DataContext`. The name of this class is based on the name of the `.dbml` file; if you named the `.dbml` file Pubs, this class is named `PubsDataContext`.