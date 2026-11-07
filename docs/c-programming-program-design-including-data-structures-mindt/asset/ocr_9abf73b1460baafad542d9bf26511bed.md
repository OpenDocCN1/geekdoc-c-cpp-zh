```
~~~cpp
int number;                                      //Line 9

cout << "Line 10: Enter 5 integers: ";            //Line 10

for (int i = 0; i < 5; i++)                      //Line 11
{                                                 //Line 12
    cin >> number;                                //Line 13
    intList1.insertEnd(number);                   //Line 14
}                                                 //Line 15

cout << endl;                                     //Line 16
cout << "Line 17: intList1: ";                    //Line 17
intList1.print();                                 //Line 18

intList3 = intList2 = intList1;                   //Line 19

cout << "Line 20: intList2: ";                    //Line 20
intList2.print();                                 //Line 21

intList2.destroyList();                           //Line 22

cout << endl;                                     //Line 23
cout << "Line 24: intList2: ";                    //Line 24
intList2.print();                                 //Line 25

cout << "Line 26: After destroying intList2, "    //Line 26
     << "intList1: ";                             //Line 27
intList1.print();

cout << "Line 28: After destroying intList2, "    //Line 28
     << "intList3: ";                             //Line 29
intList3.print();                                 //Line 30
cout << endl;

return 0;                                         //Line 31
}                                                 //Line 32
~~~
```

**Sample Run:** In this sample run, the user input is shaded.

```
~~~
Line 10: Enter 5 integers: 9 12 3 7 10

Line 17: intList1: 9 12 3 7 10
Line 20: intList2: 9 12 3 7 10

Line 24: intList2: The list is empty.
Line 26: After destroying intList2, intList1: 9 12 3 7 10
Line 28: After destroying intList2, intList3: 9 12 3 7 10
~~~
```

The statement in Line 6 creates intList1 of size 10; the statements in Lines 7 and 8 create intList2 and intList3 of (default) size 50. The statements in Lines 11 through 15 input the data into intList1, and the statement in Line 18 outputs intList1.