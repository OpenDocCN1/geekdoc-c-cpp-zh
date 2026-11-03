place true with 1, false with 0 and bool with the keyword _Bool. Figure E.5 uses a function named isEven (lines 29–37) that returns a bool value of true if the function's argument is even and false if it's odd.

```
```c
1  // Fig. E.5: figE_05.c
2  // Using the type bool and the values true and false in C99.
3  #include <stdio.h>
4  #include <stdbool.h> // allows the use of bool, true, and false
5
6  bool isEven(int number); // function prototype
7
8  int main(void)
9  {
10    // loop for 2 inputs
11    for (int i = 0; i < 2; ++i) {
12       printf("Enter an integer: ");
13       int input; // value entered by user
14       scanf("%d", &input);
15
16       bool valueIsEven = isEven(input); // determine if input is even
17
18       // determine whether input is even
19       if (valueIsEven) {
20          printf("%d is even\n\n", input);
21       }
22       else {
23          printf("%d is odd\n\n", input);
24       }
25    }
26 }
27
28 // isEven returns true if number is even
29 bool isEven(int number)
30 {
31    if (number % 2 == 0) { // is number divisible by 2?
32       return true;
33    }
34    else {
35       return false;
36    }
37 }
```
```

![](bbox=[0.11, 0.755, 0.92, 0.895])

Fig. E.5 | Using the type bool and the values true and false in C99.

Line 16 declares a bool variable named valueIsEven. Lines 13–14 in the loop prompt for and obtain the next integer. Line 16 passes the input to function isEven (lines 29–37).