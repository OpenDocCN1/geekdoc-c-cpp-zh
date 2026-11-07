Next, we discuss the definitions of the functions to implement the operations of the `class studentType`.

The function `setInfo` first initializes the `private` member variables to the incoming parameter values. This function then calls the function `sortCourses` to sort the array `coursesEnrolled` by course number. The `class studentType` is derived from the `class personType`, and the variables to store the first and last name are `private` member variables of that class. Therefore, we call the member function `setName` of the `class personType` to pass the appropriate variables to set the first and last names.

The definition of the function `setInfo` is as follows:

```
void studentType::setInfo(string fName, string lName, int ID,
                           int nOfCourses, bool isTPaid,
                           courseType courses[], char cGrades[])
{
    setName(fName, lName);                 //set the name

    sId = ID;                               //set the student ID
    isTuitionPaid = isTPaid;               //set istTuitionPaid
    numberOfCourses = nOfCourses;          //set the number of courses

          //set the course information
    for (int i = 0; i < numberOfCourses; i++)
    {
        coursesEnrolled[i] = courses[i];
        coursesGrade[i] = cGrades[i];
    }

    sortCourses();   //sort the array coursesEnrolled
} //end setInfo
```

The default constructor initializes the `private` member variables to the default values. Note that because the `private` member variable `coursesEnrolled` is an array of type `courseType`, the default constructor of the `class courseType` executes automatically, and the entire array is initialized.

```
studentType::studentType()
{
    numberOfCourses = 0;
    sId = 0;
    isTuitionPaid = false;

    for (int i = 0; i < 6; i++)
        coursesGrade[i] = '*';
} //end default constructor
```

The function `print` prints the grade report. The parameter `outF` specifies the output device. If the student has paid his or her tuition, the grades and the GPA are shown. Otherwise, three stars are printed in place of each grade, the GPA is not