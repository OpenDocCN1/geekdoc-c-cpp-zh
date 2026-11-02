
When you're using the recognizer directly, in other words, you'll be listening for pointer* events, feeding them to the recognizer, and then listening for and acting on the recognizer's specific events as above rather than the MSGesture* events that come out of the default recognizer configured by the MSGesture object.

Again, refer to the documentation on Windows.UI.Input.GestureRecognizer for all the details and refer to the sample for some bits of code. As one extra example, here's a snippet to capture a small horizontal motion using the manipulationTranslateX setting:

```javascript
var recognizer = new Windows.UI.Input.GestureRecognizer();
recognizer.gestureSettings = Windows.UI.Input.GestureSettings.manipulationTranslateX;
var DELTA = 10;

myElement.addEventListener('pointerdown', function (e) {
    recognizer.processDownEvent(e.getCurrentPoint(e.pointerId));
});
myElement.addEventListener('pointerup', function (e) {
    recognizer.processUpEvent(e.getCurrentPoint(e.pointerId));
});
myElement.addEventListener('pointermove', function (e) {
    recognizer.processMoveEvents(e.getIntermediatePoints(e.pointerId));
});

// Remember removeEventListener as needed for this event
recognizer.addEventListener('manipulationcompleted', function (args) {
    var pt = args.cumulative.translation;
    if (pt.x < -DELTA) {
        // move right
    }
    else if (pt.x > DELTA) {
        // move left
    }
});
```

Beyond the recognizer, do note that you can always go the low-level route and do your own processing of pointer* events however you want, completely bypassing the gesture recognizer. This would be necessary if the configurations allowed by the recognizer object don't accommodate your specific need. At the same time, now is a good opportunity to re-read “Sidebar: Creating Completely New Gestures?” at the end of the earlier section on the touch language. It addresses a few of the questions about when and if custom gestures are really needed.

## Keyboard Input and the Soft Keyboard

After everything to do with touch and other forms of input, it seems almost anticlimactic to consider the humble keyboard. Yet of course the keyboard remains utterly important for textual input, whether it's a physical keyboard or the on-screen “soft” keyboard. It is especially important for accessibility as well, as some users are physically unable to use a mouse or other devices. In fact, the App certification requirements (section 3.5) make keyboard input mandatory.

Fortunately, there is nothing special about handling keyboard input in a Windows Store app, but a little goes a long way. Drawing from Implementing keyboard accessibility, here's a summary:

- Process `keydown`, `keyup`, and `keypress` events as you already know how to do, especially for implementing special key combinations. See "Standard Keystrokes" later in this section for a quick run-down of typical mappings.
- Have `tabindex` attributes on interactive elements that should be tab stops. Avoid adding `tabindex` to noninteractive elements as this will interfere with screen readers.
- Have `accesskey` attributes on those elements that should have keyboard shortcuts.
- Call the DOM focus API on whatever element should be the default.
- Take advantage of the keyboard support that already exists in built-in controls, such as the App Bar.

As an example, the Here I Am! we've been working with in this book has been updated in this chapter's companion content with full keyboard support. This was mostly a matter of adding `tabindex` to a few elements, setting focus to the image area, and picking up `keydown` events on the `img` elements for the Enter key and spacebar where we've already been handling `click`. Within those `keydown` events, note that it's helpful to use the `WinJS.Utilities.Key` enumeration for comparing key codes:

```javascript
var key = WinJS.Utilities.Key;
var image = document.getElementById("photo");

image.addEventListener("keydown", function (e) {
    if (e.keyCode == key.enter || e.keyCode==key.space) {
        image.click();
    }
});
```

All this works for both the physical keyboard as well as the soft keyboard. Case closed? Well, not entirely. There are two special concerns with the soft keyboard: how to make it appear, and the effect of its appearance on app layout. At the end of this section I'll also provide a quick run-down of standard keystrokes for app commands.

## Soft Keyboard Appearance and Configuration

The appearance of the soft keyboard happens for one reason and one reason only: the user touches a text input element or an element with the `contenteditable="true"` attribute (such as a `div` or `canvas`). There isn't an API to make the keyboard appear, nor will it appear when you click in such an element with the mouse or a stylus, or tab to it with a physical keyboard.

The configuration of the keyboard is also sensitive to the type of input control. We can see this through scenario 2 of the Input Touch keyboard text input sample, where `html/ScopedViews.html` contains a bunch of `input` controls (surrounding table markup omitted), which appear as shown in Figure 12-5:

```html
<input type="url" name="url" id="url" size="50" />
<input type="email" name="email" id="email" size="50" />
<input type="password" name="password" id="password" size="50" />
<input type="text" name="text" id="text" size="50" />
<input type="number" name="number" id="number" />
<input type="search" name="search" id="search" size="50" />
<input type="tel" name="tel" id="tel" size="50" />
```

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_641_0.png)

**FIGURE 12-5** The soft keyboard appears when you touch an input field, as shown in the Input Touch keyboard text input sample (scenario 2). The exact layout of the keyboard changes with the type of input field.

What’s shown in Figure 12-5 is the default keyboard. If you tap in the Search field, you get pretty much the same view except the Enter key turns into Search. For the Email field, it’s much like the default view except you get @ and .com keys to either side of the spacebar.

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_641_1.png)

The URL keyboard is the same except a few keys change and Enter turns into Go:

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_642_0.png)

For passwords you get a key to hide keypresses (to the left of the spacebar), which prevents a visible animation from happening on the screen—a very important feature if you're recording videos!

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_642_1.png)

And finally, the Number and Telephone fields bring up a number-oriented view:

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_642_2.png)

In all of these cases, the key on the lower right (whose icon looks a bit like a keyboard), lets you switch to other keyboard layouts:

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_642_3.png)

The options here are the normal (wide) keyboard, the split keyboard, a handwriting recognition panel, and a key to dismiss the soft keyboard entirely. Here's what the default split keyboard and handwriting panels look like:

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_643_0.png)

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_643_1.png)

This handwriting panel for input is simply another mode of the soft keyboard: you can switch between the two, and your selection sticks across invocations. (For this reason, Windows does not automatically invoke the handwriting panel for a pen pointer, because the user may prefer to use the soft keyboard even with the stylus.)

And although the default keyboard appears for text input controls, those controls also provide text suggestions for touch users. This is demonstrated in scenario 1 of the sample and shown below:

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_643_2.png)

Control using the Windows 8.1 Touch Keyboard, spellchecking and text suggestion services will be a

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_643_3.png)

## Adjusting Layout for the Soft Keyboard

The second concern with the soft keyboard (no, I didn’t forget!) is handling layout when the keyboard might obscure the input field with the focus.

When the soft keyboard or handwriting panel appears, the system will try to make sure the input field is visible by scrolling the page content if it can. This means that it just sets a negative vertical offset to your entire page equal to the height of the soft keyboard. For example, on a 1366x768 display (as in the simulator), touching the Telephone Input Type field in scenario 2 of the [Input_Touch_keyboard_text_input_sample](#) will slide the whole page upward, as shown in Figure 12-6 and also [Video 12-3](#).
