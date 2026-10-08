# 18.3 Sorting Algorithms 795

```
58 // display a array of the algorithm
59 public static void PrintPass(int[] values, int pass, int index)
60 {
61 Console.Write("after pass: {pass}\
```

Unsorted array:
86 97 83 45 19 31 86 13 57 61

after pass 1: 13 97 83 45 19 31* 86 86 57 61
--

after pass 2: 13 19 31 45 97* 31 86 86 57 61
--

after pass 3: 13 19 31 45 97 83* 86 86 57 61
--

> Fig. 18.4 | Class that creates an array filled with random integers. Provides a method to sort the array with selection sort. (Part 2 of 3.)