Next, we discuss the functions `calculateAverage` and `printResult`. Then, we will put the function `main` together.

# calculate Average

This function calculates the average for a course. Because the input is stored in a file and the input file is opened in the function `main`, we must pass the `ifstream` variable associated with the input file to this function. Furthermore, after calculating the course average, this function must pass the course average to the function `main`. Therefore, this function has two parameters, and both parameters must be reference parameters.

To find the course average, we must first find the sum of all scores for the course and the number of students who took the course and then divide the sum by the number of students. Thus, we need a variable to find the sum of the scores, a variable to count the number of students, and a variable to read and store a score. Of course, we must initialize the variable to find the sum and the variable to count the number of students to zero.

In the previous discussion of data manipulation, we identified three variables for the function `calculateAverage`:

```
```cpp
double totalScore = 0.0;
int numberOfStudents = 0;
int score;
```
```

# Local Variables: (Function calculate Average)

The above discussion translates into the following algorithm for the function `calculateAverage`:

+   1. Declare and initialize variables.
+   2. Get the (next) course score, `score`.
+   3. `while` the score is not -999
+      a. Update `totalScore` by adding the course score.
+      b. Increment `numberOfStudents` by 1.
+      c. Get the (next) course score, `score`.
+   4. `courseAvg = totalScore / numberOfStudents;`

We are now ready to write the definition of the function `calculateAverage`.

```
```cpp
void calculateAverage(ifstream& inp, double& courseAvg)
{
    double totalScore = 0.0;
    int numberOfStudents = 0;
    int score;

    inp >> score;
    while (score != -999)
    {
        totalScore = totalScore + score;
        numberOfStudents++;
        inp >> score;
    } //end while
```
```