right below the existing element. Then modify the copy so it blocks access to the MyProfile.aspx file in the root of the site to all unauthenticated users. You should end up with these settings:

```
</location>
<location path="MyProfile.aspx">
  <system.web>
    <authorization>
      <deny users="?"/>
    </authorization>
  </system.web>
</location>
</configuration>
```

+   8. In the Solution Explorer, right-click the MyProfile.aspx file and choose View in Browser. You can only view this file when you're logged in; if you weren't logged in previously, you are taken to Login.aspx first. Log in with the username and password you created in the previous chapter and click Login. You're taken back to MyProfile.aspx. Although you don't see anything new in the page, the code in Page_Load has run and has created a profile for you in the database.
+   
+   9. To see this profile, close your browser and go back to Visual Studio. Open the Database Explorer (the Server Explorer in paid versions of VS) and expand the Tables element of the PlanetWrox_mdf database. Locate the Profiles table, right-click it, and choose Show Table Data. You should see something similar to Figure 17-2.

![](bbox=[0.15, 0.73, 0.85, 0.84])

FIGURE 17-2

This figure shows the profile data for a single user. The first and last name you entered in step 5 are stored in the column PropertyValueStrings. Because of the special format this data is stored in, you shouldn't modify this data manually. Instead, you should use Profile to change the underlying data.

# How It Works

When you define profile properties in Web.config, the ASP.NET run time creates a class for you in the background. This class, called ProfileCommon, gives you access to the strongly typed properties such as FirstName, LastName, and FavoriteGenres. The ProfileCommon class is then made accessible to the Page through its Profile property. ProfileCommon inherits from ProfileBase, the base class defined in the .NET Framework that contains the behavior to access the profile in the database by talking to the configured provider, the ASP.NET Profile provider. The provider in turn takes care of all the hard work of persisting the data in the configured database. Just as the Membership and Roles providers you saw in the preceding chapter, the Profile provider uses the connection string defined in the connectionStringName attribute of the configured provider.