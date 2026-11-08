
The preceding discussion translates into the following algorithm:

- 1. Initialize the variables.
- 2. Get the course IDs for group 1 and group 2.
- 3. If the course IDs are different, print an error message and exit the program.
- 4. Calculate the course averages for group 1 and group 2.
- 5. Print the results in the form given above.
- 6. Repeat Steps 2 through 5 for each course.
- 7. Print the final results.

## Variables (Function `main`)

The preceding discussion suggests that the program needs the following variables for data manipulation in the function main:

```cpp
string courseId1;     //course ID for group 1
string courseId2;     //course ID for group 2
int numberOfCourses;
double avg1;          //average for a course in group 1
double avg2;          //average for a course in group 2
double avgGroup1;     //average group 1
double avgGroup2;     //average group 2
ifstream group1;      //input stream variable for group 1
ifstream group2;      //input stream variable for group 2

ofstream outfile;     //output stream variable
```

Next, we discuss the functions calculateAverage and printResult. Then, we will put the function main together.

## calculateAverage

This function calculates the average for a course. Because the input is stored in a file and the input file is opened in the function main, we must pass the ifstream variable associated with the input file to this function. Furthermore, after calculating the course average, this function must pass the course average to the function main. Therefore, this function has two parameters, and both parameters must be reference parameters.

To compute the course average, we must first find the sum of all scores for the course and the number of students who took the course and then divide the sum by the number of students. Thus, we need a variable to find the sum of the scores, a variable to count the number of students, and a variable to read and store a score. Of course, we must initialize the variable to find the sum and the variable to count the number of students to zero.

### Local Variables (Function `calculateAverage`)

In the previous discussion of data manipulation, we identified three variables for the function calculateAverage:

```cpp
double totalScore = 0.0;
int numberOfStudents = 0;
int score;
```

The above discussion translates into the following algorithm for the function calculateAverage:

- 1. Declare and initialize variables.
- 2. Get the (next) course score, score.
- 3. while the score is not -999
  - a. Update totalScore by adding the course score.
  - b. Increment numberOfStudents by 1.
  - c. Get the (next) course score, score.
- 4. courseAvg = totalScore / numberOfStudents;

We are now ready to write the definition of the function calculateAverage.

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

    courseAvg = totalScore / numberOfStudents;
} //end calculateAverage
```

The function printResult prints the group’s course ID, group number, and course average. The output is stored in a file. So we must pass four parameters to this function: the ofstream variable associated with the output file, the group number, the course ID, and the course average for the group. The ofstream variable must be passed by reference. Because the function uses only the values of the other variables, the remaining three parameters should be value parameters. Also, from the output, it is clear that we print the course ID only before the group number.

- 1. In pseudocode, the algorithm is:

```cpp
if (group number == 1)
    print course ID
else
    print a blank

print group number and course average
```

The definition of the function `printResult` follows:

```cpp
void printResult(ofstream& outp, string courseID, int groupNo,
                 double avg)
{
    if (groupNo == 1)
        outp << " " << courseID << " ";
    else
        outp << "        ";

    outp << setw(8) << groupNo << setw(17) << avg << endl;
} //end printResult
```

Now that we have designed and defined the functions calculateAverage and printResult, we can describe the algorithm for the function main. Before outlining the algorithm, however, we note the following: It is quite possible that in both input files, the data is ordered according to the course IDs, but one file might have fewer courses than the other. We do not discover this error until after we have processed both files and discovered that one file has unprocessed data. Make sure to check for this error before printing the final answer—that is, the averages for group 1 and group 2.

## MAIN ALGORITHM: Function main

- 1. Declare the variables (local declaration).
- 2. Open the input files.
- 3. Print a message if you are unable to open a file and terminate the program.
- 4. Open the output file.
- 5. To output floating-point numbers in a fixed decimal format with the decimal point and trailing zeros, set the manipulators fixed and showpoint. Also, to output floating-point numbers to two decimal places, set the precision to two decimal places.
- 6. Initialize the course average for group 1 to 0.0.
- 7. Initialize the course average for group 2 to 0.0.
- 8. Initialize the number of courses to 0.
- 9. Print the heading.
- 10. Get the course ID, courseId1, for group 1.
- 11. Get the course ID, courseId2, for group 2.
- 12. For each course in group 1 and group 2,
  - a. if (courseId1 != courseId2)
    {
        cout << "Data error: Course IDs do not match.\n";
        return 1;
    }

```cpp
//Function prototypes
void calculateAverage(ifstream& inp, double& courseAvg);
void printResult(ofstream& output, string courseId,
                 int groupNo, double avg);

int main()
{
    //Step 1
    string courseId1;       //course ID for group 1
    string courseId2;       //course ID for group 2
    int numberOfCourses;    //number of courses
    double avg1;            //average for a course in group 1
    double avg2;            //average for a course in group 2
    double avgGroup1;       //average group 1
    double avgGroup2;       //average group 2
    ifstream group1;        //input stream variable for group 1
    ifstream group2;        //input stream variable for group 2
    ofstream outfile;       //output stream variable

    group1.open("group1.txt");                       //Step 2
    group2.open("group2.txt");                       //Step 2

    if (!group1 || !group2)                          //Step 3
    {
        cout << "Unable to open files." << endl;
        cout << "Program terminates." << endl;
        return 1;
    }

    outfile.open("student.out");                     //Step 4
    outfile << fixed << showpoint;                   //Step 5
    outfile << setprecision(2);                      //Step 5

    avgGroup1 = 0.0;                                 //Step 6
    avgGroup2 = 0.0;                                 //Step 7

    numberOfCourses = 0;                             //Step 8

    outfile << "Course No        Group No     "
            << "Course Average" << endl;             //Step 9

    group1 >> courseId1;                             //Step 10
    group2 >> courseId2;                             //Step 11
    while (group1 && group2)                         //Step 12
    {
        if (courseId1 != courseId2)                  //Step 12a
        {
            cout << "Data error: Course IDs "
                 << "do not match." << endl;
```
