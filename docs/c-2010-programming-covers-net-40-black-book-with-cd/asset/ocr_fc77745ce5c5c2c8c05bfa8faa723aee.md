# Chapter 16: Login and Web Parts Controls in ASP.NET 4.0

The Login class contains various methods, properties, and events used to work with the Login control. These members enable you to customize Login control, such as displaying customized messages and creating links to change password or recovering a forgotten password. The Login control contains built-in authentication logic; however, you can create your own logic by handling the Authenticate event.

Table 16.1 lists the noteworthy methods of the Login class:

| Table 16.1: Noteworthy Methods of the Login Class | |
|---|---|
| Method name | Description |
| `CreateChildControls` | Creates individual controls of the Login control and associates event handlers with their events |
| `OnAuthenticate` | Raises the Authenticate event to authenticate users |
| `OnLoggedIn` | Raises the LoggedIn event when users log into a website after successful authentication |
| `OnLoggingIn` | Raises the LoggingIn event after users enter login information before authentication takes place |
| `OnLoginError` | Raises the LoginError event when users fail to log in |

Noteworthy properties of the Login class are listed in Table 16.2:

| Table 16.2: Noteworthy Properties of the Login Class | |
|---|---|
| Property | Description |
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