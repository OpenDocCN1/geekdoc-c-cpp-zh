```
```c
// Determine the average grade for a particular student
double average(const int setOfGrades[], size_t tests)
{
    int total = 0; // sum of test grades

    // total all grades for one student
    for (size_t i = 0; i < tests; ++i) {
        total += setOfGrades[i];
    }

    return (double) total / tests; // average
}

// Print the array
void printArray(const int grades[][EXAMS], size_t pupils, size_t tests)
{
    // output column heads
    printf("%s",             "[0]  [1]  [2]  [3]");

    // output grades in tabular format
    for (size_t i = 0; i < pupils; ++i) {

        // output label for row
        printf("\nstudentGrades[%u] ", i);

        // output grades for one student
        for (size_t j = 0; j < tests; ++j) {
            printf("%4d", grades[i][j]);
        }
    }
}
```
```

```
```
The array is:

                  [0]   [1]   [2]   [3]
studentGrades[0]  77    68    86    73
studentGrades[1]  96    87    89    78
studentGrades[2]  70    90    86    81

Lowest grade: 68
Highest grade: 96
The average grade for student 0 is 76.00
The average grade for student 1 is 87.50
The average grade for student 2 is 81.75
```
```

**Fig. 6.22** | Two-dimensional array manipulations. (Part 3 of 3.)

Functions minimum, maximum and printArray each receive three arguments—the studentGrades array (called grades in function), the number of students (rows of the array) and the number of exams (columns of the array). Each function loops through array grades using nested for statements. The following nested for statement is from the function minimum definition: