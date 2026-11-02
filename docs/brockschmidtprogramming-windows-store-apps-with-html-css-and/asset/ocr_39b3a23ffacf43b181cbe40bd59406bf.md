to be marked for strict processing. The constructor is automatically marked through WinJS.Class.define, but the event handler needs extra treatment: we place the function in a namespace (to make it globally visible) and use WinJS.UI.eventHandler to do the marking:

```
    WinJS.Namespace.define("CalendarDemo", {
        dateselected: WinJS.UI.eventHandler(function (e) {
            document.getElementById("message").innerText = JSON.stringify(e.detail) + " selected";
        })
    });
```

Again, if you forget to mark the function in this way, the control won't be instantiated at all. (Remove the WinJS.UI.eventHandler wrapper to see this.)

To demonstrate creating a control outside of markup, the control on the right of Figure 5-9 is created as follows, within the calendar2 div:

```
    //Because we're creating this calendar in code, we're independent of WinJS.UI.processAll.
    var element = document.getElementById("calendar2");

    //Because we're providing an element, this will be automatically added to the DOM.
    var calendar2 = new Controls.Calendar(element);

    //Because this handler isn't part of markup processing, it doesn't need to be marked.
    calendar2.ondateselected = function (e) {
        document.getElementById("message").innerText = JSON.stringify(e.detail) + " selected";
    }
```

There you have it!

**Note** For a control you really intend to share with others, you'll want to include the necessary comments that provide metadata for IntelliSense. See the "Sidebar: Helping Out IntelliSense" in Chapter 3 for more details. You'll also want to make sure that the control fully supports considerations for accessibility and localization, as discussed in Chapter 19.

# # Custom Controls in Blend

Blend is an excellent design tool for working with controls directly on the artboard, so you might be wondering how custom controls integrate into that story.

First, because custom controls are just elements in the DOM, Blend works with them like all other parts of the DOM. Try loading the Calendar Control example into Blend to see for yourself.

Next, a control can determine if it's running inside Blend's design mode if the Windows.ApplicationModel.DesignMode.designModeEnabled property is true. One place where this is very useful is when handling resource strings. We won't cover resources in full until Chapter 19, but it's important to know here that resource lookup through the data-win-res attribute works just fine in design mode but not through Windows.ApplicationModel.Resources.ResourceLoader (it throws exceptions). If you run into this, you can use the design-mode flag to just provide a suitable default instead of doing the lookup.