
# Access Data in ASP.NET

| SQLWebSelect Project | Page_Load(object sender, EventArgs e) |
| :--- | :--- |
| using System.Data;using System.Data.SqlClient;namespace SQLWebSelectProject { public partial class Selection : System.Web.UI.Page { protected void Page_Load(object sender, EventArgs e) { ComboSelection.Items.Add("Faculty Information"); ComboSelection.Items.Add("Course Information"); ComboSelection.Items.Add("Student Information"); } } | | |

FIGURE 8.16 The coding for the Page_Load() method of the selection page.

| SQLWebSelect Project | cmdSelect_Click(object sender, EventArgs e) |
| :--- | :--- |
| protected void cmdSelect_Click(object sender, EventArgs e) { if (ComboSelection.Text == "Faculty Information") Response.Redirect("Faculty.aspx");else if (ComboSelection.Text == "Student Information") Response.Redirect("Student.aspx");else if (ComboSelection.Text == "Course Information") Response.Redirect("Course.aspx"); } | | |

FIGURE 8.17 The coding for the select button's click.

Finally, let's take care of coding for the Exit click method. The function of this piece of code is to close the database connection and the Web application. Double click the Exit button from the Design View of the Selection page to open this method. Enter the codes that are shown in Figure 8.18 into this method.

Let's have a closer look at this piece of codes to see how it works.
First need to check if the database is still connected to our application. If it is, the global connection object stated with the Close() method to close the database connection. Then the Write() method of the server Response object is called to close the Web application. A key point is that the Application function stores an object, the connection object in this case. In order to access and use that object stored in the Application global function, a casting SqlConnection must be clearly prefixed before that; therefore, a two-layer parenthesis

| SQLWebSelect Project | cmdExit_Click(object sender |

FIGURE 8.18 The coding for the exit button's click method.

![](img/d59a47501d0a20fc0460a49c469c6fb7_458_0.png)

FIGURE 8.19 The running status of the second page – selection page.

otherwise a compiling error will be encountered since the compiler cannot recognize and convert the general object stored in the Application state function to a specific Connection object.

We have now finished coding for the Selection page. Before we can run the project to test this page, we need to do some modifications to the codes in the Login button's Click method in the Login page to allow the application to switch from the Login page to the Selection page as the Login process is successful.

Open the Login and the Login button's Click method, replace the body code that is inside if(sqlReader.HasRows == true) block under the sqlReader.Close();

``````
Response.Write('<script>alert('Login is successful!')</script>');
```

with the following:

```
Response.Redirect("Selection.aspx");
```

In this way, as long as the login process is successful, the next page, the Selection page, will be opened by executing the Redirect method of the Response object. The argument of this method is the URL address of the page. Since the Selection page is located at the same application as the Login page does, a direct page name is used.

Now let's run the application to test two pages. Make sure the Login page is the starting page for our application. To do that, right click the Login.aspx from the Solution explorer and select the item Set As Start Page from the popup menu. Click the IIS Express button to run our project. Enter the suitable username and password as yobai and come, then click the Login button. The Selection page is displayed if the login process is successful, as shown in Figure 8.19.

Click on the Exit button to close our application. Now let's develop our next page, Faculty page.

## 8.4.7 CREATE THE THIRD INTERFACE – FACULTY PAGE

Right-click the project folder SQLSelectProject from the Solution explorer and select the Add | New Item from the popup menu. On the opened window, select the Template Web Form and then enter Faculty.aspx in the Name box as the new name for this page, and click Add button to add this new page into our project.

On the opened Web form, all the controls that are shown in Figure 8.20 into this page. As mentioned in the last section, you can drag controls from the Toolbox window and place them into the page, you must first use the Space or the Enter keys from the keyboard

## Accessing Data in ASP.NET

| Type | ID | Text | HorizontalAlign | BackColor | Font |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Label | Label1 | CSE DEPT Faculty Page | | #E0E0E0 | Bold/Large |
| FileUpload | FileUploadImage | | | | |
| Label | Label3 | Faculty Name | | | Bold/Small |
| DropDownList | ComboName | | | | Bold/Small |
| Image | PhotoBox | | | | |
| Panel | Panel1 | | Right | #FFFFCC | |
| Label | Label4 | Faculty ID | | | Bold/Small |
| TextBox | txtFacultyID | | | | |
| Label | Label5 | Name | | | Bold/Small |
| TextBox | txtName | | | | Bold/Small |
| TextBox | txtTitle | | | | |
| Label | Label7 | Office | | | Bold/Small |
| TextBox | txtOffice | | | | |
| Label | txt8 | Phone | | | Bold/Small |
| TextBox | txtPhone | | | | |
| Label | Label9 | College | | | Bold/Small |
| TextBox | txtCollege | | | | |
| Label | Label10 | Email | | | Bold/Small |
| TextBox | txtEmail | | | | |
| Button | cmdSelect | Select | | | Bold/Small |
| Button | cmdInsert | Insert | | | |
| Button | cmdUpdate | Update | | | Bold/Small |
| Button | cmdDelete | Delete | | | |
| Button | cmdBack | Back | | | Bold/Small |

FIGURE 2.20 Controls for the faculty form.

to locate the position on page for controls. However, if you want to add and place controls onto the Web Form at any random location as you did with the Forms object, you need to set the Position property of each control to the Absolute value (refer to Section 8.4.1 to get more details for this issue).

When building this Faculty Web Page, the following points should be kept in mind:

- 1) The first important point to be noted is the position of the Image control on the page form. After drag and place the Image control into page, go to the Properties window and set the ImageAlign property to left.
- 2) The second important point is position style of this Web Form. Click on any place in this page and go to the Properties window. Select the Style property and click on the expansion button to open the Modify Style wizard. Click on the Position item from the left panel and select the absolute item from the position: combobox in the right pane.
- 3) The third important point is the horizontal alignment property for the Panel. This panel works as a container and all text boxes added to this panel should be aligned to the right to make them correct. To set this up, select the Panel and go to Properties window, and set the HorizontalAlignment to Right in its Properties window.
- 4) The fourth point is font size and style for all labels' captions. For example, for the Label1, its caption is CSE DEPT Faculty Page. To set its style and size, by clicking on it and go to the Format menu item and select the lower Font item from the sub-menu to set its style as Arial Black and size as medium (14 pt), and click on the OK button.
- 5) For all other labels, set its caption's style as Arial Black and size as small (12 pt).

Now you can enlarge this image and place it in the left side of this Web page. Your finished Faculty page should match one that is shown in Figure 8.21.

![](img/d59a47501d0a20fc0460a49c469c6fb7_460_0.png)

**FIGURE 8.21** The finished page.

Another easy way to build this Faculty page is to add an existing Faculty page Faculty.aspx that can be found from the folder Web Forms under the Students folder in the CRC Fpt site (refer to Figure 1.2 in Chapter 1). Performing the operations to add this existing Faculty page into your project:

- 1- Right-click on our project SQLSelectProject from the Solution explorer, and select the Add | Existing Item.
- 2- Browse to the folder StudentsWeb Forms on the CRC Fpt site and select three items, Faculty.aspx, Faculty.aspx.designer.cs and Faculty.aspx.cs. Then click the Add button to add them into your project. You can also download and save these pages into a temporary folder in your computer and perform this adding action.

## 8.4.8 Develop the Codes to Select the Desired Faculty Information

First let's run the project to build the configuration Web.config to configure all controls we just added into the Faculty page. Click on the IIS Express button to run the project, enter the suitable username and password to open the Selection page. Select the Faculty Information item from this page to open the Faculty page. Click on the Close button that is located at the upper-right corner of this page to close the project.
