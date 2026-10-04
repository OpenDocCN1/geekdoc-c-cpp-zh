# Appendix O: Solutions to Odd Numbered Review Questions

65. File should be opened as

```
fstream file("info.dat", ios::in | ios::out);
or
fstream file:
file.open("info.dat", ios::in | ios::out);
```

67. File access logs must be specified with fstream objects.

69. The file class flag should be ios::in. Also, the get member function cannot be used to read a string.

71. The file class flag should be ios::out. Also, the last line should read
dataFile.write(reinterpret_cast<char *>(&dt), sizeof(dt));

# Chapter 13

+   1. A class describes a data type. An instance of a class is an object of the data type that exists in memory.

+   3. private

+   5. A class is analogous to the blueprint.

+   7. Yes it is. This protects the variables from being directly manipulated by code outside the class, and prevents them from receiving invalid data.

+   9. When the function is for internal processing, but not useful to the program outside the class. In some cases a class may contain member functions that initialize member variables or destroy their contents. These functions should not be accessible by an external part of the program because they be called at the wrong time.

+   11. A default constructor is a constructor that is called without any arguments. It is not to have more than one default constructor.

+   13, the constructor executes when the object is created.

+   15. A class's responsibilities are the things that the class is responsible for knowing and the actions that the class is responsible for doing.

+   17. procedural programming, object-oriented programming

+   19. object-oriented

+   21. class

+   23. access specifier

+   25. public

+   27. ->

+   29. canine.cpp

+   31. constructor

+   33. constructors