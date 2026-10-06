# CHAPTER 9 Using Classes and Objects

```
Sorted employees:
Employee #0: 111 $0.00
Employee #1: 222 $0.00
Employee #2: 333 $0.00
Employee #3: 444 $0.00
Employee #4: 555 $0.00
Employee #222 was found at position 1
```

Figure 9-42 Output of the ComparableEmployeeArray program

Notice that the seekEmp object matches the Employee in the second array position based on the idNumber—not the salary—because the CompareTo() method in the Employee class uses only idNumber to make comparisons. You could have code that requires both the idNumber and salary values to match before returning a positive number.

![](bbox=[0.139, 0.445, 0.872, 0.773])

Copyright 2018 Cengage Learning. All Rights Reserved. May not be copied, scanned, or duplicated, in whole or in part. WCN 02-200-202