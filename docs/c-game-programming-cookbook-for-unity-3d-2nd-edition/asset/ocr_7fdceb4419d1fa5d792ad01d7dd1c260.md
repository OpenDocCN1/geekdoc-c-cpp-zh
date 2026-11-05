# 2.3 Open the Main Game Scene

In the Project panel, there are a lot of folders. Most of them are sub-folders inside the GPC_Framework folder. We do not need to get into these just yet, but you should know that the files in GPC_Framework make up the framework and they are separated from everything else to keep framework files and your games files separated and neat.

Find the Games folder and click the little arrow next to it to expand out the folder to show its contents. It is intended that, whenever you build a game with the framework, you use the Games folder to put the assets that are specific to your game only.

The folder structure under Games looks like this:

+   - Games
+     - RunMan
+       - Audio
+       - Prefabs
+       - Scenes
+       - Scripts
+       - Sprites

Stay as organized as possible as you move forward with game projects. This will help a lot as your project grows (and, often, they grow much bigger than you might expect!) to stay on course and spend less time looking for lost assets.

In the Project panel, click on the Scene folder to show its contents. There is a single Scene inside that folder, named runMan_core. This is the Scene that will contain the main game. There will also be a main menu Scene, which we will add later in this chapter.

Double click on the runMan_core Scene in the Project panel, to open it. The Game panel will show the user interface already set up (Figure 2.6) but there's no other logic in the Scene yet, so pressing Play will do nothing. By using the framework, at the end of this chapter you will have a fun infinite runner game to play here instead. The books game framework takes care of most of the heavy lifting

![](bbox=[0.31, 0.6, 0.79, 0.81])

Figure 2.6 To save time, the User Interface is already set up in the game Scene of the example project for this chapter.