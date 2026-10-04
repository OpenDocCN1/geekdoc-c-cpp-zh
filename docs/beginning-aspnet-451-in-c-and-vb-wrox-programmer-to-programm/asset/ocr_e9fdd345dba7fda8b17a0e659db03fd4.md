selectors to style individual elements of the menu. For example, the main menu items are styled as:

```
ul.level {
  font-size: 14px;
  font-weight: bold;
-height: 19px;
  line-height: 19px;
}
```

This code is applied to all <ul> elements with a CSS class of level1, which means it's applied to all main menu items such as Home, Reviews, and About. Take a look at the first <a> element in the HTML of the menu, which represents the selected item. Notice how it has a second class called selected:

```
<a title="To the homepage" class="level1 selected" href="/Site/Default.aspx">Home</a>
```

Selected items are then given a different color using this CSS selector:

```
ul.level .selected {
  background-color: #BCD1FE;
}
```

The same principle is used for the other selectors, the pseudo :hover selector that applies to <a> elements when you hover your mouse over them:

```
a.level:hover, a.level2:hover {
  background-color: #BCD1FE;
}
```

To override some of the Menu control adds to the top of the page, the CSS rule for the static menu items looks like this:

```
a.level {
  padding-left: 5px !important;
}
```

The inclusion of !important marks this property as more important than the inline style targeting the same menu item. Without !important, your menu item has a tiny bit of padding on the left.

The Menu control in horizontal mode is for the Monochrome theme, because it features a horizontal navigation bar. For the DarkGrey you can use the same Menu and set its Orientation to Vertical. This creates a vertical menu with the main items stacked on top of each other, whereas the submenus will fold out to the right of the main menus. Instead of the Menu control, you can also use a TreeView control to display a hierarchical overview of the site map. This is discussed next.

# Using the TreeView Control

A TreeView is capable of displaying a hierarchical list of items, similar to how the tree in Windows Explorer looks. Items can be expanded and collapsed with the small plus and minus icons in front of