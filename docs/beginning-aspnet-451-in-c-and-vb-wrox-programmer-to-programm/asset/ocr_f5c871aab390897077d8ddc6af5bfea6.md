the browser resubmits the cookie to the server so the system knows it’s still dealing with a valid user. The different settings for the Membership provider are all configured in the <membership /> element of the Web.config file. You learn more about this element later in this chapter.

To create a fully functional Login page, you need only the following control declaration:

```
<asp:Login ID="Login1" runat="server" />
```

However, in most situations you want to enhance the appearance and behavior of the control by setting one or more of the properties, shown in the following table.

| PROPERTY | DESCRIPTION |
|---|---|
| DestinationPageUrl | Defines the URL the user is sent to after a successful login attempt. When you leave this property empty, the value is taken from the defaultUrl attribute of the <forms> element in Web.config which defaults to Default.aspx. |
| CreateUserText | Controls the text that is displayed to invite users to sign up for a new account. If you leave this property empty, the sign-up link is not shown. |
| CreateUserUrl | Controls the URL where users are taken to sign up for a new account. |
| DisplayRememberMe | Specifies whether the control displays the Remember Me option. When set to False, the check box for this option is not shown. |
| RememberMeSet | Specifies whether the Remember Me option is initially checked. |
| PasswordRecoveryText | Controls the text of a link that is displayed to tell users they can reset or recover their password. If you leave this property empty, the link is not shown. |
| PasswordRecoveryUrl | Specifies the URL where users are taken to get their (new) password. |
| VisibleWhenLoggedIn | Determines whether the control is visible when the current user is logged in. True by default. |

The authentication mechanism of ASP.NET by default assumes you have a page called Login.aspx in the root of your site that is used to let users log in. To be functional, the minimum that this page requires is a Login control. If you want to use a different page, you can specify its path in the <forms /> element under <authentication /> like this:

```
<authentication mode="Forms">
    <forms loginUrl="~/Account/MyLoginPage.aspx" />
</authentication>
```