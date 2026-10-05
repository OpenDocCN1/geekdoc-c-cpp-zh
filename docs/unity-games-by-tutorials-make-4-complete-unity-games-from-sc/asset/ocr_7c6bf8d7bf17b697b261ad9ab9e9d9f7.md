Unity Games by Tutorials

Chapter 11: Introducing the UI

![](bbox=[0.387, 0.093, 0.612, 0.237])

An anchor acts like an anchor in real life: It keeps something in place. If you wanted to position a UI element in the top-left corner and always stay relative to that top-left corner, you would simply set its anchor to top-left.

Anchors also can stretch a control. This is useful if you want a control to expand or contract based on the screen size. The anchor breaks into individual arrows to form a rectangle. This allows you to define the size of the stretching.

![](bbox=[0.387, 0.413, 0.612, 0.557])

When talking about anchors, it's important to understand what a pivot is. The pivot is the point on the Image that the position is applied to, and it's what the anchors use for keeping it in the right place. The pivot point is also the rotation point.

Having the pivot at the top-left corner is the most common position, but it can be useful to have the pivot set in various positions. For example, if you want something to be positioned in the top-middle of the screen, setting the pivot to the top-middle can make things a lot easier.

The pivot is set in normalized coordinates. This means that it goes from 0 to 1 for both height and width where (0,0) is the bottom left corner and (1,1) is the top right corner.

raywenderlich.com

299