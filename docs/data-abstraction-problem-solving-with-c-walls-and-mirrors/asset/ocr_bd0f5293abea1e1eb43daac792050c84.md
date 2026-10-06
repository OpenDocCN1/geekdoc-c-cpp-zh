the function's header followed by a semicolon—that is, its prototype—at the beginning of the program that calls it. For example, the prototype of the function realCube is

```
double realCube(double x);
```

Then you can place the function definition anywhere within your program.
in large programs, function prototypes are placed into one or more header files, as described in Section K.1 of Appendix C. You then include the header files in your program. Prototypes are also important in the creation of classes, as you will see in the next section. Section A.8.1 of Appendix A also discusses header files.
Note that you can pass a function as an argument to another function or method. This is discussed in Section 15.2.1 of Chapter 15.

# L.4 Classes

Python classes permit clients of the classes to access all data and methods. In C++, this is called public access and is recommended only for methods. In Python, when you create a class member that should be used only by methods, you typically prefix the member's name with underscores. This convention is only a signal to the programmer; the interpreter does not enforce it. C++ restricts direct access to certain data fields and methods by labeling them private, and the compiler enforces this restriction by permitting only methods to access private members.
Classes in C++ have constructors that are similar to the __init__ method. When writing a method in a Python class, you prefix the names of data fields by self to indicate that they are instance variables of the class. Instance variables in a C++ class do not need a special prefix, if they are referenced within a method of the class.
Here is a simple Python class, PlainBox:

```
class PlainBox
```

```
def __init__(self, item):
    self.item = item

def setItem(self, item):
    self.item = item

def getItem(self):
    return self.item
```

You can also define the same class in a form that is closer to that of a C++ class:

```
class PlainBox
    item = ""

def __init__(self, item):
    self.item = item

def setitem(self, item):
    self.item = item
ndef getItem(self):
    return self.item
```

Though it is possible to define a class in C++ in a single file, we will use two files, since this is a more common and flexible approach. The first file is the class header file; it contains the data fields for the class and prototypes for all methods defined in the class. It is a description of the class and does