# Chapter 8

Class dialog box that displays and the C++ Class template in the right pane and press Enter. You can then enter the name of the class that you want to create, CBox, in the Generic Class Wizard dialog box as shown in Figure 8-9.

![](bbox=[0.17, 0.16, 0.77, 0.49])

Figure 8-9

The name of the file that’s indicated on the dialog, Box.cpp, is used to contain the class implementation, which consists of the definitions for the function members of the class. This is the executable code for the class. You can change the name of this file if you want, but Box.cpp looks like a good name for the file in this case. The class definition will be stored in a file called Box.h. This is the standard way of structuring a program. Code that consists of class definitions is stored in files with the extension .h, and code that defines functions is stored in files with the extension .cpp. Usually, each class definition goes in its own .h file, and each class implementation goes in its own .cpp file.

When you click on the Finish button in the dialog box, two things happen:

+   1. A file Box.h is created, containing a skeleton definition for the class CBox. This includes a no-argument constructor and a destructor.
+   2. A file Box.cpp is created containing a skeleton implementation for the functions in the class with definitions for the constructor and the destructor(both bodies are empty, of course.

The editor pane displaying the code should be as shown in Figure 8-10. If it is not presently displayed, just double-click CBox in Class View, and it should appear.