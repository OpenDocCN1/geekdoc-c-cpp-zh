
```cpp
std::cout << "Constructed with:\n\n";
displayTime("t1: all arguments defaulted", t1);
displayTime("t2: hour specified; minute and second defaulted", t2);
displayTime("t3: hour and minute specified; second defaulted", t3);
displayTime("t4: hour, minute and second specified", t4);

// attempt to initialize t5 with invalid values
try {
    const Time t5{27, 74, 99}; // all bad values specified
}
catch (const std::invalid_argument& e) {
    std::cerr << std::format("t5 not created: {}\n", e.what());
}
```

```
Constructed with:

t1: all arguments defaulted
24-hour time: 00:00:00
12-hour time: 12:00:00 AM

t2: hour specified; minute and second defaulted
24-hour time: 02:00:00
12-hour time: 2:00:00 AM

t3: hour and minute specified; second defaulted
24-hour time: 21:34:00
12-hour time: 9:34:00 PM

t4: hour, minute and second specified
24-hour time: 12:25:42
12-hour time: 12:25:42 PM

t5 not created: hour was out of range
```

**Fig. 9.12** | Constructor with default arguments. (Part 2 of 2.)

## Software Engineering Notes Regarding Class Time’s Set and Get Functions and Its Constructor

Time’s `set` and `get` functions are called throughout the class’s body. In particular, the constructor (Fig. 9.11, lines 9–11) calls `setTime`, and `to24HourString` and `to12HourString` call `getHour`, `getMinute` and `getSecond` in lines 54 and lines 60–61. We could have accessed the class’s private data in each case directly.

Our internal time representation requires 12 bytes of memory on systems with four-byte ints. Consider changing this to the total seconds since midnight—a single int requiring only four bytes of memory. If we made this change, only the bodies of functions directly accessing the private data would need to change. In this class, we’d modify `setTime` and the `set` function’s bodies for `m_hour`, `m_minute` and `m_second`. There would be no need to modify the constructor or functions `to24HourString` or `to12HourString` because they do not access the data directly.

Duplicating statements in multiple functions or constructors makes changing the class’s internal data representation more difficult. Implementing the Time constructor and functions to24HourString and to12HourString, as shown in this example, reduces the likelihood of errors when altering the class’s implementation.

As a general rule: Avoid repeating code. This principle is called DRY—“don’t repeat yourself.”²⁵ Rather than duplicating code, place it in a member function that can be called by the class’s constructor or other member functions. This simplifies code maintenance and reduces the likelihood of an error if the code implementation is modified.

25. “Don’t Repeat Yourself.” Wikipedia. Wikimedia Foundation. Accessed April 14, 2023, https://en.wikipedia.org/wiki/Don%27t_repeat_yourself.

A constructor can call the class’s other member functions. You must be careful when doing this. The constructor initializes the object, so data members used in the called function may not yet be initialized. Logic errors may occur if you use data members before properly initializing them.

Making data members private and controlling access (especially write access) to those data members through public member functions helps ensure data integrity. The benefits of data integrity are not automatic simply because data members are private. You must provide appropriate validity checking.

### Checkpoint

- 1. *(Discussion)* A constructor can call the class’s other member functions. Explain why you must be careful when doing this.

   **Answer:** The constructor initializes the object, so data members used in the called function may not yet be initialized. Logic errors may occur if you use data members before they have been properly initialized.

- 2. *(True/False)* Making data members private ensures the benefits of data integrity.

   **Answer:** False. Actually, the benefits of data integrity are not automatic simply because data members are private. You must provide appropriate validity checking.

- 3. *(Discussion)* Consider a Time class definition that includes both of the following constructor prototypes:

   ```cpp
   Time(int h = 0, int m = 0, int s = 0);  
   Time();
   ```

   Can this class be used to default construct a Time object? If not, explain why.

   **Answer:** This class cannot be used to default construct a Time object because both constructors may be called with no arguments. If a call is ambiguous, the C++ compiler will issue an error message.

## 9.11.2 Overloaded Constructors and Delegating Constructors

Section 5.14 showed how to overload functions. A class’s constructors and member functions also can be overloaded. Overloaded constructors allow objects to be initialized with different types and/or numbers of arguments. To overload a constructor, provide a prototype and definition for each overloaded version. This also applies to overloaded member functions.

