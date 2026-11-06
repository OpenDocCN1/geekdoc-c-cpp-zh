Then the returns follow: The Cook object returns an object called MyHamburger (which is of class Food). The Server object receives this and returns it to the user.

Think about this: How can the user call a function? A user can do it through a user interface, such as a window on the screen with buttons on it or, perhaps, a menu item. That is, the user interface is the part that you see on the screen! And the name makes sense: It's the interface to the application for the user. Thus, you have a deeply philosophical concept here: By using the screen, keyboard, and mouse, you are interfacing with the computer application, calling member functions. Pretty good!

And finally, notice that the user deletes the object. How can this be? Remember that this use case has a function that the user called. That function then calls destroy. The object's lifetime ends with the deletion, and you see a big X to show that the line ends.

When an object on a sequence diagram calls a member function of an object to the right, a common term for this process is that the first object is sending a message to the second object. If you are using a tool to help you draw UML diagrams, the arrows might be called something like message arrows.

Book II Chapter 4
Demonstrating Behavior with UML

# Notating sequence diagrams

When you create a sequence diagram, you are free to put some notes to the left of the sequence diagram. These notes on the left describe what the thing does. Figure 4-5 shows an example of this.

![](bbox=[0.31, 0.6, 0.65, 0.85])

The MySquid object creates a new Kladdbubble object

The MySquid object sends the skiddadle message to the Kladdy object

> **Figure 4-5:** You can notate a sequence diagram by putting text along the left side.