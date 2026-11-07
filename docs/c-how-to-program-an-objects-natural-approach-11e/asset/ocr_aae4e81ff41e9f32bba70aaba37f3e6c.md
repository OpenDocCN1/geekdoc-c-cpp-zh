assignment and destructors. Chapter 11 introduces the three-way comparison operator and discusses the details of all these special member functions, including

+   - when you might need to define custom versions of each and
+   - the various C++ Core Guidelines for these special member functions.

You'll see that you should design your classes so the compiler can auto-generate the special member functions for you. This is called the “Rule of Zero,” meaning that you provide no special member functions in the class's definition.

# ## Checkpoint

+   1. *(Discussion)* Why are constructors usually public?  
+      Answer: So any code with access to the class definition can create and initialize objects of that class.
+   2. *(Discussion)* In any class that does not define a constructor, the compiler generates a default constructor with no parameters. What does that default constructor do?  
+      Answer: The default constructor does not initialize the class's fundamental-type data members but does call the default constructor for each data member that's an object of another class.
+   3. *(Code)* Assume class `Account` has two data members named `m_firstName` and `m_lastName`. Define a constructor that would initialize both data members using strings passed to the constructor. This constructor must be called with two arguments, so you do not need to declare it `explicit`.  
+      Answer:

```
```cpp
Account(std::string_view firstName, std::string_view lastName)
    : m_firstName{firstName}, m_lastName{lastName} {
    } // empty body
```
```

# ## 9.5 Software Engineering with Set and Get Member Functions

As you'll see in the next section, set member functions can validate attempts to modify private data, and get member functions can control how that data is presented to the caller. These are compelling software engineering benefits.

A client of the class is any other code that calls the class's member functions. If a data member were public, any client could see the data and do whatever it wanted with it, including setting it to an invalid value.

You might think that even though a client cannot directly access a private data member, the client can do whatever it wants with the variable by calling public set and get functions. You'd think that you could call the public get function to peek at the private data and see exactly how it's stored in the object, and that you could call the public set function to modify the private data at all.

Actually, set functions can be written to validate their arguments and reject any attempts to set the data to incorrect values, such as

+   - a negative body temperature,