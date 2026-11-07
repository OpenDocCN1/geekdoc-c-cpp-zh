```
```cpp
if (location != list1 + 10)                         //Line 22
    cout << "Line 23: list3 is found in list 1. "
         << "The last occurrence of list3 in "
         << endl << "list 1 is at position "
         << (location - list1) << endl;              //Line 23
else                                                   //Line 24
    cout << "Line 25: list3 is not in list1."
         << endl;                                     //Line 25

//find first of
cout << "Line 26: list4: ";                           //Line 26
copy(list4, list4 + 5, screenOut);                    //Line 27
cout << endl;                                         //Line 28

location = find_first_of(list1, list1 + 10,
                         list4, list4 + 5);           //Line 29

if (location != list1 + 10)                            //Line 30
    cout << "Line 31: The first element "
         << " of list4 is found in "
         << endl << " list 1 at position "
         << (location - list1) << endl;               //Line 31
else                                                   //Line 32
    cout << "Line 33: No element of list4 is "
         << "in list1." << endl;                      //Line 33

return 0;
}
```
```

# Sample Run:

```
Line 7: list1: 12 34 56 21 34 78 34 56 12 25
Line 10: list2: 34 56
Line 15: list2 is found in list 1. The last occurrence of
         list2 in list 1 is at position 6
Line 18: list3: 56 21 35
Line 25: list3 is not in list1.
Line 26: list4: 33 48 21 34 73
Line 31: The first element 34 of list4 is found in
         list 1 at position 1
```

The statements in Lines 1 through 4 create and initialize the `int` arrays list1, list2, list3, and list4. The statements in Lines 5 and 6 declare an `int` pointer and an ostream iterator, respectively. The statements in Lines 8 and 11 output the values of list1 and list2. (In the output, see the lines marked Line 7 and Line 10.) The statement in Line 13 uses the function `find_end` to find the last occurrence of list2, as a subsequence, within list1. The last occurrence of list2 in list1 starts at position 6 (that is, at the seventh element). The statements in Lines 14 through 17 output the result of the search. (In the output, see Line 15.) The statement in Line 19 outputs list3. The statement in Line 21 uses the function `find_end` to find the last occurrence of list3, as a subsequence, within list1. Because list3 does not appear as a subsequence in list1, it is an unsuccessful search.