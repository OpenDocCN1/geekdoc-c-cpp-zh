```
```cpp
int main()
{
    Student *ptrObject=new Student;
    // perform the task with object
    delete ptrObject;
    return 0;

}
```
```

In the preceding code snippet, a pointer object, ptrObject of the Student class is created. The ptrObject object gets the memory by using the new operator and the same object gets destroyed by using the delete operator.

# Creating Data Members

You can store data in objects by creating data members. The following code snippet shows the declaration of data members inside a class:

```
```cpp
#include<iostream.h>

class Student
{
/* Declaring data members */
    char s_name[20];
    int s_roll no, s_age, s_class;
    char father_name[20];
    int s_subject, s_marks;
};

int main()
{
    Student object1;
    return 0;
}
```
```

In the preceding code snippet, data members in classes are private by default. You can make data members in a class private, protected, or public by explicitly declaring them with the `private`, `protected`, and `public` keywords.

Let’s now learn how to use these keywords in C++.

# Using Access Specifiers

In C++, the access specifiers are used to identify access rights for the data members and member functions of a class. The following are the three types of access specifiers in C++: