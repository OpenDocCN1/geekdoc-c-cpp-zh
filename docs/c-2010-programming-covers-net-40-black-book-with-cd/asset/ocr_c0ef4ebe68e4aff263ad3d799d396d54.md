![](bbox=[0.25, 0.06, 0.78, 0.42])

# The LoginView Control

The LoginView control is a Web server control, which is used to display two different views of a Web page of any website, depending on whether the user has logged on to a Web page as a registered user or a visitor. The LoginView control provides a way of altering the look of the page or showing different content to different groups of users. This control has the built-in functionality to gather the current user’s status and roles. If the user is authenticated, the control displays the appropriate information to the user with the help of the following view templates:

+   - AnonymousTemplate – Displayed when the user is not logged in
+   - LoggedInTemplate – Displayed when the user is logged in
+   - RoleGroups – Displayed when the user, who has logged in, is a member of a specific role with defined role-group templates

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