![](bbox=[0.13, 0.14, 0.22, 0.26])

You never need to memorize the names or features of Java's API classes. Instead, you keep Java's API documentation handy. When you need to know about a class, you look it up in the documentation. If you need a certain class often enough, you'll remember its features. For classes that you don't use often, you always have the docs.

For tips on using Java's API documentation, see my article “Making Sense of Java's API Documentation,” at www.dummies.com/extras/beginningprogrammingwithjava. To find gobs of sample Java code, visit some of the websites listed in Chapter 21.

# Just another class

What is a JFrame? Like any other class, a JFrame has several parts. For a simplified view of some of these parts, see Figure 20-2.

Figure 20-2:
A simplified depiction of the JFrame class.

![](bbox=[0.25, 0.55, 0.78, 0.75])

Like the String in Figure 18-6 in Chapter 18, each object formed from the JFrame class has both data parts and method parts. The data parts include the frame's height and width. The method parts include add, setDefaultCloseOperation, pack, and setVisible. All told, the JFrame class has about 320 methods.

For technical reasons too burdensome for this book, you can't use dots to refer to a frame's height or width. But you can call many JFrame methods with those infamous dots. In Listing 20-1, I call the frame's methods by writing add(label), frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE), frame.pack(), and frame.setVisible(true).