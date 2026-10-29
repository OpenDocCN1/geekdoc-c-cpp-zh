# FIGURE 7.10

The Transform Gizmo is located at the object's pivot point.

![](bbox=[0.02, 0.26, 0.38, 0.52])

# Note

Using the Scale transformation while one of these modes is selected alters the selected object but has no effect on the pivot point or the link.

# Aligning pivot points

Below the mode buttons are three more buttons that are used to align the pivot points. These buttons are active only when a mode is selected. These buttons are Center to Object/Pivot, Align to Object/Pivot, and Align to World. The first two buttons switch between Object and Pivot, depending on the mode selected. You may select only one mode at a time. The button turns light blue when selected.

The Center to Object button moves the pivot point so that it is aligned with the object center, and the Center to Pivot button moves the object so it is centered on its own pivot point. The Align to Object/Pivot button rotates the object or pivot point until the object's Local Coordinate System and the pivot point are aligned. The Align to World button rotates either the object or the pivot to the World Coordinate System. For example, if the Affect Object Only mode is selected and the object is separated from the pivot point, clicking the Center to Pivot button moves the object so that its center is on the pivot point.

Under these three alignment buttons is another button labeled Reset Pivot, which you use to reset the pivot point to its original location.

# Using the Working Pivot

Underneath the Adjust Pivot rollout is the Working Pivot rollout. Working Pivots are handy if you want to position an object using a temporary pivot without having to change the default object pivot. To position a Working Pivot, click the Edit Working Pivot button. This enters a mode just like the Affect Pivot Only button described previously, except it works with the working pivot.

After the Working Pivot is in place, you can select to use it instead of the object pivot by clicking the Use Working Pivot button. The Working Pivot stays active until you disable it in the Hierarchy panel. The Working Pivot works for all objects in the scene. When the Working Pivot is active, reminder text "USE WP" appears in all the viewports under the viewport name; when the Edit Working Pivot mode is enabled, this text reads, "EDIT WP."