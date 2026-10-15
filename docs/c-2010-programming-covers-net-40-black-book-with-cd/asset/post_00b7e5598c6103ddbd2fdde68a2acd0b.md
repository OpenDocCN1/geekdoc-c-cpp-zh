
- Storing the membership information, such as username, password, e-mail address, and other supporting data
- Authenticating the visitors of the website
- Allowing the user to create and reset passwords
- Creating a unique identification system for authenticated users

The ASP.NET 4.0 login controls are as follows:

- Login
- LoginView
- LoginStatus
- LoginName
- CreateUserWizard
- PasswordRecovery
- ChangePassword

You can find these controls under the Login tab of the Toolbox, as shown in Figure 16.1:

![](img/e073a4882197be4ab61103cbe0bcb394_782_0.png)

**Figure 16.1: The Login Controls Displayed in the Toolbox**

### The Login Control

The Login control provides a user interface, which authenticates users and grants them access to the desired services or resources on the basis of the credentials, such as user name and password, filled in by them. As it can restrict the access to other Web pages, the Login control is generally placed in the Home page of a website.

The Login control is provided by the Login class. The following code snippet shows the class hierarchy of the Login class:

```
System.Object
    System.Web.UI.Control
        System.Web.UI.WebControls.WebControl
            System.Web.UI.WebControls.CompositeControl
                System.Web.UI.WebControls.Login
```

## Chapter 16: Login and Web Parts Controls in ASP.NET 4.0

The Login class contains various methods, properties, and events used to work with the Login control. These members enable you to customize Login control, such as displaying customized messages and creating links to change password or recovering a forgotten password. The Login control contains built-in authentication logic; however, you can create your own logic by handling the Authenticate event.

Table 16.1 lists the noteworthy methods of the Login class:

| Method name | Description |
|---|---|
| `CreateChildControls` | Creates individual controls of the Login control and associates event handlers with their events |
| `OnAuthenticate` | Raises the Authenticate event to authenticate users |
| `OnLoggedIn` | Raises the LoggedIn event when users log into a website after successful authentication |
| `OnLoggingIn` | Raises the LoggingIn event after users enter login information before authentication takes place |
| `OnLoginError` | Raises the LoginError event when users fail to log in |

Noteworthy properties of the Login class are listed in Table 16.2:

| Property | Description |
|---|---|
| `BorderPadding` | Retrieves or specifies the padding of borders of the Login control. |
| `CheckBoxStyle` | Retrieves the reference of the Style object to define the display settings of the Remember Me check box. |
| `CreateUserIconUrl` | Retrieves the location of an image to display the link for new users for registration. |
| `CreateUserText` | Retrieves or specifies the text of a link to a registration page for new users. |
| `CreateUserUrl` | Retrieves or specifies the URL of the new user registration page. |
| `DestinationPageUrl` | Retrieves or specifies the URL of the page displayed to the user when a login attempt is successful. |
| `DisplayRememberMe` | Retrieves or specifies the value that indicates whether or not to display the Remember Me check box. |
| `FailureAction` | Retrieves or specifies the action that occurs when a login attempt fails. |
| `FailureText` | Retrieves or specifies the text displayed when a login attempt fails. |
| `FailureTextStyle` | Retrieves the reference of style properties to define the look of the failure text. |
| `HelpPageIconUrl` | Retrieves the location of an image to display the link to the login help page. |
| `HelpPageText` | Retrieves or specifies the text of a link to the login help page. |
| `HelpPageUrl` | Retrieves or specifies the URL of the login help page. |
| `HyperLinkStyle` | Retrieves a collection of properties to define the look of hyperlinks in Login control. |
| `InstructionText` | Retrieves or specifies the login instruction text for users. |
| `InstructionTextStyle` | Retrieves a reference of the TableItemStyle object to define the style of the instruction text. |
| `LayoutTemplate` | Retrieves or specifies the template to display Login control. |
| `LoginButtonImageUrl` | Retrieves or specifies the URL of an image to use as the Login button. |

![](img/e073a4882197be4ab61103cbe0bcb394_785_0.png)

### The LoginView Control

The LoginView control is a Web server control, which is used to display two different views of a Web page of any website, depending on whether the user has logged on to a Web page as a registered user or a visitor. The LoginView control provides a way of altering the look of the page or showing different content to different groups of users. This control has the built-in functionality to gather the current user’s status and roles. If the user is authenticated, the control displays the appropriate information to the user with the help of the following view templates:

- AnonymousTemplate – Displayed when the user is not logged in
- LoggedInTemplate – Displayed when the user is logged in
- RoleGroups – Displayed when the user, who has logged in, is a member of a specific role with defined role-group templates

The LoginView control is provided by the LoginView class. The following code snippet shows the class hierarchy of the LoginView class:

```
System.Object
  System.Web.UI.Control
    System.Web.UI.WebControls.LoginView
```

The LoginView class contains various methods, properties, and events used to work with the LoginView control.

Table 16.4 lists the noteworthy methods of the LoginView class:

| Method | Description |
|---|---|
| DataBind | Binds a data source to the LoginView control and all its child controls |
| Focus | Specifies input focus to the LoginView control |
| OnViewChanged | Raises the ViewChanged event after the LoginView control changes its view |
| OnViewChanging | Raises the ViewChanging event before the LoginView control changes its view |

### The LoginName Control

The LoginName control is responsible for displaying the names of all the authenticated users. It uses the Page.User.Identity.Name namespace to return the value for the user's name. If no user is logged in, then this control is not displayed on the page. The LoginName control is provided by the LoginName class.

The following code snippet shows the class hierarchy of the LoginName class:

```
System.Object
  System.Web.UI.Control
    System.Web.UI.WebControls.WebControl
      System.Web.UI.WebControls.LoginName
```

The LoginName class does not contain any method, property, or event that is not inherited from any other class, such as the Control class. The only non-inherited property that it contains is FormatString, which is used to display the format item string in the LoginName control. You can simply drag-and-drop this control from the Toolbox to add it on a Web page.

Figure 16.4 displays the LoginName control at design time:

![](img/e073a4882197be4ab61103cbe0bcb394_787_0.png)

Figure 16.4: Displaying the LoginName Control

### The LoginStatus Control

The LoginStatus control specifies whether or not a particular user has logged on to the website. The text displayed on this control changes according to the login status of the user. When the user is not logged in, this control displays the Login text as a hyperlink that facilitates the user in navigating to the login page. To do this, the LoginStatus control uses the authentication section of the web.config file and retrieves the URL of the login page. The LoginStatus control displays the Logout text as hyperlink, when the user is logged on to the website, and deletes the authentication information as soon as the user clicks the Logout link.

The LoginStatus control provides the following two views:

- Logged Out — Displayed when the user is not logged in. This view provides a link to the login page.
- Logged In — Displayed when the user is logged in. This view provides a link to logout of the website.

The LoginStatus control is provided by the LoginStatus class. The following code snippet shows the class hierarchy of the LoginStatus class:

```
System.Object
  System.Web.UI.Control
    System.Web.UI.WebControls.WebControl
      System.Web.UI.WebControls.CompositeControl
        System.Web.UI.WebControls.LoginStatus
```
