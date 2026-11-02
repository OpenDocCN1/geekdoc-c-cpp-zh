**Tip** Pointer events won't fire if the system is trying to do a manipulation like panning or zooming. To disable manipulations on an element, set the `-ms-content-zooming: none` or `-ms-touch-action: none`, and avoid using `-ms-touch-action` styles of `pan-x`, `pan-y`, `pinch-zoom`, and `manipulation`.

As with other events, you can listen to `pointer*` events on whatever elements are relevant to you, remembering again that these are translated into legacy mouse events, so you should not listen to both. The specific events are described as follows, given in the order of their typical sequencing:

+   - `pointerover`, `pointerenter` Pointer moved into the bounds of the element from outside; `pointerover` precedes `pointerenter`.
+   - `pointerdown` Pointer down occurred on the element.
+   - `pointermove` Pointer moved across the element, where a positive button state indicates pen hover (this replaces the Windows 8 `MSPointerHover` event). This will precede both `pointerover` and `pointerenter` when a pointer moves into an element.
+   - `pointerup` Pointer was released over the element. (If an element previously captured the touch, `msReleasePointerCapture` is called automatically.) Note that if a pointer is moved outside of an element and released, it will receive `pointerout` but not `pointerup`.
+   - `pointercancel` The system canceled a pointer event.
+   - `pointerout` Pointer moved out of the bounds of the element, which also occurs with an up or cancel event.
+   - `pointerleave` Pointer moved out of the bounds of the element or one of its descendants, including as a result of a down event from a device that doesn't support hover. This will follow `pointerout`.
+   - `gotpointercapture` The pointer is captured by the element.
+   - `lostpointercapture` The pointer capture has been lost for the element.

These are the names you use with `addEventListener`; the equivalent property names are of the form `onpointerdown`, as usual. It should be obvious that some of these events might not occur with all pointer types—touch screens, for instance, generally don't provide hover events, though some that can detect the proximity of a finger are so capable.

**Tip** If for some reason you want to prevent the translation of a `pointer*` event into a legacy mouse event, call the `eventArgs.preventDefault` method within the appropriate event handler.

The PointerEvents example provided with this chapter's companion content and shown in Figure 12-1 lets you see what's going on with all the mouse, pointer, and gesture events, selectively showing groups of events in the display.