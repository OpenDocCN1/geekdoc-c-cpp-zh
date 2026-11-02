As another reference point, refer to the [Adaptive layout with CSS sample](#), which really takes the same approach as the Grid App project template, relying on controls to resize themselves. In the sample, you will see that the app isn’t doing any direct calculations based on view size.

**Hint** If you have an adaptive layout and want a background image specified in CSS to scale to its container (rather than being repeated), style `background-size` to either `contain` or `100% 100%`.

Finally, let me again recommend the [Guidelines for scaling to screens](#) topic in the documentation, which goes into many more design questions, such as:

+   - Which regions of a view are fixed and which are adaptive?
+   - How do adaptive regions make use of available space, including the directions in which that region adapts?
+   - How do adaptive and fixed regions relate in the wireframe?
+   - How does the view’s layout overall make use of space—that is, how does whitespace itself expand so that content doesn’t become too dense? This can mean collapsing some areas of the UI in narrower views to lighten the density when there’s less room.
+   - How does the view make use of multicolumn text?

Answering these sorts of questions will help you understand how the layout should adapt.

# # Handling Orientations

If you’ve worked with any kind of accelerometer-equipped device, you know that one of the most natural things to do is rotate it 90 degrees in some direction to reorient an app. On other systems, the user can change orientation manually through PC Settings > PC & Devices > Display > Orientation:

![](bbox=[0.143, 0.628, 0.287, 0.767])

When this happens, an app receives a `window.onresize` event and is expected to update its view accordingly. A key point here is that landscape orientations support multiple side-by-side views, but portrait does not. In fact, Windows locks the orientation when you have multiple apps showing side by side. To switch to portrait, make sure the app you want is running full screen by itself.

If you structure your CSS appropriate for different view states and handle resize events as needed, you typically don’t care about the actual physical orientation of the device—you care only about the