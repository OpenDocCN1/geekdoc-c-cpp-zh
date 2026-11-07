number (to print * or #), the course ID, and the course average for the department.
To print the bar graph, we can use a loop to print one symbol for every two points.
To find the number of symbols to print, we can use integer division as follows:

```
numberOfSymbols = static_cast<int>(average) / 2;
```

For example, static_cast<int> / 2 = 78 /2 = 39. If the average is 78.45, we must print 39 symbols to represent this average.

Following this discussion, the definition of the function printResult is:

```
void printResult(ofstream& outp, string courseID,
                 int groupNo, double avg)
{
    int noOfSymbols;
    int count;

    if (groupNo == 1)
        outp << setw(4) << courseID << "    ";
    else
        outp << "        ";

    noOfSymbols = static_cast<int>(avg)/2;

    if (groupNo == 1)
        for (count = 1; count <= noOfSymbols; count++)
            outp << '*';
    else
        for (count = 1; count <= noOfSymbols; count++)
            outp << '#';

    outp << endl;
}//end printResult
```

We also include a function printHeading to print the first two lines of the output.
The definition of this function is:

```
void printHeading(ofstream& outp)
{
    outp << "Course        Course Average" << endl;
    outp << "  ID    0   10   20   30   40   50   60   70"
         << "    80   90  100" << endl;
    outp << "       |....|....|....|....|....|....|....|....|....|....|"
         << endl;
}//end printHeading
```

Replace the function printResult in the preceding program, include the function printHeading, include the statements to output—Group 1 --**** and Group 2 --####—, and rerun the program. Your program should generate a bar graph similar to the bar graph shown earlier. (The complete program listing is available on the website accompanying this book.)