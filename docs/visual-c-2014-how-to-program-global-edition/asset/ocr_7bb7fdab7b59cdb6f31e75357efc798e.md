discussed in Section 14.6). Anchoring places controls a fixed distance from the sides of the container. For example, if the user expects a control to appear in a particular corner of the app, anchoring ensures that the control will be in that corner—even if the user resizes the Form. Docking attaches a control to a container such that the control stretches across an edge or fills an entire area. For example, a control as a status bar typically should remain at the bottom of the Form and stretch across the entire bottom of Form, regardless of the Form's width. When the part resized, the docked control resizes as well.

# Anchoring Demonstration

When a window (or other type of container like a Pane) is resized so that the distance from the sides to which they're anchored does not vary. By default, most controls are anchored to the top-left corner of the Form. To see the effects of anchoring a control, create a simple Windows Forms app that contains two Buttons. Anchor one to the right and bottom sides by setting the Anchor property as shown in Fig. 14.12. Leave the other with its default anchoring (top, left). Execute the app and enlarge the Form. The Button anchored to the bottom-right corner is always the same distance from the bottom right (Fig. 14.13). The other control stays its original distance from the top left.

![](bbox=[0.196, 0.477, 0.857, 0.693])

Fig. 14.12 | Manipulating the Anchor property of a control.

Before resizing

After resizing

![](bbox=[0.147, 0.777, 0.857, 0.903])

Fig. 14.13 | Anchoring demonstration.