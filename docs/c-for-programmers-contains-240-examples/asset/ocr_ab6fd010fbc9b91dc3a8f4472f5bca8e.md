```
// Fig. 9.1: Time.h
// Declaration of class Time.
// Member functions are defined in Time.cpp

// prevent multiple inclusions of header file
#ifndef TIME_H
#define TIME_H

// Time class definition
class Time
{
public:
    Time(); // constructor
    void setTime( int, int, int ); // set hour, minute and second
    void printUniversal(); // print time in universal-time format
    void printStandard(); // print time in standard-time format
private:
    int hour; // 0 - 23 (24-hour clock format)
    int minute; // 0 - 59
    int second; // 0 - 59
}; // end class Time

#endif
```

Fig. 9.1 | Time class definition.

been defined. If the header has not been included previously in a file, the name TIME_H is defined by the #define directive and the header file statements are included. If the header has been included previously, TIME_H is defined already and the header file is not included again. Attempts to include a header file multiple times (inadvertently) typically occur in large programs with many header files that may themselves include other header files. [Note: The commonly used convention for the symbolic constant name in the preprocessor directives is simply the header file name in upper case with the underscore character replacing the period.]

# Error-Prevention Tip 9.1

Use #ifndef, #define and #endif preprocessor directives to form a preprocessor wrapper that prevents header files from being included more than once in a program.

# Good Programming Practice 9.2

Use the name of the header file in upper case with the period replaced by an underscore in the #ifndef and #define preprocessor directives of a header file.

# Time Class Member Functions

In Fig. 9.2, the Time constructor (lines 14–17) initializes the data members to 0 (i.e., the universal-time equivalent of 12 AM). This ensures that the object begins in a consistent state. Invalid values cannot be stored in the data members of a Time object, because the constructor is called when the Time object is created, and all subsequent attempts by a client to modify the data members are scrutinized by function setTime (discussed shortly). Finally, it is important to note that you can define several overloaded constructors for a class.