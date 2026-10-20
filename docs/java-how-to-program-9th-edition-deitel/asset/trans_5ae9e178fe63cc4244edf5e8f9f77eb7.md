

## 常见编程错误 28.10

如果在关闭创建 ResultSet 的 Statement 之后尝试操作该 ResultSet，就会发生 SQLException。当 Statement 关闭时，ResultSet 会被丢弃。

## 软件工程观察 28.7

每个 Statement 对象一次只能打开一个 ResultSet 对象。当一个 Statement 返回新的 ResultSet 时，该 Statement 会关闭先前的 ResultSet。若要并行使用多个 ResultSet，必须由不同的 Statement 对象返回这些 ResultSet。

## Java SE 7：自动关闭 Connection、Statement 和 ResultSet

从 Java SE 7 开始，Connection、Statement 和 ResultSet 接口均扩展了 AutoCloseable 接口，因此你可以将实现了这些接口的对象与新的 try-with-resources 语句一起使用，该语句已在 11.13 节中介绍。在图 28.23 示例的文件夹中，子文件夹 JavaSE7Version 包含一个使用 try-with-resources 语句分配 Connection、Statement 和 ResultSet 对象的示例版本。这些对象会在 try 块结束时，或执行 try 块中的代码发生异常时自动关闭。

## 28.8.2 查询 books 数据库

下一个示例（图 28.25 和图 28.28）允许用户向程序输入任意查询。该示例在 JTable 中显示查询结果，使用 TableModel 对象向 JTable 提供 ResultSet 数据。JTable 是一个 Swing GUI 组件，可以绑定到数据库以显示查询结果。ResultSetTableModel 类（图 28.25）通过 TableModel 建立与数据库的连接，并维护 ResultSet。DisplayQueryResults 类（图 28.28）创建 GUI，并指定 ResultSetTableModel 类的实例为 JTable 提供数据。

## ResultSetTableModel 类

ResultSetTableModel 类（图 28.25）扩展了 AbstractTableModel 类（包 javax.swing.table），后者实现了 TableModel 接口。ResultSetTableModel 重写了 TableModel 的方法 getColumnClass、getColumnCount、getColumnName、getRowCount 和 getValueAt。TableModel 方法 isCellEditable 和 setValueAt（由 AbstractTableModel 提供）的默认实现没有被重写，因为本示例不支持编辑 JTable 单元格。TableModel 方法 addTableModelListener 和 removeTableModelListener（由 AbstractTableModel 提供）的默认实现也没有被重写，因为 AbstractTableModel 中这些方法的实现能够正确地添加和移除事件监听器。

``` 
1  // Fig. 28.25: ResultSetTableModel.java
2  // A TableModel that supplies ResultSet data to a JTable.
3  import java.sql.Connection;
4  import java.sql.Statement;
5  import java.sql.DriverManager;
6  import java.sql.ResultSet;
7  import java.sql.ResultSetMetaData;
```

图 28.25 | 将 ResultSet 数据提供给 JTable 的 TableModel。（第 1 部分，共 5 部分。）

``` 
8  import java.sql.SQLException;
9  import javax.swing.table.AbstractTableModel;
10 
11  // ResultSet rows and columns are counted from 1 and JTable
12  // rows and columns are counted from 0. When processing
13  // ResultSet rows or columns for use in a JTable, it is
14  // necessary to add 1 to the row or column number to manipulate
15  // the appropriate ResultSet column (i.e., JTable column 0 is
16  // ResultSet column 1 and JTable row 0 is ResultSet row 1).
17  public class ResultSetTableModel extends AbstractTableModel
18  {
19      private Connection connection;
20      private Statement statement;
21      private ResultSet resultSet;
22      private ResultSetMetaData metaData;
23      private int numberOfRows;
24  
25      // keep track of database connection status
26      private boolean connectedToDatabase = false;
27  
28      // constructor initializes resultSet and obtains its meta data object;
29      // determines number of rows
30      public ResultSetTableModel( String url, String username,
31          String password, String query ) throws SQLException
32      {
33          // connect to database
34          connection = DriverManager.getConnection( url, username, password );
35  
36          // create Statement to query database
37          statement = connection.createStatement(
38              ResultSet.TYPE_SCROLL_INSENSITIVE,
39              ResultSet.CONCUR_READ_ONLY );
40  
41          // update database connection status
42          connectedToDatabase = true;
43  
44          // set query and execute it
45          setQuery( query );
46      } // end constructor ResultSetTableModel
47  
48      // get class that represents column type
49      public Class getColumnClass( int column ) throws IllegalStateException
50      {
51          // ensure database connection is available
52          if ( !connectedToDatabase )
53              throw new IllegalStateException( "Not Connected to Database" );
54  
55          // determine Java class of column
56          try
57          {
58              String className = metaData.getColumnClassName( column + 1 );
59
```

``` 
// return Class object that represents className
return Class.forName( className );
} // end try
catch ( Exception exception )
{
    exception.printStackTrace();
} // end catch

return Object.class; // if problems occur above, assume type Object
} // end method getColumnClass

// get number of columns in ResultSet
public int getColumnCount() throws IllegalStateException
{
    // ensure database connection is available
    if ( !connectedToDatabase )
        throw new IllegalStateException( "Not Connected to Database" );

    // determine number of columns
    try
    {
        return metaData.getColumnCount();
    } // end try
    catch ( SQLException sqlException )
    {
        sqlException.printStackTrace();
    } // end catch

    return 0; // if problems occur above, return 0 for number of columns
} // end method getColumnCount

// get name of a particular column in ResultSet
public String getColumnName( int column ) throws IllegalStateException
{
    // ensure database connection is available
    if ( !connectedToDatabase )
        throw new IllegalStateException( "Not Connected to Database" );

    // determine column name
    try
    {
        return metaData.getColumnName( column + 1 );
    } // end try
    catch ( SQLException sqlException )
    {
        sqlException.printStackTrace();
    } // end catch

    return ""; // if problems, return empty string for column name
} // end method getColumnName
```

``` 
111  // return number of rows in ResultSet
112  public int getRowCount() throws IllegalStateException
113  {
114      // ensure database connection is available
115      if ( !connectedToDatabase )
116          throw new IllegalStateException( "Not Connected to Database" );
118      return numberOfRows;
119  } // end method getRowCount
121  // obtain value in particular row and column
122  public Object getValueAt( int row, int column )
123      throws IllegalStateException
124  {
125      // ensure database connection is available
126      if ( !connectedToDatabase )
127          throw new IllegalStateException( "Not Connected to Database" );
129      // obtain a value at specified ResultSet row and column
130      try
131      {
132          resultSet.absolute( row + 1 );
133          return resultSet.getObject( column + 1 );
134      } // end try
135      catch ( SQLException sqlException )
136      {
137          sqlException.printStackTrace();
138      } // end catch
140      return ""; // if problems, return empty string object
141  } // end method getValueAt
143  // set new database query string
144  public void setQuery( String query )
145      throws SQLException, IllegalStateException
146  {
147      // ensure database connection is available
148      if ( !connectedToDatabase )
149          throw new IllegalStateException( "Not Connected to Database" );
151      // specify query and execute it
152      resultSet = statement.executeQuery( query );
154      // obtain meta data for ResultSet
155      metaData = resultSet.getMetaData();
157      // determine number of rows in ResultSet
158      resultSet.last(); // move to last row
159      numberOfRows = resultSet.getRow(); // get row number
161      // notify JTable that model has changed
162      fireTableStructureChanged();
163  } // end method setQuery

