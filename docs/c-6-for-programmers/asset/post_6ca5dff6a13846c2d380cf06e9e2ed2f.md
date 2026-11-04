
- Get a list of all the authors and the ISBNs of the books they've authored, sorted by last name, then first name (Fig. 20.27).
- Get a list of all the authors and the titles of the books they've authored, sorted by last name, then first name; for each author sort the titles alphabetically (Fig. 20.28).
- Get a list of all the book titles grouped by author, sorted by last name, then first name; for a given author sort the titles alphabetically (Fig. 20.29).

![](img/3f5ef6be1748bb746e5f71a483bba4d0_691_0.png)

**Fig. 20.27** | Joining Tables with LINQ app showing the list of authors and the ISBNs of the books they've authored. The authors are sorted by last name, then first name.

![](img/3f5ef6be1748bb746e5f71a483bba4d0_691_1.png)

**Fig. 20.28** | Joining Tables with LINQ app showing the list of authors and the titles of the books they've authored. The authors are sorted by last name, then first name, and the titles for a given author are sorted alphabetically.

![](img/3f5ef6be1748bb746e5f71a483bba4d0_692_0.png)

**Fig. 20.29** | Joining Tables with LINQ app showing the list of titles grouped by author. The authors are sorted by last name, then first name, and the titles for a given author are sorted alphabetically.

## GUI for the Joining Tables with LINQ App

For this example (Fig. 20.30–Fig. 20.33), perform the steps in Section 20.5.2 to create a new Windows Forms Application project named JoinQueries in the same solution as the previous examples. Rename the Form1.cs source file to JoiningTableData.cs. Set the Form’s Text property to Joining Tables with LINQ. Be sure to add references to the Books-Examples and EntityFramework libraries, add the connection string to the project’s App.Config file and set the JoinQueries project as the startup project. We set the following properties for the outputTextBox:

- **Font property:** Set to Lucida Console to display the output in a fixed-width font.
- **Multiline property:** Set to True so that multiple lines of text can be displayed.
- **Anchor property:** Set to Top, Bottom, Left, Right so that you can resize the window and the outputTextBox will resize accordingly.
- **Scrollbars property:** Set to Vertical, so that you can scroll through the output.

## Creating the DbContext

The code uses the entity data model classes to combine data from the tables in the Books database and display the relationships between the authors and books in three different ways. We split the code for class JoiningTableData into several figures (Figs. 20.30–20.33) for presentation purposes. As in previous examples, the DbContext object (Fig. 20.30, line 19) allows the program to interact with the database.

database's AuthorISBN table to get the appropriate ISBNs. The combined result of the two from clauses is a collection of all the authors and the ISBNs of the books they’ve authored. The two from clauses introduce two range variables into the scope of this query—other clauses can access both range variables to combine data from multiple tables. Line 25 orders the results by the author’s LastName, then FirstName. Line 26 creates a new anonymous type containing an author’s FirstName and LastName from the Authors table and the ISBN for one of that author’s books from the Titles table.

## Anonymous Types

Recall from Section 9.3.5 that a LINQ query’s select clause can create an anonymous type with the properties specified in the initializer list—in this case, FirstName, LastName and ISBN (line 26). Note that all properties of an anonymous type are public and read-only. Because the type has no name, you must use implicitly typed local variables to store references to objects of anonymous types (e.g., line 31). Also, in addition to the ToString method in an anonymous type, the compiler provides an Equals method, which compares the properties of the anonymous object that calls the method and the anonymous object that it receives as an argument.

## Combining Author Names with the Titles of the Books They’ve Written

The second query (Fig. 20.32, lines 38–42) gives similar output, but uses the foreign-key relationships to get the title of each book that an author wrote.

```csharp
// get authors and titles of each book they co-authored
var authorsAndTitles =
    from book in dbcontext.Titles
    from author in book.Authors
    orderby author.LastName, author.FirstName, book.Title1
    select new {author.FirstName, author.LastName, book.Title1};

outputTextBox.AppendText("\r\n\r\nAuthors and titles:");

// display authors and titles in tabular format
foreach (var element in authorsAndTitles)
{
    outputTextBox.AppendText($"{element.FirstName,-10} " +
        $"{element.LastName,-10} {element.Title1}");
}
```

