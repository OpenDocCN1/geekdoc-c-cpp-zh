Fortunately, there is nothing special about handling keyboard input in a Windows Store app, but a little goes a long way. Drawing from Implementing keyboard accessibility, here's a summary:

+   - Process `keydown`, `keyup`, and `keypress` events as you already know how to do, especially for implementing special key combinations. See "Standard Keystrokes" later in this section for a quick run-down of typical mappings.
+   - Have `tabindex` attributes on interactive elements that should be tab stops. Avoid adding `tabindex` to noninteractive elements as this will interfere with screen readers.
+   - Have `accesskey` attributes on those elements that should have keyboard shortcuts.
+   - Call the DOM focus API on whatever element should be the default.
+   - Take advantage of the keyboard support that already exists in built-in controls, such as the App Bar.

As an example, the Here My Am! we've been working with in this book has been updated in this chapter's companion content with full keyboard support. This was mostly a matter of adding `tabindex` to a few elements, setting focus to the image area, and picking up `keydown` events on the `img` elements for the Enter key and spacebar where we've already been handling `click`. Within those `keydown` events, note that it's helpful to use the `WinJS.Utilities.Key` enumeration for comparing key codes:

```
```javascript
var key = WinJS.Utilities.Key;
var image = document.getElementById("photo");

image.addEventListener("keydown", function (e) {
    if (e.keyCode == key.enter || e.keyCode==key.space) {
        image.click();
    }
});
```
```

All this works for both the physical keyboard as well as the soft keyboard. Case closed? Well, not entirely. There are two special concerns with the soft keyboard: how to make it appear, and the effect of its appearance on app layout. At the end of this section I'll also provide a quick run-down of standard keystrokes for app commands.

# ## Soft Keyboard Appearance and Configuration

The appearance of the soft keyboard happens for one reason and one reason only: the user touches a text input element or an element with the `contenteditable="true"` attribute (such as a `div` or `canvas`). There isn't an API to make the keyboard appear, nor will it appear when you click in such an element with the mouse or a stylus, or tab to it with a physical keyboard.

The configuration of the keyboard is also sensitive to the type of input control. We can see this through scenario 2 of the Input Touch keyboard text input sample, where `html/ScopedViews.html` contains a bunch of `input` controls (surrounding table markup omitted), which appear as shown in Figure 12-5: