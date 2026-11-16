![](bbox=[0.115, 0.065, 0.215, 0.225])

# HOW'D YOU DO?

The DockPanel allocates space on a strictly first-come, first-serve basis. The first child element receives the full width or height of the panel. Subsequent child elements are allocated the full width or height of the remaining space. Elements docked to the same side are stacked.

![](bbox=[0.235, 0.255, 0.675, 0.545])

The first element gets all the available side.

Subsequent elements are allocated space from what's left over.

If LastChildFill is set to "False", the last element behaves like any other. But remember, the default values for HorizontalAlignment and VerticalAlignment are "Stretch", so if you don't set them, the element will fill the available space anyway.

Elements docked to the same side are stacked.

![](bbox=[0.11, 0.755, 0.28, 0.88])

# MAKE A NOTE

Unlike Canvas, the zIndex property has no effect on the arrangement of elements in the DockPanel—only the order in which the elements are added controls their arrangement.