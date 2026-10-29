
## FIGURE 37.2

This bone includes fins that make understanding its orientation easier.

![](img/ebbb4844f027f7d1c580e48108d2b6cb_987_0.png)

## Tutorial: Creating a bones system for an alligator

To practice creating a bones system, you'll take a trip to the Deep South to gator country. The main movement for this gator is going to be in its tail, so you need the most bones there. The front legs are smaller and can be controlled with only two simple bones. You also won't worry about fingers.

To create a bones system for an alligator, follow these steps:

- 1. Open the Alligator bones.max file from the Chap 37 directory on the DVD. This file includes an alligator model created by Viewpoint Datalabs.
- 2. Select Create ⇨ Systems ⇨ Bones IK Chain, and in the IK Chain Assignment rollout, select IK Limb from the IK Solver drop-down list. Then set the Width and Height values to 10 and enable all the bone fins and set their Size to 5.
- 3. In the Top viewport, click once at the pelvis and then again at the mid-abdomen, the base of the neck, and the end of the nose. Then right-click to end the bones chain.
- 4. While still in Bones mode, click below the pelvis and create an additional five bones to define the tail. Then right-click to end the chain. Select the first bone in the tail chain and link it to the first joint with the Select and Link tool that moves from the pelvis to the nose, which is the root joint.

### Tip

If you can't see the bones to make the link, then hide the body so the bones are clearly visible.

## Chapter 37: Understanding Rigging and Working with Bones

- 5. Click on the Bones button in the Create panel and select the bone just in front of the legs in the Top viewport (the cursor changes to a crosshair when it is over a bone) and drag to the top to form the left shoulder, left upper-arm and left lower-arm bones. Right-click to end the chain. Repeat to create bones for the left leg.

- 6. Select the Animation → Bone Tools menu command to open the Bone Tools dialog box. Select all the bones in the left arm and leg and click the Mirror button. In the Bone Mirror dialog box, select the Y axis and click OK.

- 7. Click the Select Objects button on the main toolbar to exit Bones mode, and select and name each bone object so it can be easily identified later.

### Tip

The Schematic View window is a good interface for quickly labeling bones.

Figure 37.3 shows the completed bones system for the alligator.

## FIGURE 37.3

This bones system for an alligator was easy to create.

![](img/ebbb4844f027f7d1c580e48108d2b6cb_988_0.png)

## Using the Bone Tools

After you've created a bones system, you can use the Bone Tools to edit and work with the bones system. You access these tools from a panel that is opened using the Animation → Bone Tools menu command.

## Part IX: Working with Characters

Figure 37.4 shows this panel of tools, which includes three separate rollouts: Bone Editing Tools, Fin Adjustment Tools, and Object Properties.

## FIGURE 37.4

The Bone Tools palette includes several buttons for working with bones systems.

![](img/ebbb4844f027f7d1c580e48108d2b6cb_989_0.png)

## Reordering bones

You can use the transform buttons on the main toolbar to move, rotate, and scale a bone along with all its children, but if you want to transform the parent without affecting any of the children, you need to open the Bone Tools panel using the Animation > Bone Tools menu command. Bone Edit Mode lets you move and realign a bone without affecting its children.

Clicking the Remove Bone button removes the selected bone and reconnects the bone chain by stretching the child bone. If you hold down the Shift key while removing a bone, the parent is stretched. Clicking the Delete Bone button deletes the selected bone and adds an End bone to the last child.

### Caution

Using the Delete key to delete a bone does not add an End bone, and the bone chain does not work correctly with an IK Solver.

If a Bone exists that isn't connected to another bone, you can add an End bone to the bone using the Create End button. The bone chain must end with an End bone in order to be used by an IK Solver.

The Connect Bones button lets you connect the selected bone with another bone. After clicking this button, you can drag a line from the selected bone to another bone to connect the two bones.

Use the Reassign Root button to reverse the chain and move the End bone from the parent to the last child.

## Refining and mirroring bones

As you start to work with a bones system that you've created, you may discover that the one long bone for the backbone of your monster is too long to allow the monster to move like you want. If this happens, you can refine individual bones using the Refine button. This button appears at the bottom of the Bone Tools section of the Bone Editing Tools rollout.

Clicking the Refine button enables you to select bones in the viewport. Every bone that you select is divided into two bones at the location where you click. Click on the Refine button again to exit Refine mode.

The Mirror button lets you create a mirror copy of the selected bones. This button makes the Bone Mirror dialog box appear, where you can select the Mirror Axis and the Bone Axis to Flip. You also can specify an Offset value. In the previous example, you created arms and legs manually, but you could have created one of them and used the Mirror button to create its opposite.

## Coloring bones

Bones, like any other objects, are assigned a default object color, and materials can be applied from the Material Editor. For each separate bone, its object color can be changed in the Modify panel or in the Bone Tools panel.

You can also apply a gradient to a bone chain using the Bone Tools palette. This option is available only if two or more bones are selected. The Start Color is applied to the chain's head, and the End Color is applied to the last selected child. The colors are applied or updated when the Apply Gradient button is clicked. Figure 37.5 shows a long, spiral bone chain with a white-to-black gradient applied.

## FIGURE 37.5

A white-to-black gradient was applied to this spiral bone chain.

![](img/ebbb4844f027f7d1c580e48108d2b6cb_990_0.png)

## Part IX: Working with Characters

## Adjusting fins

The Fin Adjustment Tools rollout includes the same parameters as those found in the Bone Parameters rollout. You can specify the dimensions and taper of a bone and its fins. But you can also specify that the parameters are applied using Absolute or Relative values. Relative values are based on the parameters of the bone that is above the current bone in the chain.

This rollout also includes Copy and Paste buttons that you can use to copy the bone parameters from one bone to another.

## Making objects into bones

You can make any object act like a bone. To make an object into a bone, you need to open the Object Properties rollout in the Bone Tools panel. The Object Properties rollout includes a setting for Bone On. If enabled, the object acts like a bone. When the Bone On/Off option is enabled, the remaining Bone controls become available. The Auto-Align option causes the pivot points of adjacent bones to be aligned automatically. The Freeze Length option causes a bone to keep its length as the bones system is moved. If the Freeze Length is disabled, you can specify a Stretch type. None prevents any stretching from occurring, and Scale changes the size along one axis, but Squash causes the bone to get wider as its length is decreased and thinner as it is elongated. You can also select to stretch an axis and choose whether to Flip the axis.

You can use the Realign button to realign a bone: click the Reset Stretch button to normalize the stretch value to its current value.

## Summary

The benefits of a bones system become more apparent in the next chapter when I cover inverse kinematics. In this chapter, you learned how to create and work with bones systems and the Bone Tools. This chapter covered the following topics:

- Creating bones systems
- Setting bone parameters and the IK Solver
- Using the Bone Tools
- Making objects into bones systems

If you're feeling pretty good about the skeleton you've created, the next part of rigging is applying the IK Solver that is used to tell the bones how to move relative to one another. This also gives you the chance to constrain the bone's movement. The second part of rigging characters is covered in the next chapter along with inverse kinematics.
