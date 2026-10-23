
The last thing we need is to add this functionality to the GUI. First we add the following two lines to DrawingMain so that it can keep track of a server and a client.

```
private var server:CollaborationServer = null
private var client:CollaboratorImpl = null
```

After that, the following code can be added to the “Collaborate” menu below the two options for simple sharing.

```
contents += new Separator
val joinItem = new MenuItem("Join") {
  action = Action("Join") {
    text = "View"
    if(server==null) {
      val host = Dialog.showInput(null, "What server host do you want to use?", "Server Name", Dialog.Message.Question, null, Nil, "")
      if(host.nonEmpty && host.get.trim.nonEmpty) {
        try {
          Naming.lookup("rmi://"+host.get+"/Collaborate") match {
            case svr:CollaborationServer =>
              server = svr
              client = new CollaboratorImpl(server)
            case _ => Dialog.showMessage(tabbedPane,"The wrong type of object was found on that server.")
          }
        } catch {
          case ex:NotBoundException =>
            server = new CollaborationServerImpl()
            Naming.bind("Collaborate",server)
            client = new CollaboratorImpl(server)
        }
      }
    }
    if(client!=null) client.showFrame
  }
}
contents += joinItem
contents += new MenuItem(Action("Share"){
  val title = Dialog.showInput(null, "What do you want to call this drawing?", "Drawing Title", Dialog.Message.Question, null, Nil, "")
  if(title.nonEmpty) {
    server.addDrawing(title.get, openDrawings(tabbedPane.selection.index))
  }
})
```

This gives a “Join” option that asks for a host, then uses RMI to try to look up a server on that host. If one is found, it connects to it. Otherwise one is created and bound to that host. The share option simply asks for a title for the drawing and then sends the currently selected drawing to the server.

This section contains a fair bit of code that really requires some exploration. It is highly recommended that you enter this all in and play with it to see how it works. It is worth noting that while the RMI code might not look like it involves threads, RMI calls do come across on a separate thread so some applications will have to take that into account.

model where there is a separate application running as the server and then various clients connect.

In the client-server model, much of the game logic will likely be processed on the server. The clients become graphical displays and the medium for user interactions. The commands given to the clients are likely sent to the server with little interpretation.

If your game is only a two-player networked game, you might skip having a server and instead have a single application where the user can set their instance up as something of a local server for a second instance to connect to. In this situation, the game logic will happen primarily on that “main” instance and the second client is primarily just sending and displaying information.

One thing that you will probably realize fairly quickly when you work on this is that distributed parallel applications, those running on multiple machines across a network, can have their own types of race conditions as the different clients might not always be seeing the same world.

- 4. A game that is not supposed to involve networking is probably the most difficult project to tie networking into. One reason that you might want to include networking is to be able to keep track of things going on in the game outside of the normal display or provide other types of basic interaction. This is largely useful for debugging.
- 
- Large and complex software often needs to have the ability to do “logging.” This is where different steps in the code write out what they are doing to a file or something similar. When things go wrong, you can consult the log files to see what happened. Instead of logging to a file, you can make your game log to the network. Have your game create a `ServerSocket` that accepts connections. All logging should go to all the connections. If there are no connections, the logging is basically skipped.
- 
- While logging to the network lacks some of the advantages of logging to a file, like an easy way to go back over things. It provides the flexibility that you can use commands written to the network connection. These commands could be to query information for use in debugging, or they could be like a superuser mode to set up situations that would be hard to create when you are testing your program.
- 5. The math workbook program could involve networking in at least two different ways. One would be that addition of collaborative features, like those added to the drawing program in this chapter, so that users can send a complete or partial worksheet from one computer to another.
- 
- It is also possible to add logging features, like those described in project 4. The logging features for a math worksheet are most likely going to be for debugging purposes to inspect what is happening in the background.
- 
- You can decide whether you want to implement one or both of these options into your code. Pick what interests you most and fits with your objectives for the project.
- 6. For the Photoshop™ project you could add networking in the form of collaboration, logging, and/or using a URL to pull down images from the web. The collaboration could be much like what was shown in the chapter, though it should be altered to fit the flow of the program you are developing. Logging would be most useful for debugging as described in project 4. Both of those options are fairly significant, and you only need to pick one.
- 
- The addition of loading images from URLs across the web is very straightforward and really is something that should be in this type of application. Whichever of the other

two networking options you choose, you should probably add this possibility on top of it.

7. The simulation workbench provides a very different feature to add networking to the application. The fact that simulations can be highly processor intensive means that there can be benefits to breaking the work-load not only across threads, but also across multiple machines. This form of distributed computing requires networking.

You should make a second application for a helper node that you can run on other computers. That helper application will make a network connection to the main application and wait to be given work. The simplest way to divide the work is to have separate simulations on each machine with information passed back occasionally for the purposes of displaying data to the user and perhaps saving. If the number of particles in a simulation is really large, it can make sense to distribute that one simulation across multiple machines. This is a more challenging problem as the different machines have to communicate the state of the particles they are controlling for force calculations.

It is left to the student to decide how involved you wish to get with distributing your simulations.

# Chapter 24

# Stacks and Queues

- 24.1 Abstract Data Types (ADTs) ......................................................... 634
- 24.2 Operations on Stacks and Queues .................................................... 634
- 24.3 Real Meaning of O ............................................................... 635
- 24.4 O(1) Requirement ............................................................... 636
- 24.5 Array-Based Stack .............................................................. 637
- 24.6 Array-Based Queue .............................................................. 641
- 24.7 Unit Tests ............................................................... 644
- 24.7.1 Setup ............................................................... 644
- 24.7.2 Writing Tests ........................................................ 645
- 24.7.3 Test Suites ........................................................ 648
- 24.7.4 Test-Driven Development ............................................... 649
- 24.8 RPN Calculator .............................................................. 649
- 24.9 End of Chapter Material ...................................................... 653
- 24.9.1 Summary of Concepts ................................................... 653
- 24.9.2 Exercises ........................................................... 654
- 24.9.3 Projects ........................................................... 654

The last few chapters have extended the depth of your knowledge in libraries so that you have the capability to do more inside of your programs. Now we are going to switch gears for a while and start looking at what goes into constructing data structures and writing some basic libraries. You started using simple data structures in the default libraries in chapter 7. We saw other types of data structures in chapter 20. Most of the time you are writing programs, you will use these types of pre-existing libraries. After all, they have been written by experienced people who put a lot of time and effort into tuning them so that they are flexible and efficient.

The fact that you will typically use libraries written by others might tempt you to believe that you really do not need to know what is going on inside of these data structures. On the contrary, understanding the inner working of data structures is an essential skill for any competent developer. One reason for this is that you often have many different options to choose from when you select a data structure and picking the right one requires knowing certain details. For example, so far we have treated the List and Array types almost interchangeably when we need a Seq with the exception that the List type is immutable. In chapter 25 we will see that the two are much more different than that and that even when we just focus on lists, there are many options.

Knowing how different data structures work and how to implement them is also required if you ever have to implement your own. This might happen for one of several reasons. One is that you are developing for a system where you are required to use a lower-level language that does not come with advanced collections libraries. Another is that you have a problem with very specific requirements for which none of the provided structures are really appropriate. If you do not understand and have experience writing data structures, you will
