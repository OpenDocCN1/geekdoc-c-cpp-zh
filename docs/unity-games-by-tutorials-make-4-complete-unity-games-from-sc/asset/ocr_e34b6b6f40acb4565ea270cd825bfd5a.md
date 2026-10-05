Save this script and return to the editor. Now, stand up with both the HMD and the right controller, and play the scene. By buying and creating new towers and upgrading them. The windows will appear around the spot where you make your selections.

Nice job! That's for the Game scene. Open up the TitleScreen scene to make that work in VR as well.

# Modifying the title screen

Start off by disabling the Main Camera. Now drag the ViveRig prefab from the Prefabs VR folder into the Hierarchy and set its position to (0, -10, -8). Select EventSystem and disable the Standalone Input Module. Add the Vive Controller Look Module script to edit it. You can do this in the Inspector panel by clicking the Add Component and searching for it.

Now drag the Reticle and Laser prefabs from the Prefabs VR folder into the scene and drag them into the Reticle and Laser Transform fields of Vive Controller Look Module.

Next, fully expand ViveRig and its child Controller (right). Drag ControllerCamera and Controller (right) onto the Controller Camera and Right Controller fields.

Next, select Title Canvas and drag the ControllerCamera to the Canvas component's Event Camera field.

Finally, select Camera (head)'s child Camera (eye). Set its Clear Flags to Solid Color and change the Background color to pure black (00000000).

Now try out the changes by playing the scene with the HMD on your head and on the right controller in your hand. You should be able to select the Start button and start the game now.

That concludes the HTC section!

# Where to go from here?

Congratulations on taking the first steps into the virtual world!

VR is still in an early stage in life, so there is a lot to discover about how to make use of this new technology. Make sure you experiment a lot and share your findings, or some best practices with the rest of us game developers!

![](bbox=[0.119, 0.933, 0.281, 0.955])