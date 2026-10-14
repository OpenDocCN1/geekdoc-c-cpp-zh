# The directory structure for a theme

![](bbox=[0.154, 0.103, 0.403, 0.435])

# The order in which styles and control attributes are applied

+   1. Style sheet theme styles and control attributes
+   2. External, internal, and inline styles and control attributes
+   3. Customization theme styles and control attributes

# Description

+   - The App_Themes folder can contain multiple subfolders with each subfolder defining one theme.
+   - Each theme folder can contain a file that contains the cascading style sheet (CSS) that defines the appearance of the HTML elements, files that define the skins that control the appearance of the ASP.NET server controls, and files for any images or other resources that are used by the cascading style sheet or the skins.
+   - ASP.NET provides for both style sheet themes and customization themes. The difference between the two has to do with when the styles and control attributes they contain are applied, as shown above.
+   - To create the App_Themes folder, you can right-click on the root folder, select the Add ASP.NET Folder submenu, select the Theme item, and enter a name for the theme folder. To create another folder, right-click the App_Themes folder instead of the root folder.