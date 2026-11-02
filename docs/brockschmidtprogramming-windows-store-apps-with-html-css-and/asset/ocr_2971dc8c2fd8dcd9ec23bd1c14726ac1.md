# Edge Gestures

As we saw in Chapter 9, “Commanding UI,” you don’t need to do anything special for commands on the app bar or navigation bar to appear: Windows automatically handles the edge swipe from the top and bottom of your app, along with right-click, Win+Z, and the context menu key on the keyboard. That said, you can detect when these events happen directly by listening for the starting, completed, and canceled events on the Windows.UI.Input.EdgeGesture object.

```
var edgeGesture = Windows.UI.Input.EdgeGesture.getForCurrentView();
edgeGesture.addEventListener("starting", onStarting);
edgeGesture.addEventListener("completed", onCompleted);
edgeGesture.addEventListener("canceled", onCanceled);
```

The completed event fires for all input types; starting and canceled occur only for touch. Within these events, the eventArgs.kind property contains a value from the EdgeGestureKind enumeration that indicates the kind of input that invoked the event. The starting and canceled events will always have the kind of touch, obviously, whereas completed can be any touch, keyboard, or mouse:

```
function onCompleted(e) {
    // Determine whether it was touch, mouse, or keyboard invocation
    if (e.kind === Windows.UI.Input.EdgeGestureKind.touch) {
        id("ScenarioOutput").innerText = "Invoked with touch.";
    }
    else if (e.kind === Windows.UI.Input.EdgeGestureKind.mouse) {
        id("ScenarioOutput").innerText = "Invoked with right-click.";
    }
    else if (e.kind === Windows.UI.Input.EdgeGestureKind.keyboard) {
        id("ScenarioOutput").innerText = "Invoked with keyboard.";
    }
}
```

The code above is taken from scenario 1 of the Edge gesture invocation sample (js/edgeGestureEvents.js). In scenario 2, the sample also shows that you can prevent the edge gesture event from occurring for a particular element by handling its contextmenu event and calling eventArgs.preventDefault in your handler. It does this for one element on the screen such that right-clicking that element with the mouse or pressing the context menu key when that element has the focus will prevent the edge gesture events:

```
document.getElementById("handleContextMenuDiv").addEventListener("contextmenu", onContextMenu);

function onContextMenu(e) {
    e.preventDefault();
    id("ScenarioOutput").innerText = "The ContextMenu event was handled. The EdgeGesture event will not fire.";
}
```

Note that this method has no effect on edge gestures via touch and does not affect the Win+Z key combination that normally invokes the app bar. It’s primarily to show that if you need to handle the