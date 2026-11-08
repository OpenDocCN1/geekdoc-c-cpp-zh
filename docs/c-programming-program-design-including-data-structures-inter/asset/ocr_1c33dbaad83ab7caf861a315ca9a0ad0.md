![](bbox=[0.188, 0.105, 0.263, 0.157])

Let us take a look at the formal parameter of the function print. The formal parameter `outF` is an object of the class `ostream`. We can use this function to send the output to the standard output device, the screen, or to a file. As indicated in the definition of the class, if the actual parameter is, say, `cout`, then the output is displayed on the screen. If the actual parameter is, say, `outfile`, an object of the class `ofstream`, then the output is sent to the device indicated by `outfile`. As mentioned in the section, “C++ Stream Classes,” the class `ofstream` is derived from the class `ostream`. Therefore, the class `ostream` is the base class. In C++, if a formal reference parameter is of the type `ostream`, it can refer to an object of the class `ofstream`.

In general, C++ allows a formal reference parameter of the base class type to refer to an object of the derived class. Of course, for user-defined classes, some other things need to be taken into account for this mechanism to work properly, which we will discuss in Chapter 12 (in the section “Inheritance, Pointers, and Virtual Functions”).

The function `getHoursEnrolled` calculates and returns the total credit hours that a student is taking. These credit hours are needed to calculate both the GPA and the billing amount. The total credit hours are calculated by adding the credit hours of each course in which the student is enrolled. Because the credit hours for a course are in the private member variable of an object of type `CourseType`, we use the member function `getCredits` of the class `CourseType` to retrieve the credit hours. The definition of this function is:

```
```cpp
int StudentType::getHoursEnrolled()
{
    int totalCredits = 0;
    int i;

    for (i = 0; i < numberOfCourses; i++)
        totalCredits += coursesEnrolled[i].getCredits();

    return totalCredits;
} //end getHoursEnrolled
```
```

If a student has not paid the tuition, the function `billingAmount` calculates and returns the amount due, based on the number of credit hours enrolled. The definition of this function is:

```
```cpp
double StudentType::billingAmount(double tuitionRate)
{
    return tuitionRate * getHoursEnrolled();
} //end billingAmount
```
```