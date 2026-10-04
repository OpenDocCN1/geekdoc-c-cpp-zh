
brave, you can look at the file by requesting it in your browser, copying and pasting it right after the port number of your website in the browser (for example, http://localhost:50404). You can safely ignore the file, because you don't need to make any changes to it to function correctly. The WebResource.syntax is used by other controls, like the TreeView that it retrieves the images in the TreeView.

In addition to Java, you can find a CSS <style> block at the top of the page, which sets the default layout for your menu items. Among other things, it removes the bullet from that <ul> elements display and removes underlining from the <a> elements. In the Monochrome theme, you can style it using CSS.

To better integrate the Menu with the existing design of the Monochrome theme, you can style it using CSS.

## Styling the Menu Control

The Menu control exposes a number of complex style properties that enable you to change the look of items such as the main and submenu items. You can also define how these items look when they are active (selected) or when you hover your mouse over them. Each of these style properties has a number of properties for visual aspects, such as font, color, and spacing. Figure 7-7 shows the Properties for the StaticMenuStyle property, which defines the look of the main menu items that are visible when the page first loads.

Most of the properties, like BackColor, Foreground, and Font, are added to the <style> block at the top of the page that contains the menu. This makes it difficult to reuse the design in other pages or with other themes, so it's better to use CSS instead. You can see how this works.

![](img/9e033e3b9560597824f8b22941d6d8bb_288_0.png)

FIGURE 7-7

## TRY OUT Styling the Menu Control

In this exercise you add some CSS rules to the Monochrome.css file to influence the way the Menu control is styled. By default, the Menu control adds CSS classes to the menu items, such as level1 and level2, which makes it easy to apply styling at various levels in the menu.

- 1. Open Monochrome.css from the Monochrome theme folder and add the following CSS rules. You can leave out the comments placed between /* and */; they only serve to describe the purpose of the selectors. If you don't feel like typing this CSS, you can also get a copy of this file from the code download that this book and copy it into that file into yours. Remember, CSS is case sensitive, so type the selectors exactly as shown here:

```css
ul.level1 {
  /* Defines the appearance of main menu items. */
  font-size: 14px;
  font-weight: bold;
  height: 19px;
  line-height: 19px;
}
```

```css
ul.level1 .selected {
  /* Defines the appearance of active menu items. */
  background-color: #509EE7;
}
```

```css
a.level1 {
  /* Adds some white space to the left of the main menu item text.
  !!important is used to override the inline CSS that the menu generates */
  padding-left: 5px !important;
}
```

```css
a.level2 {
  /* Defines the appearance of the sub menu items. */
  background-color: #555555;
  padding-left: 8px;
}
```

```css
a.level1.hover, a.level2.hover {
  /* Defines the hover style for the main and sub items. */
  background-color: #509EE7;
}
```

- 2. Save and close the file.
- 3. Next, create the following folders and Web Forms that you'll use in this and later chapters. Use the MyBasePage template to create the new files. Also, in Markup View, give each page a meaningful title to avoid errors later.

| FOLDER | FILENAME | TITLE |
|---|---|---|
| /About | Default.aspx | About this Site |
| /About | Contact.aspx | Contact Us |
| /About | AboutUs.aspx | About Us |
| /Reviews | Default.aspx | My Favorite Reviews |
| /Reviews | All.aspx | All Reviews |
| /Reviews | AllByGenre.aspx | Reviews Grouped by Genre |

- 4. Save all changes and open the Default.aspx page from the root in your browser. Your site menu now looks a lot better and more in line with the rest of the Monochrome theme. When you hover the mouse over a main menu, the submenus appear, showing the text on a light gray background. When you hover over a submenu, its background color changes. Figure 7-8 shows the expanded Reviews menu with the hover style applied to the By Genre menu in Opera.

![](img/9e033e3b9560597824f8b22941d6d8bb_290_0.png)

FIGURE 7-8

> COMMON MISTAKES If you get an error when you navigate to one of the new pages, make sure you gave all of them a valid title. Because they all inherit from the base page, the title is checked when the page loads. If the menu hasn't been updated, press Ctrl+F5 to get a fresh copy of the sheet from server.

## How It Works

The menu control render itself as a series of `<ul>` and `<li>` elements. The menu items themselves are simple `<a> elements with a class attribute to indicate at what level they are. If you look in the HTML for the page in the browser you will see something like this:

```html
<ul class="level1">
  <li title="Go to the homepage" href="Default.aspx">HomeHome</a>
  <li title="Reviews published on this site">
    <ul class="level2">
      <li title="All Reviews Grouped by Genre">
        <ul class="level3">
          <li><a title="By Genre" href="/Reviews/AllByGenre.aspx">By Genre</a></li>
          <li><a title="All Reviews" href="/Reviews/All Reviews.aspx">All Reviews</a></li>
        </ul> <!-- Fixed closing tag in original -->
      </li>
    </li>
  </li> <!-- Other menu items go here -->
</ul>
```

Because this code is pure HTML with a few `class` attributes applied, it's easy to style this information using the CSS techniques you learned in earlier chapters. The code you added in step 1 uses a number of selectors to style individual elements of the menu. For example, the main menu items are styled as:

```css
ul.level1 {
  font-size: 14px;
  font-weight: bold;
  height: 19px;
  line-height: 19px;
}
```

This code is applied to all `<ul>` elements with a CSS class of level1, which means it's applied to all main menu items such as Home, Reviews, and About. Take a look at the first <a> element in the HTML of the menu, which represents the selected item. Notice how it has a second class called selected:

```html
<a title="To the homepage" class="level1 selected" href="/Site/Default.aspx">Home</a>
```

Selected items are then given a different color using this CSS selector:

```css
ul.level1 .selected {
  background-color: #BCD1FE;
}
```

The same principle is used for the other selectors, the pseudo :hover selector that applies to <a> elements when you hover your mouse over them:

```css
a.level1:hover, a.level2:hover {
  background-color: #509EE7;
}
```

The inclusion of !important marks this property as important the menu item.

```css
a.level1 {
  padding-left: 5px !important;
}
```

## Using the TreeView

A TreeView is capable of displaying a hierarchical list of items, similar to how the tree in Explorer looks. Items can be expanded and collapsed with the small and minus icons in front of them. This makes the TreeView an ideal tool to display the site map (although you can also use it for non-navigation purposes). The data used by the TreeView is not limited to the sitemap file, however. You can also bind it to regular XML files and create a TreeView or its items (nodes) programmatically.

The following table lists the most common properties of the TreeView. Again, the MSDN online is a good place to get a detailed overview of all available properties.

| PROPERTY | DESCRIPTION |
|---|---|
| CssClass | Enables you to set a CSS class attribute that applies to the entire control. |
| CollapseImageUrl | The image that collapses a part of the tree when clicked. The default is an icon with a minus symbol on it. |
| ExpandImageUrl | The image that expands a part of the tree when clicked. The default is an icon with a plus symbol on it. |
| CollapseImageToolTip | The tooltip that is shown when a user hovers over a collapsible menu item. |
| ExpandImageToolTip | The tooltip that is shown when a user hovers over an expandable menu item. |
| ShowExpandCollapse | Determines whether lines in the TreeView can be collapsed and expanded by clicking an image in front of them. |
| ShowLines | Determines whether lines are used to connect the individual items in the tree. |
| ExpandDepth | Determines the level at which items are expanded when first loads. The default setting is FullyExpand, which means all items in the tree are visible. Other allowed settings are numeric values to indicate the level to expand. |

To tell the TreeView which items to show, bind it to a SiteMapDataSource control, which is demonstrated next.

## TRY OUT Building a Navigation System with the TreeView Control

In this exercise, you add a TreeView control to the <nav> element, right below the Menu you created earlier, and then bind the TreeView to the same data source as the Menu. Next, you will write some code that shows either the Menu or the TreeView, depending on the active theme.

- 1. Open the master page in Markup View and just below the Menu control, add a TreeView control by dragging it from the Toolbox.
