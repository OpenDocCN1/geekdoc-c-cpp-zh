the mouse over a main menu, the submenus appear, showing the text on a light gray background. When you hover over a submenu, its background color changes. Figure 7-8 shows the expanded Reviews menu with the hover style applied to the By Genre menu in Opera.

![](bbox=[0.166, 0.178, 0.814, 0.381])

FIGURE 7-8

> COMMON MISTAKES If you get an error when you navigate to one of the new pages, make sure you gave all of them a valid title. Because they all inherit from the base page, the title is checked when the page loads. If the menu hasn't been updated, press Ctrl+F5 to get a fresh copy of the sheet from server.

# How It Works

The menu control render itself as a series of `<ul>` and `<li>` elements. The menu items themselves are simple `<a>` elements with a class attribute to indicate at what level they are. If you look in the HTML for the page in the browser you will see something like this:

```
<ul class="level1">
  <li title="Go to the homepage" href="Default.aspx">Home</a>
  <li title="Reviews published on this site">
    <ul class="level2">
      <li title="All Reviews Grouped by Genre">
        <ul class="level3">
          <li><a title="By Genre" href="/Reviews/AllByGenre.aspx">By Genre</a></li>
          <li><a title="All Reviews" href="/Reviews/All Reviews.aspx">All Reviews</a></li>
        </ul>
      </li>
    </li>
  </li> <!-- Other menu items go here -->
</ul>
```

Because this code is pure HTML with a few `class` attributes applied, it's easy to style this information using the CSS techniques you learned in earlier chapters. The code you added in step 1 uses a number