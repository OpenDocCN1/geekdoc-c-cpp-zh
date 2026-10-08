
22.9 Address Book Case Study 973

```csharp
// when the form loads, fill it with data from the database
private void Contacts_Load(object sender, EventArgs e)
{
    RefreshContacts(); // fill binding with data from database
}
```

**Fig. 22.42** | Calling RefreshContacts to fill the TextBox when the app loads.

## Method addressBindingNavigatorSaveItem_Click

MethodBindingNavigatorSaveItem_Click (Fig. 22.43) saves the changes to the database when the BindingNavigator's Save Data button is clicked.(Remember to enable this.) The Address database requires values for the first name, last name, phone number and email. If a field is empty when you attempt to save, a DbEntityValidation exception occurs. We call RefreshContacts (line 72) after saving to re-sort the data and move back to the first element.

```csharp
// Click event handler for the Save Button in
// BindingNavigator saves the changes to the data
private void addressBindingNavigatorSaveItem_Click(
    object sender, EventArgs e)
{
    Validate(); // validate input fields
    addressBindingSource.EndEdit(); // complete current edit, if any
    // try to save
    try {
        dbcontext.SaveChanges(); // write changes to database file
    } catch (DbEntityValidationException) {
        MessageBox.Show("Columns cannot be empty",
        "Entity Validation Exception");
    }
    RefreshContacts(); // change back to updated unfiltered data
}
```

**Fig. 22.43** | Saving changes to the database when the user clicks Save Data.

## Method FindButton_Click

MethodFindButton_Click (Fig. 22.44) uses LINQ query syntax (lines 81–85) to select only people whose last name start with the characters in the TextBox. The query sorts the results by name, first name. In LINQ to Entities, you cannot bind a LINQ query directly to a BindingSource.DataSource. So, line 88 gets the object's ToList to get a List representation of the filtered data and assigns the List to the BindingSource.DataSource. When you convert the query to a List, any changes to existing records in the DbContext are tracked by the DbContext—any records that you add or remove while viewing the filtered data would be lost. For this reason disabled the Add new and Delete buttons when the data is filtered. When you enter a last name and Find, the BindingNavigator allows the user to browse only the rows containing the matching names. This is because the data bound to the Form's controls (the result of the LINQ query) has changed and now only a limited number of rows.

```csharp
// use LINQ to create a data source that contains only
// with last names that start with the specified text
private void findButton_Click(object sender, EventArgs e)
{
    // use LINQ to filter contacts with last names that
    // start with findTextBox contents
    var lastName =
        from address in dbcontext.Addresses
        where address.LastName.StartsWith(findTextBox.Text)
        orderby address.LastName, address.FirstName
        select address;

    // display matching contacts
    addressBindingSource.DataSource = lastQuery.ToList();
    addressBindingSource.MoveFirst(); // go to first result
    // don't add/delete when contacts are filtered
    bindingNavigatorAddNewItem.Enabled = false;
    bindingNavigatorDeleteItem.Enabled = false;
}
```

Fig. 22.44 Finding the contacts whose last names begin with a specified String.

Method browseAllButton_Click
Method browseAllButton_Click (Fig. 22.45) allows users to return to browsing all the rows after searching for specific rows. Double click browseButton to create a Click event handler. The event handler handles the Add and Delete buttons, then calls RefreshContacts to restore the data source to the full list of people (in sorted order) and clear the findTextBox.

```csharp
// reload addressBindingSource with all rows
private void browseAllButton_Click(object sender, EventArgs e)
{
    // allow add/delete when contacts are not filtered
    bindingNavigatorAddNewItem.Enabled = true;
    bindingNavigatorDeleteItem.Enabled = true;
    RefreshContacts(); // change back to initial unfiltered data
}
```

Fig. 22.45 Allowing the user to browse all contacts.

## 22.10 Tools and Web Resources

Our LINQ Center at www.deitel.com/LINQ contains many links to additional information, including blogs by Microsoft LINQ team members, sample chapters, tutorials, videos, downloads, FAQs, forums, webcasts and other resource sites.

