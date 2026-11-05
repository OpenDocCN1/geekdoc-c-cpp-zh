FirstName and LastName from memberTable are retrieved. The SQL statement arranges the result by LastName. When there are duplicate records with the same last name, the records are arranged in ascending order by FirstName. The sql string object is set as the CommandText property value. The connection string, dbConn, is set as the Connection property as follows:

```
dbCmd.CommandText = sql;
dbCmd.Connection = dbConn;
```

To use the Fill( ) method with the DataSet object, an object of the DataAdapter class is instantiated. Notice that each of these classes is part of the OleDb namespace, thus class names are prefixed with OleDb. The SelectCommand property of the DataAdapter class is set to the CommandText object holding the SQL statement. Using the DataAdapter’s Fill( ) method, the table from the actual Access database (memberTable) is used to populate the DataSet object (memberDS). The last statement in the try block for Example 15-14 binds the DataGrid object to the DataSet. Recall that this is the only statement that changed from the Windows application.

Remember, Figure 15-19 shows this application running after all the controls are added to the page and event-handler methods are wired.

The complete program listing for the code-behind file for the WebControls project is shown in Example 15-15.

# Example 15-15

```
 // WebControls
using System;
using System.Collections.Generic;
using System.Data;
using System.Web;
using System.Web.UI;
using System.Data.OleDb;
namespace WebControls
{
    public class WebForm1 : System.Web.UI.Page
    {
        protected DataSet memberDS;
        protected void Page_Load(object sender,
                                 System.EventArgs e)
        {
            try
            {
                Calendar1.SelectedDate = DateTime.Today;
            }
        }
```