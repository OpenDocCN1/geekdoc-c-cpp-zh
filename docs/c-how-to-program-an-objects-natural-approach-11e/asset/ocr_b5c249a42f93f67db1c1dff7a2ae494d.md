the Time.cpp file (lines 9, 23 and 28). When compiling Time.cpp, the compiler uses the information in Time.h to ensure that

+   - the first line of each member function matches its prototype in Time.h and
+   - each member function knows about the class's data members and other member functions.

# ### 9.7.6 Scope Resolution Operator (::)

Each member function's name (lines 9, 23 and 28) is preceded by the class name and the scope resolution operator (::). This "ties" them to the (now separate) Time class definition (Fig. 9.7), which declares the class's members. The Time:: tells the compiler that each member function is in that class's scope, and its name is known to other class members.

Without "Time::" preceding each function name, the compiler would treat these as global functions with no relationship to class Time. Such functions, also called "free" functions, cannot access Time's private data or call the class's member functions without receiving a Time object or a pointer or reference to one. So, the compiler would not be able to compile these functions because it would not know that class Time declares variables m_hour, m_minute and m_second. In Fig. 9.8, lines 17–19, 24 and 30–31 would cause compilation errors because m_hour, m_minute and m_second are not declared as local variables in each function, nor are they declared as global variables.

# ### 9.7.7 Member Function setTime and Throwing Exceptions

Function setTime (lines 9–20) is a public function that declares three int parameters and uses them to set the time. Lines 11–12 test each argument to determine whether the value is in range. If so, lines 17–19 assign the values to the m_hour, m_minute and m_second data members, respectively. The hour argument must be greater than or equal to 0 and less than 24 because the 24-hour time format represents hours as integers from 0 to 23. Similarly, the minute and second arguments must be greater than or equal to 0 and less than 60.

If any of the values is outside its range, setTime throws an exception (lines 13–14) of type invalid_argument (header <stdexcept>), notifying the client code that an invalid argument was received. As you saw in Section 6.15, you can use try...catch to catch exceptions and attempt to recover from them, which we'll do in Fig. 9.9. The throw statement creates a new invalid_argument object, initializing it with a custom error message string. After the exception object is created, the throw statement terminates function setTime. Then, the exception is returned to the code that called setTime.

Invalid values cannot be stored in a Time object because

+   - when a Time object is created, its default constructor is called, and each data member is initialized to 0, as specified in lines 14–16 of Fig. 9.7—this is the equivalent of 12 AM (midnight)—and
+   - all subsequent attempts by a client to modify the data members are scrutinized by function setTime.

# ### 9.7.8 Member Functions to24HourString and to12HourString

Member function to24HourString (lines 23–25 of Fig. 9.8) takes no arguments and returns a formatted 24-hour string with three colon-separated digit pairs. So, if the time