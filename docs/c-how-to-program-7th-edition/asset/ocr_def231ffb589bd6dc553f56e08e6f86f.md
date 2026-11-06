```
```cpp
17    // print integers2 size and contents
18    cout << "\nSize of Array integers2 is "
19         << integers2.getSize()
20         << "\nArray after initialization:\n" << integers2;

22    // input and print integers1 and integers2
23    cout << "\nEnter 17 integers: " << endl;
24    cin >> integers1 >> integers2;

26    cout << "\nAfter input, the Arrays contain:\n"
27         << "integers1:\n" << integers1
28         << "integers2:\n" << integers2;

30    // use overloaded inequality (!=) operator
31    cout << "\nEvaluating: integers1 != integers2" << endl;

33    if ( integers1 != integers2 )
34       cout << "integers1 and integers2 are not equal" << endl;

36    // create Array integers3 using integers1 as an
37    // initializer; print size and contents
38    Array integers3( integers1 ); // invokes copy constructor

40    cout << "\nSize of Array integers3 is "
41         << integers3.getSize()
42         << "\nArray after initialization:\n" << integers3;

44    // use overloaded assignment (=) operator
45    cout << "\nAssigning integers2 to integers1:" << endl;
46    integers1 = integers2; // note target Array is smaller

48    cout << "\nSize of integers1: " << integers1
49         << "\nintegers2:\n" << integers2;

51    // use overloaded equality (==) operator
52    cout << "\nEvaluating: integers1 == integers2" << endl;

54    if ( integers1 == integers2 )
55       cout << "integers1 and integers2 are equal" << endl;

57    // use overloaded subscript operator to create rvalue
58    cout << "\nintegers1[5] is " << integers1[ 5 ];

60    // use overloaded subscript operator to create lvalue
61    cout << "\nAssigning 1000 to integers1[5]" << endl;
62    integers1[ 5 ] = 1000;
63    cout << "\nintegers1:\n" << integers1;

65    // attempt to use out-of-range subscript
66    cout << "\nAttempting to assign 1000 to integers1[15]" << endl;
67    integers1[ 15 ] = 1000; // ERROR: out of range
68 } // end main
```
```

Fig. 11.8 | Array class test program. (Part 2 of 3.)