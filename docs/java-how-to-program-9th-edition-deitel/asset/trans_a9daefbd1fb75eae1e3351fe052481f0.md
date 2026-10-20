
现在你已经准备好执行第28.11节中的AddressBook应用程序了。也可以使用MySQL或任何其他支持JDBC PreparedStatement的数据库。

## 28.11 PreparedStatement

**PreparedStatement**使你可以创建编译好的SQL语句，其执行效率比Statement更高。PreparedStatement还可以指定参数，使其比Statement更灵活——你可以使用不同的参数值重复执行同一条查询。例如，在books数据库中，你可能想要根据作者的姓和名查找其所有书名的标题，并且可能想要对多个作者执行该查询。使用PreparedStatement，该查询定义如下：

```
PreparedStatement authorBooks = connection.prepareStatement(
    "SELECT LastName, FirstName, Title " +
    "FROM Authors INNER JOIN AuthorISBN " +
        "ON Authors.AuthorID=AuthorISBN.AuthorID " +
    "INNER JOIN Titles " +
        "ON AuthorISBN.ISBN=Titles.ISBN " +
    "WHERE LastName = ? AND FirstName =?" );
```

上述SQL语句最后一行中的两个问号（?）是占位符，用于表示将作为查询的一部分传递给数据库的值。在执行PreparedStatement之前，程序必须使用PreparedStatement接口的set方法指定参数值。

对于前面的查询，两个参数都是字符串，可以使用PreparedStatement的**setString**方法进行设置，如下所示：

```
authorBooks.setString( 1, "Deitel" );
authorBooks.setString( 2, "Paul" );
```

方法setString的第一个参数表示要设置的参数编号，第二个参数是该参数的值。参数编号从1开始计数，从第一个问号（?）开始。当程序使用上述设置的参数值执行前面的PreparedStatement时，传递给数据库的SQL为：

```
SELECT LastName, FirstName, Title
FROM Authors INNER JOIN AuthorISBN
    ON Authors.AuthorID=AuthorISBN.AuthorID
INNER JOIN Titles
    ON AuthorISBN.ISBN=Titles.ISBN
WHERE LastName = 'Deitel' AND FirstName = 'Paul'
```

方法setString会根据需要自动转义String参数值。例如，如果姓氏是O’Brien，则语句

```
authorBooks.setString( 1, "O'Brien" );
```

会将O’Brien中的'字符转义为两个单引号字符，以便'在数据库中正确显示。

![](img/009e962758dcc71dbc43a493362e6dc0_1248_0.png)

## 错误预防提示 28.2

对于接收String值作为参数的查询，请使用带参数的PreparedStatement，以确保在SQL语句中正确引用这些字符串。

PreparedStatement接口为每种支持的SQL类型都提供了set方法。务必使用与数据库中参数的SQL类型相匹配的set方法——当程序尝试将参数值转换为不正确的类型时，会发生SQLException。

## 使用PreparedStatement的地址簿应用程序

我们现在介绍一个地址簿应用程序，它允许你浏览现有条目、添加新条目以及按特定姓氏搜索条目。我们的AddressBook Java DB数据库包含一个Addresses表，其中有addressID、FirstName、LastName、Email和PhoneNumber列。addressID列是一个所谓的标识列。这是表示自动递增列的SQL标准方式。我们为这个数据库提供的SQL脚本使用SQL IDENTITY关键字将addressID列标记为标识列。有关使用IDENTITY关键字和创建数据库的更多信息，请参阅download.oracle.com/javadb/10.6.1.0/devguide/devguide-single.html上的Java DB开发者指南。

## 类Person

我们的地址簿应用程序由三个类组成——Person（图28.30）、PersonQueries（图28.31）和AddressBookDisplay（图28.32）。类Person是一个简单的类，表示地址簿中的一个人。该类包含用于存储地址ID、名字、姓氏、电子邮件地址和电话号码的字段，以及用于操作这些字段的set和get方法。

