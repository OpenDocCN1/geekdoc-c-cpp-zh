# Using the Map Path Utility

After you have all your maps in place, losing them can really make life troublesome. However, Max includes a utility that helps you determine which maps are missing and lets you edit the path to them to quickly and easily locate them. The Bitmap/Photometric Path Editor utility is available in the Utility panel. To find it, click the More button and select Bitmap/Photometric Path Editor from the list of utilities.

# Cross-Ref

This utility is used for bitmaps as well as photometric lights. You can learn about photometric lights in Chapter 20, “Using Lights and Basic Lighting Techniques.”

When opened, the Path Editor rollout includes the Edit Resources button that opens the Bitmap/Photometric Path Editor window, shown in Figure 17.37. The rollout also includes two options for displaying the Materials Editor and Material Library bitmap paths. The Close button closes the rollout.

# FIGURE 17.37

The Bitmap/Photometric Path Editor window lets you alter map paths.

![](bbox=[0.08, 0.62, 0.52, 0.78])

The Info button in the Bitmap/Photometric Path Editor dialog box lists all the nodes that use the selected map. The Copy Files button opens a File dialog in which you can select a location to which to copy the selected map. The Select Missing Files button selects any maps in the list that can’t be located. The Find Files button lists the maps in the current selection that can be located and the number that are missing. Stripping paths removes the path information and leaves only the map name. The New Path field lets you enter the path information to apply to the selected maps. The button with three dots to the right of the New Path field lets you browse for a path, and the Set Path button applies the path designated in the New Path field to the selected maps.

# Using Map Instances

Using the same bitmap for many different map channels is common. For example, you may use the same bitmap for the Diffuse and Bump map channels. If a file includes the same bitmaps over and over, the file size can increase, and replacing a bitmap when you make changes can become difficult. This potential problem can be fixed easily by making the maps into instances instead of copies. If you have an existing