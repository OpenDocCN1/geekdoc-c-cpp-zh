KEY CONCEPT
Establishing the relationship between a listener and the component it listens to is accomplished using polymorphism.

The answer is polymorphism. If you examine the source code for the addActionListener method, you'll discover that it accepts a parameter of type ActionListener, the interface. Therefore, instead of accepting a parameter of only one object type, the addActionListener method can accept any object of any class that implements the ActionListener interface. All other add listener methods work in similar ways.

The JButton object doesn't know anything particular about the object that is passed to the addActionListener method, except for the fact that it implements the ActionListener interface (otherwise the code wouldn't compile). The JButton object simply stores the listener object and invokes its actionPerformed method when the event occurs.

In Chapter 9 we discussed that we can also create a listener by extending an adapter class. Well, it turns out that using an adapter class isn't really a new way to create a listener after all. Each adapter class is written to implement the appropriate listener interface, providing empty methods for all event handlers. So by extending an adapter class, the new listener class automatically implements the corresponding listener interface. And that is what really makes it a listener such that it can be passed to an appropriate add listener method.

Thus, no matter how a listener object is created, we are using polymorphism via interfaces to set up the relationship between a listener and the component it listens to. GUI events are a wonderful example of the power and versatility provided by polymorphism.

# 10.8 File Choosers

KEY CONCEPT
A file chooser allows the user to browse a disk and select a file to be processed.

Dialog boxes were introduced in Chapter 6. We used the JOptionPane class to create several dialog boxes to present information, accept input, and confirm actions.

The JFileChooser class represents another specialized dialog box, a file chooser, which allows the user to select a file from a hard disk or other storage medium. You have probably run many programs that allow you to open a file using a similar dialog box.

The program shown in Listing 10.13 uses a JFileChooser dialog box to select a file. This program also demonstrates the use of another GUI component, a text area, which is similar to a text field but can display multiple lines of text at one time. After the user selects a file using the file chooser dialog box, the text contained in that file is displayed in a text area.