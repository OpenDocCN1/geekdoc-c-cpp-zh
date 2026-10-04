
| ASP.NET 4.5.1 Websites and Applications |
| --- |
| ASP.NET Services | Membership | Roles | Profile | Other Services |
| Providers | MembershipProvider | RoleProvider | ProfileProvider | Other Providers |
| Data Stores | SQL Server | Active Directory | Oracle | Microsoft Access | Other Data Stores |

FIGURE 16-1

At the top of the diagram, you see the ASP.NET 4.5.1 websites and web applications that represent the websites that you build. These websites can contain controls like the login controls (discussed next) in turn can talk to the ASP.NET application services such as membership and roles. To create a flexible solution, these services don't talk to an underlying data source directly, but instead talk to a configured provider. A provider is an interchangeable piece of software that is designed for a specific task. For example, in the case of the membership services, the Membership provider is designed to work with users in the underlying data store. You can configure different providers for the same application depending on your needs. Previous versions of ASP.NET shipped with a SQL Server provider that enables to talk to a SQL database and an Active Directory provider (that lets you create and manage users in Active Directory on Windows). These are still available, but there is now a new alternative. In June 2012, Microsoft released Universal Providers that work the same as the SQL Server providers, but can be used for all targets of SQL Server, including SQL Compact and SQL Azure. This makes it easy to switch the underlying database, simply changing the configuration for the application. The Universal Providers are available for .NET 4 and later and are ideal for Internet-connected websites like PlanetWrox. If you create a new ASP.NET Web Forms site, the Universal Providers are already set up for you. If you create an empty website instead (as is the case with PlanetW project), you need to add the providers yourself using NuGet, as you see in later exercise.

The beauty of the provider model is that you can swap providers through configuration without any changes to your programming code. If you have your own custom data store, you could write your own provider and plug it into your website to replace one of the default providers with very little effort. Each provider needs a data store — represented by the bottom part of the diagram in Figure 16-1 — and is written to work with one or more specific data stores. For example, the DefaultMembershipProvider (to handle membership services such as creating users, logging in, and resetting passwords) and the DefaultRoleProvider (to handle role-related tasks) are designed to work with any version of Microsoft SQL Server, including Express, LocalDB, and SQL Azure. These two providers replace the SqlMembershipProvider and the SqlRoleProvider that shipped with earlier versions of ASP.NET. In the remainder of this chapter, you see how to use the DefaultMembershipProvider and the DefaultRoleProvider. In the next chapter, you work with the DefaultProfileProvider. You can configure all three providers to use the same SQL database, making it easy to centralize all your user data.

NOTE ASP.NET 4.5.1 ships with a new authentication and authorization system called ASP.NET Identity. It’s designed to replace the Membership system that has been part of ASP.NET for a long time. However, this new framework targets advanced scenarios and doesn’t support the various controls you’ll see in this chapter. I therefore won’t discuss this new system in this book, but you can learn more about it on the official ASP.NET website at www.asp.net/identity.

Ideally you don’t deal with these providers directly. Under normal circumstances, the various providers are configured for your website at a central location. You then use these providers by talking to the application services. Although you could access these services directly from code, you often use the ASP.NET built-in login controls to do the hard work for you. These controls are discussed next.

## INTRODUCING THE LOGIN CONTLS

The login controls that ship with ASP.NET 4.5.1 take away much of the complexity usually associated with writing a security layer in a website. The available login controls effectively encapsulate all the code and logic you need to validate and manage users. These controls work by communicating with the configured provider through the application services, instead of talking to a database directly. To see how this works, the following exercise shows you how to create a simple Login and Sign Up page that enables new users to create an account and then log in. The section that follows looks at the seven login controls that ship with ASP.NET 4.5.1.

### Creating Login and Sign-Up Pages

In this exercise, extend the Login page that you created earlier. You also create a new page that enables you to sign up for an account on the PlanetWrox website.

- 1. Open your page in VS and then open the Package Manager (choose Tools > Package Manager > Package Manager Console).
- 2. Enter the following command at the Package Manager Console and press Enter: `Install-Microsoft.AspNet.Providers`

By executing this package, VS downloads the providers, adds an assembly System.Web.Providers.dll to the Bin folder of your site and adds configuration information for the providers to Web.config. When you have completed, your Solution Explorer should look like Figure 16-2.

- 3. From the root of the site, open the Login.aspx page in Markup View. If you don't have the page, create it now based on your custom template and set its Title to Log in to PlanetWrox. Then add an <h1> element with the text in the MainContent placeholder.
- 4. From the Login category of the Toolbox, drag a Login control and drop it in the page after the <h1> element.
- 5. Switch to Design View and from the Toolbox, drag a Login control and drop it on the LoginStatus, so it ends up right above the control. Both controls are visible in Figure 16-3 (the LoginStatus appears as a small Login link below the Login control).

![](img/9e033e3b9560597824f8b22941d6d8bb_631_0.png)
FIGURE 16-2

![](img/9e033e3b9560597824f8b22941d6d8bb_631_1.png)
FIGURE 16-3

- 6. Open the Properties Grid for the Login control and set the three properties shown in the following table:

| PROPERTY | VALUE |
| :--- | :--- |
| DestinationPageUrl | ~/Default.aspx |
| CreateUserText | Sign Up for a New Account at PlanetWrox |
| CreateUserUrl | ~/SignUp.aspx |

- 7. In the root of the website, create a new Web Form called SignUp.aspx based on your custom template and give it a Title of Sign Up for a New Account at PlanetWrox.
- 8. Switch the page to Design View and from the Toolbox, drag a CreateUser control into the main content area for the page. Save and close the page.
- 9. Open the Web.config file from the root of the site and add an <authentication> element with its attribute set to Forms as a direct child of the <system.web> element:

```xml
<system.web>
<authentication mode="Forms" />
</system.web>
```

- 10. Still in the Web.config file, take a look at the <connectionStrings> section. Notice how the NuGet package added a new connection string for you called DefaultConnection. You could leave this connection string there, and everything would work. However, with this connection string, .NET creates a new database and attaches to SQL Server. From a management perspective, it will be easier if your user data is stored in the same database as your reviews, pictures, and photo albums. This is quite easy to accomplish: first remove the connection string DefaultConnection and replace the value for the connectionString attribute on all four providers (Profile, Membership, Roles, and Session state) with the value of your Planet Wrox connection string (which should be PlanetWroxConnectionString). You should end up with configuration code that looks like the following. Note that I left out a lot of code and only show the code for the Membership provider attribute on all four providers that points to the Planet Wrox connection string:

```xml
<connectionStrings>
<add name="PlanetWroxConnectionString" connectionString="... />
<add name="PlanetWroxEntries" connectionString="... />
</connectionStrings>

<system.web>
  .. Other code here
  <membership defaultProvider="DefaultMembership">
    <providers>
      <add name="DefaultMembershipProvider"
           Other attributes here
           connectionName="PlanetWroxConnectionString1"
           enablePasswordRetrieval="false" enablePasswordReset="true"
           .. Other attributes here
      />
    </providers>
  </membership>
  .. Other code here
</system.web>
```

- 11. Save all your changes, go back to Login.aspx, and press Ctrl+F5 to open that page in your browser. You are greeted with a login box, as shown in Figure 1-4.