**Fig. 20.32** | Getting a list of authors and the titles of the books they authored.

The first from clause (line 39) gets each book from the Titles table. The second from clause (line 40) uses the generated Authors property of the Title class to get only the authors for the current book. The entity data model uses the foreign-key information stored in the database’s AuthorISBN table to get the appropriate authors. The author objects give us access to the names of the current book’s authors. The select clause (line 42) uses the author and book range variables to get the FirstName and LastName of each author from the Authors table and the title of one of the author’s books from the Titles table.

## Organizing Book Titles by Author

Most queries return results with data arranged in a relational-style table of rows and columns. The last query (Fig. 20.33, lines 55–62) returns hierarchical results. Each element in the results contains the name of an author and a list of Titles that the author wrote. The LINQ query does this by using a nested query in the select clause. The outer query iterates over the authors in the database. The inner query takes a specific author and retrieves all titles that the author wrote. The select clause (lines 58–62) creates an anonymous type with two properties:

- The property Name (line 58) is initialized with a string that separates the author’s first and last names by a space.
- The property Titles (lines 59–62) is initialized with the result of the nested query, which returns the title of each book written by the current author.

In this case, we’re providing names for each property in the new anonymous type. When you create an anonymous type, you can specify the name for each property by using the format name = value.

```csharp
53  // get authors and titles of each book
54  // they co-authored; group by author
55  var titlesByAuthor =
56      from author in dbcontext.Authors
57      orderby author.LastName, author.FirstName
58      select new { Name = author.FirstName + " " + author.LastName,
59                  Titles =
60                      from book in author.Titles
61                      orderby book.Title
62                      select book.Title};

64  outputTextBox.AppendText("\r\n\r\nTitles grouped by author:");

66  // display titles written by each author, grouped by author
67  foreach (var author in titlesByAuthor)
68  {
69      // display author's name
70      outputTextBox.AppendText($"\r\n\t{author.Name}:");

72      // display titles written by that author
73      foreach (var title in author.Titles)
74      {
75          outputTextBox.AppendText($"\r\n\t\t{title}");
76      }
77  }
78 }
79 }
80 }
```

**Fig. 20.33**  Getting a list of titles grouped by authors.

The range variable book in the nested query iterates over the current author’s books using the Titles property. The Title1 property of a given book returns the Title column from that row of the Titles table in the database.

![](img/3f5ef6be1748bb746e5f71a483bba4d0_697_0.png)

**Fig. 20.35**   Finished design of the Master/Detail app.

## Step 2: Adding a Data Source for the Authors Table

Follow the steps in Section 20.5.3 to add a data source for the Authors table. Although you’ll be displaying records from the Titles table for each author, you do not need to add a data source for that table. The title information will be obtained from the Titles navigation property in the Author entity data model class.

## Step 3: Creating GUI Elements

Next, you’ll use the **Design** view to create the GUI components by dragging-and-dropping items from the **Data Sources** window onto the Form. In the earlier sections, you dragged an object from the **Data Sources** window to the Form to create a DataGridView. The IDE allows you to specify the type of control(s) that it will create when you drag-and-drop an object from the **Data Sources** window onto a Form. To do so:

- 1. Switch to **Design** view for the Details class.
- 2. Click the **Author** node in the **Data Sources** window—it should change to a drop-down list. Open the drop-down by clicking the down arrow and select the Details option—this indicates that we’d like to generate Label–TextBox pairs that represent each column of the Authors table.
- 3. Drag the **Author** node from the **Data Sources** window onto the Form in **Design** view. This creates the authorBindingSource, the authorBindingNavigator and the Label–TextBox pairs that represent each column in the table. Initially, the controls appear as shown in Fig. 20.36. We rearranged the controls as shown in Fig. 20.35.
- 4. By default, the **Titles** navigation property is implemented in the entity data model classes as a HashSet<Titles>. To bind the data to GUI controls properly, you must change this to an ObservableCollection<Title>. To do this, expand
