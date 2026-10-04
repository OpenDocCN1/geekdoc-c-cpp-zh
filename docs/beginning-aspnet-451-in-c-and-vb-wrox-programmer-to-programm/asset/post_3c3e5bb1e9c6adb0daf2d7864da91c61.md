
# 596 | CHAPTER 16 SECURITY IN YOUR ASP.NET WEBSITE

![](img/9e033e3b9560597824f8b22941d6d8bb_633_0.png)

FIGURE 16-4

Note that the login status below the Login control is currently set to Login (as a call to action) to indicate you are not logged in. If the text says Logout indent, verify that you set authentication to Forms in the web.config file. Otherwise, Windows authentication is used, which is logs in if you have Windows accounts.

- 12. Try to log in by entering a random username and password. Obviously, this fails because the account doesn't exist. It may take a few seconds before you see the result because ASP.NET is busy setting up the membership database.

- 13. Follow the Sign Up link below the Login control to go to SignUp.aspx and create an account by entering your personal details (see Figure 16-5). By default, the password needs a minimum length of six characters. Note that the password is case sensitive. Write down the username and password you entered, because you'll need this information again later.

![](img/9e033e3b9560597824f8b22941d6d8bb_633_1.png)

FIGURE 16-5

- 14. Click the Create User button to have the account created for you. When the page reloads, you get a confirmation that the account was created successfully. Click the Login item from the main Menu or TreeView (depending on the theme you have selected). You are taken to the Login page again where the LoginStatus control below the Login control now indicates that you are logged in (see Figure 1-6). When you create a new account using CreateUser, you're logged in automatically, although you can change that by setting the LoginCreatedUser property of the table.

- 15. Click Logout and you are logged out, the LoginStatus to display the text Login again. In the Login control, enter your username and password to enter in 13 and click Log In button. You're logged in and redirected to the homepage. On the main Menu or TreeView, click Logout to return to the Login page again. Note that the LoginStatus has changed and now shows Logout again, illustrating the fact that you successfully logged in.

At this stage, being logged in doesn't add much value; all you see is the LoginStatus change from logged-in. However, in this chapter you can see how different content to

## How It Works

Besides adding and configuring an ASP.NET Server Controls, you didn't do any coding in this exercise. Still, you were able to implement a fully login procedure that enables a user to sign up for an account and log in to the site. So how does this work? As you learned, the ASP.NET controls talk to the configured application service providers; a software layer that sits between the login controls and the SQL database that keeps track of the users.

The first time you try to log in (or other login controls that require database), the provider checks if you are using a database with the necessary database objects, such as tables. By default, it checks the database by looking at a connection string pointed to the connectionString attribute of the configuration. If the database from the connection string doesn't exist, or doesn't contain the necessary tables, .NET creates a SQL script to prepare the database for you. Why was there a delay when you entered your username and password in step 12? To find out what the database looks like, go back to VS, expand the App_Data folder, and double-click your PlanetWrox.mdf database. This opens the Server Explorer and shows your database. Expand the Tables node to see which database objects have been added for you, as shown in

After this database has been created successfully, the login controls can use it. For example, when you create a new account using the CreateUserWizard control, records are inserted in the Members and Users tables. Similarly, when you try to log in, your username and password are checked against these.

![](img/9e033e3b9560597824f8b22941d6d8bb_634_0.png)

FIGURE 16-6

![](img/9e033e3b9560597824f8b22941d6d8bb_634_1.png)

FIGURE 16-7

To force the ASP.NET run time to use forms-based authentication (which the configured Membership provider uses under the hood), you need to set the mode attribute of the authentication element to Forms in the Web.config file:

```
<authentication mode="Forms" />
```

Other options for the mode attribute include Windows (where security is handled by Windows itself) and None, which disables security altogether. In the remainder of this book, the Forms option is used exclusively because it's the most common solution for Internet-facing web applications.

The Remember Me Next Time option of the Login control is more forgetful than you may think. When you check this option, you are logged in automatically the next time you visit the site, provided your authentication cookie hasn't expired. The first time you log in, the server sets a cookie that is saved for future sessions. However, this cookie expires after 30 minutes, which means a user returning to the site after that period needs to reauthenticate. To extend the period that users remain logged in, you need to set the timeout attribute of the <forms> element (which itself is a child of <authentication>) in Web.config. The timeout value represents the period in minutes:

```
<authentication mode="Forms">
    <forms timeout="24" />
</authentication>
```

The authentication mechanism of ASP.NET by default assumes you have a page called Login.aspx in the root of your site that is used to let users log in. To be functional, the minimum that this page requires is a Login control. If you want to use a different page, you can specify its path in the <forms /> element under <authentication /> like this:

```
<authentication mode="Forms">
    <forms loginUrl="~/Account/MyLoginPage.aspx" />
</authentication>
```
