```
```cpp
    << "The last occurrence of list3 in "
    << endl << "list1 is at position "
    << (location - list1) << endl;                                      //Line 29
else                                                                  //Line 30
    cout << "Line 31: list3 is not in list1."                         //Line 31
         << endl;

//find_first_of                                                        //Line 32
    cout << "Line 32: list4: ";                                      //Line 33
    copy(list4, list4 + 5, screenOut);
    cout << endl;                                                       //Line 34

    location = find_first_of(list1, list1 + 10,
                             list4, list4 + 5);                         //Line 35

    if (location != list1 + 10)                                        //Line 36
        cout << "Line 37: The first element "
             << "<location> of list4 is found in "
             << endl << "        list1 at position "
             << (location - list1) << endl;                            //Line 37
    else                                                               //Line 38
        cout << "Line 39: No element of list4 is "
             << "in list1." << endl;                                  //Line 39

    return 0;                                                          //Line 40
}                                                                      //Line 41
```
```

# Sample Run:

```
```text
Line 13: list1: 12 34 56 21 34 78 34 56 12 25
Line 16: list2: 34 56
Line 21: list2 is found in list1. The last occurrence of
          list2 in list1 is at position 6
Line 24: list3: 56 21 35
Line 31: list3 is not in list1.
Line 32: list4: 33 48 21 34 73
Line 37: The first element 34 of list4 is found in
          list1 at position 1
```
```

The statements in Lines 7 through 10 create and initialize the int arrays list1, list2, list3, and list4. The statements in Lines 11 and 12 declare an int pointer and an ostream iterator, respectively. The statements in Lines 14 and 17 output the values of list1 and list2. (In the output, see the lines marked Line 13 and Line 16.) The statement in Line 19 uses the function find_end to find the last occurrence of list2, as a subsequence, within list1. The last occurrence of list2 in list1 starts at position 6 (that is, at the seventh element). The statements in Lines 20 through 23 output the result of the search. (In the output, see Line 21.) The statement in Line 25 outputs list3. The statement in Line 27 uses the function find_end to find the last occurrence of list3, as a subsequence, within list1. Because list3 does not appear as a subsequence in list1, it is an unsuccessful search.