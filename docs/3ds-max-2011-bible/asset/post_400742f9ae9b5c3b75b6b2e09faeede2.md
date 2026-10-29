
## Part II: Working with Objects

### Cross-Ref

For more information on using the Schematic View, see Chapter 25, “Working with the Schematic View.”

The Track View (opened with the Graph Editors ⇨ New Track View menu command) displays lots of scene details in addition to the object hierarchy. In the Track View, you can easily expand and contract the hierarchy to focus on just the section you want to see or select.

### Cross-Ref

For more information on using the Track View, see Chapter 36, “Working with Function Curves in the Track View.”

## Working with Linked Objects

If you link some objects together and set some animation keys, and the magical Play button starts sending objects hurtling off into space, chances are good that you have a linked object that you didn’t know about. Understanding object hierarchies and being able to transform those hierarchies are the keys to efficient animation sequences.

All transformations are done about an object’s pivot point. You can move and reorient these pivot points as needed by clicking the Pivot button under the Hierarchy panel.

Several additional settings for controlling links are available under the Hierarchy panel of the Command Panel (the Hierarchy panel tab looks like a mini-organizational chart). Just click the Link Info button. This button opens two rollouts if a linked object is selected. You can use the Locks and Inherit rollouts to limit an object’s transformations and specify the transformations that it inherits.

### Cross-Ref

I present more information on object transformations in Chapter 7, “Transforming Objects, Pivoting, Aligning, and Snapping.”

### Locking inheriting transformations

The Inherit rollout, like the Locks rollout, includes check boxes for each axis and each transformation, except that here, all the transformations are selected by default. By deselecting a check box, you specify which transformations an object does not inherit from its parent. The Inherit rollout appears only if the selected object is part of a hierarchy.

For example, suppose that a child object is created and linked to a parent and the X Move Inherit check box is deselected. As the parent is moved in the Y or Z directions, the child follows, but if the parent is moved in the X direction, the child does not follow. If a parent doesn’t inherit a transformation, then its children don’t either.

### Using the Link Inheritance utility

The Link Inheritance utility works in the same way as the Inherit rollout of the Hierarchy panel, except that you can apply it to multiple objects at the same time. To use this utility, open the Utility panel and click the More button. In the Utilities dialog box, select the Link Inheritance utility and click OK. The rollout for this utility is identical to the Inherit rollout discussed in the previous section.

## Chapter 9: Grouping, Linking, and Parenting Objects

### Selecting hierarchies

You need to select a hierarchy before you can transform it, and you have several ways to do so. The easiest method is to simply double-click an object. Double-clicking the root object selects the entire hierarchy, and double-clicking an object within the hierarchy selects it and all of its children.

After you select an object in a hierarchy, pressing the Page Up or Page Down keyboard shortcut selects its parent or child objects. For example, if you select the Mommy duck object and press Page Down, the first baby duck object is selected and the Mommy duck object is deselected. Selecting any of the baby duck objects and pressing Page Up selects the duck object in front of it.

### Linking to dummies

Dummy objects are useful as root objects for controlling the motion of hierarchies. By linking the parent object of a hierarchy to a dummy object, you can control all the objects by moving the dummy.

To create a dummy object, select Create → Helpers → Dummy, or open the Create panel, click the Helpers category button (this button looks like a small tape measure), and select the Standard category. Within the Object Type rollout is the Dummy button; click it, and then click in the viewport where you want the dummy object to be positioned. Dummy objects look like wireframe box objects in the viewports, but dummy objects are not rendered.

### Tutorial: Circling the globe

When you work with complex models with lots of parts, you can control the object more easily if you link it to a Dummy object and then animate the dummy object instead of the entire model. To practice doing this, you’ll create a simple animation of an airplane flying around the globe. To perform this feat, you create a dummy object in the center of a sphere, link the airplane model to it, and rotate the dummy object. This tutorial involves transforming and animating objects, which are covered in other chapters.

### Cross-Ref

> Rotating objects is covered in Chapter 7, “Transforming Objects, Pivoting, Aligning, and Snapping,” and the basics of animation are covered in Chapter 21, “Understanding Animation and Keyframes.”

To link and rotate objects using a dummy object, follow these steps:

- 1. Open the Circling the globe.max file found in the Chap 09 directory on the DVD.
- This file includes a texture mapped sphere with an airplane model positioned above it. The airplane model was created by Viewpoint Datalabs.
- 2. Select Create → Helpers → Dummy, and then drag in the center of the Sphere to create a Dummy object.
- With Dummy object selected, choose the Tools → Align menu command (or press the Alt+A shortcut) and click on the globe. In the Align Selection dialog box, enable the X, Y, and Z Position options along with the Center options and click OK to align the centers of the dummy and globe objects.
- 3. Because the dummy object is inside the sphere, creating the link between the airplane and the dummy object can be difficult. To simplify this process, select and right-click the sphere object, and then select Hide Selection from the pop-up menu.
- This hides the sphere so that you can create a link between the airplane and the dummy object.
- 4. Click the Select and Link button on the main toolbar, and drag a line from the airplane to the dummy object.
- 5. Click the Auto Key button (or press N) to enable animation key mode, and drag the Time Slider to frame 100. Then click the Select and Rotate button on the main toolbar (or press E), and select the dummy object. Then rotate the dummy object about its X-axis, and notice how the linked airplane also rotates over the surface of the sphere.

## Part II: Working with Objects

6. Select the dummy object and right-click to access the pop-up quadmenu. Then select the Unhide All menu command to make the sphere visible again.

By linking the airplane to a dummy object, you don't have to worry about moving the airplane's pivot point to get the correct motion. Figure 9.4 shows a frame from the final scene.

### FIGURE 9.4

With a link to a dummy object, making the airplane circle the globe is easy.

![](img/ebbb4844f027f7d1c580e48108d2b6cb_305_0.png)

## Summary

As scenes become more complex, the name of the game is organization. You can organize objects within the scene in several ways, including grouping, linking, and building hierarchies.

In this chapter, you've done the following:

- Grouped objects using the Group menu and learned to work with groups
- Learned about parent, child, and root relationships
- Created a hierarchy of objects using the Link and Unlink features
- Viewed links in the viewport
- Learned how to create and use dummy objects

In the next chapter, you jump headfirst into modeling by covering the basics of modeling and working with subobjects and helper objects.

## Part III

## Modeling Basics

| IN THIS PART |
|---|
| **Chapter 10**<br>Accessing Subobjects and<br>Using Modeling Helpers |
| **Chapter 11**<br>Introducing Modifiers and Using<br>the Modifier Stack |
| **Chapter 12**<br>Drawing and Editing 2D<br>Splines and Shapes |
| **Chapter 13**<br>Modeling with Polygons<br>and Patches |
| **Chapter 14**<br>Using the Graphite Modeling<br>Tools and Painting with Objects |
