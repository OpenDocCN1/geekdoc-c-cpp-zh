```
16
17    noon.getMinute();    // const        const
18    noon.printUniversal(); // const        const
19
20    noon.printStandard(); // const        non-const
21    return 0;
22 } // end main
```

Borland C++ command-line compiler error messages:

```
Warning W8037 fig10_03.cpp 13: Non-const function Time::setHour(int)
    called for const object in function main()
Warning W8037 fig10_03.cpp 20: Non-const function Time::printStandard()
    called for const object in function main()
```

Microsoft Visual C++ 2005 compiler error messages:

```
C:\cppfp_examples\ch10\Fig10_01_03\fig10_03.cpp(13) : error C2662:
    'Time::setHour' : cannot convert 'this' pointer from 'const Time' to
    'Time &'
    Conversion loses qualifiers
C:\cppfp_examples\ch10\Fig10_01_03\fig10_03.cpp(20) : error C2662:
    'Time::printStandard' : cannot convert 'this' pointer from 'const Time' to
    'Time &'
    Conversion loses qualifiers
```

GNU C++ compiler error messages:

```
fig10_03.cpp:13: error: passing `const Time' as `this' argument of
    `void Time::setHour(int)' discards qualifiers
fig10_03.cpp:20: error: passing `const Time' as `this' argument of
    `void Time::printStandard()' discards qualifiers
```

Fig. 10.3 | const objects and const member functions. (Part 2 of 2.)

Notice that even though a constructor must be a non-const member function (Fig. 10.2, lines 15–18), it can still be used to initialize a const object (Fig. 10.3, line 8). The definition of the Time constructor (Fig. 10.2, lines 15–18) shows that it calls another non-const member function—setTime (lines 21–26)—to perform the initialization of a Time object. Invoking a non-const member function from the constructor call as part of the initialization of a const object is allowed. The “constness” of a const object is enforced from the time the constructor completes initialization of the object until that object’s destructor is called.

Also notice that line 20 in Fig. 10.3 generates a compilation error even though member function printStandard of class Time does not modify the object on which it is invoked. The fact that a member function does not modify an object is not sufficient to indicate that the function is constant function—the function must explicitly be declared const.

# Initializing a const Data Member with a Member Initializer

The program of Figs. 10.4–10.6 introduces using member initializer syntax. All data members can be initialized using member initializer syntax, but const data members and