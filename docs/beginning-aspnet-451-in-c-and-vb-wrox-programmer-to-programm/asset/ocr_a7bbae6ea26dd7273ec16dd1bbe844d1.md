594 | CHAPTER 16 SECURITY IN YOUR ASP.NET WEBSITE

# TRY IT OUT Creating Login and Sign-Up Pages

In this Try Out, extend the Login page that you created earlier. You also create a new page that enables you to sign up for an account on the Planet Wrox website.

+   1. Open your page in VS and then open the Package Console Manager (choose Tools ⌥ Package Manager ⌥ Package Manager Console).

+   2. Enter the following command at the Package Manager Console and press Enter:\`Install-Microsoft.AspNet.Providers`

By executing this package, VS downloads the providers, adds an assembly system.Web.Providers.dll to the Bin folder of your site and adds configuration information for the providers to Web.config. When you have completed, your Solution Explorer should look like Figure 16-2.

+   3. From the root of the site, open the Login.aspx page in Markup View. If you don't have the page, create it now, based on your custom template, and set its Title to Log in to Planet Wrox. Then add an <h1> element with the text in the cMainContent placeholder.

+   4. From the Login category of the Toolbox, drag a Login control and drop it in the page after the <h1> element.

+   5. Switch to Design View and from the Toolbox, drag a Login control and drop it on the LoginStatus, so it ends up right above the control. Both controls are visible in Figure 16-3 (the LoginStatus appears as a small Login link below the Login control).

![](bbox=[0.615, 0.263, 0.858, 0.455])

FIGURE 16-2

![](bbox=[0.115, 0.603, 0.608, 0.753])

FIGURE 16-3

+   6. Open the Properties Grid for the Login control and set the three properties shown in the following table:

| PROPERTY | VALUE |
| :--- | :--- |
| DestinationPageUrl | ~/Default.aspx |
| CreateUserText | Sign Up for a New Account at Planet Wrox |
| CreateUserUrl | ~/SignUp.aspx |