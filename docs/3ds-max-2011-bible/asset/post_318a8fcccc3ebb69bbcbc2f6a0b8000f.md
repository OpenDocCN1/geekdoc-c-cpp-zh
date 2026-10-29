
# Part IV: Materials, Cameras, and Lighting Basics

If you apply a material or map to an object that doesn’t look just right and tweaking it won’t help, you can always return to square one by removing the material or any mappings that have been applied to the object. The tool to remove materials and maps is the UVW Remove utility. You can access this utility by clicking the More button in the Utility panel and selecting UVW Remove from the list of utilities.

## FIGURE 15.4

The Slate Material Editor Options dialog box offers many options for controlling the Slate Material Editor window.

![](img/ebbb4844f027f7d1c580e48108d2b6cb_493_0.png)

This utility includes a single rollout that lists the number of objects selected. It also includes two buttons. The UVW button removes any mapping coordinates from the selected objects, and the Material button removes any materials from the selected objects. This button restores the original object color to the selected objects. Alternatively, you can select the Set Gray option, which makes the selected object gray when the materials are removed.

## Using the Fix Ambient utility

Standard material types always have their Ambient and Diffuse colors locked together. If you have older files with unlocked Diffuse and Ambient colors, the Fix Ambient utility can be used to locate and fix all materials in the scene with this condition. To access this utility, open the Utilities panel, click the More button, and select the Fix Ambient utility. Clicking the Find All button opens a dialog box that lists all materials in the scene with unlocked Diffuse and Ambient colors.

## Tutorial: Coloring Easter eggs

Everyone loves spring with its bright colors and newness of life. One of the highlights of the season is the tradition of coloring Easter eggs. In this tutorial, you use virtual eggs—no messy dyes and no egg salad sandwiches for the next two weeks.

# Chapter 15: Using the Slate Material Editor

To create your virtual Easter eggs and apply different colors to them, follow these steps:

- 1. Open the Easter eggs.max file from the Chap 15 directory on the DVD. This file contains several egg-shaped objects.
- 2. Open the Slate Material Editor by choosing Rendering ➜ Material Editor ➜ Slate Material Editor (or press the M key).
- 3. Double-click the Standard material in the Material/Map Browser. Select the material node in the Node View, and click the Diffuse color swatch in the Parameter Editor panel. From the Color Selector that appears, drag the cursor around the color palette until you find the color you want and then click Close.
- 4. In any viewport, select an egg and then click the Assign Material to Selection button in the Material Editor, or you can simply drag from the material node’s output socket to the viewport object.
- 5. Repeat Steps 4 and 5 for all the eggs.

Figure 15.5 shows the assortment of eggs that we just created.

![](img/ebbb4844f027f7d1c580e48108d2b6cb_494_0.png)

These eggs have been assigned materials with different Diffuse colors.

The right-click pop-up menu also offers an option to create a new library. New libraries can be saved and loaded also using the right-click pop-up menu.

# Note

Max ships with several different material libraries, including Backgrounds, Bricks, Concrete, Fabric, Ground, Metal, Nature, RayTraced, ReflectionMaps, Skys, Space, Stones, Wood, and several architecture material sets. You can find all these libraries in the matlibs directory.

Save a layout with the current materials using the Material/Map Browser Options ⇨ Additional Options ⇨ Save Layout As. These files are saved as files with the .mpl extension.

# Cross-Ref

Although materials can be saved out as libraries, perhaps the easiest ways to share materials between applications are using the Material XML Export utility or the Material ⇨ Export As XML File command.

# Tutorial: Loading a custom material library

To practice loading a material library, I've created a custom library of materials using various textures created with Kai's Power Tools.

To load a custom material library into the Slate Material Editor, follow these steps:

- 1. Choose Rendering ⇨ Material Editor (or press the M key) to open the Material Editor. Then make sure the Material/Map Browser is active or select the Tools ⇨ Material/Map Browser menu to open the Material/Map Browser.
- 2. Select the Material/Map Browser Options ⇨ Open Material Library menu.
- 3. Select and open the KPT samples.mat file from the Chap 15 directory on the DVD. The library loads into the Material/Map Browser.
- 4. In the Search field (above the sample slot), type Bug to locate and select the bug eyes material.

