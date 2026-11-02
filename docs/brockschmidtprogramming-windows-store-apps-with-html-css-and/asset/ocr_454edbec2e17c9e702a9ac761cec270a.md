Scenario 6 of the HTML AppBar control sample provides an example, though in this case the result is not something I'd recommend for your own app design: it creates a page header and a backbutton (html/custom-layout.html):

```
```html
<div id="customLayoutAppBar" data-win-control="WinJS.UI.AppBar" aria-label="Navigation Bar"
    data-win-options="{layout:'custom', placement:'top'}">
    <header aria-label="Navigation bar" role="banner">
        <button id="cmdBack" class="win-backbutton" aria-label="Back">
        </button>
        <div class="titleArea">
            <h1 class="win-type-xx-large" tabindex="0">
                Page Title</h1>
        </div>
    </header>
</div>
```
```

The result of this example is as follows (focus rectangles included!):

![](bbox=[0.141, 0.376, 0.573, 0.456])

The point, though, is that a custom layout app bar is essentially nothing more than a container for whatever arbitrary content you want to place there, and that content is entirely under your control. The app bar in these cases is just taking care of showing and hiding that content at appropriate times and firing relevant events.

A custom layout app bar is typically what you'd use to implement a completely custom nav bar, using a `placement` of top. Before going down that road, however, let's check out the WinJS NavBar control that provides a lot of functionality in this department already.

# ## Nav Bar Features

Navigation with page controls, as we know from Chapter 3, is just a matter of calling `WinJS.Navigation.navigate` at the appropriate times with the appropriate target page. Assuming there's some piece of code like the `PageControlNavigator` to pick up the navigation events and take care of the page loading, an app can wire whatever controls it sees fit to navigate calls. This includes a top placement app bar that can have whatever design you would like to use, typically with a custom layout. With the flat navigation pattern, this app bar can contain just a horizontally-panning `ListView` (using `ListLayout`) with the relevant pages. With a hierarchical system, on the other hand, the implementation gets trickier as you want to have one list that opens up a secondary list and potentially has even a third level of options.

Fortunately, the WinJS NavBar control steps in to support this pattern, which you can see demonstrated in the inbox Travel app. Let's see some of the variations to understand what the control provides for us. For starters, here's the nav bar at full width: