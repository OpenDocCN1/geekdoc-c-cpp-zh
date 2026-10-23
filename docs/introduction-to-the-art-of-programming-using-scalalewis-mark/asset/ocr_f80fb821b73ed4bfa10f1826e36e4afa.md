model where there is a separate application running as the server and then various clients connect.

In the client-server model, much of the game logic will likely be processed on the server. The clients become graphical displays and the medium for user interactions. The commands given to the clients are likely sent to the server with little interpretation.

If your game is only a two-player networked game, you might skip having a server and instead have a single application where the user can set their instance up as something of a local server for a second instance to connect to. In this situation, the game logic will happen primarily on that “main” instance and the second client is primarily just sending and displaying information.

One thing that you will probably realize fairly quickly when you work on this is that distributed parallel applications, those running on multiple machines across a network, can have their own types of race conditions as the different clients might not always be seeing the same world.

+   4.  A game that is not supposed to involve networking is probably the most difficult project to tie networking into. One reason that you might want to include networking is to be able to keep track of things going on in the game outside of the normal display or provide other types of basic interaction. This is largely useful for debugging.
+   
+       Large and complex software often needs to have the ability to do “logging.” This is where different steps in the code write out what they are doing to a file or something similar. When things go wrong, you can consult the log files to see what happened. Instead of logging to a file, you can make your game log to the network. Have your game create a `ServerSocket` that accepts connections. All logging should go to all the connections. If there are no connections, the logging is basically skipped.
+   
+       While logging to the network lacks some of the advantages of logging to a file, like an easy way to go back over things. It provides the flexibility that you can use commands written to the network connection. These commands could be to query information for use in debugging, or they could be like a superuser mode to set up situations that would be hard to create when you are testing your program.
+   
+   5.  The math workbook program could involve networking in at least two different ways. One would be that addition of collaborative features, like those added to the drawing program in this chapter, so that users can send a complete or partial worksheet from one computer to another.
+   
+       It is also possible to add logging features, like those described in project 4. The logging features for a math worksheet are most likely going to be for debugging purposes to inspect what is happening in the background.
+   
+       You can decide whether you want to implement one or both of these options into your code. Pick what interests you most and fits with your objectives for the project.
+   
+   6.  For the Photoshop<sup>B</sup> project you could add networking in the form of collaboration, logging, and/or using a URL to pull down images from the web. The collaboration could be much like what was shown in the chapter, though it should be altered to fit the flow of the program you are developing. Logging would be most useful for debugging as described in project 4. Both of those options are fairly significant, and you only need to pick one.
+   
+       The addition of loading images from URLs across the web is very straightforward and really is something that should be in this type of application. Whichever of the other