```
// Fig. 28.30: Person.java
// Person class that represents an entry in an address book.
public class Person
{
    private int addressID;
    private String firstName;
    private String lastName;
    private String email;
    private String phoneNumber;

    // no-argument constructor
    public Person()
    {} // end no-argument Person constructor

    // constructor
    public Person( int id, String first, String last,
        String emailAddress, String phone )
    {
        setAddressID( id );
        setFirstName( first );
```
```
22      setLastName( last );
23      setEmail( emailAddress );
24      setPhoneNumber( phone );
25  } // end five-argument Person constructor
26
27  // sets the addressID
28  public void setAddressID( int id )
29  {
30      addressID = id;
31  } // end method setAddressID
32
33  // returns the addressID
34  public int getAddressID()
35  {
36      return addressID;
37  } // end method getAddressID
38
39  // sets the firstName
40  public void setFirstName( String first )
41  {
42      firstName = first;
43  } // end method setFirstName
44
45  // returns the first name
46  public String getFirstName()
47  {
48      return firstName;
49  } // end method getFirstName
50
51  // sets the lastName
52  public void setLastName( String last )
53  {
54      lastName = last;
55  } // end method setLastName
56
57  // returns the last name
58  public String getLastName()
59  {
60      return lastName;
61  } // end method getLastName
62
63  // sets the email address
64  public void setEmail( String emailAddress )
65  {
66      email = emailAddress;
67  } // end method setEmail
68
69  // returns the email address
70  public String getEmail()
71  {
72      return email;
73  } // end method getEmail
74
```

## 图28.30 | 表示AddressBook条目的Person类。（第3部分，共3部分。）

```
75    // sets the phone number
76    public void setPhoneNumber( String phone )
77    {
78        phoneNumber = phone;
79    } // end method setPhoneNumber
80
81    // returns the phone number
82    public String getPhoneNumber()
83    {
84        return phoneNumber;
85    } // end method getPhoneNumber
86 } // end class Person
```

## 类PersonQueries

类PersonQueries（图28.31）管理地址簿应用程序的数据库连接，并创建应用程序用于与数据库交互的PreparedStatement。第18–20行声明了三个PreparedStatement变量。构造函数（第23–49行）在第27–28行连接到数据库。

```
// Fig. 28.31: PersonQueries.java
// PreparedStatements used by the Address Book application.
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.util.List;
import java.util.ArrayList;

public class PersonQueries
{
    private static final String URL = "jdbc:derby:AddressBook";
    private static final String USERNAME = "deitel";
    private static final String PASSWORD = "deitel";

    private Connection connection = null; // manages connection
    private PreparedStatement selectAllPeople = null;
    private PreparedStatement selectPeopleByLastName = null;
    private PreparedStatement insertNewPerson = null;

    // constructor
    public PersonQueries()
    {
        try
        {
            connection =
                DriverManager.getConnection( URL, USERNAME, PASSWORD );
```

## 图28.31 | 地址簿应用程序使用的PreparedStatement。（第1部分，共4部分。）

```
// create query that selects all entries in the AddressBook
selectAllPeople = connection.prepareStatement( "SELECT * FROM Addresses" );

// create query that selects entries with a specific last name
selectPeopleByLastName = connection.prepareStatement(
"SELECT * FROM Addresses WHERE LastName = ?" );

// create insert that adds a new entry into the database
insertNewPerson = connection.prepareStatement(
"INSERT INTO Addresses " +
"( FirstName, LastName, Email, PhoneNumber ) " +
"VALUES ( ?, ?, ?, ? )" );
} // end try
catch ( SQLException sqlException )
{
    sqlException.printStackTrace();
    System.exit( 1 );
} // end catch
} // end PersonQueries constructor

// select all of the addresses in the database
public List< Person > getAllPeople()
{
    List< Person > results = null;
    ResultSet resultSet = null;

    try
    {
        // executeQuery returns ResultSet containing matching entries
        resultSet = selectAllPeople.executeQuery();
        results = new ArrayList< Person >();

        while ( resultSet.next() )
        {
            results.add( new Person(
                resultSet.getInt( "addressID" ),
                resultSet.getString( "FirstName" ),
                resultSet.getString( "LastName" ),
                resultSet.getString( "Email" ),
                resultSet.getString( "PhoneNumber" ) ) );
        } // end while
    } // end try
    catch ( SQLException sqlException )
    {
        sqlException.printStackTrace();
    } // end catch
    finally
    {
        try
        {
            resultSet.close();
        } // end try
```

