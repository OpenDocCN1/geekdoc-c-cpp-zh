23. Suppose `averageTestScore` denotes the average test score, `highestScore` denotes the highest test score, `testScore` denotes a test score, `sum` denotes the sum of all of the test scores, `count` denotes the number of students in class, and `studentName` denotes the name of a student.

**a.** First, you design an algorithm to find the average test score. To find the average test score, first you need to count the number of students in the class and add the test score of each student. You then divide the sum by count to find the average test score. The algorithm to find the average test score is as follows:

+   i. Set `sum` and `count` to 0.
+   
+   ii. Repeat the following for each student in class:
+   
+   1. Get `testScore`
+   2. Increment `count` and update the value of `sum` by adding the current test score to `sum`.

iii. Use the following formula to find the average test score:

```
if (count is 0)
    averageTestScore = 0;
otherwise
    averageTestScore = sum / count;
```

**b.** The following algorithm determines and prints the names of all of the students whose test score is below the average test score.

+   Repeat the following for each student in class:
+   
+   i. Get `studentName` and `testScore`
+   
+   ii. if (`testScore` is less than `averageTestScore`)
+       print `studentName`

**c.** The following algorithm determines the highest test score.

+   i. Get first student's test score and call it `highestTestScore`.
+   
+   ii. Repeat the following for each of the remaining students in class:
+   
+   1. Get `testScore`
+   2. if (`testScore` is greater than `highestTestScore`)
+       `highestTestScore = testScore;`

**d.** To print the names of all of the students whose test score is the same as the highest test score, compare the test score of each student with the highest test score, and if they are equal, print the name. The following algorithm accomplishes this. Repeat the following for each student in class:

+   i. Get `studentName` and `testScore`
+   
+   ii. if (`testScore` is equal to `highestTestScore`)
+       print `studentName`