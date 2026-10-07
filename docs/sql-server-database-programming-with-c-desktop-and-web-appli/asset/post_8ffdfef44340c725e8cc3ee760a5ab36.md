
# Access Data in ASP.NET

| WebLINQSQL Project | Page_Load(object sender, EventArgs e) |
|---|---|
| using System; namespace SQLWebSelect_Project { public partial class Selection : System.Web.UI.Page { Faculty facultyPage = new Faculty(); Course coursePage = new Course(); Student studentPage = new Student(); protected void Page_Load(object sender, EventArgs e) { if (IsPostBack) { ComboSelection.Items.Add("Faculty Information"); ComboSelection.Items.Add("Course Information"); ComboSelection.Items.Add("Student Information"); ComboSelection.SelectedIndex = 0; } } } } |

**FIGURE 8.59** Codes for the selection page class.

| WebLINQSQL Project | cmdSelect_Click(object sender, EventArgs e) |
|---|---|
| protected void cmdSelect_Click(object sender, EventArgs e) { if (ComboSelection.Text == "Faculty Information") { Redirect("Faculty.aspx"); } else if (ComboSelection.Text == "Course Information") { Redirect("Course.aspx"); } else if (ComboSelection.Text == "Student Information") { Redirect("Student.aspx"); } else { Response.Write("<script>alert(\'Invalid Selection!\')</script>"); } } facultyPage.Dispose(); coursePage.Dispose(); studentPage.Dispose(); Response.Write("<script>window.close()</script>"); } |

**FIGURE 8.60** The codes for the selection-exit button click months on the selection page.

The page is also involved in this selection process, but we did not discuss the building process for that page. The reason is to save the readers' time and efforts. A completed Student page has been built and located at the Students\Web Forms from the CRC Press site. It is not needed to add this page as we will in Section 8.7 with all other pages together. If no page is selected, an error message is displayed to indicate that selection. When the Exit button is clicked, the first three pages are released to make them ready to be removed from the memory.

D. Finally, the Web application is closed by calling a system method `window.close()`.

Next let's continue to building codes for the Faculty page to perform the related data query from the Faculty sample database.

# 470 SQL Server Database Programming with C#

# 8.7.4 PERFORM LINQ TO SQL QUERY TO FACULTY TABLE BY Faculty PAGE

In this section, we divide our coding process into the following six parts:

- 1) Create a new object of the DataContext class and do some initialization coding.
- 2) Develop the codes for the Select button's Click method to retrieve back selected faculty information using the LINQ to SQL query.
- 3) Develop the codes for the Insert button's Click method to insert new faculty member using the LINQ to SQL query.
- 4) Develop the codes for the Update button's Click method to update the selected faculty member using the LINQ to SQL query.
- 5) Develop the codes for the Delete button's Click method to delete the selected faculty member using the LINQ to SQL query.
- 6) Develop the codes for the Back button click method to return to the Selection page.

Now let's start our coding process from the first list above.

# 8.7.41 Create New Object of the DataContext Class

Open the window and the Page_Load() method of the Faculty Web page, and enter the codes that are shown in Figure 8.61 into this method.

Let's have a close look at this piece of codes to see how to use.

- A. A new field-level object of the DataContext class, cse_dept, is created first since we need to use this object to connect our sample database to this Web project to perform the data actions later.
- B. A user-defined method CurrentFaculty() is executed to retrieve back all faculty members from our sample database and display them in the ComboName combobox control to allow the user to select a desired faculty later. To avoid multiple displaying of retrieved

| WebLINSQL Project | Page_Load(object sender, EventArgs e) |
|---|---|
| using System; System.Linq; public partial class _Default : System.Web.UI.Page { CSE_DEPTDataContext cse_dept = new CSE_DEPTDataContext(); protected void Page_Load(object sender, EventArgs e) { if (isPostBack) { CurrentFaculty(); ComboName.SelectedIndex = 0; } } void CurrentFaculty() { ComboName.Items.Clear(); var faculty = (from fi in cse_dept.Faculties let fields = "faculty_name" select fi); foreach (var fi in faculty) ComboName.Items.Add(fi.faculty_name); } } |

**FIGURE 8.61** Initialization codes for the faculty web page.

# Accessing Data in ASP.NET

faculty members, an if selection structure is adopted to make sure that we only displaying those current faculty members in the combbox at the first time as this Web page is loaded, and not display them each time the server sends back a refreshed Faculty page to the client.

