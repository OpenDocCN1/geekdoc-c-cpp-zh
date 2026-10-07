# Access Data in ASP.NET

| SQLWebSelect Project | Page_Load(object sender, EventArgs e) |
|--- |--- |
| using System.Data;
using System.Data.SqlClient;
namespace SQLWebSelectProject
 { public partial class Selection : System.Web.UI.Page
 { protected void Page_Load(object sender, EventArgs e)
 { ComboSelection.Items.Add("Faculty Information");
ComboSelection.Items.Add("Course Information");
ComboSelection.Items.Add("Student Information");
 } } | |

FIGURE 8.16 The coding for the Page_Load() method of the selection page.

| SQLWebSelect Project | cmdSelect_Click(object sender, EventArgs e) |
|--- |--- |
protected void cmdSelect_Click(object sender, EventArgs e)
 { if (ComboSelection.Text == "Faculty Information")
 Response.Redirect("Faculty.aspx");
else if (ComboSelection.Text == "Student Information")
 Response.Redirect("Student.aspx");
else if (ComboSelection.Text == "Course Information")
 Response.Redirect("Course.aspx");
 } | |

FIGURE 8.17 The coding for the select button's click.

Finally let's take care of coding for the Exit click method. The function of this piece of code is to close the database connection and the Web application. Double click the Exit button from the Design View of the Selection page to open this method. Enter the codes that are shown in Figure 8.18 into this method.

Let's have a closer look at this piece of codes to see how it works.
First need to check if the database is still connected to our application. If it is, the global connection object stated with the Close() method to close the database connection. Then the Write() method of the server Response object is called to close the Web application. A key point is that the Application function stores an object, the connection object in this case. In order to access and use that object stored in the Application global function, a casting SqlConnection must be clearly prefixed before that; therefore, a two-layer

| SQLWebSelect Project | cmdExit_Click(object sender

FIGURE 8.18 The coding for the exit button's click method.