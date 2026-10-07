# ASP.NET Web Services

| WebServiceSelectProject | HelloWorld() |
|---|---|
| A | using System.Web;
using System.Data.SqlClient;
using System.Configuration;
namespace WebServiceSelect_Project
{
// <summary>
// Summary description for WebServiceSelect
// </summary>
[WebService(Namespace = "https://www.routledge.com/978-1032132554//\`)]
[WebServiceBinding(ConformsTo=XmlProfiles.BasicProfile1_1)]
[System.ComponentModel.Model]
// To allow this Web Service to be called from script, using ASP.NET AJAX, uncomment the following line.
public class WebServiceSelect : WebService
{
[WebMethod]
public string HelloWorld()
{
string cmdString = ConfigurationManager.ConnectionStrings["sql_conn"].ConnectionString;
SqlConnection connection = new SqlConnection();
connection.ConnectionString = cmdString;
if (connection.State != System.Data.ConnectionState.Open)
{
return "Database open is failed!";
}
else
{
connection.Close();
return "Database open is successful!";
}
}
 |

**Figure 9.17** The modified codes to test the connection string.

containing the contents of the ConnectionStringsSection for the current application's
default configuration, and a ConnectionStringsSection object contains the contents of the
configuration file's connectionStrings section.

+   C. A new SQL Connection object is created and initialized with the connection we
tained above.

+   D. The Open() of the SQL Connection object is executed to open our sample
database and setup connection.

+   E. By checking the State property of the Connection object, we can determine whether or not
this connection is successful. If the State property is not equal to the ConnectionState.Open,
which means that a valid database connection has not been installed, a warning message is
returned and displayed.

+   F. Otherwise, the connection is successful, a successful message is displayed and the connecntion closed.

Now you can run the project by clicking on the IIS Express button. Click on the HelloWorld method
from the build-in Web interface, and then click the Invoke button to execute that method to test
our database connection.

A successful message should be displayed if the connection is fine, as shown in Figure 9.18. Click
on the Close button located at the upper-right corner of that page to terminate our Web service project.
A point is that this piece of code is only used for testing the project and we will modify this piece
of codes and place it into a user-defined function SQLConn() later when we develop our real project.