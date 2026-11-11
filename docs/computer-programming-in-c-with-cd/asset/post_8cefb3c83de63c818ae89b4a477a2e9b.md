
- **private:** Makes the members of a class accessible or visible only to the code within the same class. Note that by default, the members of a class are private.
- **protected:** Makes the members of a class accessible or visible only inside the same class and classes derived from it.
- **public:** Makes the members of a class accessible or visible to the code, inside as well as outside the class.

These access specifiers, when used in a class, provide different accessibility (or visibility) to class members. An access specifier must be followed by a colon (:) symbol, as shown in the following code snippet:

```cpp
#include<iostream.h>

class Student
{
    private:                //Optional to use private: here, as all members are
                            private by default
    char sname[20];
    int s_roll_no, sage, sclass;
    protected:
    char fatherName[20];
    public:
    int ssubject,smarks;
};

int main()
{
    Student object1;
    cout<<"Enter student's Name"<<endl;
    cin>>object1.sname;    //Not Accessible, compiler will give error for it
    cout<<"Enter student's father name"<<endl;
    cin>>object1.fatherName;  //Not Accessible, compiler will give error for it
    cout<<"Enter subject code"<<endl;
    cin>>object1.ssubject;    //Accessible
    cout<<"Enter marks scored by student"<<endl;
    cin>>object1.smarks;      //Accessible
    return 0;
}
```

In the preceding code snippet, the scope of data members in the Student class is limited by the use of public, protected, and private keywords. The data members declared after the private keyword, which is followed by a colon (:), indicates that these members cannot be accessed outside the boundary of the Student class. The private keyword is optional to use (just used for the sake of clarity), because all members of a class are private, by default. The data members declared after the protected keyword, which is followed by a colon (:), indicates that these members cannot be accessed outside the Student class, but are accessible within the derived classes of the Student class. The data members declared after the public keyword, which is followed by a colon (:), indicates that these members of the Student class are accessible outside the class structure with the help of an object (in our case, object1) of the Student class.

Besides the data members, a class also has member function inside its body. Let’s learn how to create member functions within a class.

## Creating Member Functions

At times it is difficult to implement a large program even if its algorithm is available to programmers. You can implement such a program by splitting it into a number of independent tasks that can be easily designed, implemented, and managed. The process of splitting a large program into small manageable tasks is called modular programming. In modular programming, a repeated group of instructions in a program can be organized as a function. The functions that are defined as parts of a class are known as methods or member functions of the class. There are two ways to define a method in a class: internal and external. In the internal way, you define a member function inside the body of a class. However, in the external way, you define a member function outside the body of a class using the scope resolution (::) operator.

Listing 1 shows how to define a function within a class (you can find this example in the InFunction.cpp file on the CD in the code\chapter6 folder):

### ▶ Listing 1: Defining a Function in a Class

```cpp
#include<iostream.h>

class Student
{
    private:
    char s_name[20];
    int s_roll_no,s_age, s_class;
    protected:
    char father_name[20];
    public:
    int s_subject,s_marks;

    void inputData()
    {
        cout<<"Enter student's roll number"<<endl;
        cin>>s_roll_no;
        cout<<"Enter student's name"<<endl;
        cin>>s_name;
        cout<<"Enter student's age"<<endl;
        cin>>s_age;
        cout<<"Enter student's class"<<endl;
        cin>>s_class;
        cout<<"Enter subject code"<<endl;
        cin>>s_subject;
        cout<<"Enter marks scored by student"<<endl;
        cin>>s_marks;
    }

    void displayData()
    {
        cout<<"Student's Roll Number:"<<s_roll_no<<endl;
        cout<<"Student's Name:"<<s_name<<endl;
        cout<<"Student's Age:"<<s_age<<endl;
        cout<<"Student's Class:"<<s_class<<endl;
        cout<<"Subject Code:"<<s_subject<<endl;
        cout<<"Student's Marks:"<<s_marks<<endl;
    }
};

int main()
{
    Student object1;
    object1.inputData();
    object1.displayData();
    return 0;
}
```

### Output:

