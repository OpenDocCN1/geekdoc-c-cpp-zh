and edit modes. By setting the DefaultMode to Insert, you force the control to switch to insert mode, which means you automatically get a UI for entering details for the genre, and Insert and Cancel links. The DetailsView control is actually pretty smart. When you point it to the SqlDataSource control, it is able to figure out the DataKeyNames property, which it set to Id:

```
<asp:DetailsView ID="DetailsView1" runat="server" AutoGenerateRows="False"
    DataKeyNames="Id" DataSourceID="SqlDataSource1" ...
```

It also understands that the Id column is an identity column in the database, and therefore hides it in the Insert screen (shown in Figure 13-6) by setting InsertVisible to False. Because the database generates this ID automatically, there is no point in letting the user enter a value for it.

When you enter some values and click the Insert link, a process similar to updating with the GridView takes place. The DetailsView collects the relevant information from the page's controls (the Name and the SortOrder) and forwards them to the SqlDataSource. This control in turn pushes the new values in the parameters for the INSERT statement and then sends the command off to the database, which inserts the new row in the Genre table. If you click the Insert link without entering a name or sort order, you'll get an error. In this and later chapters you see how to modify the data-bound controls to include validation functionality.

When you dropped the Genre table on the Genres.aspx page earlier in this chapter, VS not only created a bunch of controls for you, but it also stored information about the database in your Web.config file. The next section explains how this works and why it is important.

# Storing Your Connection Strings in Web.config

The first time you dropped the Genre table on your page, VS created a SqlDataSource control for you. To tell this control what database to access, VS also created a connection string in the Web.config file under the <connectionStrings> element and pointed the SqlDataSource to this connection string. The setting in Web.config looks like this:

```
<connectionStrings>
    <add name="PlanetWroxConnectionString1" connectionString="Data Source=(localdb)\v11.0;AttachDbFilename=|DataDirectory|\PlanetWrox.mdf;
        Integrated Security=True"
        providerName="System.Data.SqlClient" />
</connectionStrings>
```

The SqlDataSource then accesses this connection string as follows:

```
<asp:SqlDataSource ID="SqlDataSource1" runat="server"
    ConnectionString="<%$ ConnectionStrings:PlanetWroxConnectionString1 %>"
```

This code uses expression syntax to refer to the connection string in the Web.config. It asks the Web.config file for the connection string that listens to the name PlanetWroxConnectionString1. It also reads the providerName attribute to figure out how its internal code should talk to the database.