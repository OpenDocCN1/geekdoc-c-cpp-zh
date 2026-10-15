
Run the application by pressing the F5 key. As you enter the starting letter of the employee's last name with the % wildcard character, and click the Find button, the first name and the last name of the employee is displayed in the ListBox control. You can find the output with F% in the TextBox, as shown in Figure 24.53:

![](img/e073a4882197be4ab61103cbe0bcb394_1211_0.png)

Figure 24.53: Showing the Output of the UsingDataReader Application

Let’s summarize the main points of this chapter.

### Summary

In this chapter, you learned about the database and various SQL statements and clauses to retrieve and perform various operations on database. Next, you learned about the various aspects of ADO.NET including its architecture and ADO.NET Entity Framework. In the Immediate Solutions section, you learned about creating the connection string and also learned about creating a connection with SQL Server database, and OLEDB database. You also learned about using the ODBC data source to connect to the Microsoft Access database. In addition, you learned about creating the command objects to retrieve the data from the database using SQL commands. You have also learned about working with various DataAdapter, such as OleDbDataAdapter, SqlDataAdapter, OdbcDataAdapter, and OracleDataAdapter. Finally, you learned about using DataReader to retrieve the data from the data source.

In the next chapter, you learn about data binding in Windows and WPF applications.

## Data Binding in Windows Form and WPF Applications

| If you need an Immediate Solution to: | See page: |
| --- | ---: |
| Implementing Simple Data Binding in Windows Forms | 1176 |
| Implementing Complex Data Binding in Windows Forms | 1180 |
| Using the BindingContext Class | 1191 |
| Using Parameterized SQL Queries | 1194 |
| Binding Data in WPF | 1196 |
| Binding a CLR Object in WPF | 1197 |
| Binding an ADO.NET Object in WPF | 1200 |
| Binding an XML Object in WPF | 1202 |
| Using the DependencyObject Constructor in WPF | 1204 |
| Binding a Web Service in WPF | 1205 |
| Creating a WCF Data Service | 1209 |

### In Depth

Data binding refers to the process of binding Windows or Windows Presentation Foundation (WPF) controls to data sources. It is done to display and access the data stored in a data source directly by an application. In other words, the control bound to a data source displays the information and data stored in that data source. For example, to display the names of the employees of a company in a ListBox control, you need to bind this control to the table containing the required data. In Windows Forms applications, you can bind controls not only to data sources, but also to any programming construct that holds the data. For example, you can bind control properties to an array of values or an Excel file. These control properties can be bound to a data source to retrieve data from it.

Apart from Windows and WPF applications, you can also bind controls to data sources in Web applications. However, in this case, you need to create a Windows Communication Foundation (WCF) Data Service to connect data and information from a data source to a particular control. WCF Data Service, which is formerly called ADO.NET Data Service, is available with the .NET Framework 4.0. ADO.NET stands for ActiveX Data Object.NET and is a set of software components that are used to access and modify data stored in relational database systems (RDBMS).

In this chapter, you are introduced to the concept of data binding that is used to access data from a data source in an application. You next learn to bind data to Windows Forms controls. The chapter further discusses various types of binding, simple and complex, in a Windows Forms application. Next, you learn about different ways to bind controls to a WPF application. The chapter also focuses on the need of creating WCF Data Services to implement data binding in a WPF application.

### Introducing Data Binding

As discussed, data binding is the process that establishes a connection between the application User Interface (UI) and data sources. This means that if you modify data in a control, that change is also reflected in the original data source. In other words, data binding is a two-way process in which the changes made in the data source are reflected in the control and vice versa. Data binding is implemented between an application and a database by binding the properties of the control, in which the data needs to be accessed, to a data source.

Some of the tasks that you can perform by data binding are:

- Navigating data — Refers to the process of moving from one record to another, based upon some specific search criteria.
- Entering data — Refers to the process of entering data in a data entry form. The entered data is then sent to the database with which the data entry form is connected. For example, you can enter data by using the TextBox, RadioButton, ListBox, Dropdownlist, ListBox, and CheckBox controls.
- Creating master/detail relation — Refers to the process of binding the data of multiple tables together in a master and details relation. The master and details relation is a relation of tables where a parent table is associated with its child tables. For example, you may display the names of employees from the Employees table in a ComboBox control; however, on selecting one of the employees, the details regarding that particular employee comes up in a DataGridView control.
- Performing data lookup — Refers to the process of looking up the data of a field corresponding to another field of the table. This type of data binding is supported by the ListBox control by using the ValueMember and DisplayMember properties.

### Data Binding to Windows Forms Controls

Data binding with Windows Forms helps you to display and make changes to information in a data source. You can bind a Windows Form with any type of data structure, such as a database, a text file, or an Excel file. There are two types of data binding in the Windows applications— simple data binding and complex data binding. In simple data binding, a control can bind to only a single data element. For example, only one record of data can be displayed in a TextBox or a Label control at a time. In C#, you can also bind a property of a control to a data source from which the data needs to be accessed. On the other hand, in complex data binding, you can bind a control to more than one record in the database. For example, a DataGridView control can bind to an entire table, i.e. all the records stored in that table can be accessed through the DataGridView control.

Complex data binding consists of the following properties:

- DataSource – Specifies a dataset, for instance DataSet11
- DataMember – Specifies a data member in the data source, for instance the Customers table in the Northwind database
- DisplayMember – Specifies a column or field of a table, which is displayed by a control, for instance the CustomerID column of the Customers table
- ValueMember – Specifies the data of a column or field of a table that is returned by a control’s properties.

### Data Binding to WPF Controls

You can implement data binding in a WPF application by using the code-behind file of an application or Extensible Application Markup Language (XAML). As in other applications, such as the Windows Forms Application and the ASP.NET Web Application, WPF also needs to have a target and a source for data binding. You can select the public property of the control in WPF to bind your data, which includes properties of other controls or any data source. The target of the binding can be accessible to the public property of the control, for example, the Text property of the TextBox control.

In this section, you learn about:

- Direction of data flow in a WPF application
- Sources from which data can be accessed in a WPF application
- Different ways to bind data to a WPF application

### Data Flow Directions in WPF

WPF data binding supports different types of binding modes between the target and the source. The data flow in a binding can be either from the target to the source or from the source to the target. You should specify the mode of data binding while binding the data in a WPF application. The Mode property defines the binding mode to determine the direction of the data flow between the source and the target.

The following are the four types of binding modes available in WPF:

- OneTime data binding – Refers to the mode in which data flows from the source to the target. This type of binding occurs only once when the application starts or the source of the data changes. The OneTime data binding can only retrieve the data but cannot update data in your database.
- OneWay data binding – Refers to the mode in which data flows from the source to the target. This type of binding is useful for read-only data, as it is not possible to change the data from the user interface. The OneWay data binding mode in WPF is the default binding mode.
- TwoWay data binding – Refers to the mode in which data moves in both the directions, i.e. from source to the target and from target to the source. In the TwoWay data binding, you can make changes to the data in the user interface. The changes made in the data of the UI, using the TwoWay data binding, are reflected in the data source.
- OneWayToSource data binding – Refers to the mode in which the source property gets updated automatically according to the changes made in the target property.

Next, let’s learn about different sources of data in a WPF application.

### Sources of Data Binding in WPF

In data binding, the sources refer to the objects from where the data is obtained. WPF supports four types of binding sources: Common Language Runtime (CLR) object, ADO.NET data, eXtensible Markup Language (XML) data, and DependencyObject. Let’s learn about these sources in the following sections.
