# Part XII: MAXScript and Plug-Ins

+   - **Absolute transform assignments:** This tells the Macro Recorder that any transformations you make are not relative to an object's current position or orientation. For example, if you move a sphere from (0,0,0) to (10,0,0), the Macro Recorder writes MAXScript that says, “Move the object to (10,0,0).”
+   - **Relative transforms operations:** Use this option to have the Macro Recorder apply transformations relative to an object's current state. For example, if you move a sphere from (0,0,0) to (10,0,0), the Macro Recorder says, “Move the object +10 units in the X-direction from its current location.”
+   - **Explicit subobject sets:** If you choose this option and then record a script that manipulates a set of subobjects, running the script again always manipulates those same subobjects, even if you have other subobjects selected when you run the script again.
+   - **Selection-relative subobject sets:** This tells the Macro Recorder that you want the script to operate on whatever subobjects are selected when you run the script.
+   - **Show command panel switchings:** This option tells the Macro Recorder whether or not to write MAXScript for actions that take place on the Command Panel.
+   - **Show tool selections:** If this option is selected, the Macro Recorder records MAXScript to change to different tools.
+   - **Show menu item selections:** This option tells the Macro Recorder whether or not you want it to generate MAXScript for menu items you select while recording your script.

# Tutorial: Recording a simple script

In this tutorial, you’ll create a simple script that squashes whatever object you have selected and turns it purple.

To create a script using the Macro Recorder, follow these steps:

+   1. Open the Purple pyramid.max file from the Chap 49 directory on the DVD. This file includes a simple pyramid object.
+   2. With the pyramid object selected, choose MAXScript ⇨ MAXScript Listener (or press F11) to open the MAXScript Listener window.
+   3. In the Listener window, open the MacroRecorder menu and make sure that all the options are set to the relative and not the absolute object settings, thereby telling the script to work on any selected object instead of always modifying the same object.
+   4. Returning to the MacroRecorder menu, select Enable. The Macro Recorder is now on and ready to start writing MAXScript. Minimize the Macro Recorder window (or at least move it out of the way so you can see the other viewports).
+   5. Dock the MAXScript Listener window to the Left viewport by right-clicking the viewport name and choosing Views ⇨ Extended ⇨ MAXScript Listener. Now you can keep things out of the way while you work.
+   6. With the Pyramid01 object selected, choose Modifiers ⇨ Parametric Deformers ⇨ XForm to add an XForm modifier to the object.
+   7. Select the non-uniform scale tool and restrict it to the Y-axis. Right-click anywhere in the Front viewport to make it active (if it’s not already), and then drag the Y-axis gizmo downward to squash the pyramid.
+   8. In the Modify panel, click the color swatch next to the object name field to open the Object Color dialog box. Pick one of the purple colors, and click OK.