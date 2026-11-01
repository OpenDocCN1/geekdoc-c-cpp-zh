This is the minimum code needed for a user control in a page. Note that the control is defined by a combination of the TagPrefix and the TagName. The other two attributes—ID and runat—are standard attributes that most controls in an ASP.NET page have.

Fortunately, in most cases, you don't have to type all this code yourself. When you drag a user control from the Solution Explorer into a page in Design View, VS adds the required code for you automatically. The following exercise demonstrates how this works.

# TRY IT OUT Adding the User Control to Your Page

In this exercise, you add the user control Banner.ascx to the master page, so it displays a banner on each page in the site in the sidebar area.

+   1. Open up Frontend.master from the MasterPages folder and switch it into Design View.
+   2. Locate the drop-down list that enables you to select a theme, position your cursor right after the drop-down list, and press Enter three times to create some room.
+   3. From the Solution Explorer, drag the Banner.ascx file from the Controls folder into the empty spot you just created. Design View is updated and now looks like Figure 8-5.

![](bbox=[0.15, 0.625, 0.75, 0.775])

FIGURE 8-5

> **COMMON MISTAKES** If your Design View doesn't look like this, but looks much closer to how the file ends up in the browser, you may still have the styleSheetTheme set in the web.config file. Also, you may have more or fewer options selected in the View → Visual Aids or View → Formatting Marks menu, which may affect your display.