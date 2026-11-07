+   36. What is the difference between compile-time binding and run-time binding? (13)

+   37. Is it legal to have an abstract class with all member functions pure virtual? (14)

+   38. Consider the following definition of the class studentType:

```
~~~cpp
class studentType: public personType
{
public:
    void print();
    void calculateGPA();
    void setID(long id);
    void setCourses(const string c[], int noOfC);
    void setGrades(const char cG[], int noOfC);

    void getID();
    void getCourses(string c[], int noOfC);
    void getGrades(char cG[], int noOfC);
    void studentType(string fName = "", string lastName = "",
                     long id, string c[] = NULL,
                     char cG[] = NULL, int noOfC = 0);

private:
    long studentID;
    string courses[6];
    char coursesGrade[6];
    int noOfCourses;
};
~~~
```

Rewrite the definition of the class studentType so that the functions print and calculateGPA are pure virtual functions. (14)

+   39. Suppose that the definitions of the classes employeeType, fullTimeEmployee, and partTimeEmployee are as given in Example 12-9 of this chapter. Which of the following statements is legal? (14)

+   a. employeeType tempEmp;
+   b. fullTimeEmployee newEmp();
+   c. partTimeEmployee pEmp("Molly", "Burton", 101, 0.0, 0);

+   40. What is the effect of the following statements? (15)

+   a. unorderedArrayListType intList1(50);
+   b. unorderedArrayListType intList2(1000);
+   c. unorderedArrayListType intList3(-10);

# PROGRAMMING EXERCISES

+   1. Redo Programming Exercise 5 of Chapter 8 using dynamic arrays.
+   2. Redo Programming Exercise 6 of Chapter 8 using dynamic arrays.