
## FIGURE 39.9

The Layer Manager rollout holds the various animation layers.

Setup/Animation Mode Toggle

Layer color

Rig Coloring Mode

Delete Layer

Dope Sheet: Layer Ranges

![](img/ebbb4844f027f7d1c580e48108d2b6cb_1020_0.png)

Move Layer Up
Move Layer Down

Collapse Layers

Paste Layer

Key Pose to Layer

Copy Layer

Display Layer Transform Gizmo

Add Layer

After an animation layer is added and selected, you need to press the Setup/Animation Mode toggle button to begin adding keys to the selected animation layer. You do this using the Auto or Set Key modes to create the keys like normal. Any time a new animation is added, it is automatically placed above the currently selected animation layer.

### Tip

If you're animating some of the rig bones using Auto Key and the keys don't appear on the Track Bar, check to make sure you have clicked the Setup/Animation Mode toggle button to enable animation.

## Part IX: Working with Characters

The selected animation layer can be removed from the list using the Delete Layer button. You also can copy and paste layers between different rigs using the Copy and Paste Layer buttons. The Move Layer Up and Move Layer Down buttons are used to reorder the selected layer. Each layer can be given a unique name using the Name field.

The Ignore option disables the selected animation layer, and the Solo option disables all animation layers except for the current selection.

### Blending absolute animation layers

When several absolute animation layers are added, the layers are evaluated according to their order in the Layer Manager list from top to bottom. Each layer can have a Global Weight value that determines how much of the animation layer is blended.

For example, if the top absolute animation layer contains keys for a character raising an arm and a second absolute animation layer is added that has keys of the character waving its hand, these two can be blended to create the combined motion of the character raising its hand and waving by setting the Global Weight for the second absolute animation layer to 50 percent, as shown in Figure 39.10. If the second layer is set to 0 percent, the character simply raises its arm; if the Global Weight of the second layer is set to 100 percent, the layer takes over the entire animation; and if the character waves its hand without raising its arm.

## FIGURE 39.10

If the Layer Manager contains multiple animation layers, you can blend between them using the Global Weight values.

![](img/ebbb4844f027f7d1c580e48108d2b6cb_1021_0.png)

In addition to the Global Weight value, which affects all parts of the rig, you can also set a Local Weight value for specific bones. For example, if an absolute animation layer is set that moves the rig to a specific with the walk cycle, creating a slower run cycle. You also can open the Curve Editor to change the shape of the weight curves.

## FIGURE 39.11

The CAT Motion dialog box lets you alter the walk cycle parameters.

![](img/ebbb4844f027f7d1c580e48108d2b6cb_1023_0.png)

Open CAT Motion Preset

Save CAT Motion Preset

New CAT Motion Layer

Remove CAT Motion Preset

Open Curve Editor

### Setting global parameters

Clicking the Globals option in the leftmost pane of the CAT Motion dialog box opens a panel of global CAT motion parameters, shown in Figure 39.12. At the top of the global parameters are settings for changing the start and end frame of the walk cycle. Note that these settings are different from the start and end time settings in the Time Configuration dialog box, and they affect only the CAT rig motion.

## FIGURE 39.12

The Globals panel of the CAT Motion dialog box lets you change the walk tempo, speed, and direction.

Curve Editor

![](img/ebbb4844f027f7d1c580e48108d2b6cb_1023_1.png)

The Max Step Time defines how quickly each step is taken. Low values make the character walk crazy fast, and higher values make a slower, more casual walk. The Max Stride Length sets the distance of each step. These two values together determine the Velocity, but you can’t alter the Velocity setting.

The character by default is pointing in the direction indicated on the CAT Parent object, but you can alter the direction that the character is walking by altering the Direction value. A setting of 0 makes the character walk in the direction he is pointing, a value of 90 makes the character shuffle to his right, a value of 180 makes the character walk backward, and a value of 270 makes the character shuffle to the left. The Gradient setting controls the angle that the character is pointing. Negative values make the character point forward as if walking down a hill, and large, positive values make the character walk as if going up a hill.

### Walking along a path

The default is to have the character walk in place, but if you select the Walk On Line option, then the character walks forward in a straight line. When the range of frames is reached, the character returns to its starting position and walks the line again. If the Direction value is changed, the character moves straight in the specified direction.

If you click the Path Node button, you can choose a scene object that the character will follow. For example, if you make the Path Node a dummy object, then the character is positioned and walks on top of the dummy object. You can then animate the movement of the dummy object in the scene, and the character follows it.

To make the character walk along a path, you simply need to create a path using the Line tool. Then select the dummy object and use the Animation > Path Constraint menu to attach the dummy object to the path. If you enable the Follow option in the Motion panel after making the link, the character turns to stay on the path.

When having a character follow a path with tight corners, the character may become distorted as it attempts to stay on the path. The Preserve Character Shape setting lets you minimize the distortion. A setting of 0 allows the distortion caused by tight corners.

### Controlling footsteps and limbs

The Limb Phases panel of the CAT Motion dialog box, shown in Figure 39.13, controls the placement of footsteps and the swing of each leg and arm. The footprints that appear when a character is walking are tied to the rig, so altering the footsteps also alters the rig. If the footsteps don’t appear when you select a walk cycle, you can use the Create button to make them appear. You also can delete them with the Delete button. If you move or rotate any of the footsteps, you can use the Reset button to remove any changes for All footsteps or for just the selected footsteps.

## FIGURE 39.13

The Limb Phases panel lets you set how the arms and legs swing relative to each other.

![](img/ebbb4844f027f7d1c580e48108d2b6cb_1024_0.png)

The sliders for each leg and arm at the bottom of the Limb Phases panel let you alter how the arms and legs swing relative to each other. By default, the opposite leg and arm swing together, but you can alter these sliders to give the walk cycle a different look.

### Matching footsteps to the ground

After footsteps appear, you can select them and use the Pick Ground button. This lets you select a ground plane object. This ground object needs to be a single object, but once selected, the footsteps are moved vertically to align to the ground plane, causing the character to walk along the surface of the ground.

### Controlling secondary motions

The remaining panels in the CAT Motion dialog box are used to control the motions of the other rig groups, such as the pelvis, head, and ribcage. If you open the Pelvis group, you see several parameters that you can access including Twist, Roll, Pitch, Lift, Push, Weight Shift, and positional and rotation offsets. Each of these parameters shows an animation curve that you can use to exaggerate or calm the selected motion, such as the Twist parameter shown in Figure 39.14.

## FIGURE 39.14

Using the parameter curves in the CAT Motion dialog box, you can control motions such as the twisting of the pelvis.

![](img/ebbb4844f027f7d1c580e48108d2b6cb_1025_0.png)

### Tutorial: Animating a character walking along a path

In this example, you take the default alien character rig and make it walk along a drawn path.

To animate a character walking along a path, follow these steps:

- 1. Open the Wandering alien.max file from the Chap 39 directory on the DVD. This file includes the default CAT alien rig and a random path.
