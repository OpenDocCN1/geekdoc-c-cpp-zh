minate immediately, without allowing the destructors of any objects to be called. Function abort is usually used to indicate an abnormal termination of the program.

# Constructors and Destructors for Local Objects

The constructor for a local object is called when execution reaches the point where that object is defined—the corresponding destructor is called when execution leaves the object's scope (i.e., the block in which that object is defined has finished executing). Constructors and destructors for local objects are called each time execution enters and leaves the scope of the object. Destructors are not called for local objects if the program terminates with a call to function exit or function abort.

# Constructors and Destructors for static Local Objects

The constructor for a static local object is called only once, when execution first reaches the point where the object is defined—the corresponding destructor is called when main terminates or the program calls function exit. Global and static objects are destroyed in the reverse order of their creation. Destructors are not called for static objects if the program terminates with a call to function abort.

# Demonstrating When Constructors and Destructors Are Called

The program of Figs. 17.7–17.9 demonstrates the order in which constructors and destructors are called for objects of class CreateAndDestroy (Fig. 17.7 and Fig. 17.8) of various storage classes in several scopes. Each object of class CreateAndDestroy contains an integer (objectID) and a string (message) that are used in the program's output to identify the object (Fig. 17.7, lines 16–17). This mechanical example is purely for pedagogic purposes. For this reason, line 19 of the destructor in Fig. 17.8 determines whether the object being destroyed has an objectID value 1 or 6 (line 19) and, if so, outputs a newline character. This line makes the program's output easier to follow.

```
1 // Fig. 17.7: CreateAndDestroy.h
2 // CreateAndDestroy class definition.
3 // Member functions defined in CreateAndDestroy.cpp.
4 #include <string>
5 using namespace std;
6
7 #ifndef CREATE_H
8 #define CREATE_H
9
10 class CreateAndDestroy
11 {
12 public:
13   CreateAndDestroy( int, string ); // constructor
14   ~CreateAndDestroy(); // destructor
15 private:
16   int objectID; // ID number for object
17   string message; // message describing object
18 }; // end class CreateAndDestroy
19
20 #endif
```

Fig. 17.7 | CreateAndDestroy class definition.