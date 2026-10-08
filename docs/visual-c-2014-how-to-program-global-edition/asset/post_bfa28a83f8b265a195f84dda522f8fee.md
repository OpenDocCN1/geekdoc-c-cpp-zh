
Now, when you use the BindingNavigator to change the selected Author, the corresponding titles are displayed in the DataGridview.

```c
// Fig. 22.37: Details.cs
// Using a DataGridView to display details based on a selection.
using System;
using System.Data.Entity;
using System.Linq;
using System.Windows.Forms;

namespace MasterDetail {
    public partial class Details : Form {
        InitializeComponent();
    }

    // Entity Framework DbContext
    BooksExamples.BooksEntities dbcontext = new BooksExamples.BooksEntities();
    
    // initialize data sources when the Form is loaded
    private void Details_Load(object sender, EventArgs e) {
        // load Authors table ordered by LastName then FirstName
        dbContext.Authors
            .OrderBy(author => author.LastName)
            .ThenBy(author => author.FirstName)
            .Load();
    }
    // specify DataSource for authorBindingSource
    authorBindingSource.DataSource = dbcontext.Authors.Local;
}
```

Fig. 22.37 | Using a DataGridView to display details based on a selection.

## 22.9 Address Book Case Study

Our final example implements a simple AddressBook app (with sample outputs in Figs. 22.38–40) that enables users to perform the following tasks on the database AddressBook.mdf (which is included in the directory with this chapter's examples):

- Insert new contacts.
- Find contacts whose last names begin with the specified letters.
- Update existing contacts.
- Delete contacts.

We populated the database with six fictional contacts.

## 22.9 Address Book Case Study

![](img/57baed2319be0bb1b5f98674846f2711_969_0.png)

Fig. 22.38 | Use the BindingNavigator's controls to navigate through the contacts.

![](img/57baed2319be0bb1b5f98674846f2711_969_1.png)

Fig. 22.39 | Type a search string in the Last Name TextBox, then press Find to locate contacts whose last names begin with that string. Only two names start with Br, so the BindingNavigator shows the first of two matching records.

![](img/57baed2319be0bb1b5f98674846f2711_969_2.png)

Fig. 22.40 | Click Browse All Entries to clear a search and return to browsing all contacts.

## Chapter 22 Databases and LINQ

Rather than displaying a database table in a DataGridView, this app presents the details of one contact at a time in several TextBoxes. The BindingNavigator at the top of the window allows you to control which row of the table is displayed at any given time. The BindingNavigator also allows you to add a contact and delete a contact—but only when browsing the complete contact list. When you filter the contacts by last name, the app disables the Add new

![](img/57baed2319be0bb1b5f98674846f2711_970_0.png)

Delete

![](img/57baed2319be0bb1b5f98674846f2711_970_1.png)

buttons (we'll explain shortly). Clicking Browse All Entries enables these buttons. Adding a row clears the TextBoxes and sets the TextBox to the right of Address ID to zero to indicate that the TextBoxes now represent a new record. When you save a entry, the Address field is automatically changed from zero to a unique ID number by the database. No changes are made to the underlying database unless you click the Save Data:

### 22.9.1 Creating the Address Book App's GUI

We discuss the app's code momentarily. First you'll set up a new solution containing the entity model and a Windows Forms App. Close the BooksExamples solution you used in this chapter's previous examples.

Step 1: Creating a Class Library Project for the Entity Data Model
Perform the steps in Section 22.5 to create a Class Library project named AddressExample that contains entity data for the AddressBook.mdb database, which contains only an Addresses table with AddressID, FirstName, LastName, Email and PhoneNumber columns. Make the entity data model AddressModel. The AddressBook.mdb database is located in the Databases folder for this chapter's examples.

Step 2: Creating a Windows Application Project for the Address Book App
Perform the steps in Section 22.5.2 to create a new Windows Application project named AddressBook in the AddressExample solution. Set the Form's filename to Contacts.cs, then set the Form's Text property to Address Book. Set the AddressBook project as the solution's startup project.

Step 3: Adding the Address Object as a Data Source
Add the entity data Address's object as a data source, as you did with the Author in Step 1 of Section 22.5.

Step 4: Displaying the Details of Each Row
Design view, select the Address node in the Data Sources window. Click the Address's down arrow and select the Details option to indicate that the IDE should create a set of Label-TextBox pairs to show the details of a single record at a time.

## 22.9 Address Book Case Study

Step 5: Dragging the Address Node to the Form
Drag the node from the Form. This automatically creates the Navigator and the TextBoxes. Design view, select the Address node in the Data Sources window. Click the Address's down arrow and select the Details option to indicate that the IDE should create a set of Label-TextBox pairs to show the details of a single record at a time.

Step 5: Making the Address ReadOnly
While we maintained one dbcontext for the duration of the program, if the user changed a person's last name, the records would still remain in their order. Lines 36–39 order the objects in memory.

Step 6: Adding Controls to Allow Users to Specify Last Name
To allow users to search, add a Label named findLabel, a TextBox named findTextBox, and a Button named findButton. Place these controls in findGroup, then set the Text property of find Name.

Step 7: Allowing the User to Return to Browsing All
To allow users to return to all contacts after searching, add a Button named browseAll.

## 22.9.2 Coding the Address App

The Contacts.cs code-behind is split into several figures (Figs. 22.41–45) for purposes.

Method RefreshContacts
As showed in previous examples, we must connect the addressSource with the database. In this example, we declare the DbContext. create a new DbContext at line 22. We do so we can reorder records based on edits.

```c
// Fig. 22.41: Contact.cs
// Manipulating an address book.
using System;
using System.Data;
using System.Data.Entity;
using System.Data.Validation;
using System.Linq;
using System.Windows.Forms;

namespace AddressBook
{
    public partial class Contacts : Form
    {
        public Contacts()
        {
            InitializeComponent();
        }

        // Entity Framework DbContext
        private BindingExample.AddressBookEntities dbcontext = null;

        // fill our bindingSource with all rows, ordered by name
        private void RefreshContacts()
        {
            // Dispose old DbContext, if any
            if (dbContext != null)
            {
                dbContext.Dispose();
            }

            // create new DbContext so we can reorder records based on edits
            dbContext = new AddressExample.AddressBookEntities();

            // use LINQ to order the Addresses table contents
            dbContext.Addresses
.OrderBy(entry => entry.LastName).ThenBy(entry => entry.FirstName).Load();

            // specify DataSource for the addressBindingSource
            addressBindingSource.DataSource = dbcontext.Addresses.Local;
            addressBindingSource.MoveFirst(); // go to first result
            TextBox.Clear(); // clear the Text Box
        }
    }
}
```

Fig. 22.41 | Creating the BooksEntities and defining method RefreshContacts for use in other methods.

**Method Contacts_Load**
Method Contacts_Load (Fig. 22.42) calls RefreshContacts (line 50) so that the first record is displayed when the app starts. As before, you create the Load event handler by double-clicking the Form's title bar.