```text
Enter student's roll number
1001
Enter student's name
Kabir
Enter student's age
12
Enter student's class
7
Enter subject code
104
Enter marks scored by student
87
Student's Roll Number:1001
Student's Name:Kabir
Student's Age:12
Student's Class:7
Subject Code:104
Student's Marks:87
```

In Listing 1, the Student class has two member functions— `inputData()` and `displayData()`. The return type of both these functions is `void`. The `inputData()` method performs the task of accepting the students' information, such as roll number, name, and marks. The displayData() method, on the other hand, is used to display the information about these students.

Besides defining a method inside the class definition, there is an external way to define a method’s body outside the class structure by using the scope resolution operator. Listing 2 shows how to code a member function’s definition outside the class structure by using the scope resolution operator (you can find this example in the ExFunction.cpp file on the CD in the code\chapter6 folder):

### ▶ Listing 2: Defining a Function outside a Class Using Scope Resolution Operator

```cpp
#include<iostream.h>

class Student
{
    private:
    char sname[20];
    int sage,sclass;
    protected:
    char fatherName[20];
    public:
    int ssubject,smarks;
    void inputData();
    void displayData();
};

void Student::inputData()
{
    cout<<"Enter student's name"<<endl;
    cin>>sname;
    cout<<"Enter student's age"<<endl;
    cin>>sage;
    cout<<"Enter student's class"<<endl;
    cin>>sclass;
    cout<<"Enter subject code"<<endl;
    cin>>ssubject;
    cout<<"Enter marks scored by student"<<endl;
    cin>>smarks;
}

void Student::displayData()
{
    cout<<"Student's Name:"<<sname<<endl;
    cout<<"Student's Age:"<<sage<<endl;
    cout<<"Student's Class:"<<sclass<<endl;
    cout<<"Subject Code:"<<ssubject<<endl;
    cout<<"Student's Marks:"<<smarks<<endl;
}

int main()
{
    Student object1;
    object1.inputData();
    object1.displayData();
    return 0;
}
```

### Output:

```text
Enter student's roll number
1001
Enter student's name
Kabir
Enter student's age
12
Enter student's class
7
Enter subject code
104
Enter marks scored by student
87
Student's Roll Number:1001
Student's Name:Kabir
Student's Age:12
Student's Class:7
Subject Code:104
Student's Marks:87
```

In Listing 2, the Student class has the declaration of two member functions, `inputData()` and `displayData()`. The declaration of a function, without definition, is also called the prototype of a function. The return type of the `inputData()` and `displayData()` functions is `void`. The `inputData()` function is defined outside the boundary of the class Student using the scope resolution operator (`::`). Consider the following code snippet:

```cpp
void Student::inputData()
{
...
...
...
}
```

In the preceding code snippet, `void` is the return type of the `inputData()` function. Student is the name of the user-defined class followed by scope resolution operator (`::`), and `inputData()` is the name of a function declared in the Student class. The `inputData()` function is defined outside the boundary of the Student class to accept the information, such as, roll number, name, and marks of any student.

Similar to the inputData() function, the displayData() function is a class member of the Student class. The displayData() function is also defined outside the boundary of the Student class by using the scope resolution operator (::). Consider the following code snippet:

```cpp
void Student::displayData()
{
...
...
...
}
```

In the preceding code snippet, void is the return type of the displayData() function, and Student is the name of a user-defined class followed by scope resolution operator (::). The displayData() function, however, is used to display the student information.

In C++, the functions declared in a class are private, by default. However, you can make the functions of a class as private, protected, or public explicitly by using the private, protected, or public keyword, respectively. The functions defined in a class are invoked by using the dot (.) operator or class member access indirection (->) operator. The following code snippet shows a function access using the dot operator:

```cpp
object1.inputData();
```

In the preceding code snippet, object1 is the name of an object of the Student class, and inputData() is a function of the class.

Let's create the following functions in a class:

- A const function
- A nested function

## Creating const Functions

A const function does not allow modifying the values of data members of a class. Listing 3 shows an example of the const function (you can find this example in the ConstFunction.cpp file on the CD in the code\chapter6 folder):

### ▶ Listing 3: Creating a const Function in a Class

```cpp
#include<iostream.h>

class ConstFunction
{
    int x,y;
    public:
    void setval();
    void display() const;
    // prototype of a const function
};
```
