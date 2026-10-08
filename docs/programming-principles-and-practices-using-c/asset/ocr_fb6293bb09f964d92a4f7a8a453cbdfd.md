by **new**, etc.). Then add a copy constructor and a copy assignment so that you can use **Tracer** objects to see when copying is done.

+   14. Provide a GUI interface and a bit of graphical output to the “Hunt the Wumpus” game from the exercises in Chapter 18. Take the input in an input box and display a map of the part of the cave currently known to the player in a window.

+   15. Modify the program from the previous exercise to allow the user to mark rooms based on knowledge and guesses, such as “maybe bats” and “bottomless pit.”

+   16. Sometimes, it is desirable that an empty **vector** be as small as possible. For example, someone might use **vector< vector< vector< int > > >** a lot but have most element vectors empty. Define a **vector** so that **sizeof( vector< int > )==sizeof( int \*)**, that is, so that the **vector** itself consists only of a pointer to a representation consisting of the elements, the number of elements, and the **space** pointer.

# # Postscript

Templates and exceptions are immensely powerful language features. They support programming techniques of great flexibility – mostly by allowing people to separate concerns, that is, to deal with one problem at a time. For example, using templates, we can define a container, such as **vector**, separately from the definition of an element type. Similarly, using exceptions, we can write the code that detects and signals an error separately from the code that handles that error. The third major theme of this chapter, changing the size of a **vector**, can be seen in a similar light: **push_back()**, **resize()**, and **reserve()** allow us to separate the definition of a **vector** from the specification of its size.