
```cs
case 1: // titles with 2016 copyright
// use LINQ to get titles with 2016
// copyright and sort them by title
titleBindingSource.DataSource =
dbcontext.Titles.Local
    .Where(book => book.Copyright == "2016")
    .OrderBy(book => book.Title);
break;
case 2: // titles ending with "How to Program"
// use LINQ to get titles ending with
// "How to Program" and sort them by title
titleBindingSource.DataSource =
dbcontext.Titles.Local
    .Where(
book => book.Title.EndsWith("How to Program")
    ).OrderBy(book => book.Title);
break;
titleBindingSource.MoveFirst(); // move to first entry
```

Fig. 22.26 | Displaying the result of a user-selected query in a DataGridView (Part 2 of 2).

# Customizing the Form's Load Event Handler

Create the TitleQueries_Load event handler (lines 22–29) by double clicking the table in Design view. When the Form loads, display the list of books from the Titles table, sorted by Title. Line 24 calls the Load extension from the BookDbContext.Titles property or defining the LINQ query in lines 40-41, we can programmatically cause the queriesComboBox_SelectedIndexChanged event handler to execute simply by setting the queriesComboBox.SelectedIndex to 0 (line 28).

# queriesComboBox_SelectedIndexChanged Event Handler

Next you must write that that executes the appropriate query each time the user chooses a different item from queriesComboBox. Double click queriesComboBox_SelectedIndexChanged event handler in Design to generate a query (lines 32–63) in the TitleQueries.cs file. In the event, add a switch statement (lines 36–60). Each case in the switch will return the titleBindingSource.DataSource property to the results of a query that returns the correct set of data. The data bindings by the IDE automatically update the titleGridView each time we change its DataSource. The BindingSource makes a Position property that represents the current item in the data source. The MoveFirst method of the BindingSource (line 62) sets the Position property to 0 to move to the first row of the result set each query executes. The results of the queries in lines 40–41, 46–49 and 54–58 are shown in Figs. 22.23–22.25, respectively. Because we do not modify the data in this app, each of the queries is performed on the in-memory representation of the Titles table, which is accessible through dbcontext.Titles.Local.

# 22.7 Retrieving Data from Multiple Tables with LINQ

# Ordering Books By Title

Lines 40–41 invoke the OrderBy extension method on dbcontext.Titles.Local to order the Title objects by their Title property values. As mentioned previously, the IDE renamed the Title column of the database's Tables as Title1 in the generated entity data model to avoid a naming conflict with the class's name. Recall that Local returns an ObservableCollection<T> containing the row objects of the specified table—in this case, Local returns an ObservableCollection<Title>. When you invoke OrderBy on an ObservableCollection<T>, the method assigns object to the titleBindingSource.DataSource property. When the DataSource changes, the DataGridView iterates through the contents of the IEnumerable<T> and displays the data.

# Selecting Books with 2016 Copyright

Lines 46–49 filter the titles displayed by using the where extension method with the lambda expression

```cs
book => book.Copyright == "2016"
```

as an argument. The where extension method expects as its parameter a Func delegate representing a method that receives one parameter and returns a boolean indicating whether the method's argument matches the specified criteria. The lambda expression used here takes Title object (named book) as its parameter and uses it to check whether the given Title's Copyright property (a string in the database) is 2014. A lambda expression for this lambda returns true. We use OrderBy to get the results by the Title1 property so the books are displayed in ascending order. The type of the book's parameter is inferred from dbcontext.Titles.Local, which contains Title objects. As soon as the titleBindingSource.DataSource property changes, the DataGridView is updated with the query results.

# Selecting Books with Title End in "How to Program"

Lines 54–58 filter the titles displayed by using the where extension method with the lambda expression

```cs
book.Title1.EndsWith("How to Program")
```

as an argument. The lambda expression takes one Title object (named book) as its parameter and uses it to check whether the given Title's Title property value ends with "How to Program". The expression returns the string stored in that property, then we use the string class method to perform the test. We return the results by the Title1 property so the books are displayed in ascending order.

