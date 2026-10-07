
# Data Selection Query with Visual C#.NET

B. This line indicates that your LogIn class is derived from the system class.

C. The constructor of our LogIn class contains a built-in method, **InitializeComponent()**. This method is used to initialize new instances and variables in this form. Starting Visual C# 2008, this method is moved to the **Login.Designer.cs**.

D. The **LogIn_Load()** is the first method to be executed when this LogLogIn runs. All original code inside this method have been removed since we do not need them.

E. Our Login Button's click contains two arguments: the sender indicates the current object that triggers this method, and the second argument contains the additional information for this event.

F. As this is triggered and executed, we first need to create an instance of our next form window, **SelectionForm.**

G. Before we fill the DataSet, we need to clean up that in the DataSet. As we mentioned in Section 5.1.1.1, the DataSet is a table holder and contains multiple data tables. These tables are only mappings to show real data in the database. All data can be loaded into these tables by the DataSet using the TableAdapter when the project runs. Here a property ClearFill, which belongs to the TableAdapter, is set to True to perform this cleaning job for that mapped Login table in the DataSet.

H. Now we need to call the FillByUsernamePassword method we created in Section 5.5. Because we have bound two textbox controls on the Login form, **txtUsername** and **txtPassword**, with two columns in the Login table in the DataSet, **user_name** and **pass_word**, by using the **loginBindings**, so these two filled columns in the Login data table will also be reflected when this **FillByUsernamePassword** method is executed. This method has three arguments; the first is the data in the table, the second is the Login table that is held by the DataSet, **CSE_DataSets**. The following two are dynamic parameters that were temporarily replaced by two question marks "?" when we built this method in Section 5.5. Now we can use two parameters, **usernameText** and **passwordText**, extracted from the user, to complete these two parameters in order to complete dynamically.

I. If no username and password can be found from the Login table in the base, the **FillByUsernamePassword** method cannot be executed to fill the Login table in the DataSet. This can be detected by checking the Count property of the Login table in the DataSet. The Count property represents the number of rows that have successfully filled into the Login table in the DataSet. A zero value means that no matched username and password has been found and this failed. A warning message is displayed if this happened and some cleaning jobs are performed for two textboxes in the Login. By checking this property, we will know if this Fill is successful or not, or if a matched username and password have been found from the database.

J. Otherwise, if a matched username and password is found from the Login table in the database and the login process is successful, the current window or the LoginForm should be hidden by calling the **Hide()**, and the next form, **SelectionForm**, will be displayed to users to continue to the next step. After displaying the next form, the current Login form should be closed. The keyword this represents the current form.

K. The code for the **Cancel** button click is very simple. The **Application.Exit()** should be called to terminate your project if this is clicked by the user. Double-click on the Cancel button from the LoginForm Designer to open this method, and enter this coding line.

Before we test this piece of code to running the project, make sure that the LoginForm has been selected as the Startup form. To confirm this, double-click the **Program.cs** folder from the Solution explorer to use the **Main()** method. Make sure that the argument of the **Application.Run() method is new LoginForm(). This means that a new instance of LoginForm class is created and displayed as the Run() method is executed.**

# 212 SQL Server Database Programming with C#

![](img/d59a47501d0a20fc0460a49c469c6fb7_240_0.png)

FIGURE 5.43 The running status of the project.

![](img/d59a47501d0a20fc0460a49c469c6fb7_240_1.png)

FIGURE 5.44 The warning message.

Click the Start button to run the project and the Login form is shown up in Figure 5.43.

Enter a valid username henry to the User Name textbox, and enter a password test to the Pass Word textbox, then click the Login button. FillUserNamePassword() will be called to fill the Login table in the database. Because we entered a correct username and password, the fill will be successful and the next form, SelectionForm, will be displayed to users to perform the next action. Now run the project again and try to enter an wrong username or password. To do this process, a MessageBox will be displayed, as shown in Figure 5.44, to indicate this situation.

In this section, we use the Login form and Table to show how to perform a dynamic data query and fill a mapped data in the DataSet using the Visual design tools and wizards. The coding process is simple and easy to follow up. In the next section, we will show how to use another method provided by the TableAdapter to pick a single value from the database.

# 5.8 USE A SINGLE VALUE TO QUERY DATA FOR LOGIN FORM

Many people have experienced forgetting either the username or password when they try to login to a specified website to get some information, to order merchandise or pay bills for their monthly utilities or cell phones. In this section, we show how to use a method to retrieve a single data value from the database. This method belongs to the TableAdapter class.

We still use the Login form and Login table as an example. Suppose you forget your password, but you want to login to this project by using the Login form with your username. By using this example, you can retrieve your password by using your username.

# Data Selection Query with C#.NET

The DataSet Designer allows us to edit the structure of the DataSet. As we discussed in Section 5.1.2,3, by using this Designer, you can configure an existing query, add a new query, and add a new column with a new key to database. The Add method allows us to add a new query with a SQL SELECT statement which returns a single value from the Solution.

Open the Login form from the Solution explorer and open the Data Source window. Right-click on any place in that window and select the Edit DataSet with Designer. Next click the Login table and right-click on the last line of that, which contains our modified Filter:LoginUsernamePassword; which we built in the last section. Then Add Query to open the Tableadapter Configuration Wizard.

On the opened window keep the default selection Use SQL statements, click the Next and choose the SELECT which returns a single value ratio. Click the Next button to go to the next window and click the Query Builder to build your query.

On the opened Query Builder wizard, perform the following operations to complete this single query:

- Click the first row from the second pane to select.
- Right-click on this row and select Delete from the popup to delete this row.
- Go to the top panel and select the pass_word and user_name columns from the Login table by checking the checkboxes related to those columns.
- Go to the second pane and uncheck the checkbox for the user_name column from the Output column since we do not want to use it as the output, but instead we need to use it as a criterion to filter query.
- Still in the second pane, right-click on the Group By and select Delete from the popup to remove this Group By.
- Type a mark '?' on the Filter field in the user_name column, and press the Enter key from your keyboard. Your finished Query Builder should match one that is shown in Figure 5.45.

![](img/d59a47501d0a20fc0460a49c469c6fb7_241_0.png)

FIGURE 5.45 The finished query builder.
