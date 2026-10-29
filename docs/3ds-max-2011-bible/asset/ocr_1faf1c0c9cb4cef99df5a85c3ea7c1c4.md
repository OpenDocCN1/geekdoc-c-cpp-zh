# Part VIII: Advanced Animation Techniques

Block controllers. Others include separate interfaces, such as the Waveform controller for defining the controller’s functions.

Most of these special-purpose controllers can be assigned only by using the Track View window. The Motion panel contains only the tracks for transformations.

# Boolean controller

The Boolean controller, like the On/Off controller, can hold one of two states: 0 for off and 1 for on. But, unlike the On/Off controller, the Boolean controller changes only when a different state is encountered.

# Limit controller

The Limit controller sets limits for the motion or parameters of the selected controller. It is applied on top of the existing controller and opens the Limit Controller dialog box, shown in Figure 34.25, when applied.

![](bbox=[0.074, 0.396, 0.251, 0.557])

# FIGURE 34.25

The Limit controller dialog box lets you set upper and lower limits for the current controller value.

The upper limit is the maximum value to which the controller can be set, and the lower limit is the minimum value that the controller uses. Controller values may exceed the upper and lower limit values, but the object’s motion stops at the limit values when the Limit controller is enabled. The Smoothing Buffer value provides a range that gradually alters the value as it approaches the limit value.

After a Limit controller is applied to an object, you can quickly change its upper and lower limit values by right-clicking the object in the Track View and accessing the Limit Controller option in the quadmenu.

# Tip

You can disable all limits at once using the Animation ▷ Toggle Limits menu command.

# List controller

You can use the List controller to apply several controllers at once. This feature enables you to produce smaller, subtler deviations, such as adding some noise to a normal Path controller.

When the List controller is applied, the default track appears as a subtrack along with another subtrack labeled Available. By selecting the Available subtrack and clicking the Assign Controller button, you can assign additional controllers to the current track.

All subtrack controllers are included in the List rollout of the Motion panel. You also can access this list by right-clicking the track and selecting Properties from the pop-up menu. The order of the list is important because it defines which controllers are computed first.