# 22.7 Retrieving Data from Multiple Tables with LINQ

In this section, you will perform LINQ to queries using the LINQ query syntax that was introduced in Chapter 9. In particular, you will learn to obtain query results that combine data from multiple tables (Figs. 22.27–22.29). The Joining Tables with LINQ uses LINQ to Entities to combine and organize data from multiple tables, and shows the results of queries that perform the following tasks:

- Get a list of all the authors and the ISBNs of the books they've authored, sorted by last name, first name (Fig. 22.27).

- Get a list of all the authors and the titles of the books they've authored, sorted by last name, first name; for each author sort the titles alphabetically (Fig. 22.28).

- Get a list of all book titles grouped by author, sorted by last name; for any given author sort the titles alphabetically (Fig. 22.29).

![](img/57baed2319be0bb1b5f98674846f2711_960_0.png)

**Fig. 22.27** | Joining Tables with LINQ showing the authors and the ISBNs of the books they've authored. The authors are sorted by last name, first name.

![](img/57baed2319be0bb1b5f98674846f2711_960_1.png)

**Fig. 22.28** | Joining Tables with LINQ showing the authors and the titles of the book's they authored. The authors are sorted by last name, first name, and the titles for a given author are sorted alphabetically.

![](img/57baed2319be0bb1b5f98674846f2711_961_0.png)

**22.29 | Joining Tables with LINQ app showing the list of titles grouped by author.** The authors are sorted by last name, first name, and the titles for a given author are sorted alphabetically.

# GUI for the Joining Tables with LINQ App

For this example (22.30–22.23), perform the steps in Section 22.5.2 to create a new Forms Application project named JoinQueries in the same solution as the previous examples. Rename the Form1.cs source file to JoiningTableData.cs. Set the Form’s Text property to Joining Tables with LINQ. Be sure to add references to the Books-Examples and EntityFramework libraries, adding the connection string to the project’s App.Config file and set the JoinQueries project as the startup project. We set the following properties for textBox:

- Font property: Set to Lucida Console to display the output.
- Multiline property: Set to True so that multiple lines can be displayed.
- Anchor property: Set to Top, Bottom, Left, Right so that you can resize the window and the textBox accordingly.
- Scrollbars property: Set to Vertical so that you can scroll through the output.

# Creating the DbContext

The code uses the entity model to combine data from the tables and display the relationships between authors and books in several figures (Fig. 22.30–22.33) for presentation purposes. As in previous examples, the DbContext object (Fig. 22.30, line 19) allows the program to interact with the database.

```cs
// Fig. 22.30: JoiningTableData.cs
// Using LINQ to perform a join and aggregate data across tables.
using System;
using System.Linq;
using System.Windows.Forms;

namespace JoinQueries
{
    public class JoiningTableData : Form
    {
        public JoiningTableData()
        {
            InitializeComponent();
        }

        private void JoiningTableData_Load(object sender, EventArgs e)
        {
            // Entity Framework DbContext
            var dbcontext = new BooksExamples.BooksEntities();
        }}```

# 22.30 | Creating the BooksEntities for querying the Books database.

**Combining Author Names with the ISBNs of the Books They've Written**
The first query (Fig. 22.31, lines 22–26) joins from two tables and returns a list of author names representing the books they've written, sorted by LastName, then FirstName. The query takes advantage of properties in the entity model classes that were created based on foreign-key relationships between the database' tables. These properties enable you to easily combine rows from multiple tables.

```cs
// get authors and ISBNs of each book they-authored
var authorsAndISBNs =
    from author in dbcontext.Authors
    from book in author.Titles
    orderby author.LastName, author.FirstName
    select new{author.FirstName, author.LastName, book.ISBN};
```

```cs
// display authors and ISBNs in tabular format
foreach (var element in authorsAndISBNs)
{
    outputTextBox.AppendText("\r\n${element.FirstName
```

The first from clause (line 23) gets each author from the Authors table. The second from clause (line 24) uses the Author's Titles property to get the ISBNs for the current author. The entity model uses the foreign-key information stored in the data-
