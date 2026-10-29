drawn between the beginning and ending joints. The pivot point of the end joint is the goal for the IK solver. It is known as the End Effector. The End Effector of the IK solver is marked by a blue cross. Several rollouts within the Motion panel also appear. These rollouts let you set the parameters for the IK solver.

The first rollout, after the Assign Controller rollout, is the IK Solver rollout, shown in Figure 38.6. Using this rollout, you can select to switch between the HI IK solver and the IK Limb solver. The Enabled button lets you disable the solver. By disabling the solver, you can use forward kinematics to move the objects. To return to the IK solution, simply click the Enabled button again. The IK for FK Pose option enables IK control even if the IK solver is disabled. This lets you manipulate the hierarchy of objects using forward kinematics while still working with the IK solution. If both the IK for FK Pose and the Enabled buttons are disabled, then the goal can move without affecting the hierarchy of objects.

# FIGURE 38.6

The IK Solver rollout lets you enable or disable the IK solver.

![](bbox=[0.06, 0.48, 0.68, 0.68])

If the goal ever gets moved away from the end link, clicking the IK/FK Snap button automatically moves the goal to match the end links position. Auto Snap automatically keeps the goal and the end link together. The Set as Preferred Angle button remembers the angles for the IK system. These angles can be recalled at any time using the Assume Preferred Angle button.

When you choose Animation ▶ IK Solvers ▶ HI Solver, the start joint is the selected object, and the end joint is the object to which you drag the dotted line. If you want to change these objects, you can click the Pick Start Joint or Pick End Joint buttons.

# Tip

The best way to select an object using the Pick Start or End Joint buttons is to open the Select by Name dialog box by pressing the H key. Using this dialog box, you can select an exact object without having to miss selecting it in a complex viewport.

# Caution

If you select a child as the start joint and an object above the child as the end joint, then moving the goal has no effect on the IK chain.