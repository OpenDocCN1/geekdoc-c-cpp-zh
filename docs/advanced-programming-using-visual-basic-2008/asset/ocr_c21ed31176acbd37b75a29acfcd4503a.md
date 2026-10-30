# Adding Login Controls to an Application

You can add the login controls by simply dragging and dropping them on a form. You may want your login form on the home page or you may want to have it on a separate page. It is common to have the password recovery and change password available through a link. You will be able to control access to pages best if you have the login forms and public pages in the root directory of the Web site and maintain the member-only pages in a separate folder.

# Using the Web Site Administration Tool

To set up user logins, you must use the ASP.NET Web Site Administration Tool (Figure 7.42). The Administration Tool is accessible from the Website / ASP .NET Configuration menu item, from the icon at the top of the Solution Explorer window, or from the smart tag of any login control.

![](bbox=[0.108, 0.437, 0.948, 0.716])

Use the Web Site Administration Tool to set up user login. Click the How do I use this tool? link in the upper-right corner for detailed instructions on using the tool.

You will use the Security tab of the Administration Tool (Figure 7.43), which allows you to create and manage users, manage roles, and establish access rules. The Roles feature enables you to add groups (roles) that you can use to assign access privileges for groups of users. Access Rules determine which users or roles have access to individual folders.

You can create your first user from the Security tab if you wish, or you can add users from the CreateUserWizard control that you added to a Web page. Note that the information for the users is stored in a Microsoft SQL Server Express database by default. You can set a different database provider using the Provider tab of the Administration Tool.