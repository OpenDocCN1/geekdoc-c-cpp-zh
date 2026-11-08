```
```cpp
private:
    void sortCourses();
        //Function to sort the courses.
        //Postcondition: The array coursesEnrolled is sorted.
        //              For each course, its grade is stored in
        //              the array coursesGrade. Therefore, with
        //              the array coursesEnrolled is sorted, the
        //              corresponding entries in the array
        //              coursesGrade are adjusted.

    int sId;                 //variable to store the student ID
    int numberOfCourses;     //variable to store the number
                             //of courses
    bool isTuitionPaid;      //variable to indicate whether the
                             //tuition is paid
    courseType coursesEnrolled[6]; //array to store the courses
    char coursesGrade[6];          //array to store the course grades
};
```
```

Figure 11-10 shows the UML class diagram of the class `studentType` together with the inheritance and composition (aggregation) relation.

![](bbox=[0.273, 0.481, 0.879, 0.744])

**FIGURE 11-10** UML class diagram of the class `studentType` together with inheritance and composition (aggregation) relation.

Before writing the definitions of the member functions of the class `studentType`, we make the following note.