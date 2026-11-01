```
integrated security=True;User Instance=True;
MultipleActiveResultSets=True;App="EntityFramework&..."
providerName="System.Data.EntityClient" />
</connectionStrings>
```

10. To check if the site works, open a browser and go to http://localhost. You should see the Planet Wrox website appear. To verify that everything is in order, browse through the site by requesting pages from the main menu, filling in the contact form, creating a new album, uploading pictures, and so on. If you get an error, refer to the section "Troubleshooting Web Server Errors."

> NOTE If you still can't make it work, try configuring the filesystem for the Everyone group. Although, from a security point of view, this is absolutely not the recommended group to use in a production environment, it may help you in finding out whether it's a security issue. If it works for the Everyone account, it's indeed security-related, so you need to make sure you configured the correct accounts. Don't forget to remove the Everyone account later again. If you keep having problems, refer to the next section where you find a number of problems you may run into while deploying as well as a solution.

# How It Works

On a standard Windows system, all files and folders are protected using Windows NTFS. To ensure proper operation of your website, you need to grant the account used by the web server the necessary permissions to the files and folders of your website. For most files and folders, Read permission is enough. However, for a few folders you need to change the permissions. Both App_Data and GigPics are written to at run time so you need to grant Modify permissions to these folders. In addition, you need to configure C:\TempMail if your site drops e-mails there locally.

In order for your site to connect to a database, you changed both connection strings in Web.config to target an instance of SQL Server called SqlExpress. The Local DB Edition you used before is great for local development, but not for running your production sites. Instead, you can use SQL Server Express Edition or one of the commercial versions of SQL Server. Appendix B digs much deeper into configuring your site to work with versions of SQL Server other than Express.

# Troubleshooting Web Server Errors

When you try to access your site in a web browser, you may run into a number of problems. The first thing you need to do to get helpful error messages is to change the <customErrors> section in Web.config from On to Off or RemoteOnly. This makes it easier to see what's going on. Additionally, you may want to check out the Windows Event Viewer (type eventvwr from the Start menu or Start screen) for more details about errors and hints how to solve them.

This section lists the most common problems and provides a fix for them. You should realize a large number of possible reasons exist for the errors you may get, so it's impossible to cover them all here. If you run into a problem you can't solve, turn to this book's forum at the Wrox community site at