After your database is re-created at your target server, you need to reconfigure your ASP.NET application to use the new database by changing the connection strings in your website. For this to work, you need to modify two connection strings: the PlanetWroxConnectionString1 and the PlanetWroxEntities you created in an earlier chapter. How your connection string must look depends on the database you are using and its configuration. Your hosting company or database administrator typically provides this information. For many examples of proper connection strings, check out www.connectionstrings.com. The following snippet provides a simple example that reconfigures your application to use a database server called DatabaseServer. This example shows a connection string for a SQL Server that requires you to log in with a username and password (in your configuration file, each connection string should be on a single line):

```
<connectionStrings>
  <add name="PlanetWroxConnectionString1" connectionString="Data Source=DatabaseServer;Initial Catalog=PlanetWrox;User Id=YourUserName; Password=YourPassword;" providerName="System.Data.SqlClient"/>
  <add name="PlanetWroxEntities" connectionString="metadata=res:///* /App_Code.PlanetWrox.csdl|res:///* /App_Code.PlanetWrox.ssdl|res:///* /App_Code.PlanetWrox.msl;provider=System.Data.SqlClient; provider connection string="Data Source=DatabaseServer; Initial Catalog=PlanetWrox;User Id=YourUserName;Password=YourPassword; MultipleActiveResultSets=True"" providerName="System.Data.EntityClient"/>
</connectionStrings>
```

This points both connection strings for the PlanetWrox database to a different SQL Server. Consult Appendix B for more information about configuring your ASP.NET application and SQL Server to operate with each other. Don’t forget to add the same code to your deployment .config file in Visual Studio so the next time you publish the site the target Web.config has the correct settings.

At this stage, you’re pretty much done configuring your newly created website. Congratulations! However, before you relax and start enjoying your new website, read the following checklist that helps you secure your site and improve its performance.

# THE DEPLOYMENT CHECKLIST

Instead of ending this chapter with general tips about deployment, this section gives you a practical list of things to check when you’re ready to put your website in production:

+   > Make sure you don’t have debugging enabled in the Web.config file. This causes unnecessary overhead and decreases performance of your website, because code executes slower and important files cannot be cached by the browser. To ensure debugging is disabled, open the Web.config file you are using for your production environment, and verify that debug is set to false:

```
<compilation debug="false">
```