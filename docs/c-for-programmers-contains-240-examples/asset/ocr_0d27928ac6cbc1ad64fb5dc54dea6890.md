```
17 // display all data members of Derived
18 ostream &operator<<( ostream &output, const Derived &derived )
19 {
20     output << "    Integer: " << derived.value << "\n Character: "
21         << derived.letter << "\nReal number: " << derived.real;
22     return output; // enables cascaded calls
23 } // end operator<<
```

Fig. 22.10 | Demonstrating multiple inheritance—Derived.cpp. (Part 2 of 2.)

Now let us examine the main function (Fig. 22.11) that tests the classes in Figs. 22.7–22.10. Line 13 creates Base1 object base1 and initializes it to the int value 10, then creates the pointer base1Ptr and initializes it to the null pointer (i.e., 0). Line 14 creates Base2 object base2 and initializes it to the char value 'Z', then creates the pointer base2Ptr and initializes it to the null pointer. Line 15 creates Derived object derived and initializes it to contain the int value 7, the char value 'A' and the double value 3.5.

```
1 // Fig. 22.11: fig22_11.cpp
2 // Driver for multiple-inheritance example.
3 #include <iostream>
4 using std::cout;
5 using std::endl;
6 
7 #include "Base1.h"
8 #include "Base2.h"
9 #include "Derived.h"
10 
11 int main()
12 {
13     Base1 base1( 10 ), *base1Ptr = 0; // create Base1 object
14     Base2 base2( 'Z' ), *base2Ptr = 0; // create Base2 object
15     Derived derived( 7, 'A', 3.5 ); // create Derived object
16 
17     // print data members of base-class objects
18     cout << "Object base1 contains integer " << base1.getData()
19         << "\nObject base2 contains character " << base2.getData()
20         << "\nObject derived contains:\n" << derived << "\n\n";
21 
22     // print data members of derived-class object
23     // scope resolution operator resolves getData ambiguity
24     cout << "Data members of Derived can be accessed individually:"
25         << "\n    Integer: " << derived.Base1::getData()
26         << "\n Character: " << derived.Base2::getData()
27         << "\nReal number: " << derived.getReal() << "\n\n";
28     cout << "Derived can be treated as an object of either base class:\n";
29 
30     // treat Derived as a Base1 object
31     base1Ptr = &derived;
32     cout << "base1Ptr->getData() yields " << base1Ptr->getData() << '\n';
33
```

Fig. 22.11 | Demonstrating multiple inheritance. (Part 1 of 2.)