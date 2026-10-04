# List Controls

<asp:DropDownList ID="FavoriteLanguage" runat="server">
<asp:ListItem Value="C#">C#</asp:ListItem>
<asp:ListItem Value="Visual Basic">Visual Basic</asp:ListItem>
<asp:ListItem Value="CSS">CSS</asp:ListItem>
</asp:DropDownList>

```
<asp:DropDownList ID="FavoriteLanguage" runat="server">
<asp:ListItem Value="C#">C#</asp:ListItem>
<asp:ListItem Value="Visual Basic">Visual Basic</asp:ListItem>
<asp:ListItem Value="CSS">CSS</asp:ListItem>
</asp:DropDownList>
```

The DropDown enables a user to select only one item at a time. To see the currently active and selected item of a list control programmatically, you can look at its SelectedValue, SelectedItem, or'. SelectedValue returns a string that contains the value for the selected item, like C# or Visual Basic in the preceding example. Selected returns the zero-based index of the item in the list. If the user had chosen C#, SelectedIndex would be 0. Similarly, if the user had chosen CSS, the index would be 2 (the third item in the list).

For controls that allow multiple selections (like CheckListBox and ListBox), you can loop through the Items collection and see what items are selected. In this case, SelectedItem returns only the first selected item in the list; not all of them. You learn how to access all the selected items in the next exercise. Note that in the browser, the DropDownList and List control render as a <select> element, attributes such as size and multiple, set by these controls determine the appearance and behavior of the HTML element in the browser.

The Bulletedlist control doesn't allow a user to make selections, and as such doesn't support these properties.

To see how to add items to your list control, and how to read the selected values, the following exercise guides you through creating a simple Web Form with two list controls that ask users for their favorite programming language.

# TRY OUT Working with List Controls

In this exercise you add two list controls to a page. Additionally, you add a button that, when clicked, displays the selected items as text in a Label control.

+   1. In the Demo folder, create a new Web Form named ListControls.aspx. Make sure you create a Code Behind file by checking the Place Code in Separate file.
2. Switch to Design View and drag a DropDownList from the Toolbox onto the design view of the page within the <div> element that is already present in your page.
3. Notice that as you drop the DropDownList control on the page, a pop-up menu appears that is labeled DropDownList Tasks, as shown in Figure 4-6.

![](bbox=[0.643, 0.747, 0.836, 0.863])

FIGURE 4-6