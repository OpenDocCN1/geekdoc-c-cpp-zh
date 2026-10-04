
4. Save all your changes and request SignUp.aspx in the browser.

5. Fill in the form, but for both password fields, type something like pass.

6. Click the Create User button. Note that the control now forces you to enter a password with a minimum length of seven characters that contains at least one non-alphanumeric character. It displays an appropriate error message below the control, shown in Figure 16-13. Note that numbers are not considered non-alphanumeric characters, so you need to make sure your password contains at least one character like # $ or \*. For example, PassWord is not a valid password, but Pass##Word will be accepted. Also note that the password is case sensitive.

7. Enter a password of at least seven characters with at least one non-alphanumeric character # or click the Create User button. This time your password is accepted and the account is created.

![](img/9e033e3b9560597824f8b22941d6d8bb_649_0.png)

| Sign Up for Your New Account | |
|---|---|
| User Name | ImarTest |
| Password | |
| Confirm Password | |
| E-mail | imar@spanjaars.com |

FIGURE 16-15

## How It Works

The CreateUser uses the configured Member provider under the hood to validate the data and create the user. The provider in turn consults the Web.config file for the configuration information such as the minimum password length. When you try to create the user, the provider enforces the rules set in Web.config and cancels the user creation process as soon as one of the rules is not fulfilled.

Having the configuration information in Web.config is especially useful when you deploy your application to a different server that uses a different database, because all you need to do is change the settings in this file. Chapter 19 and Appendix B show you to do this.

So far, you have seen how to users sign up for an account so they can log in. But how can you differentiate between the different users in the system? How can you block access to specific folders such as the Management folder for unauthorized users? You do this with the Role Manager, another application service that ships with ASP.NET.

## THE ROLE MANAGER

Although it's nice that users can sign up and log in to your site, it would be a lot more useful if you could differentiate your users. That would enable you to grant access rights to one or a few users to the Management folder so only they can change your reviews and genres. With the Role Manager that ships with ASP.NET, this is pretty easy to do. The Role Manager enables you to assign users to different roles. You can then use these roles to open or block specific functionality in your site. For example, you can block access to the Management folder for all users except for those in the Managers role. Additionally, you can display different content based on roles users have with the LoginView as you saw earlier.

## The Role Manager Configuration

As membership, the settings for the Role Manager are placed in Web.config files. The default settings added by NuGet when you installed the Universal Providers look like this (except for the connection string that you changed):

```
<roleManager defaultProvider="DefaultRoleProvider">
  <providers>
    <add name="DefaultRoleProvider"
      type="System.Web.Providers.DefaultRoleProvider, System.Web.Providers,Version=2.0.0.0, Culture=neutral, PublicKey=31bf356ad364e35"
      connectionString="PlanetWxConnectionString1" />
  </providers>
</roleManager>
```

The Role Manager is not enabled by default, and to enable it, you need to add an enabled="true" attribute to the <roleManager> element. In this exercise, you will see a way to enable the Role Manager through the Web Site Administration Tool (WSAT). Like membership, the Role Manager uses a provider under the hood.

Besides the settings here, the <roleManager /> element also has a few attributes you can configure. Most of them are related to how the cookies with the role information are created and stored. For most cases, the default configuration should be fine, but check out the complete list of configuration settings for the Role Manager on the MSDN website at http://bit.ly/Lmtcb3 if you need to further configure the Role Manager.

With the Membership and Role Manager providers configured and the database created, it's time to manage the users and roles in your system. You have a few ways to accomplish this:

- Using the Web Site Administration Tool, generally referred to as the WSAT Chapter 19
- Using IIS (the Windows web server) on Windows editions (you may see more about this in Chapter 20)
- Programmatically, using the Role Manager API (application programming interface)

Managing roles using the Role Manager API is beyond the scope of this book. If you want to learn more about, get a copy of Wrox's ASP.NET 4,5 in C# and VB (Jason N. Gaylord, Christian Wen, Pranav Rastogi, Todd Miranda, Charles Hanselman; Wiley 2013; ISBN: 978-1-118-31182-0).

The Web Site Administration Tool is used for a lot more than managing roles, and it's great for detail in the next section. It is only available from your local machine and, it's not suitable for managing users in a production environment.

## Managing Users with the WSAT

The WSAT is used for the following tasks:

- Managing users
- Managing roles
- Managing access rules — for example, to determine what user can access which files and folders
- Configuring application, mail, and debug settings
- Taking the site offline so users can't recount any pages and get a friendly error message instead

Some of the changes you make with the WSAT are persisted in the Web.config file for the application. Other settings, like users and roles, are stored in the database for the configured provider.

In the next exercise you will see how to start and use the WSAT. You see how to create a new role and a new user, and how to assign that user to the role.

## TRY OUT Using the WSAT to Manage User Accounts and Roles

To protect your Management folder from users who are not authorized to access it, you need to create a role that is allowed to access this folder. After you have set up this role, you can grant all users in it while keeping all other users out. In this Try Out, you learn how to create the Managers role and assign a user to it. In a later exercise, you will see how to limit access to the Management folder to Managers only.

> NOTE In versions of Visual Studio before VS 2013, Microsoft included a short-cut to the WSAT in the Project menu. However, Microsoft decided to remove that feature.

1. Start a command prompt by typing CMD on the Windows screen and press Enter.
2. Navigate to the folder where IIS is installed (which default is C:\Program Files) by entering the following command:
```
cd c:\Program Files\IIS Express
```
3. Enter the following command and hit enter:
```
iisexpress.exe /path:"C:\Windows\Microsoft.NET\Framework\v4.0.30319\ASP.WebFiles" /port:8082 /clr:4.0 /ntlm
```
Note: You should enter all of this on one line. This command should work on 32- and 64-bit versions of Windows, but check the path to the ASP.WebFiles folder in case you get an error running the command.

When you press Enter, you should see that IIS Express has started, as shown in Figure 16-16.

##

![](img/9e033e3b9560597824f8b22941d6d8bb_652_0.png)

Don't close the command prompt as it will also close IIS.

1. Start your browser and navigate to the following URL:
`http://localhost:8082/asp.webadminfiles/default.aspx?applicationPhysicalPath=C:\BegASPNET\Site`

Again, all of this could be one line without any spaces. Update the path for the applicationPhysicalPath parameter in case you placed your site in a folder other than C:\BegASPNET\Site. When asked for a username and password, enter the credentials you use to log in to your Windows machine. After a short delay, the Site Administration Tool is loaded, shown in Figure 16-17.

![](img/9e033e3b9560597824f8b22941d6d8bb_652_1.png)

- In the top-right corner, you see a Help link that takes you to a help file describing how to use the tool. Click the logo of the application, you see four tabs: Home, Security, Application, and Provider. The Home tab takes you back to the start page in Figure 16-17. You use the Application tab to configure different application settings, and the Provider tab enables you to configure the connection for the application. In this exercise, all that matters is the Security, so go ahead and click it. You will see the screen displayed in Figure 16-18.
