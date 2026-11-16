If we can ensure that any code searching through the BSP tree always visits the front child of a node before the back node, we make maximal use of the data cache. This is because the data for the front child is very likely to be located in the data cache due to its proximity to its parent node.

# Creating the BSP Tree

Creating this BSP tree is almost trivial, especially if we treat each widget instance as a point. After creating an array of all the widget instances in the world, we calculate an axis-aligned bounding box for them. At each node, we find the longest axis of this box. This axis becomes the splitting plane. After sorting the nodes by their position along this axis, we then position the plane between the two median widgets. That is, if there are 63 widgets in the world, the cutting plane would be placed between the 31st and 32nd widgets.

We continue creating nodes in this fashion until there are only a small number of widget instances remaining in each node; the node is then said to be a leaf node. A leaf node in this instance is considered to be an array of WIDGETLEAF structures. The count of widgets remaining in the array is located inside each element of the array. The WIDGETLEAF structure as described also takes only 16 bytes of memory, maintaining efficiency and cache-friendliness.

```
typedef struct
{
    float position[3]; // position of the widget
    s8 sinAngle; // sin of its orientation (*127)
    s8 cosAngle; // cos of its orientation (*127)
    u8 scale; // scale of this widget (*32)
    u8 pad;
} WIDGETLEAF;
```

![](bbox=[0.092, 0.64, 0.162, 0.68])

The FoliageDemo application included on the CD-ROM contains the files widgetbsp.cpp and widgetbsp.h, which describe the CWidgetBSP class. This class is responsible for the creation and management of a widget BSP tree. The CreateTree member function takes an array of WIDGETLEAF structures as a parameter and creates a BSP tree from them, as described in this section. Once the tree has been created, we can efficiently search it to find the list of widget instances that must be drawn.

# Searching the BSP Tree

Now that we have a compact, memory access-efficient BSP tree definition, we can look at how to calculate the set of widgets that should be rendered. To do this, we must retrieve from the BSP tree all the widgets within the view frustum that are within a certain distance of the view position. We can use the size of the viewport, the camera matrix, and the field of view to construct an axis-aligned box that encloses the area of interest, as shown in Figure 5.3.4.