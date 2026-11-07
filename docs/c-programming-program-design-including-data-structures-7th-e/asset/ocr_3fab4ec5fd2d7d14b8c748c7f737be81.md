```
```cpp
intList2 = intList1;                                      //line 15

cout << "Line 16: intList2: ";                           //line 16
copy(intList2.begin(), intList2.end(), screen);           //line 17
cout << endl;                                             //line 18

intList1.unique();                                        //line 19

cout << "Line 20: After removing the consecutive "
     << "duplicates," << endl
     << "        " << intList1: ";                    //line 20
copy(intList1.begin(), intList1.end(), screen);           //line 21
cout << endl;                                             //line 22

intList2.sort();                                          //line 23

cout << "Line 24: After sorting, intList2: ";            //line 24
copy(intList2.begin(), intList2.end(), screen);           //line 25
cout << endl;                                             //line 26

intList3.push_back(13);                                   //line 27
intList3.push_back(25);                                   //line 28
intList3.push_back(25);                                   //line 29
intList3.push_back(136);                                  //line 30
intList3.push_back(198);                                  //line 31

cout << "Line 32: intList3: ";                           //line 32
copy(intList3.begin(), intList3.end(), screen);           //line 33
cout << endl;                                             //line 34

intList4.push_back(-2);                                   //line 35
intList4.push_back(-7);                                   //line 36
intList4.push_back(-8);                                   //line 37

cout << "Line 38: intList4: ";                           //line 38
copy(intList4.begin(), intList4.end(), screen);           //line 39
cout << endl;                                             //line 40

intList3.splice(intList3.begin(), intList4);              //line 41

cout << "Line 42: After moving the elements of "
     << "intList4 into intList3," << endl
     << "        intList3: ";                             //line 42
copy(intList3.begin(), intList3.end(), screen);           //line 43
cout << endl;                                             //line 44

intList3.sort();                                          //line 45

cout << "Line 46: After sorting, intList3: ";             //line 46
copy(intList3.begin(), intList3.end(), screen);           //line 47
cout << endl;                                             //line 48
intList2.merge(intList3);                                 //line 49
```
```