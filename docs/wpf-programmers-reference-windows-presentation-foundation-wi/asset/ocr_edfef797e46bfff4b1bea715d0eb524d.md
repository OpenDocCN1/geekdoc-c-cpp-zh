This code gets the menu item that triggered the event and looks at the item's Tag property to see which resource file to load. It creates a ResourceDictionary object loaded from the file, removes old resource dictionaries from the application's MergedDictionaries collection, and adds the new dictionary.

# REMOVED RESOURCES REDUCX

The program doesn't remove the first resource dictionary so that WPF doesn't get confused about missing resources and issue a flood of warnings. For more information, see the note “Removed Resources” in the “Dynamic Resources” section of Chapter 12.

When the program loads the new resource dictionary, WPF detects the changes and updates all of the window's dynamic resources.

This technique is what most developers think of skinning in WPF applications: The program loads multiple resource files at run to provide different skins.

# Animated Skins

The skins described in the previous section use separate resource dictionaries to provide different appearances. The program's XAML file sets its control properties to resource values so that when you change the resource values, the interface changes accordingly.

Another way to change property values is use property animation. Chapter 14 covers property animation in greater detail, but this section explains briefly how to use animation to skinning.

XAML files allow you to define triggers that launch storyboards represent represent properties. For example, when the user presses the mouse down over a rectangle, the XAML code can run a storyboard that varies the Rectangle's Width property smoothly from 100 to 200 over a 1-second period.

The AnimatedSkins program uses this technique to provide skinning. Figure 16-9 shows the program displaying its green skin. Figure 16-10 shows its blue skin.

When you click the appropriate control, a trigger launches a storyboard that:

+   - Resizes the main window and changes its Background brush.
- Hides and displays the small blue or green ellipses in the upper-right corner that you click to switch skins.
- Moves Labels.

![](bbox=[0.598, 0.566, 0.928, 0.693])

FIGURE 16-9

![](bbox=[0.598, 0.736, 0.928, 0.891])

FIGURE 16-10