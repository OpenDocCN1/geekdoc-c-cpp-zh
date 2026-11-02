In html/appbar-flyout.html of this sample we see the app bar button declared as follows:

```
<button data-win-control="WinJS.UI.AppBarCommand"
data-win-options="{'id':'respondButton', 'label':'Respond', 'icon':'edit', 'type':'flyout',
flyout:select('#respondFlyout') }">
```

The respondFlyout element identified here is defined earlier in html/appbar-flyout.html; note that such an element must be declared prior to the app bar to make sure it's instantiated before the app bar is created:

```
<div id="respondFlyout" data-win-control="WinJS.UI.Menu">
<button data-win-control="WinJS.UI.MenuCommand"
data-win-options="{'id':'alwaysSaveMenuItem', 'label':'Always save drafts', 'type':'toggle', 'selected':'true'}">
</button>
<hr data-win-control="WinJS.UI.MenuCommand"
data-win-options="{'id':'separator', 'type':'separator'}" />
<button data-win-control="WinJS.UI.MenuCommand"
data-win-options="{'id':'replyMenuItem', 'label':'Reply'}">
</button>
<button data-win-control="WinJS.UI.MenuCommand"
data-win-options="{'id':'replyAllMenuItem', 'label':'Reply All'}">
</button>
<button data-win-control="WinJS.UI.MenuCommand"
data-win-options="{'id':'forwardMenuItem', 'label':'Forward'}">
</button>
</div>
```

It should come as no surprise by now that the menu is just another WinJS control, WinJS.UI.Menu, where its child elements define the menu's contents. As all these elements are, once again, just elements in the DOM; their click events are wired up in js/appbar-flyout.js with the ever-present addEventListener. (By the way, the sample uses document.getElementById to obtain the elements in order to call addEventListener; it would be more efficient to use the app bar's getCommandById method instead.)

Each menu item, as you can see, is a MenuCommand object, and we'll come back to the details later— for the time being, you can see that those items have an id, a label, and a type, very similar to AppBarCommand objects.

That's pretty much all there is to it—the one added bit is that when a menu item is selected, you'll want to dismiss the menu and perhaps also the app bar (if it's not sticky). This is shown in the sample within js/appbar-flyout.js in a function called hideFlyoutAndAppBar:

```
function hideFlyoutAndAppBar() {
document.getElementById("respondFlyout").winControl.hide();
document.getElementById("appBar").winControl.hide();
}
```