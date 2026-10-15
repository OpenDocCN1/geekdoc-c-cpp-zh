applications, to avoid problems at a later time. Someone who later uses the class directly or extends the class may assume the existence of a valid toString method.

SR 9.22 The final modifier can be applied to a particular method, which keeps that method from being overridden in a child class. It can also be applied to an entire class, which keeps that class from being extended at all.

# 9.6 The Component Class Hierarchy

SR 9.23 a. True, b. True, c. False, d. False, e. False, f. True

SR 9.24 The benefits include not having to worry about the details of applet creation and execution, or how the applet interacts with the browser, or security concerns. Essentially, you do not have to worry about anything that would be a common concern across all applets; such concerns have already been handled. You just have to worry about what makes your applet different from other applets.

# 9.7 Extending Adapter Classes

SR 9.25 An adapter class is a class that implements a listener interface, providing empty definitions for all of its methods. A listener class can be created by extending the appropriate adapter class and overriding the methods of interest.

SR 9.26 The OffCenterPanel class extends the JPanel class. The JPanel class inherits from all of the other classes mentioned. Therefore, an OffCenterPanel object “is” a JPanel, and a JComponent, and a Container, and an Object.

SR 9.27 The OffCenterListener class extends the MouseAdapter class. Since the MouseAdapter class includes methods for each of the mouse events, the OffCenterListener class inherits those methods and does not need to define them directly.

# 9.8 The Timer Class

SR 9.28 An object created from the Timer class produces an action event at regular intervals. It can be used to control the speed of an animation.

SR 9.29 The Timer constructor is called in the ReboundPanel constructor to set the initial delay and to associate a listener with the timer. The start