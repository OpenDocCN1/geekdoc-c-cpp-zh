

```
83        catch ( SQLException sqlException )
84        {
85            sqlException.printStackTrace();
86            close();
87        } // end catch
88        } // end finally
89
90        return results;
91    } // end method getAllPeople
92
93    // select person by last name
94    public List< Person > getPeopleByLastName( String name )
95    {
96        List< Person > results = null;
97        ResultSet resultSet = null;
98
99        try
100    {
101        selectPeopleByLastName.setString( 1, name ); // specify last name
102
103        // executeQuery returns ResultSet containing matching entries
104        resultSet = selectPeopleByLastName.executeQuery();
105
106        results = new ArrayList< Person >();
107
108        while ( resultSet.next() )
109        {
110            results.add( new Person( resultSet.getInt( "addressID" ),
111                resultSet.getString( "FirstName" ),
112                resultSet.getString( "LastName" ),
113                resultSet.getString( "Email" ),
114                resultSet.getString( "PhoneNumber" ) ) );
115        } // end while
116    } // end try
117    catch ( SQLException sqlException )
118    {
119        sqlException.printStackTrace();
120    } // end catch
121    finally
122    {
123        try
124        {
125            resultSet.close();
126        } // end try
127        catch ( SQLException sqlException )
128        {
129            sqlException.printStackTrace();
130            close();
131        } // end catch
132    } // end finally
133
134        return results;
135    } // end method getPeopleByName
```

```
// add an entry
public int addPerson(
    String fname, String lname, String email, String num )
{
    int result = 0;

    // set parameters, then execute insertNewPerson
    try
    {
        insertNewPerson.setString( 1, fname );
        insertNewPerson.setString( 2, lname );
        insertNewPerson.setString( 3, email );
        insertNewPerson.setString( 4, num );

        // insert the new entry; returns # of rows updated
        result = insertNewPerson.executeUpdate();
    } // end try
    catch ( SQLException sqlException )
    {
        sqlException.printStackTrace();
        close();
    } // end catch

    return result;
} // end method addPerson

// close the database connection
public void close()
{
    try
    {
        connection.close();
    } // end try
    catch ( SQLException sqlException )
    {
        sqlException.printStackTrace();
    } // end catch
} // end method close
} // end class PersonQueries
```

Fig. 28.31 | 地址簿应用程序使用的 PreparedStatements。 （第 4 部分，共 4 部分。）

## 创建 PreparedStatements

第 31–32 行调用 Connection 方法 prepareStatement 来创建名为 selectAllPeople 的 PreparedStatement，用于选择 Addresses 表中的所有行。第 35–36 行创建名为 selectPeopleByLastName 且带有一个参数的 PreparedStatement。该语句选择 Addresses 表中与特定姓氏匹配的所有行。请注意用于指定姓氏参数的 ? 字符。第 39–42 行创建名为 insertNewPerson 且带四个参数的 PreparedStatement，表示新条目的名字、姓氏、电子邮件地址和电话号码。同样，请注意用于表示这些参数的 ? 字符。

## PersonQueries 方法 getAllPeople

方法 getAllPeople（第 52–91 行）通过调用方法 executeQuery 执行 PreparedStatement selectAllPeople（第 60 行），该方法返回包含匹配查询结果的 ResultSet（在本例中为 Addresses 表中的所有行）。第 61–71 行将查询结果放入 Person 对象的 ArrayList 中，并在第 90 行将其返回给调用者。方法 getPeopleByLastName（第 94–135 行）使用 PreparedStatement 方法 setString 设置 selectPeopleByLastName 的参数（第 101 行）。然后，第 104 行执行查询，第 106–115 行将查询结果放入 Person 对象的 ArrayList 中。第 134 行将 ArrayList 返回给调用者。

## PersonQueries 方法 addPerson 和 Close

方法 addPerson（第 138–161 行）使用 PreparedStatement 方法 setString（第 146–149 行）为 insertNewPerson PreparedStatement 设置参数。第 152 行使用 PreparedStatement 方法 executeUpdate 插入新记录。此方法返回一个整数，表示数据库中已更新（或插入）的行数。方法 close（第 164–174 行） simply 关闭数据库连接。

## 类 AddressBookDisplay

AddressBookDisplay（图 28.32）应用程序使用 PersonQueries 对象与数据库交互。第 59 行创建 PersonQueries 对象。当用户按下 Browse All Entries JButton 时，会调用 browseButtonActionPerformed 处理程序（第 309–335 行）。第 313 行在 PersonQueries 对象上调用方法 getAllPeople 以获取数据库中的所有条目。然后用户可以使用 Previous 和 Next JButtons 滚动浏览条目。当用户按下 Find JButton 时，会调用 queryButtonActionPerformed 处理程序（第 265–287 行）。第 267–268 行在 PersonQueries 对象上调用方法 getPeopleByLastName 以获取数据库中与指定姓氏匹配的条目。如果有多个此类条目，用户可以使用 Previous 和 Next JButtons 滚动浏览它们。

