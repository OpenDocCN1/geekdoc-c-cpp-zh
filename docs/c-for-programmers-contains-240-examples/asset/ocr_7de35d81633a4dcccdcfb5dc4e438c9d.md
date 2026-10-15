```
12
13  // display default true booleanValue
14  cout << "booleanValue is " << booleanValue << endl;
15
16  // display booleanValue after using boolalpha
17  cout << "booleanValue (after using boolalpha) is "
18      << boolalpha << booleanValue << endl << endl;
19
20  cout << "switch booleanValue and use noboolalpha" << endl;
21  booleanValue = false; // change booleanValue
22  cout << noboolalpha << endl; // use noboolalpha
23
24  // display default false booleanValue after using noboolalpha
25  cout << "booleanValue is " << booleanValue << endl;
26
27  // display booleanValue after using boolalpha again
28  cout << "booleanValue (after using boolalpha) is "
29      << boolalpha << booleanValue << endl;
30  return 0;
31 } // end main
```

booleanValue is 1
booleanValue (after using boolalpha) is true

switch booleanValue and use noboolalpha

booleanValue is 0
booleanValue (after using boolalpha) is false

Fig. 15.20 | Stream manipulators boolalpha and noboolalpha. (Part 2 of 2.)

# 15.7.8 Setting and Resetting the Format State via Member Function flags

Throughout Section 15.7, we have been using stream manipulators to change output format characteristics. We now discuss how to return an output stream’s format to its default state after having applied several manipulations. Member function flags without an argument returns the current format settings as a fmtflags data type (of class ios_base), which represents the format state. Member function flags with a fmtflags argument sets the format state as specified by the argument and returns the prior state settings. The initial settings of the value that flags returns might differ across several systems. The program of Fig. 15.21 uses member function flags to save the stream’s original format state (line 22), then restore the original format settings (line 30).

```
1  // Fig. 15.21: Fig15_21.cpp
2  // Demonstrating the flags member function.
3  #include <iostream>
4  using std::cout;
5  using std::endl;
6  using std::ios_base;
```

Fig. 15.21 | flags member function. (Part 1 of 2.)