A useful tool for learning LINQ is LINQCPad

```
http://www.linq.net
```

which allows you to execute and view the results of any C# or Visual Basic expression, including LINQ queries. It also supports the ADO.NET Entity Framework and LINQ to Entities.

This chapter is meant as an introduction to databases, the ADO.NET Entity Framework and LINQ to Entities. Microsoft's Entity Framework site

```
https://msdn.microsoft.com/en-us/data/aa937723
```

provides lots of information on working with the ADO.NET Entity Framework and LINQ to Entities, including tutorials, videos and more.

## 22.11 Wrap-Up

This chapter introduced the relational database model, the ADO.NET Entity Framework, LINQ to Entities and Visual Studio's visual programming tools for working with databases. You examined the contents of a sample database and learned about the relationships among tables in the database. You used LINQ to Entities and the entity data classes generated by the IDE to retrieve data, add new data, delete data and update in a SQL Server Express database.

We discussed the data model classes automatically generated by the IDE, such as the DbContext class that connects an app's interactions with a database. You learned how to use the IDE's tools to connect to databases and generate entity data model classes based on an existing schema. You used the IDE's drag-and-drop capabilities to automatically generate GUIs for displaying and manipulating database data. In the next chapter, we will show how to use asynchronous programming with C#'s async modifier and await operator to take advantage of multicore architectures.

## Summary

### 22.1 Introduction

- A database is an organized collection of data.
- A database management system (DBMS) provides mechanisms for storing, organizing, retrieving and modifying data.
- SQL Server Express provides most of the features of Microsoft's full (fee-based) SQL Server product, but has some limitations, such as a maximum database size.
- A SQL Server Express database can be easily migrated to a full version of SQL Server.
- The ADO.NET Entity Framework and LINQ to Entities allow you to manipulate relational data stored in a relational database, such as a SQL Server Express database.

### Section 22.2 Relational Databases

- A relational database organizes data simply in tables.
- Tables are composed of rows and columns (also called fields) in which values are stored.
- A column (or group of columns) of each row is the primary key—a column (or group of columns) requiring a unique value that cannot be duplicated in other rows. This guarantees that a primary-key can be used to uniquely identify a row.
- A primary key composed of two or more columns is known as a composite key.
- Each column represents a different data attribute.
- Rows are unique (by primary key) within a table, but some column values may be duplicated between rows.

### Section 22.3 A Books About Database

- A database's table, its fields and the relationships between them are collectively known as a database schema.
- A foreign key is a column in one table that matches the primary-key in another.
- Foreign keys, which are specified when a database table is created, link the data in multiple tables.
- Every foreign-key value must appear as another primary-key so the DBMS can ensure the foreign-key is valid.
- Foreign keys also allow relation in multiple tables to be selected from these tables—this is known as joining the data.
- There's a one-to-many relationship between a primary key and a corresponding foreign key—a foreign key can appear many times in its own table but only once in another table.
- An entity-relationship (ER) diagram shows the tables in a database and their relationships.
- Every row must have a value in the primary-column, and the value of the key must be unique in the table.

### Section 22.4 LINQ to Entities and the ADO.NET Framework

- With the ADO.NET Entity Framework, you interact with the database via classes that the IDE generates from the database schema when you add ADO.NET Entity Data Model to your project.
- The IDE creates two classes for a table. The first class represents a row of the table and properties for each table column. Objects of this class are called rows and store the data from individual rows of the table. The IDE uses the singular version of a table's plural name as the row class's name. The second class represents table itself. An object of this class stores a collection of rows that corresponds to all of the rows in the table.
- The entity data model has full IntelliSense support in the IDE.
- Navigation properties in row classes represent the relationships between tables.
- A DbContext (namespace System.Data.Entity) manages the data flow between the program and the database. When the IDE generates the entity model's row and table classes, it also creates a derived class of DbContext that is specific to the database being manipulated. This class contains properties that represent the database's tables.
- Changes to the data managed by a DbContext can be saved to the database using the DbContext's Changes method.
