```
PageControlNavigator: WinJS.Class.define(
  // Define the constructor function for the PageControlNavigator.
  function PageControlNavigator (element, options) {
    this.element = element || document.createElement("div");
    this.element.appendChild(this._createPageElement());

    this.home = options.home;

    // ...

    // Adding event listeners; addRemovableEventListener is a helper function
    addRemovableEventListener(nav, 'navigating',
      this._navigating.bind(this), false);
    addRemovableEventListener(nav, 'navigated',
      this._navigated.bind(this), false);
  }, { // ...
  // ...
```

First we see the definition of the Application namespace as a container for the PageControlNavigator class (see "Sidebar: WinJS.Namespace.define and WinJS.Class.define" later). Its constructor receives the element that contains it (the contenthost div in default.html), or it creates a new one if none is given. The constructor also receives an options object that is the result of parsing the data-win-options string of that element. The navigator then appends the page control's contents to this root element, adds listeners for the WinJS.Navigation.onnavigated event, among others.24

The navigator then waits for someone to call WinJS.Navigation.navigate, which happens in the activated handler of js/default.js, to navigate to either the home page or the last page viewed if previous session state was restored:

```
if (app.sessionState.history) {
  nav.history = app.sessionState.history;
}
args.setPromise(WinJS.UI.processAll(), then(function () {
  if (nav.location) {
    nav.history.current.initialPlaceholder = true; // Don't add first page to nav stack
    return nav.navigate(nav.location, nav.state);
  } else {
    return nav.navigate(Application.navigator.home);
  }
}));
```

Notice how this code is using the WinJS sessionState object exactly as described earlier in this chapter, taking advantage again of sessionState being automatically reloaded when appropriate.

When a navigation happens, the navigator's _navigating handler is invoked, which in turn calls WinJS.UI.Pages.render to do the loading, the contents of which are then appended as child