Figure 15.7 shows the Material/Map Browser with the custom material library open.

# Using the Material Explorer

The Scene Explorer has been well received and has made working with scene objects much easier. So easy in fact that the Max team has looked for other places where a similar interface can be used, and the first stop is with materials. The result is the Material Explorer.

The Material Explorer, shown in Figure 15.8, lets you quickly view all the scene materials along with their hierarchies and all their properties in a single interface. It also lets you sort the materials by their various properties and even make changes to multiple materials at once. You can access the Material Explorer with the Rendering ⇨ Material Explorer command.

The Material Explorer works exactly like the Scene Explorer and has configurable columns. It is divided into two panels. The top panel shows all the materials in the current scene; the bottom panel shows the hierarchy of the selected material or submaterial.

In addition to the menus, several toolbar buttons run horizontally under the menus and several display buttons run vertically down the left side of the interface. These buttons are described in Tables 15.2 and 15.3.

# Part IV: Materials, Cameras, and Lighting Basics

## FIGURE 15.7

The Material/Map Browser also lets you work with saved custom material libraries.

![](img/ebbb4844f027f7d1c580e48108d2b6cb_497_0.png)

# Cross-Ref

To learn more about the Scene Explorer interface, see Chapter 6, “Selecting Objects and Setting Object Properties.”

## FIGURE 15.8

The Material Explorer shows the layered material as a hierarchy.

![](img/ebbb4844f027f7d1c580e48108d2b6cb_497_1.png)

Scene panel

Material panel

### TABLE 15.2

#### Material Explorer Display Buttons—Vertical

| Toolbar Button | Name | Description |
|---|---|---|
| [图标] | Display Thumbnails | Displays thumbnails of the various material components as displayed in the sample slots |
| [图标] | Display Materials | Includes materials within the hierarchy |
| [图标] | Display Maps | Includes maps within the material hierarchy |
| [图标] | Display Objects | Includes the applied object in the material hierarchy |
| [图标] | Display Sub-Materials/Maps | Includes any applied submaterials/maps within the material hierarchy |
| [图标] | Display Unused Map Channels | Includes all unused map channels as part of the hierarchy |
| [图标] | Sort by Object | Sorts the materials based on the objects they are applied to and lists the materials underneath |
| [图标] | Sort by Material | Sorts the materials and lists the objects underneath |

### TABLE 15.3

#### Material Explorer Toolbar Buttons—Horizontal

| Toolbar Button | Name | Description |
|---|---|---|
| Find | Find text field | Allows searching for specific named materials and maps |
| [图标] | Select All Materials | Selects all materials in the scene |
| [图标] | Select All Maps | Selects all maps in the scene |
| [图标] | Select All | Selects all entries in the list |
| [图标] | Select None | Deselects all entries in the list |

*continued*

# Part IV: Materials, Cameras, and Lighting Basics

**TABLE 15.3 (continued)**

**Material Explorer Toolbar Buttons—Horizontal**

| Toolbar Button | Name | Description |
|---|---|---|
| [icon] | Select Invert | Inverts the current selection |
| [icon] | Lock Cell Editing | Locks all cells so they cannot be edited |
| [icon] | Sync to Material Explorer | Causes the material selected in the top panel to be visible in the lower panel |
| [icon] | Sync to Material Level | Displays the entire hierarchy for the selected material in the lower panel when enabled |

The Material Explorer lets you apply materials directly to scene objects by simply dragging and dropping the material thumbnail onto the object. You also can drag and drop maps onto other materials and channels. The Material Explorer also works with the Material Browser; for example, you can drag the material type and drop it on the Type column in the Material Explorer to change a material type.

# Summary

Materials can add much to the realism of your models. Learning to use the Material Editor, the Material/Map Browser, and the Material/Map Navigator enables you to work with materials. This chapter covered the following topics:

- Understanding various material properties
- Working with the Material Editor buttons and sample slots
- Using the Material/Map Browser and material libraries
- Using the Material Explorer to quickly see all materials in a scene

The next chapter delves more into the topic of material, including the standard material and all its settings.
