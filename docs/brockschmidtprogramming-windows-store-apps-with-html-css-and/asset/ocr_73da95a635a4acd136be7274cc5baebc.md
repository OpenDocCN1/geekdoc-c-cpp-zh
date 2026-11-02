Click the Switch To Fixed Width button, and you'll see that at certain view widths you get a gap on the right side (or left in right-to-left languages):

![](bbox=[0.15, 0.15, 0.8, 0.35])

If you size the view all the way down to 500px (and it must be 500px, because the manifest isn't set for anything smaller!), the sample changes the layout to vertical with the following result:

![](bbox=[0.2, 0.46, 0.55, 0.62])

As for implementing additional levels of navigation hierarchy, this is where we make use of the splitButton option for a command along with the splitToggle event on the container. As shown in scenario 6, a command with splitButton: true (html/6-UseSplitButton.html):

```
<div data-win-control="WinJS.UI.NavBarCommand" data-win-options="{ label: 'Favorite', icon: 'favorite' , splitButton: 'true' }"></div>
```

appears with a down arrow (if in the closed state, left) or an up arrow (if in the open state, right):

![](bbox=[0.2, 0.81, 0.8, 0.88])

By itself, a split button just makes this one visual change when you invoke it, updates its splitOpen property, and—and as a result—causes its container to fire a splitToggle event. This latter event is then where you then show or hide whatever additional controls you want to attach to it. Note that I didn't specifically say a NavBarContainer—though you'll probably want to use a NavBarContainer to implement the expected UI pattern, this is not required by any means.

The key here is to make those other controls appear as an overlay within the NavBar, which is exactly what the generic WinJS.UI.Flyout control is meant for (and which we'll learn about right after