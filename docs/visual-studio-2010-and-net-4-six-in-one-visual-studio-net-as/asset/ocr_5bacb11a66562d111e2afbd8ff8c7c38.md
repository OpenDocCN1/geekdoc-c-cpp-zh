![](bbox=[0.095, 0.102, 0.652, 0.495])

**FIGURE 17-26:** Page with new title and header

For example, you can make the necessary changes to use alternating background colors by following these steps:

+   1. Open the Site.css file.

+   2. Add a new style to define an aqua background color for an alternating row style, tars:
```css
table.DDGridView .tars {
    background-color: Aqua;
}
```

+   3. Now, open the ListDetails.aspx page template and switch to the Design view.
4. Click on the grid, asp:GridView#GridView. Go to its properties and enter tars in Styles AlternatingStyle Css Class. The GridView will apply the previously defined style to alternate styles in the different rows. The design view will display an aqua background alternating in the different rows of the grid, as shown in Figure 17-27.