```
1  // Fig. 28.32: AddressBookDisplay.java
2  // A simple address book
3  import java.awt.event.ActionEvent;
4  import java.awt.event.ActionListener;
5  import java.awt.event.WindowAdapter;
6  import java.awt.event.WindowEvent;
7  import java.awt.FlowLayout;
8  import java.awt.GridLayout;
9  import java.util.List;
10 import javax.swing.JButton;
11 import javax.swing.Box;
12 import javax.swing.JFrame;
13 import javax.swing.JLabel;
14 import javax.swing.JPanel;
15 import javax.swing.JTextField;
16 import javax.swing.WindowConstants;
17 import javax.swing.BoxLayout;
18 import javax.swing.BorderFactory;
19 import javax.swing.JOptionPane;
```

```
20
21 public class AddressBookDisplay extends JFrame
22 {
23     private Person currentEntry;
24     private PersonQueries personQueries;
25     private List< Person > results;
26     private int numberOfEntries = 0;
27     private int currentEntryIndex;
28
29     private JButton browseButton;
30     private JLabel emailLabel;
31     private JTextField emailTextField;
32     private JLabel firstNameLabel;
33     private JTextField firstNameTextField;
34     private JLabel idLabel;
35     private JTextField idTextField;
36     private JTextField indexTextField;
37     private JLabel lastNameLabel;
38     private JTextField lastNameTextField;
39     private JTextField maxTextField;
40     private JButton nextButton;
41     private JLabel ofLabel;
42     private JLabel phoneLabel;
43     private JTextField phoneTextField;
44     private JButton previousButton;
45     private JButton queryButton;
46     private JLabel queryLabel;
47     private JPanel queryPanel;
48     private JPanel navigatePanel;
49     private JPanel displayPanel;
50     private JTextField queryTextField;
51     private JButton insertButton;
52
53     // no-argument constructor
54     public AddressBookDisplay()
55     {
56         super( "Address Book" );
57
58         // establish database connection and set up PreparedStatements
59         personQueries = new PersonQueries();
60
61         // create GUI
62         navigatePanel = new JPanel();
63         previousButton = new JButton();
64         indexTextField = new JTextField( 2 );
65         ofLabel = new JLabel();
66         maxTextField = new JTextField( 2 );
67         nextButton = new JButton();
68         displayPanel = new JPanel();
69         idLabel = new JLabel();
70         idTextField = new JTextField( 10 );
71         firstNameLabel = new JLabel();
72         firstNameTextField = new JTextField( 10 );
```

```
73    lastNameLabel = new JLabel();
74    lastNameTextField = new JTextField( 10 );
75    emailLabel = new JLabel();
76    emailTextField = new JTextField( 10 );
77    phoneLabel = new JLabel();
78    phoneTextField = new JTextField( 10 );
79    queryPanel = new JPanel();
80    queryLabel = new JLabel();
81    queryTextField = new JTextField( 10 );
82    queryButton = new JButton();
83    browseButton = new JButton();
84    insertButton = new JButton();
85
86    setLayout( new FlowLayout( FlowLayout.CENTER, 10, 10 ) );
87    setSize( 400, 300 );
88    setResizable( false );
89
90    navigatePanel.setLayout(
91        new BoxLayout( navigatePanel, BoxLayout.X_AXIS ) );
92
93    previousButton.setText( "Previous" );
94    previousButton.setEnabled( false );
95    previousButton.addActionListener(
96        new ActionListener()
97    {
98        public void actionPerformed( ActionEvent evt )
99        {
100       previousButtonActionPerformed( evt );
101    } // end method actionPerformed
102 } // end anonymous inner class
103 ); // end call to addActionListener
104
105    navigatePanel.add( previousButton );
106    navigatePanel.add( Box.createHorizontalStrut( 10 ) );
107
108    indexTextField.setHorizontalAlignment(
109        JTextField.CENTER );
110    indexTextField.addActionListener(
111        new ActionListener()
112    {
113        public void actionPerformed( ActionEvent evt )
114        {
115           indexTextFieldActionPerformed( evt );
116    } // end method actionPerformed
117 } // end anonymous inner class
118 ); // end call to addActionListener
119
120    navigatePanel.add( indexTextField );
121    navigatePanel.add( Box.createHorizontalStrut( 10 ) );
122
123    ofLabel.setText( "of" );
124    navigatePanel.add( ofLabel );
125    navigatePanel.add( Box.createHorizontalStrut( 10 ) );
```
