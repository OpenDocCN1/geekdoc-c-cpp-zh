
# Accessing Data in ASP.NET

| Type | ID | Text | TabIndex | BackColor | TextMode | Font |
|---|---|---|---|---|---|---|
| Label | Label1 | Welcome to CSE DEPT | 0 | #E0E0E0 | | Bold/Large |
| Label | Label2 | User Name | 1 | | | Bold/Small |
| Textbox | txtUserName | | 2 | | | |
| Label | Label3 | Pass Word | 3 | | | Bold/Small |
| Textbox | txtPassWord | | 4 | | Password | |
| Button | cmdLogin | Login | 5 | | | Bold/Medium |
| Button | cmdCancel | Cancel | 6 | | | Bold/Medium |

**FIGURE 8.7** Controls for the Login form.

Another difference with the Windows-based form is when you add these controls into our Web form, you must first locate a position for the control to be added using the **Space** key on your keyboard in the Web form, and then pick up a control from the Toolbox window and drag it to that location. You cannot pick or drag a control to a random location as you want in this Web form and this is a significant difference between the Windows-based form and the Web-based forms.

However, an exception or good news is that for Visual Studio 2022, you can still add and place any control to any random location as you did on a Windows Form as long as you set the **Position** property of each control to **Absolute** value. To do that, one needs to:

- 1. Add a control to the Web Form at a location.
2. Select that control by clicking on it.
3. Go to **Format | Set Position** menu item and check the **Absolute** property.

After this setup, you can move any control to any random location as you like, and this greatly increased the flexibility and efficiency of building our Web Form.
Your finished user interface should show the match in Figure 8.8.

![](img/d59a47501d0a20fc0460a49c469c6fb7_449_0.png)

**FIGURE 8.8** The finished Login web form.

Before we can add the codes into the code-behind page to rename the controls to perform the logon process, first we must run the project to allow the Web.config file to recognize those controls we have added into the Web form. The IIS Express button on the toolbar to run our project. We may need to click Yes to two prompted dialogues to enable our Web page to be certificated and recognized by the local server. The running Web page should match one is shown in Figure 8.8. Click the Close button that is located at the upper-right of the form to finish this phase.

- One important and interesting point to add a control to a Web Form to a random location is to set the Position property of each control to the Absolute value. After this setting, you can add any control and move it to any location as one did for the Windows Form.

Now's develop the codes to access the database to perform the logon process.

## 8.4.2 DEVELOP THE CODES TO ACCESS AND SELECT DATA FROM THE DATABASE

Open the code-behind page Login.aspx by right-clicking on it and select the View Code button from the Solution Explorer. Window. first need to add a SQL Server data-related namespace as we did for projects in the previous chapters. Adding the following namespace to the top of this code window to involve the namespaces for the database and the SQL Server Data Provider:

```csharp
using System.Data;
using System.Data.SqlClient;
```

Next we need to create a class or field-level variable, sqlConnection, for our connection object. Enter the following code under the class header:

```csharp
public SqlConnection sqlConnection;
```

This connection object will be used by all Web Forms in this project later.

We need to perform the coding for the Page_Load() method, which is similar to the Form_Load() method in the Windows-based application. Open this event method and enter the codes that are shown in Figure 8.9 into this method.

Let's have a closer look at this piece of codes to see how it works.

- A. Some system data and SQL data provider-related namespaces are added into this project since we need to use those components to perform data actions against our sample SQL Server database.
- B. A class-level Connection object, sqlConnection, is declared and this object will be used by all Web Forms in this project later to connect to our sample database.
- C. As we did for the Form_Load() method in the Windows-based applications, we need to perform the database connection join in this Page_Load() method. A connection string is created with the database server name, database name and security method.
- D. A new database Connection object sqlConnection is added to the Application state function and this object can be used by any pages in this application by accessing this Application state function.
- E. The Connection object sqlConnection is added to the Application state function and this object can be used by any pages in this application by accessing this Application state function later. Unlike global variables in the Windows-based applications, one cannot access a class variable by prefixing the form's name before the class variable declared in that form.

# Access Data in ASP.NET

| SQLWebSelect Project | Page_Load() |

