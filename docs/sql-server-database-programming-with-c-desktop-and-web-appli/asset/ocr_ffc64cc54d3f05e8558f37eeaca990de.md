# Accessing Data in ASP.NET

| SQLWebSelectProject | cmdCancel_Click(object sender, EventArgs e) |
|---|---|
| protected void cmdCancel_Click(object sender, EventArgs e) { 
  if(sqlConnection.State == ConnectionState.Open) 
  sqlConnection.Close();
  Response.Write("<script>window.close()</script>");
} | |

**FIGURE 8.11** The codes for the cancel button's click method.

The function of this piece of codes is:

+   *  We first need to check whether the database is still connected to our Web form. If it is, we need to close this connection before we terminate our Web application.
*  The server sends back a command with the Response object's method Write() to issue a Javascript window.close() to the Web application.

One key point to note is using this Cancel button to reset our Web application is that you must reset the **Validation** process of this Cancel button to **false** to skip the validation process to be built in the next section for twoboxes, **txtName** and **txtPassword**. Otherwise, you must go through this validation process by entering a username and a password to process our event when Cancel is clicked.
To reset property, on the open Design of the Login page, select the Cancel button to the Properties window, and select the **false** from the **Validation** property. In this way, you can directly close or terminate our post without going through the validation process.

At this point, we have finished developing the codes for the **Login** Web form. Before we run the project to test our Web page, we need to add some data validation functionalities in the client side to reduce the burden of the server.

# 8.4.3 VALIDATE THE DATA IN THE CLIENT SIDE

As mentioned in Section 8.3.3, in order to reduce the burden of the server, we should make every effort to perform data validation in the client side. In other words, we need to send requests to the server, we need to make sure that our information is sent to the server be as correct as possible. ASP.NET provides some tools to help us complete this data validation. These five validation controls are shown in Figure 8.12.

| Validation Control | Functionality |
|---|---|
| RequiredField | Validate whether the required field has valid data blank |
| RangeValidator | Validate whether a value is within numeric range. The range is defined by the MaximumValue and Minimum properties provided by users |
| CompareValidator | Validate whether a value is given expression using the Different Operator such as 'equal', 'greater', 'less' and the type of the value, which is set by the property |
| CustomValidator | Validate a given expression using a script function. This method provides the maximum flexibility in data validation but one needs to add to the Web page and sends it to the server to get the feedback from it |
| RegularExpression | Validate whether a value fits a regular expression using the ValidationExpression property, which should be provided by the user. |

**FIGURE 8.12** Validation controls.