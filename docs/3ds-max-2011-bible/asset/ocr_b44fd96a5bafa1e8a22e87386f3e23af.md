The Evaluate button in the Expression Controller dialog box commits the results of the expression to the current frame segment. If the expression contains an error, an alert dialog box warns you of the error. Replacing the controller with a different one can erase the animation resulting from an Expression controller.

# Managing expressions

You can use the Save and Load button to save and recall expressions. Saved expressions are saved as files with an .xpr extension. Expression files do not save variable definitions.

# Caution

**If you load a saved expression into the Expression Controller dialog box, you need to reassign all variables before you can use the loaded expression.**

# Tutorial: Creating following eyes

As a quick example, you’ll start with a simple expression. The Expression controller is very useful for setting the eye pupil objects to move along with the ball’s motion. This same functionality can be accomplished using a manipulator and wiring the parameter, but you show it with the Float Expression controller.

To make eye pupil objects follow a moving ball object, follow these steps:

+   1. Open the Following eyes.max file from the Chap 35 directory on the DVD.\
+      This file includes a face taken from a Greek model made by Viewpoint Datalabs, along with a ball that is animated to move back and forth.
+   2. Select the left eye pupil object named “pupil_l” (the right pupil has been linked to move with the left pupil), and open the Motion panel. Select the Position track, and click the Assign Controller button. Select the Position Expression controller, and click OK.\
+      The Expression Controller dialog box opens.
+   3. Create a new vector variable named **ballPos** by typing its name in the Name field, selecting the Vector option, and clicking the Create button.
+   4. With the ballPos variable selected, click the Assign to Controller button. In the Track View Pick dialog box, locate and select Objects and click the “+” to the left. Then choose Sphere01 and click the “+” to its left. Finally, choose the Position: Position XYZ, as shown in Figure 35.6, and click OK.
+   5. In the Expression pane, erase the existing expression and type the following:

```
[ -3.1 + ballPos.x/20, -2.9, 41.0 ]
```

Then click the Debug button. The Expression Debug window appears, in which you can see the variable values change as items in the scene change. With the expression complete, you can drag the Time Slider back and forth and watch the pupil follow the ball from side to side. If you’re happy with the motion, click the Evaluate button and then the Close button to exit the interface.