
```csharp
using System.Drawing;
using System.Linq;
using System.Text;
using System.Windows.Forms;

namespace Accessing_Data
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }

        private void partsBindingNavigatorSaveItem_Click(object sender, EventArgs e)
        {
            this.Validate();
            this.partsBindingSource.EndEdit();
            this.tableAdapterManager.UpdateAll(this.assets_MaintenanceDataSet);
        }

        private void Form1_Load(object sender, EventArgs e)
        {
            // TODO: This line of code loads data into the "assets_MaintenanceDataSet.Part_Faults" table. You can move, or remove it, as needed.
            this.part_FaultsTableAdapter.Fill(this.assets_MaintenanceDataSet.Part_Faults);
            // TODO: This line of code loads data into the "assets_MaintenanceDataSet.Parts" table. You can move, or remove it, as needed.
            this.partsTableAdapter.Fill(this.assets_MaintenanceDataSet.Parts);
        }
    }
}
```

While this is fairly straightforward, it obviously isn’t everything that you need. The rest of the code is in the file that generates the visual form itself, supporting the visual components.

The time may come when you want to connect to a database without using visual tools. I discuss the steps in the earlier section “How the Data Classes Fit into the Framework,” and here I show the code to go with it:

- 1. `SqlConnection mainConnection = new SqlConnection();`
- 2. `mainConnection.ConnectionString = "server=local;database=assets_Maintenance;Trusted_Connection=True";`
- 3. `SqlDataAdapter partsAdapter = new SqlDataAdapter("SELECT * FROM Parts", mainConnection);`
- 4. `DataSet partsDataSet = new DataSet();`
- 5. `mainConnection.Open();`
- 6. `partsAdapter.Fill(partsDataSet);`
- 7. `mainConnection.Close();`

![](img/80ff26f06fc9ab951e1cd4257b867366_457_0.png)

This becomes useful especially when you want to build a web service or a class library — though it should be noted that you can still use the visual tools in those project types.

Let’s talk about this a line at a time. Line 1 sets up a new data connection, and line 2 populates it with the connection string. You can get this from your Database Administrator (DBA) or from the properties panel for the data connection.

Line 3 has a SQL Query in it. In Chapter 1 of this minibook, I talk about how this is a bad deal, and you should use Stored Procedures. A Stored Procedure is a database artifact that allows you to use a parameterized query from ADO.NET, rather than dynamically generated SQL Strings. Don’t use inline SQL for production systems. I could have just as easily put a stored procedure name in there.

Line 4 builds a new dataset. This is where the schema of the returned data is held and what I would use to navigate the data.

Lines 5, 6, and 7 perform the magic: Open the connection, contact the database, fill the dataset using the adapter, and then close the database. It’s all straightforward in this simple example. More complex examples make for more complex code.

After running this code, you would have the Products table in a DataSet container, just as you did in the visual tools in the earlier section, "How the Data Classes Fit into the Framework." To access the information, you set the value of a text box to the value of a cell in the DataSet container, like this:

```
TextBox1.Text = myDataSet.Tables[0].Rows[0]["name"];
```

To change to the next record, you need to write code that changes the Rows[0] to Rows[1] in the next example. As you can see, it would be a fair amount of code.

That’s why few people use the basic data code to get the databases. Either you use the visual tools, or you use an Object Relationship Model of some sort, like Entity Framework.

## Using the Entity Framework

I don’t want to get into much programming philosophy here, but object models (which I discuss in much of this book) and databases just don’t go together. They’re two different ways of thinking of the same information.

The problem mostly lies in inheritance, which I discuss in Book II. If you have a class called ScheduledEvent, which has certain properties, and a bunch of classes that inherit from it, like Courses, Conferences, and Parties, there just isn’t a good way to show this in a relational type of database. If you make a big table for `ScheduledEvents` with all possible types of properties and just make a `Type` property so that you can tell the `Courses` from the `Parties`, you have a lot of empty table cells. If you make a table for just the properties that are in `ScheduledEvents` and then separate tables for `Courses` and `Parties`, you make the database remarkably complex.

