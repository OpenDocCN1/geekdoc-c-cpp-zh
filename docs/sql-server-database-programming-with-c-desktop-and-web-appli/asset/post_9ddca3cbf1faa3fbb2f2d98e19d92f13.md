
# Accessing Data in ASP.NET

| SQLWebSelectProject | cmdCancel_Click(object sender, EventArgs e) |
|---|---|
| protected void cmdCancel_Click(object sender, EventArgs e) { \n  if(sqlConnection.State == ConnectionState.Open) \n  sqlConnection.Close();\n  Response.Write("<script>window.close()</script>\");\n} } | |

**FIGURE 8.11** The codes for the cancel button's click method.

The function of this piece of codes is:

- We first need to check whether the database is still connected to our Web form. If it is, we need to close this connection before we terminate our Web application.
- The server sends back a command with the Response object's method Write() to issue a Javascript window.close() to the Web application.

One key point to note is using this Cancel button to reset our Web application is that you must reset the **Validation** process of this Cancel button to **false** to skip the validation process to be built in the next section for two textboxes, **txtName** and **txtPassword**. Otherwise, you must go through this validation process by entering a username and a password to process our event when Cancel is clicked.

To reset property, on the open Design of the Login page, select the Cancel button to the Properties window, and select the **false** from the **Validation** property. In this way, you can directly close or terminate our post without going through the validation process.

At this point, we have finished developing the codes for the **Login** Web form. Before we run the project to test our Web page, we need to add some data validation functionalities in the client side to reduce the burden of the server.

## 8.4.3 VALIDATE THE DATA IN THE CLIENT SIDE

As mentioned in Section 8.3.3, in order to reduce the burden of the server, we should make every effort to perform data validation in the client side. In other words, we need to send requests to the server, we need to make sure that our information is sent to the server be as correct as possible. ASP.NET provides some tools to help us complete this data validation. These five validation controls are shown in Figure 8.12.

| Validation Control | Functionality |
|---|---|
| RequiredField | Validate whether the required field has valid data blank |
| RangeValidator | Validate whether a value is within numeric range. The range is defined by the MaximumValue and Minimum properties provided by users |
| CompareValidator | Validate whether a value is given expression using the Different Operator such as 'equal', 'greater', 'less' and the type of the value, which is set by the property |
| CustomValidator | Validate a given expression using a script function. This method provides the maximum flexibility in data validation but one needs to add to the Web page and sends it to the server to get the feedback from it |
| RegularExpression | Validate whether a value fits a regular expression using the ValidationExpression property, which should be provided by the user. |

**FIGURE 8.12** Validation controls.

# 426 SQL Server Database Programming with C#

All of these five controls are located at the Validation tab in the Toolbox window in Visual Studio.

Here we want to use the first control, RequiredFieldValidator, to validate our two textboxes, txtUsername and txtPassword in the page to make sure that both of them are not empty when the Login button is clicked by the user as project runs.

Open the Design of the Login Web form, go to the Toolbox window and click the Validation tab to expand it. Drag the RequiredFieldValidator control from the Toolbox and place next to the username text. Set the following properties for this control in the property window:

| ErrorMessage: UserName Required |
| ControlToValidate: txtUsername |

Perform the similar dragging and placing operations to the second RequiredFieldValidator next to the password text. Set the following properties for this control in the property window:

| ErrorMessage: PassWord is Required |
| ControlToValidate: txtPassword |

Your finished Login Web form should match what is shown in Figure 8.13.
Now run our project to test this data validation by clicking the IIS Express button, without entering any data into two textboxes, and then click the Login button. Immediately, two error messages, which are created by the RequiredFieldValidators, are displayed to ask users to enter these two pieces of information. After entering the username and password, click the Login again, a successful

![](img/d59a47501d0a20fc0460a49c469c6fb7_454_0.png)

# Accessing Data in ASP.NET

login message is displayed. So you can see how the RequiredFieldValidator works to reduce the processing load for the server.

When we run our Web application project we do not specify or select a Web browser, instead we just used the default browser. Google Chrome. However, to effectively run and execute our Web applications built in this chapter we should use our desired Web browser, Internet Explorer. The reason for that is because this kind of browser contained more powerful tools and classical components to meet the functions and requirements for our applications.

## 8.4.4 SELECT A DESIRED BROWSER TO EFFECTIVELY RUN OUR WEB APPLICATION PROJECT

To select the Internet Explorer as our Web browser, perform the following operational steps:

- 1. In the opened Visual Studio 2012 and SQLWebSelect Project, click on the drop-down arrow at light the IIS button on the top.
- 2. On the opened sub-menu, click on the Web Browser (Google Chrome) item.
- 3. Select the Internet Explorer by checking it from the sub-menu.

Now the default browser is changed to Internet Explorer attached with the IIS button on the top.

One of the most important features when using this Internet Explorer as our Web browser is to execute some classical Web API functions to effectively run our Web applications to perform our desired functions. For example, to effectively terminate our Web application project, we used a Javascript method, window.close(). This method can be used to effectively stop our Web applications. However, this method can only be worked under the Internet browser but not any other browser.

## 8.4.5 CREATE THE SECOND USER INTERFACE – SELECTION PAGE

Now let's develop our Web application by adding another Web page, the selection. As we did in the previous chapters, after the process is finished, the next step is to allow users to select different functionalities from the Selection form to perform the associated data actions.

The function of this Selection page is to allow users to visit different pages to perform different data actions as inserting, updating or deleting data against the database via the tables by selecting different items. This Selection page needs to perform the following jobs:

- 1) Provide and display all selections to allow users to select them.
- 2) Open the associated page based on the users' selection.

