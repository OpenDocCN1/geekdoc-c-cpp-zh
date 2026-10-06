# Case Classes

The input for the program will have a first line that is the number of bodies, the timestep, the stopping time, and the number of steps between outputs. This will be followed by lines with the x, y, vy, and mass values for each particle. A sample input file can be found on the book's website on the page for this chapter. Note the central mass in that file has a mass of 1 and all the others are much smaller.

As output, you will write out the positions of all the particles in your simulation to file once for every n steps, where n is a value given on the first line of the input. If you do this then you can run a spreadsheet of gnuplot to plot it. If you use gnuplot and give it the command 'output' it will make a little scatter plot showing the paths of the particles in the simulation.

+   2. Project builds on top of project 8.1. You have likely been using tuples or separate values to represent the geometry elements in your ray tracer. This is information that is much more naturally represented as a case class. For this project you should go and edit your existing code so that it includes three case classes, for spheres, for planes, and for a scene which has a List[Sphere] and a List[Plane].

+   3. This is the first installment for you building your own text adventure. Your program will read in a map file that you will write and let the user run around that map by using commands like "north" to move from one room to another. The map file will have a fairly simple format right now and you can create your own map file using. Make sure when you turn in this program you turn in both the script and the map file so it can be tested with your map.

The format of the map file should start with a line telling the number of rooms then has something like this. You can change this if you want to use a slightly different format:

```
room_number
room_name
long line of room description
number_of_links
direction1
destination1
direction2
destination2
...
```

This is repeated over and over. (The number of rooms helps for storing things in an Array that you know big to make it.) Each room should have a unique room number, and they should start at 0. The reason is that you will be putting all the room information into Arrays. There is a link on the book's website to a sample map file, but you do not have to stick exactly to that format if you do not want to. Use it if you are thinking about other options you might want in later. Odds are good if you will be refactoring your code for later projects.

The interface for your program is quite simple. When you run the program it should read in the map file and keep all the map information stored in an Array[Room Where is a case class you have made to keep the significant information for each room.³ You will start the user in room 0 and print the description of that room

> ⁴Many implementations also make a case class to represent an Exit from a room.