# Introduction to ADO.NET

To add a Parameter to the Parameters collection of a Command object accCommand, you need to use the Add() method as below:

```
accCommand.Parameters.Add("user_name", OleDbType.Char).Value =
txtUserName.Text;
accCommand.Parameters.Add("pass_word", OleDbType.Char, 8).Value =
txtPassWord.Text;
```

You must be careful with the order in which you add these parameters, user_name and pass_word, and make sure that the order is identical to the order in which those two dynamic parameters appear in the above SQL statement.

Both Server and Oracle Data Provider use the Named Parameter Mapping, which means that each parameter, either defined in an SQL statement or added into a Parameters collection, is identified by the name. In other words, the name of the parameter in an SQL statement or a stored procedure must be identical with the name of the parameter you added to a Parameters collection. For example, the following SQL statement is used for a SQL Server Data Provider on a query:

```
SELECT user_name, pass_word FROM LOGIN WHERE user_name LIKE @Param1
AND (pass_word LIKE @Param2)
```

The user_name and pass_word are mapped to two columns in the Log data table. Compared with the above SQL statement, two dynamic parameters are represented by no names of the dynamic parameters @Param1 and @Param2 in the SQL statement. The operator is replaced by the keyword LIKE for these two parameters. This is required by the SQL Server Data Provider.

Then you need two Parameter objects associated with your Command object, example of initializing these two Parameter objects is shown in Figure 3.11.

When you have ParameterProperties assigned with dynamic parameters, "@Param1" and "@Param2", Both Param1 and Param2 are nominal names of the dynamic parameters and a symbol is prefixed before each parameter since this is the requirement of the SQL Server database when a dynamic parameter is used in an SQL statement.

You can see from this piece of code that the name of each parameter used for each Parameter object must be identical with the name you defined in your SQL statement. Since the SQL Server and Oracle Data Provider use Named Parameter Mapping, you do not need to worry about the order in which you add Parameter objects into the Parameters collection of the Command object.

To add Parameters into a Parameters collection of a Command, you need to use some methods defined in the ParameterClass.

# 3.4.3.4 Methods of the ParameterCollection Class

Each ParameterClass has more than ten methods, but only two of them are often utilized in the data-driven applications, which are the Add() and AddWithValue() methods. Each Parameter object must be added to the Parameters collection of a Command before you execute that Command to perform any query or data operation.

```
SqlParameter paramUserName = new SqlParameter();
 SqlParameter paramPassWord = new SqlParameter();

paramUserName.ParameterName = "@Param1";nparamUserName.Value = txtUserName.Text;
paramPassWord.ParameterName = "@Param2";nparamPassWord.Value = txtPassWord.Text;
```

FIGURE 3.11 An example of initializing the property of a Parameter object.