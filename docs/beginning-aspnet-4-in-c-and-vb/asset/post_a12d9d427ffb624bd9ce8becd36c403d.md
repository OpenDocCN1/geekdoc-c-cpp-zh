
```
<div id="nav">
  <div class="navTree">
    <asp:TreeView ID="TreeView1" runat="server"
      DataSourceID="SiteMapDataSource" ShowLines="True" />
    <br />
    <br />
    <asp:LoginView ID="LoginView1" runat="server">
      <LoggedInTemplate>
        You are currently logged in as
        <b><asp:LoginName ID="LoginName1" runat="server" /></b>.
        <asp:LoginStatus ID="LoginStatus1" runat="server" />
      </LoggedInTemplate>
    </asp:LoginView>
  </div>
  <div id="body">
    <asp:ContentPlaceHolder ID="ContentPlaceHolder1" runat="server" />
  </div>
</form>
<asp:SiteMapDataSource ID="SiteMapDataSource1" runat="server" />
</body>
</html>

*code snippet PCSDemoSite/MasterPage.master*
```

Many of the controls here are ones that you haven’t looked at yet, and you will come back to those shortly.

The important things to note here are the <div> elements that hold the various content sections (header, navigation bar, and body), and the use of <%$ AppSettings:SiteTitle %> to obtain the site title from the web.config file:

```
<appSettings>
  <add key="SiteTitle" value="Professional C# Demo Site"/>
</appSettings>

*code snippet PCSDemoSite/web.config*
```

There is also a style sheet link to StyleSheet.css:

```
<link rel="stylesheet" href="StyleSheet.css" type="text/css" />
```

This style sheet contains the basic layout information for the <div> elements on this page, as well as for a section of the meeting room booker control. Note that none of the style information in this file includes colors, fonts, and so on. This is achieved by style sheets within themes, which you see later in this chapter. The only information here is layout information, such as <div> sizes.

> Note that web site best practices have been adhered to in this chapter whenever possible. Using CSS for layout rather than tables is fast becoming the industry standard for web site layout and is well worth learning about. In the preceding code, # symbols are used to format <div> elements with specific id attributes, whereas .mrbEventList will format an HTML element with a specific class attribute.

## SITE NAVIGATION

The three navigation web server controls, SiteMapPath, Menu, and TreeView, can work with an XML site map that you provide for your web site, or a site map provided in a different format if you implement an alternative site map provider. When you have created such a data source, these navigation web server controls are able to automatically generate location and navigation information for users.

The data from this data source is consumed by Menu and TreeView controls simply by setting their DataSourceID to the ID of the SiteMapDataSource. Both controls include numerous styling properties and can be themed, as you see later in this chapter.

## Navigating in PCSDemoSite

The site map for PCSDemoSite is as follows:

```
<?xml version="1.0" encoding="utf-8" ?>
<siteMap>
  <siteMapNode url="~/Default.aspx" title="Home">
    <siteMapNode url="~/About/Default.aspx" title="About" />
    <siteMapNode url="~/HRB/Default.aspx" title="Meeting Room Booker"
    roles="RegisteredUser,SiteAdministrator" />
  </siteMapNode>
  <siteMapNode url="~/Configuration/Default.aspx" title="Configuration"
    roles="RegisteredUser,SiteAdministrator" />
  <siteMapNode url="~/Configuration/Themes/Default.aspx" title="Themes"
    roles="RegisteredUser,SiteAdministrator"/>
  </siteMapNode>
  <siteMapNode url="~/Users/Default.aspx" title="User Area"
    roles="SiteAdministrator" />
  <siteMapNode url="~/Login.aspx" title="Login Details" />
</siteMapNode>
</siteMap>
```

*code snippet PCSDemoSite/Web.sitemap*

The PCSDemoSite web site uses a custom provider to obtain information from Web.sitemap — which is necessary because the default provider ignores the roles attributes. The provider is defined in the web.config file for the web site as follows:

```
<siteMap defaultProvider="CustomProvider">
  <providers>
    <add name="CustomProvider"
      type="System.Web.XmlSiteMapProvider"
      siteMapFile="Web.sitemap" securityTrimmingEnabled="true" />
  </providers>
</siteMap>
```

*code snippet PCSDemoSite/web.config*

The only difference between this and the default provider is the addition of securityTrimmingEnabled="true", which instructs the provider to supply data for just those nodes that this current user is allowed to see. This visibility is determined by the role membership of the user, as you see in the next section.

The MasterPage.master page in PCSDemoSite includes SiteMapPath and TreeView navigation displays along with a data source, as follows:

