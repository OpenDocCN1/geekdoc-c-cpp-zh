Introduction to ADO.NET 59

Command, DataAdapter and DataReader, which belong to Data Provider, are often called Provider-dependent components.

To get a clearer picture of the ADO.NET, let's first take a look at the architecture of the ADO.NET.

# 3.3 THE ARCHITECTURE OF THE ADO.NET 2.0

The ADO.NET 2.0 architecture can be divided into two logical pieces: command execution and caching.

Command execution requires features such as connectivity, execution, and reading of results. These features are embedded in ADO.NET Data Providers. The caching of results is handled by the DataSet.

The Data Provider enables connectivity and connection to underlying data sources. Note that these data sources do not have to relational databases. Once a command has been executed, the result can be read using a DataReader. A DataReader provides efficient forward-only stream-level access to the results. In addition, results can be used to render a DataSet as aDataAdapter. This is typically called 'Filling the DataSet'.

Figure 3.1 shows a typical architecture of the ADO.NET 2.0.

In this architecture, the data tables are not embedded into the DataSet but treated as independent data tables and the data transactions between the DataSet and the Data Provider, as SELECT, INSERT, UPDATE and DELETE, are made using the DataAdapter via its four different methods: SelectCommand, InsertCommand, UpdateCommand and DeleteCommand, respectively. The Connection object is only used to set a connection between your data and your sources. The DataReader object is not used for this architecture. As you will see from the sample project in the following chapters, to execute the different methods under theDataAdapter to perform the data query is exactly to call the Command object shown in Figure 3.2.

Another ADO.NET architecture, the data tables are not embedded into the DataSet but treated as independent data tables and each can be considered as an individual DataTable object. The data transactions between the Data Provider and the DataSet are realized by executing the different methods of the Command object with the specified parameters. The ExecuteReader() method of the Command object is called when a data query is made from the data source, which is equivalent to an SQL SELECT statement, and the returned data should be stored to the DataReader object. When performing other data-accessing operations as INSERT, UPDATE or DELETE, the ExecuteNonQuery() method of the Command should be called with the suitable parameters attached to the Command object.

![](bbox=[0.116, 0.706, 0.883, 0.9])

FIGURE 3.1 A typical architecture of the ADO.NET 2.0.