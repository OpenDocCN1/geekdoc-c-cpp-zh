```
```xml
</system.web>
</location>
<system.web>
  <authorization>
    <deny users="?" />
  </authorization>
</system.web>
```
```

*code snippet PCSDemoSite/web.config*

Here a <location> element is used to override the default setting for a specific file specified using a path attribute, in this case for the file StyleSheet.css. <location> elements can be used to apply any <system.web> settings to specific files or directories, and can be used to centralize all directory-specific settings in one place, if desired (as an alternative to multiple web.config files). In the preceding code, permission is given for anonymous users to access the root style sheet for the web site, which is necessary because this file defines the layout of the <div> elements in the master page. Without this, the HTML shown on the login page for anonymous users would be difficult to read.

Another point to note is in the code-behind file for the meeting room booker user control, in the Page_Load() event handler:

```
```csharp
void Page_Load(object sender, EventArgs e)
{
    if (!this.IsPostBack)
    {
        nameBox.Text = Context.User.Identity.Name;
        DateTime trialDate = DateTime.Now;
        calendar.SelectedDate = GetFreeDate(trialDate);
    }
}
```
```

*code snippet PCSDemoSite/MRB/MRB.ascx.cs*

Here the username is extracted from the current context. Note that in your code-behind files you will probably also use Context.User.IsInRole() frequently to check access.

# THEMES

By combining ASP.NET pages with master pages and CSS style sheets, you can go a long way in separating form and function, whereby the look and feel of your pages are defined separately from their operation. With themes you can take this a step further and dynamically apply this look and feel from one of several themes that you supply yourself.

A theme consists of the following:

+   - A name for the theme
+   - An optional CSS style sheet
+   - Skin (.skin) files allowing individual control types to be styled

These can be applied to pages in two different ways — with Theme or StyleSheetTheme attributes:

+   - **Theme** — All skin properties are applied to controls, overriding any properties that the controls on the page may already have.
+   - **StyleSheetTheme** — Existing control properties take precedence over properties defined in skin files.

CSS style sheets work in the same way whichever method is used because they are applied in the standard CSS way.