To address this problem, Microsoft created the Entity Framework. It's the latest edition of a product that Microsoft and everyone else has tried to create since the popularity of relational databases and object-oriented programming made object role modelers necessary.

Object Role Modelers try to take the whole shootin' match and turn it on its head. The goal is to design the database first (which I recommend anyway) and then make an object model to work with it automatically. Then, keep it up to date.

The Entity Framework does an acceptable job at that process. It generates a context for you that you can use to communicate with your data in a way that looks more like an object model than it does a database.

### Generating the entity model

To get started, you need the model itself. Just follow these steps to generate the entity model:

- 1. **Create a new project.**
    I used a Windows Forms project again, called EntityFramework.
- 2. **Right-click the project and click Add New in the context menu; Select ADO.NET Entity Data Model and name it PartsDatabase.**
- 3. **Choose Generate from Database Option in the Choose Model Contents window.**
- 4. **Select the `Assets_Database.mdf` from the Connection drop-down list.**
    If it isn't there, see the earlier section "Connecting to a data source."
- 5. **If you get a message asking whether you'd like to copy the database into the project, select No.**
    Copying the database is usually a bad practice, especially if you're on a shared project. If you're building a standalone project and are working alone, it is an acceptable solution.
- 6. **Select the Asset_Parts, Assets, Part_Faults, and Parts tables, just for fun (see Figure 2-13) and keep the default name.**

![](img/80ff26f06fc9ab951e1cd4257b867366_460_0.png)

Figure 2-13: Select a few tables.

The next thing you see is the designer canvas for the Class Designer. A sample diagram is shown in Figure 2-14. It's just a class diagram, like the ones in Book III, Chapter 2.

![](img/80ff26f06fc9ab951e1cd4257b867366_460_1.png)

Figure 2-14: Looks like a class model, walks like a database.

Notice something missing? The `Asset_Parts` table is gone; it's been abstracted into the model for you because the table was there only to link the Assets and Parts tables in a many-to-many relationship. Slick, isn't it?

### Writing code for the entity model

After you have an interesting addition to your coding environment and the database is meshed nicely into the C# object model, you can code with the objects provided in this new entity model. To start, follow these steps:

- 1. Go back to the window designer and double-click the window to go to **Code View**.
- 2. In the `window.Load` event handler, type `Part part = new Part();`.
- 3. In the next line, type `part.` and check out the IntelliSense.

It contains all columns in the Parts table as properties to the class.

What you now have is a context to work against. No complex LINQ queries — they're all done under the covers. No inline SQL. No stored procedures. You can do it all with a scoped object.

## Chapter 3: Fishing the FileStream

### In This Chapter

- Reading and writing data files
- Using the Stream classes
- Using the using statement
- Dealing with input/output errors

I once caught two trout on a single hook, in a lovely mountain stream in my native Colorado — quite a thrill for an 11-year-old. Fishing the “file stream” with C# isn’t quite so thrilling, but it’s one of those indispensable programming skills.

File access refers to the storage and retrieval of data on the disk. I cover basic text-file input/output in this chapter. Reading and writing data from databases is covered in Chapter 2 of this minibook, and reading and writing information to the Internet is covered in Chapter 4.

### Going Where the Fish Are: The FileStream

The console application programs in this book mostly take their input from, and send their output to, the console. Programs outside this chapter have better — or at least different — things to do with file manipulation. I don’t want to confuse their message with the extra baggage of involved input/output (I/O). However, console applications that don’t perform file I/O are about as common as Sierra Club banners at a paper mill.

The I/O classes are defined in the `System.IO` namespace. The basic file I/O class is `FileStream`. In days past, the programmer would open a file. The `open` command would prepare the file and return a handle. Usually, this handle was nothing more than a number, like the one they give you when you place an order at a Burger Shop. Every time you wanted to read from or write to the file, you presented this ID.

### Streams

C# uses a more intuitive approach, associating each file with an object of class `FileStream`. The constructor for `FileStream` opens the file and manages the underlying handle. The methods of `FileStream` perform the file I/O.