In Figs. 9.10–9.12, class Time's constructor had a default argument for each parameter. We could have defined that constructor instead as four overloaded constructors with the following prototypes (and appropriate definitions in Time.cpp):

```cpp
Time(); // default m_hour, m_minute and m_second to 0
explicit Time(int hour); // default m_minute & m_second to 0
Time(int hour, int minute); // default m_second to 0
Time(int hour, int minute, int second); // no default values
```

Just as a constructor can call a class's other member functions to perform tasks, constructors can call other constructors in the same class. The calling constructor is called a delegating constructor—it delegates its work to another constructor. The C++ Core Guidelines recommend defining common code for overloaded constructors in one constructor, then using delegating constructors to call it.26

26. C++ Core Guidelines, "C.51: Use Delegating Constructors to Represent Common Actions for all Constructors of a Class." Accessed April 14, 2023. https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#Rc-delegating.

The first three of the four Time preceding constructor declarations can delegate work to one with three int arguments, passing 0 as the default value for the extra parameters. To do so, you use a member initializer with the name of the class, as in:

```cpp
Time::Time() : Time{0, 0, 0} {}
Time::Time(int hour) : Time{hour, 0, 0} {}
Time::Time(int hour, int minute) : Time{hour, minute, 0} {}
```

### Checkpoint

- 1. *(True/False)* Overloaded constructors allow objects to be initialized with different types and/or numbers of arguments.

   **Answer:** True.

- 2. *(True/False)* Constructors cannot call other constructors in the same class.

   **Answer:** False. Actually, delegating constructors can call other constructors in the same class to delegate their work.

## 9.12 Destructors

A destructor is a special member function that may not specify parameters or a return type. A class's destructor name is the tilde character (~), followed by the class name, such as ~Time.

A class's destructor is called implicitly when an object is destroyed, typically when program control leaves the scope in which that object was created. The destructor itself does not actually remove the object from memory. It performs termination housekeeping (such as closing a file and cleaning up other resources used by the object) before the object's memory is reclaimed for later use.

Even though destructors have not been defined for the classes presented so far, every class has exactly one destructor. If you do not explicitly define a destructor, the compiler defines a default destructor that invokes any class-type data members' destructors.27 In Chapter 12, we'll explain why exceptions should not be thrown from destructors.

27. We'll see that such a default destructor also destroys class objects that are created through inheritance (Chapter 10).

### Checkpoint

- 1. *(True/False)* A class’s destructor is called implicitly when an object is destroyed, typically when program control leaves the scope in which that object was created.

   **Answer:** True.

- 2. *(Fill-in)* Every class has one destructor. If you do not explicitly define one, the compiler defines a ________ destructor that invokes any class-type data members’ destructors.

   **Answer:** default.

## 9.13 When Constructors and Destructors Are Called

The order in which constructors and destructors are called depends on the objects’ scopes. Generally, destructor calls are made in the reverse order of the corresponding constructor calls, but as we’ll see in Figs. 9.13–9.15, global and static objects can alter the order in which destructors are called.

### Constructors and Destructors for Objects in Global Scope

Constructors are called for objects defined in the global scope (also called global namespace scope) before executing any other function in that file. The execution order of global object constructors among multiple files is not guaranteed, so global objects in separate files should not depend on one another. When `main` terminates via a `return` statement or by reaching its closing brace, the corresponding destructors are called in the reverse order of their construction.

### Destructors on Program Termination

The `exit` function often is called to terminate a program immediately when a fatal unrecoverable error occurs. In this case, the destructors of local objects do not execute.^28 Function `abort` performs similarly to function `exit` but forces the program to terminate immediately without allowing programmer-defined cleanup code of any kind to be called.

Function `abort` is usually used to indicate abnormal program termination.^29

### Constructors and Destructors for Non-static Local Objects

A non-static local object’s constructor is called when execution reaches the object’s definition. Its destructor is called when execution leaves the object’s scope—that is, when the block in which that object is defined finishes executing normally or due to an exception. Destructors are not called for local objects if the program terminates with a call to function `exit` or `abort`.

### Constructors and Destructors for static Local Objects

The constructor for a static local object is called only once when execution first reaches the point where the object is defined. The corresponding destructor is called when `main` terminates or the program calls function `exit`. Global and static objects are destroyed in
