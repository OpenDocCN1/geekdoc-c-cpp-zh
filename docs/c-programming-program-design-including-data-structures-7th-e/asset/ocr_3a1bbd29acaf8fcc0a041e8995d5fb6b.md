The default constructor initializes the private member variables to the default values. Note that because the private member variable `coursesEnrolled` is an array of type `courseType`, the default constructor of the class `courseType` executes automatically, and the entire array is initialized.

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

The function print prints the grade report. The parameter outF specifies the output device. If the student has paid his or her tuition, the grades and the GPA are shown. Otherwise, three stars are printed in place of each grade, the GPA is not shown, a message indicates that the grades are being held for nonpayment of the tuition, and the amount due is shown. This function has the following steps:

+   1. Output the student’s name.
+   2. Output the student’s ID.
+   3. Output the number of courses in which the student is enrolled.
+   4. Output the heading:
+      ```text
+      Course No  Course Name  Credits  Grade
+      ```
+   5. Print each course’s information.
+      For each course, print:
+      a. Course No, Course Name, Credits
+      b. if `isTuitionPaid` is true
+         Output the grade
+   
+         else
+         Output three stars.
+   6. Print the total credit hours.
+   7. To output the GPA and billing amount in a fixed decimal format with the decimal point and trailing zeros, set the necessary flag. Also, set the precision to two decimal places.
+   8. if `isTuitionPaid` is true
+      Output the GPA
+   
+      else
+      Output the billing amount and a message about withholding the grades.