# Part IX: Working with Characters

The selected animation layer can be removed from the list using the Delete Layer button. You also can copy and paste layers between different rigs using the Copy and Paste Layer buttons. The Move Layer Up and Move Layer Down buttons are used to reorder the selected layer. Each layer can be given a unique name using the Name field.

The Ignore option disables the selected animation layer, and the Solo option disables all animation layers except for the current selection.

# Blending absolute animation layers

When several absolute animation layers are added, the layers are evaluated according to their order in the Layer Manager list from top to bottom. Each layer can have a Global Weight value that determines how much of the animation layer is blended.

For example, if the top absolute animation layer contains keys for a character raising an arm and a second absolute animation layer is added that has keys of the character waving its hand, these two can be blended to create the combined motion of the character raising its hand and waving by setting the Global Weight for the second absolute animation layer to 50 percent, as shown in Figure 39.10. If the second layer is set to 0 percent, the character simply raises its arm; if the Global Weight of the second layer is set to 100 percent, the layer takes over the entire animation; and if the character waves its hand without raising its arm.

# FIGURE 39.10

If the Layer Manager contains multiple animation layers, you can blend between them using the Global Weight values.

![](bbox=[0.071, 0.488, 0.783, 0.886])

In addition to the Global Weight value, which affects all parts of the rig, you can also set a Local Weight value for specific bones. For example, if an absolute animation layer is set that moves the rig to a specific