
- `supportedUsages` An array of `PointerDeviceUsage` structures that supply what's called HID (human interface device) usage information. This subject is beyond the scope of this book, so I'll refer you to the [HID Usages](HID Usages) page on MSDN for starters.

The Input Device capabilities sample in the Windows SDK retrieves this information and displays it to the screen through the code in js/pointer.js. I won't show that code here because it's just a matter of iterating through the array and building a big HTML string to dump into the DOM. In the simulator, the output appears as follows—notice that the simulator reports the presence of touch and mouse both in this case.

```
Output
(1) Pointer Device Type Touch
(1) Is Integrated true
(1) Max Contacts 5
(1) Physical Device Rect 0.0,491.3389525292969,907.086608868787
(1) Screen Rect 0.0,0.1366,768
(2) Pointer Device Type Mouse
(2) Is Integrated false
(2) Max Contacts 1
(2) Physical Device Rect 0.0,0.1366,768
(2) Screen Rect 0.0,0.1366,768
```

## Curious Forge?

Interestingly, I ran this same sample in Visual Studio's Local Machine debugger on a laptop that is definitely not touch-enabled, and yet a touch device was still reported as in the image above! Why was that? It's because I still had the Visual Studio simulator running, which adds a virtual touch device to the hardware profile. After closing the simulator completely (not just minimizing it), I got an accurate report for my laptop's capabilities. So be mindful of this if you're writing code to test for specific capabilities.

## Tried remote debugging yet?

Speaking of debugging, testing an app against different device capabilities is a great opportunity to use remote debugging in Visual Studio. If you haven't done so already, it takes only a few minutes to set up and makes it far easier to test apps on multiple machines. For details, see [Running Windows Store apps on a remote machine](Running Windows Store apps on a remote machine).

## Unified Pointer Events

For any situation where you want to directly work with touch, mouse, and stylus input, perhaps to implement parts of the touch language in this way, use the standard `pointer` events as adopted by the app host and most browsers. Art/drawing apps, for example, will use these events to track and respond to screen interaction. Remember again that pointers are a lower-level way of looking at input than gestures, which we'll see in the next section. Which input model you use depends on the kind of events you're looking to work with.

**Tip** Pointer events won't fire if the system is trying to do a manipulation like panning or zooming. To disable manipulations on an element, set the `-ms-content-zooming: none` or `-ms-touch-action: none`, and avoid using `-ms-touch-action` styles of `pan-x`, `pan-y`, `pinch-zoom`, and `manipulation`.

As with other events, you can listen to `pointer*` events on whatever elements are relevant to you, remembering again that these are translated into legacy mouse events, so you should not listen to both. The specific events are described as follows, given in the order of their typical sequencing:

- `pointerover`, `pointerenter` Pointer moved into the bounds of the element from outside; `pointerover` precedes `pointerenter`.
- `pointerdown` Pointer down occurred on the element.
- `pointermove` Pointer moved across the element, where a positive button state indicates pen hover (this replaces the Windows 8 `MSPointerHover` event). This will precede both `pointerover` and `pointerenter` when a pointer moves into an element.
- `pointerup` Pointer was released over the element. (If an element previously captured the touch, `msReleasePointerCapture` is called automatically.) Note that if a pointer is moved outside of an element and released, it will receive `pointerout` but not `pointerup`.
- `pointercancel` The system canceled a pointer event.
- `pointerout` Pointer moved out of the bounds of the element, which also occurs with an up or cancel event.
- `pointerleave` Pointer moved out of the bounds of the element or one of its descendants, including as a result of a down event from a device that doesn't support hover. This will follow `pointerout`.
- `gotpointercapture` The pointer is captured by the element.
- `lostpointercapture` The pointer capture has been lost for the element.

These are the names you use with `addEventListener`; the equivalent property names are of the form `onpointerdown`, as usual. It should be obvious that some of these events might not occur with all pointer types—touch screens, for instance, generally don't provide hover events, though some that can detect the proximity of a finger are so capable.

**Tip** If for some reason you want to prevent the translation of a `pointer*` event into a legacy mouse event, call the `eventArgs.preventDefault` method within the appropriate event handler.

The PointerEvents example provided with this chapter's companion content and shown in Figure 12-1 lets you see what's going on with all the mouse, pointer, and gesture events, selectively showing groups of events in the display.

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_627_0.png)

**FIGURE 12-1** The PointerEvents example display (screen shot cropped a bit to show detail).

