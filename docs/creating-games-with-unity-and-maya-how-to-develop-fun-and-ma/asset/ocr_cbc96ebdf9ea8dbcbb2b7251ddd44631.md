![](bbox=[0.18, 0.11, 0.65, 0.5])

FIGURE 18.14 Creating a build.

# # A Few Notes on the Output Files

When creating a Windows build, do note that there are actually two files. The first is the .exe file—the actual executable that the player launches to play the game. The second is a folder that is called NameOfYourGame_Data. To play the game, both must be present and in the same folder. When distributing the build, I find it helpful to take both files (the executable and the data folder) and zipping them into one archive and sending that off. We have had occasion here where we sent off a project to a client, who then tried to show it to someone else by just sending the .exe—it doesn't work.

On the Mac side, things are a little more elegant for the final user. An .app in Mac OS X looks to the user like a simple icon in their Finder. However, in reality it's really a folder (that OS X calls a Package) that contains a bunch of things. When Unity creates a Mac build, it creates an .app folder. On a PC, this will appear as a folder (which I usually compress into a zip archive before sending it off to someone), but when a Mac user unzips it to his machine, it will appear as a single icon that will contain all the assets he needs. The user just double-clicks to launch it.

Finally, note that when creating a Web Player build, Unity won't ask for a simple location to save the build—it will ask specifically for a Folder. The reason for this is that there are some very closely linked files that Unity will output. One will be the .html file that presents the Unity content (a .unity3d file). The specifics of this .html file can be controlled in a general way via the Player Settings in the Per-Platform Setting section. Specifically, the look of this html file can be altered and customized manually via your favorite HTML editor.