```csharp
using System.Data;
using System.Data.SqlClient;
namespace SQLWebSelect_Project
{
    public class _Default :
    {
        public SqlConnection connection;
        protected void Page_Load(object sender, EventArgs args)
        {
            string connectionString = "Server-DESKTOP-24JUPFB\SQL2019EXPRESS;" + "Initial Catalog=CSE_DEPT;" + User ID=SMART;Password=2022";
            connection = new SqlConnection(connectionString);
            Application["connection"] = connection; //define a global object
            if (connection.State != ConnectionState.Open)
            {
                connection.Open();
            }
            connection.Close();
            connection.Open();
            if (connection.State != ConnectionState.Open)
            {
                Response.Write("<script>alert('Database connection is Failed')</script>");
            }
        }
    }
}
```

**Figure 8.9** for the Page_Load method.

from other pages. In the Web-based application, the Application state function is a good to store any global variable. In ASP.NET, the Application state function is a good to store any global variable.

- F. In the Web-based application, the Application state function is a good to store any global variable. In ASP.NET, the Application state function is a good to store any global variable.
- G. A new database Connection object sqlConnection is added to the Application state function and this object can be used by any pages in this application by accessing this Application state function.
- H. The Connection object sqlConnection is added to the Application state function and this object can be used by any pages in this application by accessing this Application state function later. Unlike global variables in the Windows-based applications, one cannot access a class variable by prefixing the form's name before the class variable declared in that form.
- I. In the Web-based application, the Application state function is a good to store any global variable. In ASP.NET, the Application state function is a good to store any global variable.
- J. A new database Connection object sqlConnection is added to the Application state function and this object can be used by any pages in this application by accessing this Application state function.
- K. The Connection object sqlConnection is added to the Application state function and display it. The message is created and sent back from the server.
- L. In the Web-based application, the Application state function is a good to store any global variable. In ASP.NET, the Application state function is a good to store any global variable.
- M. A new database Connection object sqlConnection is added to the Application state function and this object can be used by any pages in this application by accessing this Application state function.
- N. The Connection object sqlConnection is added to the Application state function and this object can be used by any pages in this application by accessing this Application state function later.

- In the Web-based application, the Application state function is a good to store any global variable. In ASP.NET, the Application state function is a good to store any global variable.

- F. In the Web-based application, the Application state function is a good to store any global variable. In ASP.NET, the Application state function is a good to store any global variable.
- G. A new database Connection object sqlConnection is added to the Application state function and this object can be used by any pages in this application by accessing this Application state function.
- H. The Connection object sqlConnection is added to the Application state function and this object can be used by any pages in this application by accessing this Application state function later.

- In the Web-based application, the Application state function is a good to store any global variable. In ASP.NET, the Application state function is a good to store any global variable.

## SQL Database Programming with C#

| SQLWebSelect Project | Page_Load() |
|---|---|
| A | protected voidLogin_Click(object sender, EventArgs args) { |
| B | string cmdString = "SELECT user_name, pass_word FROM Login ";
| C | cmdString += "WHERE user_name=@username AND pass_word=@password"; |
| D | SqlCommand cmd = new SqlCommand(cmdString); |
| E | cmd.Connection = sqlConnection; |
| F | SqlDataReader reader = cmd.ExecuteReader(); |
| G | cmd.CommandText = cmdString; |
| H | cmd.Parameters.Add("@username", SqlDbType.Char).Value = xtUsername.Text; |
| I | cmd.Parameters.Add("@password", SqlDbType.Char).Value = xtPassword.Text; |
| J | if (reader.HasRows) |
| K | reader.Close(); |
| L | Response.Write("<script>alert('Login is successful!')</script>"); |
| M | } else |
| N | Response.Write("<script>alert('No matched/password found!')</script>"); |
| O | } |
| P | cmd.Dispose(); |
| Q | } |

**FIGURE 8.10** The codes for the Login button's click.

Next let's make the coding for the Cancel button's Click method.

The function of this method is to close the current page when the Cancel button is clicked, which means that the user wants to terminate the ASP.NET Web application. Double-click the Cancel button from the Design View of the Login Form to open this method and enter the codes that are shown in Figure 8.11 to this method.
