# Abstract Base Class Example

Consider two classes, Window and Door:

![](bbox=[0.222, 0.13, 0.537, 0.498])

At first glance these classes may not seem to have anything to do with each other. But both share some interesting common features:

+   - They are both holes in the wall.
+   - They both have particular locations and sizes with respect to the wall
+   - They both may exist in one of 3 states: open, closed, locked
+   - They can be sent similar messages: open, close, lock

The code below shows the declarations of the two classes: