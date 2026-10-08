2. Right-click on the new App_Code folder in the Solution Explorer and select Add New Item in the context menu that appears. A template selection dialog box will appear.

3. Select "LINQ to SQL Classes for Visual C#" under Installed Templates.

4. Enter the name for the database model, RetroGames.dbml, and click Add. The IDE will display the Object Relational Designer (O/R Designer) for App_Code/RetroGames.dbml.

5. Go to Server Explorer. Expand the database file node under Data Connections and then the Tables node. Drag the Game to the O/R Designer's left panel. It will appear as an entity with the same name, as shown in Figure 17-5.

![](bbox=[0.096, 0.303, 0.686, 0.513])

FIGURE 17-5: Entity appearing in O/R Designer

After the aforementioned steps, the App_Code/Retrogames.dbml in the Solution Explorer will contain two files:

+   - RetroGames.dbml
- RetroGames.designer.cs

The RetroGames.designer.cs file contains definitions for the RetroGamesDataContext class, an implementation of System.Linq.DataContext that represents the database:

```
[global::System.Linq.Mapping.DatabaseAttribute(Name="RetroGames")
public partial class RetroGamesDataContext : System.Linq.DataContext
```

Its parameterless constructor reads the connection string from the Web.config XML configuration file:

```
public RetroGamesDataContext() :
    base(global::System.Configuration.ConfigurationManager.ConnectionStrings
    "RetroGamesConnectionString\].ConnectionString, mappingSource)

{
    OnCreated();
}
```