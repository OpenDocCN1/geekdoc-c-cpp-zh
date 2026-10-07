# 554 SQL Server Database Programming with C#

![](bbox=[0.177, 0.085, 0.822, 0.381])

FIGURE 9.40 The modified designer view of the Faculty.aspx page.

# 9.3.11.3 Modify the Codes in the Page_Load Event Method

Perform the following changes to complete this modification:

+   1) Rename the namespace using System.Data.SqlClient; from the top of this page since we do not need it in this application.
2) Remove the entry if block and the associated global connection object is stored in the Application state function Application["SqlConnection";
3) Add codes to display three Methods in the combobox control ComboMethod by using the system method Add().
4) Setup the first item as a default for both combobox controls.

Your finished codes for the Page_Load() method should match one that is shown in Figure 9.41. The new added codes will be highlighted in bold.

The next modification is to change the codes inside the Select Button's click method.

# 9.3.11.4 Modify the Codes in the Select Button Click Method

Replace all codes in this method with the following coding sequences:

A. First let's create three new instances:

+   1. wsSQLSelect for the proxy class of the Web Service
2. wsSQLResult for the class of our Web Service and wsSQLResult,
3. wsDataSet for our DataSet class

The coding for the first two objects, `wsSQLSelect` and `wsSQLResult`, can be represented by two lines, not four. But in order to make these lines shorter, we separate them in order to make these lines shorter, we separate them with the declaration and assignment in two lines. For that long lines because the proxy class is added into our current project; thus, our current project, which works as a namespace, must be prefixed for proxy class to enable to know and use it.

B. Create a local DataSet object wsDataSet and a string variable errMsg. The former is used to work as a DataSet and the latter is used to only show possible error message.

C. If the user uses the Object Method, a try...catch block is used to catch the first Web method GetSQLSelect() that we developed in our Web Service project with the faculty name