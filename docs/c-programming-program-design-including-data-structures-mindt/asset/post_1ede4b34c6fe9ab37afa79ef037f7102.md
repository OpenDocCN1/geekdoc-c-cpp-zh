
```cpp
void print(ostream& outF);
//Function to print the course information.
//This function sends the course information to the
//output device specified by the parameter outF. If the
//actual parameter to this function is the object cout,
//then the output is shown on the standard output device.
//If the actual parameter is an ostream variable, say
//outfile, then the output goes to the file specified by
//outfile.

int getCredits();
//Function to return the credit hours.
//Postcondition: The value of courseCredits is returned.

string getCourseNumber();
//Function to return the course number.
//Postcondition: The value of courseNo is returned.

string getCourseName();
//Function to return the course name.
//Postcondition: The value of courseName is returned.

courseType(string cName = "", string cNo = "",
           int credits = 0);
//Constructor
//The object is initialized according to the parameters.
//Postcondition: courseName = cName; courseNo = cNo;
//              courseCredits = credits;
//

private:
    string courseName;   //variable to store the course name
    string courseNo;     //variable to store the course number
    int courseCredits;   //variable to store the credit hours
};
```

Figure 11-9 shows the UML class diagram of the class `courseType`.

![](img/b217c421655b51e7494cf3b89bb5432d_833_0.png)

**FIGURE 11-9** UML class diagram of the class `courseType`

The definitions of the functions to implement the operations of the `class courseType` are quite straightforward and easy to follow.

The function `setCourseInfo` sets the values of the `private` member variables according to the values of the parameters. Its definition is:

```cpp
void courseType::setCourseInfo(string cName, string cNo,
                               int credits)
{
    courseName = cName;
    courseNo = cNo;
    courseCredits = credits;
} //end setCourseInfo
```

The function `print` prints the course information. The parameter `outF` specifies the output device. Also, we print the course name and course number left-justified rather than right-justified (the default). Thus, we need to set the left manipulator. Before printing the credit hours, the manipulator is set to be right-justified. The following steps describe this function:

- 1. Set the left manipulator.
- 2. Print the course number.
- 3. Print the course name.
- 4. Set the right manipulator.
- 5. Print the credit hours.

The definition of the function `print` is:

```cpp
void courseType::print(ostream& outF)
{
    outF << left;                         //Step 1
    outF << setw(8) << courseNo << "  ";  //Step 2
    outF << setw(15) << courseName;       //Step 3
    outF << right;                        //Step 4
    outF << setw(3) << courseCredits << "  "; //Step 5
} //end print
```

![](img/b217c421655b51e7494cf3b89bb5432d_834_0.png)

The constructor is declared with the default values. If no values are specified when a `courseType` object is declared, the constructor uses the default values to initialize the object as follows: `courseNo` to blank, `courseName` to blank, and `courseCredits` to 0. Otherwise, the values specified in the object declaration are used to initialize the object. Its definition is:

```cpp
courseType::courseType(string cName, string cNo, int credits)
{
    courseName = cName;
    courseNo = cNo;
    courseCredits = credits;
} //end constructor
```

The definitions of the remaining functions are as follows:

```cpp
int courseType::getCredits()
{
    return courseCredits;
} //end getCredits

string courseType::getCourseNumber()
{
    return courseNo;
} //end getCourseNumber

string courseType::getCourseName()
{
    return courseName;
} //end getCourseName
```

Next, we discuss the student component.

> **NOTE** Notice that in the definition of the class `courseType`, the member functions, such as `print` and `getCredits`, are accessor functions. This class also has other accessor functions. As noted in Chapter 10, we typically define the accessor functions with the keyword `const` at the end of their headings. We leave it as an exercise for you to redefine this class so that the accessor functions are declared as constant functions. (See Programming Exercise 12 at the end of this chapter.)

## Student

The main characteristics of a student are the student name, student ID, number of courses in which enrolled, courses in which enrolled, and grade for each course. Because every student has to pay tuition, we also include a member to indicate whether the student has paid the tuition.

Every student is a person, and every student takes courses. We have already designed a class `personType` to process a person’s first and last name. We have also designed a class to process the information for a course. Thus, we see that we can derive the class `studentType` to keep track of a student’s information from the class `personType`, and one member of this class is of type `courseType`. We can add more members as needed.

The basic operations to be performed on an object of type `studentType` are as follows:

- 1. Set the student information.
- 2. Print the student information.
- 3. Calculate the number of credit hours taken.
- 4. Calculate the GPA.
- 5. Calculate the billing amount.
- 6. Because the grade report will print the courses in ascending order, sort the courses according to the course number.

The following class defines `studentType` as an ADT. We assume that a student takes no more than six courses per semester, so we store course information in an array of six course objects.

```cpp
class studentType: public personType
{
public:
    void setInfo(string fName, string lName, int ID,
                 int nOfCourses, bool isTPaid,
                 courseType courses[], char courseGrades[]);
    //Function to set the student's information
    //Postcondition: The member variables are set
    //              according to the parameters.

    void print(ostream& outF, double tuitionRate);
    //Function to print the student's grade report.
    //If the member variable isTuitionPaid is true, the grades
    //are shown, otherwise those stars are printed. If the
    //actual parameter corresponding to outF is the object
    //cout, then the output is shown on the standard output
    //device. If the actual parameter corresponding to outF
    //is an ofstream object, say outFile, then the output
    //goes to the file specified by outFile.

    studentType();
    //Default constructor
    //The member variables are initialized.

    int getHoursEnrolled();
    //Function to return the credit hours a student is
    //enrolled in.
    //Postcondition: The number of credit hours is
    //              calculated and returned.

    double getGpa();
    //Function to return the grade point average.
    //Postcondition: The GPA is calculated and returned.

    double billingAmount(double tuitionRate);
    //Function to return the tuition fees.
    //Postcondition: The billing amount is calculated
    //and returned.

private:
    void sortCourses();
    //Function to sort the courses.
    //Postcondition: The array coursesEnrolled is sorted.
    //              For each course, its grade is stored in
    //              the array coursesGrade. Therefore, when
    //              the array coursesEnrolled is sorted, the
    //              corresponding entries in the array
    //              coursesGrade are adjusted.

    int sId;                 //variable to store the student ID
    int numberOfCourses;     //variable to store the number
                             //of courses
    bool isTuitionPaid;      //variable to indicate whether the
                             //tuition is paid
    courseType coursesEnrolled[6]; //array to store the courses
    char coursesGrade[6];    //array to store the courses grades
};
```

Figure 11-10 shows the UML class diagram of the class `studentType` together with the inheritance and composition (aggregation) relation.

![](img/b217c421655b51e7494cf3b89bb5432d_837_0.png)

**FIGURE 11-10** UML class diagram of the class `studentType` together with inheritance and composition (aggregation) relation.

Before writing the definitions of the member functions of the class `studentType`, we make the following note.

> **NOTE** Notice that in the definition of the class `studentType`, the member functions, such as `print` and `getGpa`, are accessor functions. This class also has other accessor functions. As noted in Chapter 10, we typically define the accessor functions with the keyword `const` at the end of their headings. We leave it as an exercise for you to redefine this class so that the accessor functions are declared as constant functions. (See Programming Exercise 12 at the end of this chapter.)

Note that the member function `sortCourses` to sort the array `coursesEnrolled` is a private member of the class `studentType`. This is due to the fact that this function is needed for internal data manipulation, and the user of the class does not need to access this member.