- C. We can update the combobox control ComboBoxName by adding current faculty members into this control, a cleaning job is performed to avoid the multiple adding and displaying of these faculty members.
- D. The LINQ query is created and initialized with three classes, from, let and select. The range variable fi is selected from the Faculty entity in our sample database. All current faculty members (faculty_name) will be read back using the let clause and assigned to the query variable.
- E. The Linq query is executed to pick up all queried faculty members and add them into the ComboName combobox in our Faculty page.

Next lets take care of the coding for the Select button to get detailed information for a selected faculty member.

# 8.7.4.2 The Coding for the Data Selection Query

Double-click on the Select in the Design View of the Faculty page to open its Click method and enter the codes that are in Figure 8.62 to this method. The function of this piece is to retrieve detailed information for a selected faculty member from the Faculty table in our sample database and display them in select textboxes of the Faculty page with the selected image this Select button is clicked by the user.

Let’s have a look at this piece of code to see how it works.

- A. The LINQ query is created and initialized with three classes, from, where and select. The range variable fi is selected from the Faculty entity in our sample database based on a matched faculty members (faculty_name).
- B. The LINQ query then is executed to pick up columns for the selected faculty member and display them on the astext textbox in our Faculty page.

| WebLINSQL Project | cmdSelect_Click(object sender, EventArgs e) |
|---|---|
| protected void cmdSelect_Click(object sender, EventArgs e) { var f_info = from fi in cse_dept.Faculties where fi.faculty_name == ComboName.Text select fi; foreach (var f in f_info) { btxtFaculty.ID = f.faculty_id; btxtName.Text = f.faculty_name; btxtTitle.Text = f.title; btxtOffice.Text = f.office; btxtPhone.Text = f.phone; btxtCollege.Text = f.college; btxtEmail.Text = f.email; byte[] img = (f.image as System.Data.Linq.ToArray()); string bimg = Convert.ToBase64String(img); PhotoBox.ImageUrl = String.Format("data:image/jpg;base64,(0)", bimg); } } |

**FIGURE 8.62** The codes for the select click method.

# 472 SQL Server Database Programming with C#

C. The selected image is converted to a byte array img[], and furthermore converted to a String with a Base64String format.

D. Finally, String is formatted and assigned to the ImageUrl property of the Faculty Image box, PhotoBox, to be displayed.

Now let's concentrate on the coding for our data insertion actions. However, before we can continue building our codes to insert a new record into our database with the LINQ to SQL method, let's have a discussion about a key component, the DataContext class, with its methods to provide us a clear picture about DataContext and its implementations.

# 8.7.4.3 The DataContext Class and its Implementations

As discussed in Chapter 4, the DataContext is the source of all entities mapped over a database connection. It tracks changes that you made to all retrieved entities and an identity code that guarantees entities more than one are represented by using the same object instance.

In general, a DataContext is designed to last one unit of work; however, your application defines that. A DataContext is lightweight and not expensive to create. A LINQ to SQL application creates DataContext instances at method scope or as a map of short-lived classes that represent a logical set of related database operations.

Four constructors are involved with this class, the DataContext class contains 30 methods, the most popular methods are listed in Figure 8.64. Among these popular, the following methods are most important in the LINQ to SQL implementations:

- ExecuteCommand()
- ExecuteQuery()

FIGURE 8.63 Constructors of the DataContext class.

| Constructor | Functions |
|---|---|n| DataContext(Connection) | Initializes a new instance of the DataContext class by referencing the connection used by the .NET Framework. |
| DataContext(Connection, Source) | Initializes a new instance of the DataContext class by referencing a connection and a mapping source. |
| DataContext(String) | Initializes a new instance of the DataContext by referencing a file source. |
| DataContext(String, Source) | Initializes a new instance of the DataContext by referencing a file source and a mapping source. |

| Methods | Functions |
|---|---|n| CreateDatabase() | Dynamically creates a new database on the server. |
| DatabaseExists() | Determines whether the associated database can be opened. |
| DeleteDatabase() | Deletes the associated database. |
| ExecuteCommand(String, Object[1]) | Executes SQL commands directly on the database. |
| ExecuteQuery(Type, String, Object[1]) | Executes SQL queries directly on the database. |
| ExecuteQuery<TResult>(String, Object[1]) | Determines whether the associated database can be opened. |
| SubmitChanges() | Computes the set of modified objects to be inserted, updated, or deleted, and executes the appropriate command to implement the changes to the database. |
| ToString() | Returns a string that represents the current object (Inherited from Object). |

FIGURE 8.64 Most popular methods in the DataContext class.
