Web.config file under the <connectionStrings> element and pointed the SqlDataSource to this connection string. The setting in Web.config looks like this:

```
<connectionStrings>
  <add name="PlanetWroxConnectionString1" connectionString="Data Source=(localdb)\v11.0;AttachDbFilename=|DataDirectory|\PlanetWrox.mdf; Integrated Security=True" providerName="System.Data.SqlClient" />
</connectionStrings>
```

The SqlDataSource then accesses this connection string:

```
<asp:SqlDataSource ID="SqlDataSource1" runat="server" ConnectionString="<%$ ConnectionStrings:PlanetWroxConnectionString1 %>">
```

This code uses expression syntax to refer to the connection string in the Web.config. It asks the Web.config file for the connection string that listens to the name PlanetWroxConnectionString1. It also reads the providerName attribute to figure out how its internal code should talk to the database.

> NOTE In addition to the expression syntax that uses <%$ %> to bind control values to resources like a connection string, you'll also come across similar syntax that uses <%# %>. This is called data-binding expression syntax and it enables you to bind control values to data that comes from data sources like a database. You see more about data-binding expression syntax in this and the next two chapters.

Storing your connection strings in Web.config is considered a very good practice. By centralizing your connection strings you make it much easier to modify them when your database changes (for example, when you switch from a development environment to a production server). Never store your connection strings directly in Code Behind files or in the markup section of the page. You'll seriously regret that day you have to change your connection string and have to wade through all the pages in your site looking for connection strings.

The Express LocalDB edition of SQL Server that you have used so far enables you to work with databases that are attached to SQL Server on the fly when you need them. Take a look at the actual connection string to see how this works:

```
Data Source=(localdb)\v11.0;
AttachDbFilename=|DataDirectory|\PlanetWrox.mdf;
Integrated Security=True;
```

This connection string consists of three parts (which are all on one line in your config file). The value of the first part contains the data source to identify the SQL Server that is targeted, which in this case is a LocalDB instance of SQL Server 2012. Other valid data sources you may come across include . (just a dot, to denote the local machine), .\SqlExpress, to target a named instance version of SQL Server Express running on the local machine (where SqlExpress is the instance name), or something like MachineName or MachineName\InstanceName to target a remote machine or a named instance on a remote machine.