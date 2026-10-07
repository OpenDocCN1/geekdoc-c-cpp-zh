# Introduction to ADO.NET

![](bbox=[0.324, 0.087, 0.675, 0.368])

**FIGURE 3.52** The running result of the project EDModel project.

+   **H.** The Listbox control **FacultyList** is cleaned up before it can be filled.
**I.** A `foreach()` loop is used to pick up each faculty name from the query variable **fn** from the result **query**, and add it to the **FacultyList**.

Now let's run to test our cases. Click the **Start** button to run the project. The Form1 window is displayed, as shown in Figure 3.52. Select any query method and click on the **Show Faculty** button to connect to our sample database and retrieve all faculty names. The running result is shown in Figure 3.52.

Click the **Close** button that is located at the upper-right corner of this Form to close our project. It can be found from this piece of code that is relatively simple and easy to use the Entity Data Model to access and manipulate data the database.

# 3.5 CHAPTER SUMMARY

The main topic of this chapter is an introduction to the ADO.NET, which includes the architectures, organizations and components of the ADO.NET 2.0, 3.5 and 4.3.

Detailed discussions and descriptions are provided in this chapter to give readers both fundamental and practical pictures in how to use components in ADO.NET 2.0, 3.5 and ADO.NET 4.3 to develop professional data-driven applications. Two ADO.NET architectures are discussed to enable users to follow the directions to build and design their preferred projects based on the different organizations of ADO.NET.

A history of the development of ADO.NET is first introduced in this chapter. Different related objects are discussed, such as Data Access Object (DAO), Remote Data Object (RDO), and Database Connectivity (ODBC), OLE DB and the ADO. The difference between the ADO and the ADO.NET is also provided in detail.

Fundamentally the ADO.NET is a class-container and contains three basic components: Data Provider, DataSet and DataTable. Furthermore, the Data Provider contains four subcomponents: Connection, Command, TableAdapter and DataReader. You should be in mind that the Provider comes in multiple versions based on the type of the database you are using in your applications.