# Two ways to create a SqlDataReader object

```
sqlCommand.ExecuteReader()
sqlCommand.ExecuteReader(behavior)
```

# Common CommandBehavior enumeration members

| Member | Description |
| --- | --- |
| CloseConnection | Closes the connection when the data reader is closed. |
| Default | Equivalent to specifying no command behavior. |
| SingleRow | Only a single row is returned. |

# Common members of the SqlDataReader class

| Indexer | Description |
| --- | --- |
| [columnname] | Gets the value of the column with the specified name. |
| [index] | Gets the value of the column at the specified position. |
| Property | Gets a value that indicates if the data reader is closed. |
| Method | Closes the reader. |
| Close() | Retrieves the next row and returns a Boolean value that indicates whether there are additional rows. |

# Code that uses a data reader to read a list of State objects

```
connection.Open();
SqlDataReader reader = selectCommand.ExecuteReader(CommandBehavior.CloseConnection);
List<State> states = new List<State>();
while (reader.Read()) {
  State s = new State();
  s.Code = reader["State"].ToString();
  s.StateName = reader["StateName"].ToString();
  states.Add(s);
}
reader.Close();
```

# Description

+   * You must open the connection that's used by the data reader before you execute the ExecuteReader method of the command object.
* The data reader is opened automatically when it's created. While it's open, no other data readers can be opened on the same connection. The exception is if you're using an Oracle data reader, in which case other data readers can be open at the same time.
* When you create a data reader, it's positioned before the first row in the result set. To retrieve the first row, use the Read method.
* You can combine two or more command behavior members using the And (&) operator.

![](bbox=[0.066, 0.943, 0.545, 0.958])