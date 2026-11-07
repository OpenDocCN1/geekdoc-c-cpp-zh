```
        cout << "Line 50: After merging intList2 and "
             << "intList3, intList2: " << endl
             << "";
        copy(intList2.begin(), intList2.end(), screen);    // Line 50
        cout << endl;                                       // Line 51
        // Line 52

        intList2.unique();                                  // Line 53

        cout << "Line 54: After removing the consecutive "
             << "duplicates, intList2: " << endl
             << "";
        copy(intList2.begin(), intList2.end(), screen);    // Line 54
        cout << endl;                                       // Line 55
        // Line 56

        return 0;
    }
```

# **Sample Run:**

```
    Line 12: intList1: 23 58 58 58 36 15 93 98 58
    Line 16: intList2: 23 58 58 58 36 15 93 98 58
    Line 20: After removing the consecutive duplicates,
             intList1: 23 58 36 15 93 98 58
    Line 24: After sorting, intList2: 15 23 36 58 58 58 58 93 98
    Line 32: intList3: 13 23 25 136 198
    Line 38: intList4: -2 -7 -8
    Line 42: After moving the elements of intList4 into intList3,
             intList3: -2 -7 -8 13 23 25 136 198
    Line 46: After sorting, intList3: -8 -7 -2 13 23 25 136 198
    Line 50: After merging intList2 and intList3, intList2:
             -8 -7 -2 13 15 23 25 36 58 58 58 58 93 98 136 198
    Line 54: After removing the consecutive duplicates, intList2:
             -8 -7 -2 13 15 23 25 36 58 93 98 136 198
```

For the most part, the output of the preceding program is straightforward. The statements in Lines 3 through 11 insert the element numbers 23, 58, 58, 58, 36, 15, 93, 98, and 58 (in that order) into intList1. The statement in Line 15 copies the elements of intList1 into intList2. After this statement executes, intList1 and intList2 are identical. The statement in Line 19 removes any consecutive occurrences of the same elements. For example, the number 58 appears consecutively three times. The operation unique removes two occurrences of 58. Note that this operation has no effect on the 58 that appears at the end of intList1.

The statement in Line 23 sorts intList2. The statements in Lines 27 through 31 insert 13, 23, 25, 136, and 198 into intList3. Similarly, the statements in Lines 35 through 37 insert -2, -7, and -8 into intList4. The statement in Line 41 uses the operation splice to move the elements of intList4 to the beginning of intList3. After the splice operation, intList4 is empty. The statement in Line 45 sorts intList3, and the statement in Line 49 merges intList2 and intList3 into intList2. After the merge operation, intList3 is empty. The meanings of the remaining statements are similar.