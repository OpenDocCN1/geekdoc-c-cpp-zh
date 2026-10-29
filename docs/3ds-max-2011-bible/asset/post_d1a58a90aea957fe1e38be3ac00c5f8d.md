
# FIGURE 3.24

The View File dialog box can open an assortment of image and animation formats.

![](img/ebbb4844f027f7d1c580e48108d2b6cb_151_0.png)

The View File dialog box can open many types of files, including Microsoft videos (AVI), MPEG files, bitmap images (BMP), Kodak Cineon images (CIN), Combustion files (CWS), Graphics Image Format images (GIF), Radiance HDRI image files (HDR), Image File List files (IFL), JPEG images (JPG), OpenEXR image files (EXR), Portable Network Graphics images (PNG), Adobe Photoshop images (PSD), QuickTime movies (MOV), SGI images (RGB), RLA images, RPF images, Targa images (TGA, VST), Tagged Image File Format images (TIF), Abekas Digital Disk images (YUV), and DirectDraw Surface (DDS) images.

You use the Gamma area on the View File dialog box to specify whether an image uses its own gamma settings or the system's default setting, or whether an override value should be used.

# Summary

Working with files lets you save your work, share it with others, and reload it for more work. This chapter covered the following topics:

- Creating, saving, opening, merging, and archiving files
- Understanding the various import and export types
- Importing models from other programs, such as Illustrator, Maya, and MotionBuilder
- Working with the file utilities, such as the Asset Browser
- Using the Summary Info and File Properties dialog boxes to keep track of scene files

By now, you should be feeling more comfortable with the user interface and using files, but if you want to make some changes to the interface, the next chapter covers how to customize it.

# Customizing the Max Interface and Setting Preferences

When you get into a new car, one of the first things you do is rearrange the seat and mirrors. You do this to make yourself comfortable. The same principle can apply to software packages: Arranging or customizing an interface makes it more comfortable to work with.

Early versions of Max allowed only minimal changes to the interface, but later versions enable significant customization. The Max interface can be customized to show only the icons and tools that you want to see. Max also has a rather bulky set of preferences that you can use to set almost every aspect of the program. This chapter covers various ways to make the Max interface more comfortable for you.

## Using the Customize User Interface Window

The Customize menu provides commands for customizing and setting up the Max interface. The first menu item is the Customize User Interface menu command. This command opens the Customize User Interface dialog box. This dialog box includes five panels: Keyboard, Toolbars, Quads, Menus, and Colors. You also can access this dialog box by right-clicking any toolbar away from the buttons and selecting Customize from the pop-up menu.

### Customizing keyboard shortcuts

If used properly, keyboard shortcuts can increase your efficiency dramatically. Figure 4.1 shows the Keyboard panel of the Customize User Interface dialog box. In this panel, you can assign shortcuts to any command and define sets of shortcuts. You can assign keyboard shortcuts for any of the interfaces listed in the Group drop-down list. When an interface is selected from the Group drop-down list, all its commands are listed below, along with their current keyboard shortcuts. You can disable the keyboard shortcuts for any of these interfaces using the Active option located next to the drop-down list.

# CHAPTER 4

**IN THIS CHAPTER**

- Using the Customize User Interface dialog box
- Creating custom keyboard shortcuts, toolbars, quadmenus, menus, and colors
- Customizing the Ribbon
- Customizing the Command Panel buttons
- Loading and saving custom interfaces
- Configuring paths
- Setting system units
- Setting preferences

# Part I: Getting Started with 3ds Max

# Note

To access the defined keyboard shortcuts for the various interfaces, the Keyboard Shortcut Override Toggle button on the main toolbar must be enabled. If this button is disabled, then only the keyboard shortcuts for the Main UI are active.

![](img/ebbb4844f027f7d1c580e48108d2b6cb_153_0.png)

The Keyboard panel enables you to create keyboard shortcuts for any command.

Groups that have a large number of commands are split into categories. You can use the Category drop-down list to filter only select types of commands. This helps you to quickly locate a specific command such as controllers, modifiers, or Space Warps. Entering a keyboard shortcut into the Hotkey field shows in the Assigned to field whether that key is currently assigned to a command. You can Assign the hotkey to the selected command or Remove the hotkey from its current assignment.

