# Explanation

# 1. The SqlConnection Object

+   - To interact with a database, one must have a connection to it. The connection helps to identify the database server, the database name, user name, password, and other parameters that are required for connecting to the data base. A connection object is used by command objects so they will know which database to execute the command on.
+   - The Connection Object provides physical connection to the Data Source. Connection object needs the necessary information to recognize the data source and to log on to it properly, this information is provided through a connection string.
+   - ADO.NET connection object, which allows to establish a connection to a data source. If OleDb Data Provider is used to connect to a data source that exposes an OleDb interface, then the connection object named OleDbConnection is used. Similarly, the connection object name would be prefixed with Odbc or Sql for an OdbcConnection object on an Odbc data source or a SqlConnection object on a SQL Server database, respectively.

# 2. The SqlCommand Object

+   - The Command Object uses to perform SQL statement or stored procedure to be executed at the Data Source. The command object provides a number of Execute methods that can be used to perform the SQL queries in a variety of ways.
+   - The process of interacting with a database means that one must specify the actions that can occur on dataset. This is done with a command object. A command object is used to send SQL statements to the database. A command object uses a connection object to figure out which database to communicate with. A command object only can be used, to execute a command directly, or assign a reference to a command object to an SqlDataAdapter, which holds a set of commands that work on a group of data as described below.

# 3. The SqlDataReader Object

+   - The DataReader Object is a stream-based, forward-only, read-only retrieval of query results from the Data Source, which do not update the data. DataReader requires a live connection with the datbase and provides a very intelligent way of consuming all or part of the result set.
+   - Many data operations require a stream of data for reading. The data reader object allows to obtain the results of a SELECT statement from a command object. For performance reasons, the data returned from a data reader is a fast forward-only stream of data. This means that data is brought from the stream in a sequential manner so as to read and not to manipulate.