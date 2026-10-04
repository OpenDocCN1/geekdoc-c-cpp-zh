8. Save all your changes and request the homepage (Default.aspx) for the site in your browser. Verify that you are not logged in (check the footer of the page and, if necessary, click the Logout link).

![](img/9e033e3b9560597824f8b22941d6d8bb_657_0.png)

If you don't click the Manage Site link in the footer region, close all browser windows, go back to the WSAT as shown early, and ensure the account you are assigned is to Managers.

10. Click the Manage Site link to open the Management section of the website. Copy the current URL of the page from the browser's address bar to the clipboard (it should be like http://localhost:4966/Management/Default). Click the Back button of your browser to go back to the page and click the Logout button in the footer. Close all open windows and open a new instance of your browser. (You can do this from the Windows Start menu or Screen or you can right-click in VS and View in Browser).

11. Paste the address you just copied in the address bar of the browser and press Enter. Instead of trying to address this link,

```
http://localhost:4966/Management/Default
```

```
http://localhost:4966/login?ReturnUrl=%2fManagement%2fDefault
```

Note that the page you initially requested (Management/Default) is now appended to the query string. The forward slashes (/) in the address have been encoded to their URL-safe counterpart — %2f — automatically. Log in with your Manager account and you should see the Management section appear again. Next, log out, or log in with one of the other accounts, and then try to access the Management folder again. Because that account doesn't have permissions to access that folder, you're redirected to the Login page again.

# How It Works

To see how this works, you need to look at a couple of things. First, look at the settings you added to the Web.config file to limit the Management folder:

```xml
<location path="Management">
  <system.web>
    <authorization>
      <allow roles="Managers" />
      <deny users="*" />
    </authorization>
  </system.web>
</location>
```

When the ASP.NET run time processes the request for a page, it checks the various configuration files to see whether the user is allowed to access that resource. For requests to files in the Management folder, it encounters the rule set in the <location> element. It scans the various allow and deny elements with roles or users attributes to specify the users or roles that are affected by the rule. The roles and users attributes take one or more role or usernames, separated by a comma. As soon as a rule is found that matches, the scanning process is stopped and that rule is applied. If no rule is satisfied, access is granted! Therefore it's important to edit the rule with a deny to block all users who haven't been granted access previously.

If you'd added an authorization element to the Web.config in the Management folder, the settings you apply are looked at first because the security model works inside out. That is, by scanning the Web.config file (if present) in the folder that contains the requested page. If it there doesn't contain settings that block or grant access, it goes up in the folder hierarchy searching for configuration files with authorization elements. In the previous exercise, the run time found the settings in the Web.config file in the root that were then applied to the folder.

When an unauthenticated user logs in

After you logged in as a Manager and requested the same resource, the rule set scanned again. The run time then found the allow element that grants access to the Managers role and immediately let you in. The final rule that blocks access to all other users was not even checked. In addition to specify roles or usernames — or anonymous — Users. So, for example, to let logged-in user access the Reviews folder regardless of the role they are in, and block access to all other users, you can use the question mark (?) following the <location> element to your configuration file:

```xml
<location path="Reviews">
  <system.web>
    <authorization>
      <deny users="*" />
    </authorization>
  </system.web>
</location>
```