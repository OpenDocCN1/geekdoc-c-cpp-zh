access anything that is a Manager or an Editor access). Generally, it's best to manage users through roles as much as possible, but it's good to know that you can grant individual accounts the necessary rights as well (or explicitly take those away using a deny element).

# Exercise 3 Solution

If you want to redirect all users to the same page, all you need to set is the DestinationPageUrl: <asp:Login ID="Login" runat="server" DestinationPageUrl="MyProfile.aspx">

When a user is logged in, she's taken to MyProfile.aspx automatically.

# Exercise 4 Solution

The LoginStatus simply displays a simple link that indicates or not the user is logged in. By default the text that is displayed is Login when the user is currently not logged in, and Logout when the user is logged in. Clicking the link sends the user to the default Login page, or logs the user out.

The LoginView is somewhat similar in that it differs different content depending on whether the user is logged in. However, because the control is completely separate, you can control the content that is displayed. To enable you to differentiate between different user roles, you can use the RoleGroups element to set templates that are only shown to users in specific roles.

# CHAPTER 17

# Exercise 1 Solution

You would implement the favorite theme as a String property and call it FavoriteTheme. To ensure that you always have a valid theme, you could also set a default value. Finally, you should make the property accessible to anonymous users. Your favorite profile property could end up like this:

```
<add name="FavoriteTheme" defaultValue="Monochrome" allowAnonymous="true" />
```

To support anonymous profiles, you need to explicitly enable them by adding an <anonymousIdentification> element as a direct child of <system.web> in the Web.config file:
<system.web>
<anonymousIdentification enabled="true" cookieName="PlanetWroxAnonymous" />

# Exercise 2 Solution

Given the syntax you saw in the question, you could now access the property and use it to change the current theme in the BasePage:

```
VB.NET
Private Sub Page_PreInit(sender As Object, e As EventArgs)
   Handles Me.PreInit
Dim myProfile As ProfileCommon =
CType(HttpContext.Current.Profile, ProfileCommon)
```