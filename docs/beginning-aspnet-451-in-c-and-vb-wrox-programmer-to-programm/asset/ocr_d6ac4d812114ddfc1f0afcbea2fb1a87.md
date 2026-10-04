+   1. Open SQL Server Management Studio from the Windows Start menu or Start screen. Open your PlanetWrox database, and locate the PhotoAlbum table. Right-click it and choose Design. Add a new column called UserName, set its data type to nvarchar(256), and leave the Allow Nulls option selected. (This table already contains photo albums without a valid UserName, so you can’t make the column required at this stage unless you delete these photo albums and their related pictures from the database first, or manually enter a username for each existing row.) Save your changes to the table and close SSMS.

+   2. Back in Visual Studio, open the ADO.NET Entity Data Model file PlanetWrox.edmx from the App_Code folder, right-click an empty space in the designer, and choose Update Model from Database. Wait until VS has analyzed your database and click Finish. The UserName column in the database now shows up as a property of the PhotoAlbum class (see Figure 17-8).
Save your changes and close the file.

+   3. Open the Web.config file, and below the existing <location> elements, add the following two <location> elements to block access to the two referenced files for anonymous users:

```
</location>
<location path="ManagePhotoAlbum.aspx">
    <system.web>
        <authorization>
            <deny users="?" />
        </authorization>
    </system.web>
</location>
<location path="NewPhotoAlbum.aspx">
    <system.web>
        <authorization>
            <deny users="?" />
        </authorization>
    </system.web>
</location>
</configuration>
```

Save your changes and close the Web.config file.

+   4. Open the Code Behind of NewPhotoAlbum.aspx and add the following highlighted code that sets the UserName property of the PhotoAlbum before the changes are saved to the database:

# VB.NET

```
myEntities.PhotoAlbums.Add(photoAlbum)
photoAlbum.UserName = User.Identity.Name
myEntities.SaveChanges()
```

# C#

```
myEntities.PhotoAlbums.Add(photoAlbum);
photoAlbum.UserName = User.Identity.Name;
myEntities.SaveChanges();
```

+   5. From the PhotoAlbums folder, open Default.aspx and switch to its Code Behind.

![](bbox=[0.78, 0.21, 0.9, 0.35])