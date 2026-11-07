The definition of the function `print` is as follows:

```
```cpp
void studentType::print(ostream outF, double tuitionRate)
{
    int i;

    outF << "Student Name: " << getFirstName()
         << " " << getLastName() << endl;             //Step 1

    outF << "Student ID: " << sId << endl;            //Step 2

    outF << "Number of courses enrolled: "
         << numberOfCourses << endl;                   //Step 3
    outF << endl;

    outF << left;
    outF << "Course No" << setw(15) << " Course Name"
         << setw(8) << "Credits"
         << setw(6) << "Grade" << endl;               //Step 4

    outF << right;
    for (i = 0; i < numberOfCourses; i++)              //Step 5
    {
        coursesEnrolled[i].print(outF);                //Step 5a

        if (isTuitionPaid)                             //Step 5b
            outF << setw(4) << coursesGrade[i] << endl;
        else
            outF << setw(4) << "***" << endl;
    }
    outF << endl;

    outF << "Total number of credit hours: "
         << getHoursEnrolled() << endl;                //Step 6

    outF << fixed << showpoint << setprecision(2);      //Step 7

    if (isTuitionPaid)                                 //Step 8
        outF << "Mid-Semester GPA: " << getGpa()
             << endl;
    else
    {
        outF << "*** Grades are being held for not paying "
             << "the tuition. ***" << endl;
        outF << "Amount Due: $" << billingAmount(tuitionRate)
             << endl;
    }

    outF << "~-~-~-~-~-~-~-~-~-~-~-~-~-~-~-~-~-~-~-~-~"
         << "~-~-~-~-~-~-~" << endl << endl;
} //end print
```
```