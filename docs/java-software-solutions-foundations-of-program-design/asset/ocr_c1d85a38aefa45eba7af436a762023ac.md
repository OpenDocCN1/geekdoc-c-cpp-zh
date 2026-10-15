provide our own. This default constructor generally has no effect on the newly created object.

# SELF-REVIEW QUESTIONS (see answers in Appendix N)

+   SR 4.24 What are constructors used for?

+   SR 4.25 How are constructors defined?

# 4.6 Graphical Objects

Some objects have a graphical representation, meaning that their state and behaviors include information about what the object looks like visually. A graphical object might contain data about its size and color, for instance, and it may contain methods to draw it.

In Chapter 3 we instantiated and used graphical components such as frames, panels, labels, and images. Certainly these components can be considered graphical objects. This section examines some of them in more detail and explores how to define our own objects that have graphical characteristics.

The program in Listing 4.5 displays a smiling face and a text caption. The main method in the SmilingFace class does not deal with all of those details, however. Instead, the main method sets up the frame for the program and uses it to display an instantiation of the SmilingFacePanel class.

The SmilingFacePanel class is shown in Listing 4.6. It defines two constants on which the drawing is based (BASEX and BASEY), a constructor that sets up the key aspects of the panel, and a method called paintComponent that draws the face that we see when the program is executed. In this case, instead of adding GUI components to this panel, we are simply drawing on it.

Note that the SmilingFacePanel class extends the JPanel class. As we mentioned in Chapter 2 in our discussion of applets, the extends clause establishes an inheritance relationship. The SmilingFacePanel class inherits the characteristics of the JPanel class. That is, a SmilingFacePanel is a JPanel. At this point, that’s all you really need to know about inheritance, which is discussed in detail in Chapter 9.

The constructor of the SmilingFacePanel class sets the background color and preferred size of the panel, as well as setting the panel’s default font. Note that these calls are not made to some other object, as we did in Chapter 3 when we created a separate JPanel object. When a method is called without being invoked through a particular object, you can think of it as the object “talking to itself.” The calls in the constructor are made to the object represented by the SmilingFacePanel class.

![](bbox=[0.08, 0.78, 0.18, 0.9])