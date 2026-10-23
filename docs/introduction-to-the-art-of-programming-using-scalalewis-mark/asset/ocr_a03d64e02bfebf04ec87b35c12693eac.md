stays small and no copies are needed for most operations. Like the stack, when the Array does have to grow, it should do so by a multiplicative factor.

+   Testing is a very important part of software development. Unit Tests are tests of the functionality of small units of code, such as single classes. The JUnit framework provides a simple way of building unit tests that can be run regularly during software development.

# 24.9.2 Exercises

+   1. Add extra functions to the RPN calculator.
+   2. Write more tests for the JUnit tests that are shown in the book.
+   3. Write some code so that requests that are sent across a network are queued up and handled in the order they arrive. You can simulate a long-running calculation with Thread.sleep.
+   4. For this exercise you should implement a few possible versions of both the queue and the stack and then perform timing tests on them to see how well they scale. You will include the implementation that we developed in this chapter plus some slightly modified implementations to see how minor choices impact the final speed of the implementation.
+   5. Build your own version of BlockingQueue using synchronized.wait. and notifyAll to reproduce the behavior of the version in java.util.concurrent.

# 24.9.3 Projects

As you can probably guess, the projects for this chapter have you adding stacks and/or queues to your code. A number of them have you making thread-safe queues to put into your code in places you might have been using a java.util.concurrent.BlockingQueue.

+   1. If you have been working on the MUD project, for this iteration you should make your own thread-safe queue, specifically for handing players who have logged in from the server socket thread to the main game thread. You can decide exactly what functionality to include, but the two critical aspects are that it needs to be a FIFO and thread-safe.
+   2. If you have been working on the web spider project, make and use your own thread-safe queue for handing information between the socket reading threads and the parsing threads and back. There will be at least two instances of queues for these functions with at least one for each direction of data flow.
+   3. If you are working on a networked graphical game you need to write a thread-safe queue for the same purposes as that needed for the MUD.
+   4. Back in project 4 (p.494) on the math worksheet it was suggested that you could integrate polymorphism into your project by using the command pattern. One of the main uses of the command pattern is to implement undo and redo capabilities. A stack is an ideal data structure for doing this. You have the main application keep track of two stacks. One is the undo stack, which you push commands onto as they