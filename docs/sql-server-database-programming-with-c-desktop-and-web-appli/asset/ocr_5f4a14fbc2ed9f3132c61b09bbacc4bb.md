# 470 SQL Server Database Programming with C#

# 8.7.4 PERFORM LINQ TO SQL QUERY TO FACULTY TABLE BY Faculty PAGE

In this section, we divide our coding process into the following six parts:

+   1) Create a new object of the DataContext class and do some initialization coding.
2) Develop the codes for the Select button's Click method to retrieve back selected faculty information using the LINQ to SQL query.
3) Develop the codes for the Insert button's Click method to insert new faculty member using the LINQ to SQL query.
4) Develop the codes for the Update button's Click method to update the selected faculty member using the LINQ to SQL query.
5) Develop the codes for the Delete button's Click method to delete the selected faculty member using the LINQ to SQL query.
6) Develop the codes for the Back button click method to return to the Selection page.

Now let's start our coding process from the first list above.

# 8.7.41 Create New Object of the DataContext Class

Open the window and the Page_Load() method of the Faculty Web page, and enter the codes that are shown in Figure 8.61 into this method.

Let's have a close look at this piece of codes to see how to use.

+   A. A new field-level object of the DataContext class, cse_dept, is created first since we need to use this object to connect our sample database to this Web project to perform the data actions later.
. A user-defined method CurrentFaculty() is executed to retrieve back all faculty members from our sample database and display them in the ComboName combobox control to allow the user to select a desired faculty later. To avoid multiple displaying of retrieved

| WebLINSQL Project | Page_Load(object sender, EventArgs e) |
|---|---||
| using System;
System.Linq;
public partial class _Default : System.Web.UI.Page
{ CSE_DEPTDataContext cse_dept = new CSE_DEPTDataContext();
protected void Page_Load(object sender, EventArgs e)
{ if (isPostBack)
{ CurrentFaculty();
ComboName.SelectedIndex = 0;
 }
void CurrentFaculty()
{ ComboName.Items.Clear();
var faculty = (from fi in cse_dept.Faculties
let fields = "faculty_name"
select fi);
foreach (var fi in faculty)
ComboName.Items.Add(fi.faculty_name);
} |

FIGURE 8.61 Initialization codes for the faculty web page.