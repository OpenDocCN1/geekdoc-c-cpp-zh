```
Size of vector integers2 is 10
vector after initialization:
                 0                 0                 0
                 0                 0                 0
                 0                 0

Enter 17 integers:
1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17

After input, the vectors contain:
integers1:
                 1                 2                 3                 4
                 5                 6                 7
integers2:
                 8                 9                10                11
                12                13                14                15
                16                17

Evaluating: integers1 != integers2
integers1 and integers2 are not equal

Size of vector integers3 is 7
vector after initialization:
                 1                 2                 3                 4
                 5                 6                 7

Assigning integers2 to integers1:
integers1:
                 8                 9                10                11
                12                13                14                15
                16                17
integers2:
                 8                 9                10                11
                12                13                14                15
                16                17

Evaluating: integers1 == integers2
integers1 and integers2 are equal

integers1[5] is 13

Assigning 1000 to integers1[5]
integers1:
                 8                 9                10                11
                12              1000                14                15
                16                17

Attempt to assign 1000 to integers1.at( 15 )

abnormal program termination
```

Line 23 uses vector member function **size** to obtain the size (i.e., the number of elements) of integers1. Line 25 passes integers1 to function outputVector (lines 88–102),