AttachDbFileName contains a path to your SQL Server Express database. The `|DataDirectory|` placeholder is expanded to the full and physical path of the `App_Data` folder at run time. So, when your pages load and the `SqlDataSource` needs to connect to the database, it will open the file `PlanetWrox.mdf` in `C:\BegASPNET\Site\App_Data`. As an alternative to `AttachDbFileName` you'll also come across `Initial Catalog` in other connection strings. The `Initial Catalog` points to a database available on the SQL Server you are using. You see more of this in Appendix B.

The last part of the connection string has to do with security. With Integrated Security, the account used by the web server is used to connect to the database. In the case of VS and IIS Express, this account is the one you use to log on to your machine. In case you're using the full version of IIS, this account is an account named after an `Application Pool` in IIS, or a special account called Network Service. Chapter 19, which deals with deployment, and Appendix B, which explains how to connect to SQL Server, dig deeper into security-related issues.

So far you have seen most of the database concepts that were introduced in the previous chapter. You saw creating (with the `DetailsView` in insert mode), reading (with the `SelectCommand` and the `GridView`), updating (inline within the `GridView` and an `UpdateCommand`), and deleting (with the delete option in the `GridView` and a `DeleteCommand`). Moreover, you saw sorting that can be enabled in the `GridView` with just a single setting. What you haven't seen is filtering, a way to limit the data that is presented in the page. In the next section you see how to create a filter that enables you to display reviews that belong to a certain genre. You create the filter in the Management section in a new page called `Reviews.aspx`, which will be your main entry point for managing the reviews in your website. Subsequent sections build on top of this, gradually expanding the Reviews page with more useful features.

# Filtering Data

As you learned in the previous chapter, you use a `WHERE` clause to filter your data. VS and ASP.NET come with a bunch of tools that make creating filters very easy. To filter data, the `SqlDataSource` control (and other data source controls) have a `<SelectParameters>` element that enables you to supply values at run time that are used for filtering. These values can come from a variety of sources, including the ones described in the following table.

| WITH A | THE VALUE IS RETRIEVED FROM |
|---|---|
| `ControlParameter` | A control in the page, such as a `DropDownList` or a `TextBox`. |
| `CookieParameter` | A cookie that is stored on the user's computer and that is sent to the server with each request. |
| `FormParameter` | A value posted in the form that has been submitted to the server. |
| `Parameter` | A variety of sources. With this parameter, you set the value through code. |
| `ProfileParameter` | A property on the user's profile. The ASP.NET Profile is discussed in full detail in Chapter 17. |
| `QueryStringParameter` | A query string field. |
| `SessionParameter` | A value that is stored in a session, which is a server-side, user-specific store of data that exists during a user's visit to a site. |