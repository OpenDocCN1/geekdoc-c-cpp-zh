```
function go() {
    flyout.removeEventListener('beforehide', go);
    navbarCommand.splitOpened = false;
}
});
```

Notice the use of the flyouts beforehide event here to make sure the command's splitOpened flag is set to false when the flyout is dismissed. This is necessary because the flyout can be dismissed independently of the split button.

Because showing and hiding the flyout is under your complete control, the splitToggle event is also where you can perform animations for your subsidiary navigation controls.

# Nav Bar Styling

In the previous section, as we looked at NavBar examples from both the Travel app and the HTML NavBar control sample, you'll have easily noticed some styling differences other than the basic light or dark theme (which you can switch in the sample, by the way). The Travel app, for example, definitely uses its own template for the top-level commands and adds some color theming along the top and in the page indicators:

![](bbox=[0.15, 0.62, 0.6, 0.82])

These appearances are easy to control, as the NavBar, NavBarContainer, and NavBarCommand classes all provide the usual win-* style hooks for their different parts.

**Hint** As with the app bar, to keep it visible in Blend for Visual Studio, right-click its element and select Activate NavBar, or activate it in Interactive Mode and switch back to Design Mode. You can also make the nav bar sticky or add a call to show in an appropriate place, if you need to keep it visible within Visual Studio's debugger and DOM Explorer.

The NavBar as a whole has just one relevant class, win-navbar, that's added to the control's root element. This is where you can add something like the Travel app's top color border—try this in css/scenario1.cs: