```
20  // print integers2 size and contents
21  cout << "\nSize of Array integers2 is "
22      << integers2.getSize()
23      << "\nArray after initialization:\n" << integers2;
24
25  // input and print integers1 and integers2
26  cout << "\nEnter 17 integers:" << endl;
27  cin >> integers1 >> integers2;
28
29  cout << "\nAfter input, the Arrays contain:\n"
30      << "integers1:\n" << integers1
31      << "integers2:\n" << integers2;
32
33  // use overloaded inequality (!=) operator
34  cout << "\nEvaluating: integers1 != integers2" << endl;
35
36  if ( integers1 != integers2 )
37      cout << "integers1 and integers2 are not equal" << endl;
38
39  // create Array integers3 using integers1 as an
40  // initializer; print size and contents
41  Array integers3( integers1 ); // invokes copy constructor
42
43  cout << "\nSize of Array integers3 is "
44      << integers3.getSize()
45      << "\nArray after initialization:\n" << integers3;
46
47  // use overloaded assignment (=) operator
48  cout << "\nAssigning integers2 to integers1:" << endl;
49  integers1 = integers2; // note target Array is smaller
50
51  cout << "integers1:\n" << integers1
52      << "integers2:\n" << integers2;
53
54  // use overloaded equality (==) operator
55  cout << "\nEvaluating: integers1 == integers2" << endl;
56
57  if ( integers1 == integers2 )
58      cout << "integers1 and integers2 are equal" << endl;
59
60  // use overloaded subscript operator to create rvalue
61  cout << "\nintegers1[5] is " << integers1[ 5 ];
62
63  // use overloaded subscript operator to create lvalue
64  cout << "\n\nAssigning 1000 to integers1[5]" << endl;
65  integers1[ 5 ] = 1000;
66  cout << "integers1:\n" << integers1;
67
68  // attempt to use out-of-range subscript
69  cout << "\nAttempt to assign 1000 to integers1[15]" << endl;
70  integers1[ 15 ] = 1000; // ERROR: out of range
71  return 0;
72 } // end main
```

Fig. 11.8 | Array class test program. (Part 2 of 3.)