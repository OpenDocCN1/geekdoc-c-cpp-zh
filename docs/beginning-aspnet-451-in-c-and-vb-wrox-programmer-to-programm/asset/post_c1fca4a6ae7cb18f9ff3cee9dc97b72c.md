
With this configuration, the ASP.NET runtime to load the LoginPage.aspx page from the Account folder in the site's root whenever a user needs to provide their credentials.

> **NOTE:** If you have installed the ASP.NET FriendlyUrls package (discussed in Chapter 7) you need to configure the loginUrl to point to `/Login/` rather than the default of `~/Login.aspx`. If you don't make this change, the Login control wont not find an exact match between the page that contains the Login control and the configured Login URL. This in turn breaks the feature that sends users to the originally requested page after they log in. You will see how to configure this in the next exercise.

Note on the Login page (configured in the loginUrl property), the VisibleLoggedIn property of the Login control has no effect. On the configured Login page, the Login control is always visible. If you want to use it as a Login control, as you see in a later exercise.

In addition to these properties, the Login control has a range of Text properties, such as LoginButtonText, RememberText, TitleText, and UserNameLabelText, that are used to set the text that appears in the control and its various child controls like the Button and Label controls that make up the user interface.

Just as with the data-bound controls, the login controls have numerous style properties that enable you to tweak their appearance. You're encouraged to check out the Styles category of the Properties Grid for controls to see how you can set the styling options. Remember, you can move much of the styling information to skin and CSS files.

The Login control also exposes a few events that you typically don't need to handle, but can come in handy from time to time. For example, the isLoggedIn event fires right after the user has logged in and is a good place to send the user to another page dynamically if the DestinationUrl is not flexible enough.

# LoginView

The LoginView is a handy control that lets you display different data to different users. It enables you to differentiate between anonymous and logged-in users, and you can even differentiate between users in different roles. The LoginView is template-driven and as such lets you define different templates to show to different users. The following table describes the two main templates and the special Role element.

| TEMPLATE | DESCRIPTION |
| :--- | :--- |
| AnonymousTemplate | The content in this template is shown to unauthenticated users only. |
| LoggedInTemplate | The content in this template is shown to logged-in users only. This template is mutually exclusive with the AnonymousTemplate. Only one of the two can be visible at any time. |

# Introducing the Login Controls

# RoleGroups

This control can contain one or more RoleGroup elements that, in turn, contain a ContentTemplate element that defines the content for the specified role. The role or roles that are allowed to see the content are defined in the Roles attribute, which takes a comma-separated list of roles. The RoleGroups element is mutually exclusive with the LogInTemplate. That means if a user is a member of one of the roles for the RoleGroup, the control in the LoggedInTemplate is not visible. Additionally, only content for the first RoleGroup that matches the user’s roles is shown.

The LoginView itself doesn't output any markup than the content you define in the child elements of the control, which you can easily embed between a pair of HTML tags like `<h1>` and `<li>` to create customized headers or list items.

The following code snippet shows a LoginView that defines content for three users: anonymous visitors to the site, logged-in users, and users who have logged in and are members of the Managers:

```asp
<asp:LoginView Id="LoginView" runat="server">
  <AnonymousTemplate>
    Hi visitor. Would you be interested in signing up for an account?
  </AnonymousTemplate>
  <LoggedInTemplate>
    Hi visitor and welcome back to LoginWrox.com.
  </LoggedInTemplate>
  <RoleGroups Roles="Managers">
    <ContentTemplate>
      Hi manager. You can proceed to the Management section.
    </ContentTemplate>
  </RoleGroups>
</asp:LoginView>
```

You can see how to configure roles later in this chapter.

# LoginStatus

As demonstrated in this exercise the LoginStatus control provides information about the current status of the user. It provides a Login link when the user is not authenticated and a Logout link when the text being displayed by setting the LoginText and LogoutText properties. Alternatively, you can use the LoginImageUrl and LogoutImageUrl properties to display an image instead of text. If you set both an image and a text, the text is shown and used as the alternative text. Finally, you can set the LogoutAction to determine whether the current page refreshes the user out, or whether the user is taken to another page after logging out. This destination page is by setting the LogoutPageUrl.

Besides these properties, the control is capable of raising two events, LoggingOut and LoggedOut, which fire right before and after the user is logged out.

# LoginName

LoginName is an extremely simple control. All it does is display the name of the logged-in user. To embed the user's name in some text, such as You are logged in as Imar, you can use the FormatString property. If you include {0} in this format string, it will be replaced with the user's name.

You see how this works in the next exercise, which has you modify the login and master pages for the site so they display relevant information about the user.

# TRY IT OUT Working with the Login Controls

In this Try It Out, you hide the Login control on the Login.aspx page when the user is already logged in and display a message instead. Additionally, you add text to the footer of the page that displays the name.

1. Open Login.aspx and switch to Design View. From the Toolbox, drag a Login control onto the page.
2. Open Login.aspx and switch to Design View. From the Toolbox, drag a LoginView control onto the Login control.
3. Open Login.aspx and switch to Design View. Click the Login control and cut it. Paste it into the AnonymousTemplate.
4. Open Login.aspx and switch to Design View. From the Properties panel of the LoginView, select the AnonymousTemplate. Type the text "You are already logged in" inside the white rectangle.
5. Open Login.aspx and switch to Design View. From the Properties panel of the LoginView, select the LoggedInTemplate. From the Toolbox, drag a LoginStatus control into the white rectangle.
6. Open Login.master and switch to Markup View. Locate the <footer> element at the bottom of the page.
7. Open Login.master and switch to Markup View. Replace the text in the <footer> with a new LoginName control. Set its FormatString to "Logged in as {0}".
8. Open Login.master and switch to Design View. From the Toolbox, drag a LoginView control below the LoginName control. From the Properties panel of the LoginView, select the LoggedInTemplate.
9. Open Login.master and switch to Design View. From the Properties panel of the LoginView, select the AnonymousTemplate. From the Toolbox, drag a LoginStatus control into the white rectangle.
10. Open the Web.config file and modify the <authentication> element so it points the loginUrl to `/Login/` like this:

```xml
<authentication mode="Forms">
  <forms loginUrl="/Login/"/>
</authentication>
```
11. Save all your changes and request Login.aspx in your browser. Log in with the account and password you created in a previous exercise (you may need to log out first by clicking the Logout link). If you don’t recall the username and password, simply click the Sign Up link to create a new account. Note that as soon as you are logged in, the footer displays the text visible in Figure 16-10.

![](img/9e033e3b9560597824f8b22941d6d8bb_640.png)

12. Click the Login item in the Menu or TreeView to go to the Login page. Instead of the Login control you should now see a message indicating that you are already logged in.

13. Click the Logout link in the footer at the bottom of the page. The page refreshes and displays the Login control again. Additionally, the text from the footer has now disappeared.

# How It Works

You started by adding a LoginView to the Login page to wrap the Login control and a text message. The Login control is shown when the user is not logged in, whereas the text is displayed for logged-in users only.

The code in the footer of the master page contains a LoginName control that displays the name of the user that is logged in. To control the text being displayed, you use the FormatString property:

```asp
<asp:LoginName ID="LoginName1" runat="server" FormatString="Logged in as {0}" />
```
