them started. The great thing about this menu is that it's completely open to interpretation. It could be built out to work for just about any kind of game with the addition of some graphics and sounds. As you develop your games and develop your style, having an operational menu will help during testing.

The main menu system is used by all the example games in this book. It is easy to port between games and have sub-menus for audio and graphics options.

Unity GUI is a flexible system that caters to interfaces that can act as overlays to a regular Camera as well as 3D interfaces presented as a part of a 3D environment. In this chapter, we will look at interfaces as an overlay to the main Camera in the Scene.

# 11.2.1 Designing the Main Menu

The overall design is very basic – the title of the game and three buttons beneath it. One to start the game, one to show the options menu and a button to exit. When you click on exit, a confirmation message appears to ask if you want to leave or not. The options menu contains music and sound volume sliders, and the volume settings will be saved out and remembered for next time.

As well as an interface, this menu utilizes the CanvasManager class (explained in detail back in Chapter 5, Section 5.9.1) to show and hide interfaces. Another important note is that the volume sliders use Unity's AudioMixers to control the volume levels. For more information on using AudioMixers, refer to Chapter 9, Section 9.4.

Each button has a script attached to it by default, added by Unity when you add a button to a Canvas. That script is used in this example to call functions on another GameObject's Script Component – the BaseMainMenuManager Component. BaseMainMenuManager handles all the logic for the menu, the scripts on the UI elements simply call them.

In the Scene, an empty GameObject named UI contains one Canvas for each menu. The hierarchy for that looks like this:

+   UI
+   Menu_Canvas – the main menu
+   Options_Canvas – the options menu
+   Loading_Canvas – a screen to overlay that tells users loading is happening
+   Exit_Confirm_Canvas – yes/no to exit

The main menu script in this example uses a script Component named MenuWithProfiles, which uses another Component named Base Profile Manager for the saving and loading of music volumes. An empty GameObject named MenuManager holds the menu script along with CanvasManager and the Component Base Profile Manager. The CanvasManager contains a list of all the canvases so that we can easily call on it to show or hide them as we need to. To kick off this chapter, we take a look at the code behind the BaseMainMenuManager script and then how it is overridden to make a menu with profiles.