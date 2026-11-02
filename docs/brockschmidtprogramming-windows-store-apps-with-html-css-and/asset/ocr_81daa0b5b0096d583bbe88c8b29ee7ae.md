![](bbox=[0.141, 0.075, 0.887, 0.231])

**FIGURE 12-6** When the soft keyboard appears, Windows will automatically slide the app page up to make sure the input field isn’t obscured.

Although this can be the easiest solution to this particular concern, it's not always ideal. Fortunately, you can do something more intelligent if you'd like by listening to the hiding and showing events of the `Windows.UI.ViewManagement.InputPane` object and adjust your layout directly. Code for doing this can be found in the—are you ready for this?—*Responding to the appearance of the on-screen keyboard sample*.^91 Adding listeners for these events is simple (see the bottom of `js/keyboardPage.js`, which also removes the listeners properly):

```
```javascript
var inputPane = Windows.UI.ViewManagement.InputPane.getForCurrentView();
inputPane.addEventListener("showing", showingHandler, false);
inputPane.addEventListener("hiding", hidingHandler, false);
```
```

Within the showing event handler, the `eventArgs.occludedRect` object (a `Windows.Foundation.Rect`) gives you the coordinates and dimensions of the area that the soft keyboard is covering. In response, you can adjust whatever layout properties are applicable and set the `eventArgs.ensuredFocusedElementInView` property to true. This tells Windows to bypass its automatic offset behavior:

```
```javascript
function showingHandler(e) {
    if (document.activeElement.id === "customHandling") {
        keyboardShowing(e.occludedRect);

        // Be careful with this property. Once it has been set, the framework will
        // do nothing to help you keep the focused element in view.
        e.ensuredFocusedElementInView = true;
    }
}
```
```

^91 And although you might think this is the second longest JavaScript sample name in the Windows SDK, it actually runs a mere fifth. In fourth place is the *Input Gestures and manipulations with GestureRecognizer* sample, which we’ll see later on. The bronze goes to the *Using requestAnimationFrame for power efficient animations* sample, and the *Unselectable content areas with -ms-user-select CSS attribute* sample, which we’ve seen, gets the silver. And in first place? The *Windows Runtime in-process component authoring with proxy/stub generation* sample! I don’t mind such long names, however—I’m delighted that there we have such an extensive set of great samples to draw from.