```
<div id="header">
  <h1><asp:literal ID="Literal1" runat="server"
    text="<%$ AppSettings:SiteTitle %>" /></h1>
  <asp:SiteMapPath ID="SiteMapPath1" runat="server"
    CssClass="breadcrumb" />
</div>
<div id="nav">
  <div class="navTree">
    <asp:TreeView ID="TreeView1" runat="server"
      DataSourceID="SiteMapDataSource1" ShowLines="True" />
  </div>
  <br />
  <br />
```

- 3. Click the "Use the security Setup Wizard to configure the security step by step" link.
- 4. Click Next in Step 1 of the wizard after reading the information there.
- 5. In Step 2 of the wizard, select "From the internet" to select Forms Authentication and click Next.
- 6. Click Next again after confirming that you will be using the default "Advanced provider settings" provider to store security information.

> This provider information is configurable via the Provider tab, where you can choose to store information elsewhere, such as in an SQL Server database, but the default SQL Server Express database is fine for illustrative purposes.

- 7. Check the "Enable roles for this Web site" option and click Next.
- 8. Add two roles, Administrator and User, and click Next.
- 9. Add two user accounts, also called Administrator and User. Note that the default security rules for passwords (defined in machine.config) are quite strong; there is a seven-character minimum, including at least one symbol character and a mix of uppercase and lowercase.

> In the downloadable code for this chapter, the password for both the User and Administrator account is PaSsW0rd.

- 10. Click Next, and then Next again, skipping the Add New Access Rules page.

> By default, all users and roles will have access to all areas of your site. From the Add New Access Rules page you can restrict areas by role, by user, or for anonymous users. You can do this for each directory in your site because this is achieved via web.config files in directories, as you will see shortly.

- 11. Click Finish.
- 12. On the main page for the Security tab, click Manage users.
- 13. Click Edit Roles for each user in turn, and add the Administrator user to both roles and the User user to just the User role.

After you have done all this, you are pretty much there. You have a user system in place, as well as roles and users

To illustrate what this makes possible, you have to add a few controls to your web site to make things work. The example code in the following sections assumes that the web site is configured with the User and Administrator roles and users as described in this section.

## Implementing a Login System

If you open web.config after running the security wizard you will see that it has been modified with the following content:

```
<roleManager enabled="true" />
```

and:

```
<authentication mode="Forms" />
```

This doesn't seem like a lot for the work that you have put in, but remember that a lot of information is stored in an SQL Server Express database, which you can see in the App_Data directory (you may need to click the refresh button in the Solution Explorer to see this file, called ASPNETDB.MDF. You can inspect the data that has been stored in this file using any standard database management tool, including Visual Studio. You can even add users and roles directly to this database, if you are careful.

By default, logging in is achieved via a page called Login.aspx in the root of your web site. If users attempt to navigate to a location that they don't have permission to access, they will automatically be redirected to this page and returned to the desired location after successfully logging in.

Add two Web Forms called Default.aspx and Login.aspx to the PCSAuthenticationDemo site and drag a Login control onto the Login.aspx form from the toolbox.

This is all you need to do to enable users to log in to your web site. Open the site in a browser, and navigate to Login.aspx (you have to do this manually for now as you haven't restricted access to Default.aspx). Enter the details for a user you added in the Security Setup Wizard, as shown in Figure 41-5.

![](img/d7d2ffa0a76feaab821930e95daace93_1264_0.png)

FIGURE 41-5

After you have logged in, you will be sent to Default.aspx, currently a blank page.

## Login Web Server Controls

The Login section of the toolbox contains several controls, as shown in the following table.

| CONTROL | DESCRIPTION |
|---|---|
| Login | As you have seen, this control allows users to log in to your web site. Most of the properties of this control are for styling the supplied template. You can also use DestinationPageUrl to force redirection to a specific location after logging in, and VisibleWhenLoggedIn to determine whether the control is visible to logged-in users. And, you can use various text properties such as CreateUserText to output helpful messages to users. |
| LoginView | This control enables you to display content that varies depending on whether users are logged in, or what roles users are in. You can put content in <AnonymousTemplate> and <LoggedInTemplate>, as well as <RoleGroups> to control the output of this control. |
| PasswordRecovery | This control enables users to have their password mailed to them, and it can use the password recovery question defined for a user. Again, most properties are for display formatting, but there are properties such as MailDefinition-Subject for configuring the e-mail to be sent to the user's address, and SuccessPageUrl to redirect the users after they have requested a password. |
| LoginStatus | This control displays a Login or Logout link, with customizable text and images, to users depending on whether they are logged in. |
