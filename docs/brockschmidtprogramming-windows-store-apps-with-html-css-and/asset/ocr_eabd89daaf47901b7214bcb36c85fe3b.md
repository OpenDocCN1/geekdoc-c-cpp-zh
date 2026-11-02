Invoking a header (click, tap, spacebar, or Enter key) then raises the Hub's headerInvoked event. This scenario's code picks them up as follows to navigate to subsidiary pages. The section's index and element are included in the eventArgs.detail object (pages/interactiveheaders.js).<sup>74</sup>

```
```javascript
// Inside the page control
ready: function (element, options) {
    this._hub = element.querySelector(".win-hub").winControl;
    this._onHeaderInvokedBound = this._onHeaderInvoked.bind(this);
    this._hub.addEventListener("headerinvoked", this._onHeaderInvokedBound);
},

//navigate to deeper levels by invoking interactive headers
onHeaderInvoked: function (ev) {
    var index = ev.detail.index;      // Section index
    var section = ev.detail.section;  // Section element

    //check that the correct section is invoked
    if (index === 2) {
        WinJS.Navigation.navigate("/pages/listview.html");
    }

    if (index === 3) {
        WinJS.Navigation.navigate("/pages/video.html");
    }
},

unload: function () {
    this._hub.removeEventListener("headerinvoked", this._onHeaderInvokedBound);
},
```
```

Supporting semantic zoom, which is shown in scenario 4, is nothing new—the sample (pages/semanticzoom.html) just places the Hub control as the first child of a WinJS.UI.SemanticZoom control and declares a ListView for the zoomed-out view that just navigates to the sections:

![](bbox=[0.15, 0.65, 0.5, 0.82])

<sup>74</sup> The sample actually uses `window.addEventListener`, which works only because the otherwise unhandled event bubbles up to the window level. Adding it on `this._hub` as shown in the code here is more direct.