Now let's build this page. To do that, we need to add a New Web page. Right-click our project SQLSelect Project from the Solution explorer and select Add | New Item from the popup menu. On the opened window, select the Web Form as our Template, and edit Selection.aspx as the Name for the new page, and click the Add button to add this page into our project.

On the opened Web form, add the controls show that one is in Figure 8.14 into this page. Your finished Selection page should show the one that is in Figure 8.15.

As mentioned in the last section, before you pick up controls from the Toolbox window and drag them into the page, you must first use the Space or the Enter keys from the keyboard to locate the position for those controls. An exception is that when you set the Position property for all controls to Absolute, then you

Next let's create the codes for this Selection page to allow users to select the different page to perform the associated data actions.

# SQL Server Database Programming with C#

| Type | ID | Text | TabIndex | BackColor | Font |
|---|---|---|---|---|---|
| Label | Label1 | Make Your Selection: | 0 | #E0E0E0 | Bold/Large |
| DropDown | ComboSelection | | 1 | | |
| Button | cmdSelect | Select | 2 | | Bold/Medium |
| Button | cmdExit | Exit | 3 | | Bold/Medium |

**FIGURE 8.14** Controls for the selection method may move any of the controls to any location.

![](img/d59a47501d0a20fc0460a49c469c6fb7_456_0.png)

**FIGURE 8.15** The finished selection page.

### 8.4.6 Develop The Codes for the Selection Page to Open The Other Page

First let's run the Selection page to build the Web configuration file. Click on the **IIS** express to run this page, and then click the **Close** button that is located on the upper-right corner of the page to close it.

Right-click on the **Selection.aspx** from the Solution Explorer and click on the **View Code** item to open the code page for the Selection Web form. First let's add a SQL Data-related namespaces on the top of this page to provide a reference to all components of the SQL Data Provider:

```
using System.Data;
using System.Data.SqlClient;
```

Then enter the codes that shown in Figure 8.16 into the **Page_load()** method to add all selection items into the combobox **ComboSelection** to allow users to make their selection as the project.

The function of this piece of coding is straightforward. Three pieces of CSE dept information are added into the combobox **ComboSelection** using the **Add()** method, and these pieces of information will be selected by the user as the project results.

Next we need to create the codes for two buttons "Select". First let's do the coding for the **Select** button. Right-click on the **Selection.aspx** from the Solution Explorer window and click on the **View Designer** item to open the Selection Web form, and then Double-click the **Select** button to open its method. Enter the codes that are shown in Figure 8.17 into this method.

The function of this piece of coding is easy. Based on the information selected by the user, the related Web page is opened using the server's **Response** object, precisely by using the **Redirect()** method of the server's **Response** object. All of these three pages will be created and discussed in the following sections.