Within the handlers for all of the `pointer*` events, the `eventArgs` object contains a whole roster of properties. One of them, `pointerType`, identifies the type of input: "touch", "pen", or "mouse". This property lets you implement different behaviors for different input methods, if desired (and note that these changed from integer values in Windows 8 to strings in Windows 8.1). Each event object also contains a unique `pointerId` value that identifies a stroke or a path for a specific contact point, allowing you to correlate an initial `pointerdown` event with subsequent events. When we look at gestures in the next section, we’ll also see how we use the `pointerId` of `pointerdown` to associate a gesture with a pointer.

The complete roster of properties that come with the event is actually far too much to show here, as it contains many of the usual [DOM properties] along with many pointer-related ones from an object type called `PointerEvent` (which is also what you get for `click`, `dblclick`, and `contextmenu` events starting with Windows 8.1). The best way to see what shows up is to run some code like the [Input DOM pointer event handling sample] (a canvas drawing app), set a breakpoint within a handler for one of the events, and examine the event object. The table on the following page describes some of the properties (and a few methods) relevant to our discussion here.

**Performance tips** Pointer events are best for quick responses to input, especially to touch, because they perform more quickly than gesture events. Also, avoid using an input event to render UI directly, because input events can come in much more quickly than screen refresh rates. Instead, use `requestAnimationFrame` to call your rendering function in alignment with screen refresh.

| Properties | Description |
|---|---|
| `currentPoint` | A `Windows.UI.Input.PointerPoint` object. This contains many other properties such as `PointerDevice` (a `Windows.UI.Input.PointerDevice` object, as described in “What Input Capabilities Are Present” earlier in this chapter) and one just called `properties`, which is a `Windows.UI.Input.PointerProperties`. |
| `pointerType` | The source of the event, could be “touch” or “pen” or “mouse”. You can use this to make adjustments according to input type, if necessary. |
| `pointerId` | The unique identifier of the contact. This remains the same throughout the lifetime of the pointer. If desired, you can call `Windows.Devices.Input.GetPointerDevice` with this id to obtain a `PointerDevice` that describes the input device’s capabilities, as described earlier in “What Input Capabilities Are Present?” |
| `type` | The name of the event, as in “pointerdown”. |
| `x, screenX, y, screenY` | The x- and y-coordinates of the pointer’s center point position relative to the screen. |
| `clientX, clientY` | The x- and y-coordinates of the pointer’s center point position relative to the client area of the app. |
| `offsetX, offsetY` | The x- and y-coordinates of the pointer’s center point position relative to the element. |
| `button` | Determines the button pressed by the user (on mice and other input devices with buttons). The left is 0, middle is 1, and right is 2; these values can be combined with the bitwise OR operator for chord presses (multiple buttons). |
| `ctrlKey, altKey, shiftKey` | Indicates whether certain keys were depressed when the pointer event occurred. |
| `hwTimestamp` | The timestamp (in microseconds) at which the event was received from the hardware. |
| `relatedTarget` | Provides the element related to the current event, e.g., the `pointerout` event will provide the element to which the touch is moving. This can be `null`. |
| `isPrimary` | Indicates if this pointer is the primary one in a multitouch scenario (such as the pointer that the mouse would control). |
| *Properties surfaced depending on hardware support (if not supported, these values will be 0)* | |
| `width, height` | The contact width and height of the touch point specified by `pointerId`, in CSS pixels (note that these were screen pixels in Windows 8). |
| `pressure` | Pen pressure normalized in a decimal range of 0 to 1. This is emulated for nonsensitive hardware based on button states, returning 0.5 if buttons are down, 0 otherwise. |
| `rotation` | Clockwise rotation of the cursor around its own major axis in a range of 0 to 359. |
| `tiltX` | The left-right tilt away from the normal of a transducer (typically perpendicular to the surface) in a range of -90 (left) to 90 (right). |
| `tiltY` | The forward-back tilt away from the normal of a transducer (typically perpendicular to the surface) in a range of -90 (forward/away from user) to 90 (back/toward user). |
| Properties/Methods | |
| `currentPoint` `getCurrentPoint` | Provides the `Windows.UI.Input.PointerPoint` object for the current pointer relevant to the target element (`currentPoint`) or a given element (`getCurrentPoint`). |
| `intermediatePoints` `getIntermediatePoints` | Provides the `PointerPoint` history for the current pointer relative to the target element (`intermediatePoint`) or a given element (`getIntermediatePoints`). |

It’s very instructive to run the Input DOM pointer event handling sample on a multitouch device, because it tracks each `pointerId` separately, allowing you to draw with multiple fingers simultaneously.
