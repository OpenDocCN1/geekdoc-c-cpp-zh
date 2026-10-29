# FIGURE 21.8

The Trajectories rollout in the Motion panel enables you to see the animation path as a spline.

![](bbox=[0.02, 0.24, 0.8, 0.68])

For more control over the trajectory path, you can convert the trajectory path to a normal editable spline with the Convert To button. You can also convert an existing spline into a trajectory with the Convert From button.

To use the Convert From button, select an object, click the Convert From button, and then click a spline path in the scene. This creates a new trajectory path for the selected object. The first key of this path is placed at the spline's first vertex, and the final key is placed as the spline's final vertex position. Additional keys are spaced out along the spline based on the spline's curvature as determined by the Samples value listed in the Sample Range group. All these new keys are roughly spaced between the Start and End times, but smaller Bezier handles result in more closely packed keys.

Click the Collapse button at the bottom of the Trajectories rollout to reduce all transform keys into a single editable path. You can select which transformations to collapse, including Position, Rotation, and Scale, using the options under the Collapse button. For example, an object with several Controllers assigned can be collapsed, thereby reducing the complexity of all the keys.

# Note

If you collapse all keys, you cannot alter their parameters via the controller rollouts.

The Views menu includes an option to Show Key Times. The Show Key Times command displays frame numbers along the trajectory path where every animation key is located. Enabling this option displays the frame numbers next to any key along a trajectory path. You can make the trajectory visible for any object by enabling the Trajectory option in the Object Properties dialog box.