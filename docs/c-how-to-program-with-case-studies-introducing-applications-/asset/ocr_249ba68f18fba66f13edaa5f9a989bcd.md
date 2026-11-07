```
1  Set total to zero
2  Set grade counter to one
3
4  While grade counter is less than or equal to ten
5      Input the next grade
6      Add the grade into the total
7      Add one to the grade counter
8
9  Set the class average to the total divided by ten
10 Print the class average
```

**Fig. 3.1** | Pseudocode algorithm that uses counter-controlled iteration to solve the class-average problem.

```
1  // fig03_02.c
2  // Class average program with counter-controlled iteration.
3  #include <stdio.h>
4
5  // function main begins program execution
6  int main(void) {
7      // initialization phase
8      int total = 0; // initialize total of grades to 0
9      int counter = 1; // number of the grade to be entered next
10
11     // processing phase
12     while (counter <= 10) { // loop 10 times
13         printf("%s", "Enter grade: "); // prompt for input
14         int grade = 0; // grade counter
15         scanf("%d", &grade); // read grade from user
16         total = total + grade; // add grade to total
17         counter = counter + 1; // increment counter
18     } // end while
19
20     // termination phase
21     int average = total / 10; // integer division
22     printf("Class average is %d\\n", average); // display result
23 } // end function main
```

```
Enter grade: 98
Enter grade: 76
Enter grade: 71
Enter grade: 87
Enter grade: 83
Enter grade: 90
Enter grade: 57
Enter grade: 79
Enter grade: 82
Enter grade: 94
Class average is 81
```

**Fig. 3.2** | Class-average problem with counter-controlled iteration.