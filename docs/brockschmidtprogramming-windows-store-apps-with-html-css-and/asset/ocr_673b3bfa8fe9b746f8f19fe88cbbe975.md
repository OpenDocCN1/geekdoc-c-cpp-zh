Now let's look at the body of default.html (omitting the standard header and a commented-out AppBar control):

```
```html
<body>
    <div id="contenthost" data-win-control="Application.PageControlNavigator"
         data-win-options="{home: '/pages/home/home.html'}"></div>
</body>
```
```

All we have here is a single container div named contenthost (it can be whatever you want), in which we declare the Application.PageControlNavigator as a custom WinJS control. (This is the purpose of data-win-control and data-win-options, as we'll see in Chapter 5.) With this we specify a single option to identify the first page control it should load (/pages/home/home.html). The PageControlNavigator will be instantiated within our activated handler's call to WinJS.UI.processAll.

Within home.html we have the basic markup for a page control. Below is what the Navigation App template provides as a home page by default, and it's pretty much what you get whenever you add a new page control from the item template (with different filenames, of course):

```
```html
<!DOCTYPE html>
<html>
<head>
    <!-- ... typical HTML header and WinJS references omitted -->
    <link href="/css/default.css" rel="stylesheet">
    <link href="/pages/home/home.css" rel="stylesheet">
    <script src="/pages/home/home.js"></script>
</head>
<body>
    <!-- The content that will be loaded and displayed. -->
    <div class="fragment homepage">
        <header aria-label="Header content" role="banner">
            <button data-win-control="WinJS.UI.BackButton"></button>
            <h1 class="titlearea win-type-ellipsis">
                <span class="pagetitle">Welcome to NavApp!</span>
            </h1>
        </header>
        <section aria-label="Main content" role="main">
            <p>Content goes here.</p>
        </section>
    </div>
</body>
</html>
```
```

The div with *fragment* and *homepage* CSS classes, along with the header, creates a page with a standard silhouette and a WinJS.UI.BackButton control that automatically wires up keyboard, mouse, and touch events and again keeps itself hidden when there's nothing to navigate back to. (Isn't that considerate of it!) All you need to do is customize the text within the *h1* element and the contents within *section*, or just replace the whole smash with the markup you want. (By the way, even though the WinJS files are referenced in each page control, they aren't actually reloaded; they exist here to allow you to edit a standalone page control in Blend.)