If the Overrides Active option is enabled, then the Editable Poly commands that are marked in bold text can be activated by pressing and holding a keyboard shortcut. When you release the keyboard shortcut, the original mode is restored. For example, if you are working in Extrude mode, you can press and hold the Shift+Ctrl+B keyboard shortcut to access the Bevel command. When you release the keyboard shortcut, the Extrude mode is active again. The amount of time that passes before the press-and-hold keyboard shortcut becomes active is set by the Delay to Override value.

You can use the Write Keyboard Chart button to output all the keyboard commands to a text file. Using this feature, you can print and post a chart of keyboard shortcuts next to your computer monitor. You also can Load, Save, and Reset selected keyboard shortcut sets. Keyboard shortcut sets are saved as .kbd files in the UI directory where Max is installed.

# On the DVD

You can find a reference of the available default keyboard shortcuts, “3ds Max 2011 Keyboard Shortcuts,” on the DVD.

# Customizing toolbars

You can use the Customize User Interface dialog box’s Toolbar panel to create custom toolbars. Figure 4.2 shows this panel.

# FIGURE 4.2

The Toolbars panel in the Customize User Interface dialog box enables you to create new toolbars.

![](img/ebbb4844f027f7d1c580e48108d2b6cb_154_0.png)

The Toolbars panel of the Customize User Interface dialog box includes the same Group and Category drop-down lists and command list as the Keyboard panel. Clicking the New button opens a simple dialog box where you can create and name the new toolbar. The Delete button lets you delete toolbars. You can delete only toolbars that you’ve created. The Rename button lets you rename the current toolbar. The Hide option makes the selected toolbar hidden.

Use the Load and Save buttons to load and save your newly created interface, including the new toolbar, to a custom interface file. Saved toolbars have the .cui extension.

After you create a new toolbar, you can drag the commands in the Action list to either a new blank toolbar created with the New button or to an existing toolbar. By holding down the Alt key, you can drag a button from another toolbar and move it to your new toolbar. Holding down the Ctrl key and dragging a button retains a copy of the button on the first toolbar.

If you drag a command that has an icon associated with it, the icon appears on the new toolbar. If the command doesn’t have an icon, then the text for the command appears on the new toolbar.

On the right side of the Toolbars panel is a section where you can populate and arrange the Quick Access Toolbar that appears on the title bar.

# Tutorial: Creating a custom toolbar

If you've been using Max for a while, you probably have several favorite commands that you use extensively. You can create a custom toolbar of all your favorite commands. To learn how to do this, you'll create a custom toolbar for the compound objects.

To create a custom toolbar for creating compound objects, follow these steps:

- 1. Open the Customize User Interface dialog box by choosing Customize ▸ Custom User Interface.
- 2. Open the Toolbars panel, and click the New button. In the New Toolbar dialog box that appears, name the toolbar Compound Objects. After you click OK, a new blank toolbar appears.
- 3. Select the Main UI group and the Objects Compounds category from the drop-down lists on the left. Then drag each command in the Action list to the new blank toolbar.
- 4. Click the Save button to save the changes to the customized interface file. You can load the resulting toolbar from the Chap 04 directory on the DVD. It is named Compound Objects toolbar.cui.

# Note

Don't be alarmed if the toolbar icons show up gray. Gray icons are simply disabled. When the tool is enabled, they are shown in color.

Figure 4.3 shows the new toolbar. With the new toolbar created, you can float, dock, or edit this toolbar just like the other toolbars. Notice that some of the tools have icons and others have text names.

# FIGURE 4.3

A new toolbar of compound objects created using the Customize User Interface dialog box

![](img/ebbb4844f027f7d1c580e48108d2b6cb_155_0.png)

You can right-click any of the buttons on any of the existing toolbars, except for the main toolbar, to access a pop-up menu. This pop-up menu enables you to change the button's appearance, delete the button, edit the button's macro script, or open the Customize User Interface dialog box.

# Cross-Ref

To learn more about editing macro scripts, see Chapter 49, “Automating with MAXScript.”

# Changing a button’s appearance

Selecting the Edit Button Appearance command from the right-click pop-up menu opens the Edit Macro Button dialog box, shown in Figure 4.4. This dialog box enables you to quickly change the button's icon, tooltip, or text label. Each icon group shows both the standard icon and the grayed-out disabled version of the icon. Default buttons also can be changed. The Odd Only check box shows only the standard icons.

# Note

If a text label doesn't fit within the toolbar button, you can increase the button width using the Fixed Width Text Buttons spinner in the General panel of the Preference Settings dialog box.
