```
C#
public partial class Login : BasePage
{

}
```

4. Save the page and request it in the browser by pressing Ctrl+F5. If you haven't changed the title of the page earlier, or add one if needed, you will be greeted by the error shown in Figure 6-8 in your browser.

![](bbox=[0.117, 0.258, 0.758, 0.477])

5. Go back to VS and open the login page in Markup View. Locate the Title attribute in the @ Page directive (or add one if it isn't) and set its value to Log in to Planet Wrox. The following snippet shows the VB.NET version of the @ Page directive but the C# version is almost identical:

```
<Page Title="Log in Planet Wrox" Language="VB"
MasterPageFile="~/Pages/Frontend.master" AutoEventWire="false"
CodeFile="Login.aspx.vb" Inherits="Login">
```

6. Repeat steps 3 and 5 for all the pages in your site. To make this a quicker, you can use Find and Replace to quickly replace all the occurrences of System.Web.UI.Page with BasePage. Make sure you don't accidentally editing the BasePage in the App_Code folder itself. To prevent this from happening, make sure you search only in Code Behind files, like this:

+   - Open the Replace dialog box, press Ctrl+Shift+H or select Edit Find Replace Replace in Files.

+   - In the Find what box, enter System.Web.UI.Page. In the Replace text box, enter BasePage.

+   - Under the Look dropdown, make sure that Entire Solution is selected.

+   - Expand the Find section and look in the Look at These Files text box, enter *.aspx.vb or *.aspx.cs depending on the language you use. This leaves the BasePage file, which has a single extension of .vb or .cs, alone.

+   - Click Replace All and then click Yes to confirm the Replace operation.