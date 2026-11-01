Other options for the mode attribute include Windows (where security is handled by Windows itself) and None, which disables security altogether. In the remainder of this book, the Forms option is used exclusively because it's the most common solution for Internet-facing web applications.

The Remember Me Next Time option of the Login control is more forgetful than you may think. When you check this option, you are logged in automatically the next time you visit the site, provided your authentication cookie hasn't expired. The first time you log in, the server sets a cookie that is saved for future sessions. However, this cookie expires after 30 minutes, which means a user returning to the site after that period needs to reauthenticate. To extend the period that users remain logged in, you need to set the timeout attribute of the <forms> element (which itself is a direct child of the <authentication> element) in Web.config. The timeout takes an integer value representing the timeout period in minutes. The following code sets the timeout to 24 hours (1440 minutes):

```
<authentication mode="Forms">
  <forms timeout="1440" />
</authentication>
```

Lower timeout values are generally considered safer because they don't provide unlimited or long-lasting access, but longer timeout values are more user friendly because users don't need to reauthenticate every time they visit the site.

If you hadn't reconfigured the providers to use the Planet Wrox database, .NET would have created a new one for you.

Now that you have seen how the login controls work in conjunction with the auto-generated SQL Server Express database, it's time to look at the controls in the Login category of the Toolbox in more detail.

# The Login Controls

ASP.NET 4.5 ships with seven login controls, each serving a distinct purpose. Figure 16-8 shows the Toolbox with the seven login controls (the pointer is present in all Toolbox categories and is not a login control).

In the sections that follow, each of these controls is explained in more detail.

# Login

As you saw in the previous exercise, the Login control enables a user to log in to the site. Under the hood, the control talks to the configured Membership provider through the application services to see if the username and password represent a valid user in the system. If the user is validated, a cookie is issued that is sent to the user's browser. On subsequent requests, the browser resubmits the cookie to the server so the system knows it's still dealing with a valid user. The different settings for the Membership provider are all configured in the <membership /> element of the Web.config file. You learn more about this element later in this chapter.

![](bbox=[0.7, 0.88, 0.88, 1.0])