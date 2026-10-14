
## The CreateUserWizard control with the smart tag menu shown

![](img/c024ccf88e28c30c07dd410d4342288f_668_0.png)

## The two steps of a customized CreateUserWizard control in a browser

![](img/c024ccf88e28c30c07dd410d4342288f_668_1.png)

### Description

- If you select the CreateUserWizard control in the Web Forms Designer, you can use the smart tag menu to switch between its two steps and customize or reset either step.
- To identify the page that the user is directed to when the Continue button in the Complete step is clicked, you can set the ContinueDestinationPageUrl property of the control. Or, if you’ve customized the Complete step, you can set the PostBackUrl property of the Continue button.

Figure 19-11 How to use the CreateUserWizard control

## How to use the PasswordRecovery control

It’s inevitable that some users will forget their passwords. Fortunately, the PasswordRecovery control makes it easy to automate the process of recovering forgotten passwords. This process is described in figure 19-12, and it’s especially useful if you are managing a site with a large number of users.

When you use the PasswordRecovery control, the password is sent to the user via email. As a result, you need to make sure that your system is set up so it can send email before you test this control. By default, an application will try to send email to an SMTP server set to localhost on port 25.

The most important element of the PasswordRecovery control is the MailDefinition element. In particular, you must set the From attribute of the MailDefinition element to the email address that’s sending the email message or an error will occur when your system attempts to send the email. Typically, the From email address is set to the email address that’s used by the web site administrator. If you set this attribute correctly, a standard message will be sent to the user. To customize the subject line and message body, you can edit the other attributes of the MailDefinition element.

The PasswordRecovery control uses three views. In the Web Forms Designer, you can switch between these three views by using the smart tag menu, and you can edit the properties for any of these views as necessary.

When you display this control in a browser, the first view asks the user to enter a user name. Then, the second view requires the user to answer the security question. If the answer to this question is correct, the password is emailed to the address that’s associated with the user name, and the third view is displayed. This view displays a message that indicates that the password recovery was successful and that the password has been sent to the user via email.

## The PasswordRecovery control in the Web Forms Designer

![](img/c024ccf88e28c30c07dd410d4342288f_670_0.png)

## The first two views of the PasswordRecovery control

![](img/c024ccf88e28c30c07dd410d4342288f_670_1.png)

### The aspx code for the PasswordRecovery control

```aspx
<asp:PasswordRecovery ID="PasswordRecovery1" runat="server">
    <MailDefinition From="anne@murach.com">
    </MailDefinition>
</asp:PasswordRecovery>
```

### Description

- After the second view is completed, the password is emailed to the user. For this to work, you need to edit the From attribute of the MailDefinition element to supply the from address for this email. In addition, the web server that you’re using must be configured to work with an SMTP server.
- By default, an application will try to send email to an SMTP server set to localhost on port 25. For information on how to change these settings, see chapter 20.

Figure 19-12 How to use the PasswordRecovery control

## The first view of the ChangePassword control in the Web Forms Designer

![](img/c024ccf88e28c30c07dd410d4342288f_672_0.png)

## The second view of the ChangePassword control

![](img/c024ccf88e28c30c07dd410d4342288f_672_1.png)

### The aspx code for the ChangePassword control

```aspx
<asp:ChangePassword ID="ChangePassword1" runat="server"
    CancelDestinationPageUrl="MyAccount.aspx"
    ContinueDestinationPageUrl="MyAccount.aspx">
</asp:ChangePassword>
```

### Description

- The ChangePassword control uses two views to allow users to change their passwords. The first view lets the user change the password. The second view is displayed when the change has been successful.
- The CancelDestinationPageUrl and ContinueDestinationPageUrl attributes provide the URLs that are navigated to when the Cancel or Continue buttons are clicked.

## How to use the LoginView control

If your web site uses authentication, you often need to display one message to users who are logged in and another message to users who aren’t logged in. For example, when a user isn’t logged in, you may want to display a message that asks the user to log in. Conversely, if a user is logged in, you may want to display a message that welcomes the user back and allows the user to log out. Figure 19-14 shows how to use the LoginView control to accomplish these tasks.

The LoginView control uses two views. The first view contains the controls that are displayed to users who aren’t logged in (*anonymous users*). The second view contains the controls that are displayed to users who are logged in (*authenticated users*). In this figure, each view of the LoginView control contains a Label control followed by a LoginStatus control. This is a fairly typical use of the LoginView control. However, the LoginView control can contain additional content if that’s necessary.

## The LoginView control in the Web Forms Designer

![](img/c024ccf88e28c30c07dd410d4342288f_674_0.png)

### The aspx code for the LoginView control

```aspx
<asp:LoginView ID="LoginView1" runat="server">
    <LoggedInTemplate>
        <asp:Label ID="Label2" runat="server"
            Text="You are logged in." Width="155px"></asp:Label><br />
        <asp:LoginStatus ID="LoginStatus2" runat="server" />
    </LoggedInTemplate>
    <AnonymousTemplate>
        <asp:Label ID="Label1" runat="server"
            Text="You are not logged in." Width="175px"></asp:Label><br />
        <asp:LoginStatus ID="LoginStatus1" runat="server" />
    </AnonymousTemplate>
</asp:LoginView>
```

## The LoginView control displayed in a browser

![](img/c024ccf88e28c30c07dd410d4342288f_674_1.png)

### Description

- The LoginView control lets you change what’s on the web page depending on whether the user isn’t logged in (an *anonymous user*) or is logged in (an *authenticated user*).

Figure 19-14 How to use the LoginView control

## The Authentication application

To show how to use forms-based authentication to restrict access to a web application, this topic presents part of a Halloween Store application that we’ll refer to as the Authentication application. This application restricts access to all pages in the Maintenance folder to users with admin privileges. In addition, it restricts access to all pages in the MyAccount folder to users who have created an account and logged in.

As you review this application, please keep in mind that the authentication and authorization features don’t require any code. That’s why the figures that follow show only the pages, the directory structure, the access rules, and the web.config files.

### The pages

Figure 19-15 shows just four pages of the Authentication application, but you can also think of the pages in figures 19-11 through 19-13 as part of this application. For instance, the Forgot Your Password link on the Login page goes to the page in figure 19-12, and the Need to Create a New Account link goes to the page in figure 19-11. Also, the Change Password link on the MyAccount page goes to a ChangePassword page like the one in figure 19-13.

To start this application, the Menu page in figure 19-15 contains three links that allow you to perform some tests to make sure that the authentication and authorization features are working correctly. The first link on this page lets the user access an Order page to begin placing an order. When the user clicks on this link, the system tries to authenticate the user by checking whether the user has a cookie with a valid authentication ticket. If so, the user will be authenticated automatically. If not, the user can view the Order page as an anonymous user. Either way, the Order page will be displayed. In other words, this page is available to both anonymous and authenticated users.

The second link on the Menu page lets the user access the MyAccount page where the user can edit settings for his or her personal account. To be able to access this page, the user must be authenticated. When the user clicks on this link, the system attempts to authenticate the user by checking if the browser has a cookie with a valid authentication ticket. If so, the user will be authenticated automatically and allowed to access the MyAccount page. If not, the user will be redirected to the Login page so he or she can log in. Once the user supplies a valid user name and password to the Login page, the browser will be redirected to the MyAccount page.
