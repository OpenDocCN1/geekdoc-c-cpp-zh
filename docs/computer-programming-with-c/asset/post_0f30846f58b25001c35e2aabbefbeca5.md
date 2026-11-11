
```cpp
today.dd = system.wDay;
today.mm = system.wMonth;
today.yy = system.wYear;
return today;
}

Date getDateDiff(Date d)
{
    Date result;
    if (dd >= d.dd)
    {
        result.dd = dd - d.dd;
    }
    else
    {
        dd = dd + 30;
        mm = mm - 1;
        result.dd = dd - d.dd;
    }
    if (mm >= d.mm)
    {
        result.mm = mm - d.mm;
    }
    else
    {
        mm = mm + 12;
        yy = yy - 1;
        result.mm = mm - d.mm;
    }
    result.yy = yy - d.yy;
    return result;
}
};

class Person
{
    protected:
        char gender;
        char name[100];
        Date dob;
    public:
        void inputPerson()
        {
            cout << "Enter Name:" << endl;
            cin >> name;
            cout << "Enter Gender:" << endl;
            cin >> gender;
            cout << "Enter Date of birth:" << endl;
            dob.inputDate();
        }
        void outputPerson()
        {
            cout << "Name:" << name << endl;
            cout << "Gender:" << gender << endl;
            cout << "Date of birth is:" << endl;
            dob.outputDate();
        }
        void calculateAge()
        {
            Date today = Date::getCurrentDate();
            /*Calculate Difference between todays date and date of birth
            to determine the age*/
            Date age = today.getDateDiff(dob);
            cout << "Age is:" << endl;
            age.outputAge();
        }
};

class Student : public Person
{
    private:
        int roll_no;
        int marks;
    public:
        void inputStudent()
        {
            inputPerson(); // get generic details
            cout << "Enter RollNumber:" << endl;
            cin >> roll_no;
            cout << "Enter Marks:" << endl;
            cin >> marks;
        }
        void outputStudent()
        {
            outputPerson(); // get generic details
            calculateAge(); // Print age
            cout << "RollNumber is:" << roll_no << endl;
            cout << "Marks are:" << marks << endl;
        }
};

class Professor : public Person
{
    private:
        int prof_id;
        int salary;
    public:
        void inputProf()
        {
            inputPerson(); // get generic details
            cout << "Enter Prof Id:" << endl;
            cin >> prof_id;
            cout << "Enter salary:" << endl;
            cin >> salary;
        }
        void outputProf()
        {
            outputPerson(); // get generic details
            calculateAge(); // Print age
            cout << "Prof ID is:" << prof_id << endl;
            cout << "Salary is:" << salary << endl;
        }
};

void main()
{
    cout << "***************Student******************** " << endl;
    Student s1;
    s1.inputStudent();
    s1.outputStudent();
    cout << "***************Professor****************** " << endl;
    Professor p1;
    p1.inputProf();
    p1.outputProf();
}
```

The first statement in the `main()` function

```cpp
Student s1;
```

creates an object of class Student named as s1. This object can store data about one Student in a real world. As Student is a child class of Person, the object memory of s1 will contain members name, dob, and gender inherited from Person along with the specialized member variables (roll_no and marks) as shown in the Figure 14.34. Note that object of Date name will be the part of object memory of s1 as discussed before. The member functions inputPerson(), outputPerson(), and calculateAge() will also be inherited by class Student and can be accessed directly within the child class as they are defined as public functions in Person. Hence, it would be correct to imagine that the class Student has five functions in all (inputStudent(),

![](img/57c0d966bb33c67a5a188e6bf39e4e02_815_0.png)

Figure 14.35: Process to take members of s1 as input from the user

will print all the member values of Student object on the computer screen. This execution flow can be understood in a similar way as we have explained the input logic. The function outputStudent() calls outputPerson() to print name and gender, then calls calculateAge() to print the age of the Student. calculateAge() invokes the getDateDiff() function in class Date which gives the difference between the current date and the date of birth.

Similar to what we have done with the Student object, the statements

```cpp
Professor p1;
p1.inputProf();
p1.outputProf();
```

create an object of class Professor named as p1, input the member variables of p1 and print the details on the computer screen.

> **How do we represent a person who is neither student nor a professor in computer memory?**
>
> For such a person in real world, we cannot create object of class Student because he/she is not a student, neither can we create object of class Professor as he/she is not a professor. In order to store data about objects which do not belong to any of the child categories we must create an object of a parent class in our program. This is because we know that the real world object just falls in the general category but does not fall in any of the specialized categories. In this case, we know that the real world object is a person but he is neither a student nor a professor of the university. This object may be librarian, clerk or part of any other university staff. In this case, since we do not have the correct child class that can represent this object, we should create an object of a general class (Person) using the statement below, to store its data.
>
> Person p1;
>
> However, since p1 contains only three members name, dob and gender, we will be able to store only this information for any other object who is neither Student or Professor. If you need to store any additional information, then it is recommended that you create another child class of class Person to represent this category. For example, class Clerk may represent all clerks, class Accountant may represent all accountants etc. Remember, as mentioned before classes should be plugged into the inheritance hierarchy only if there is a considerable attribute different among them and if the object cannot be represented fully using the generalized class alone.
>
> In some cases, the business logic puts a mandate that all objects must map to at least one child class. This means that there cannot be a situation in business wherein an object does not belong to any of the child categories. In this case your inheritance tree must be complete and there should be child classes created to represent all the possible objects in the scope of business. This way there is no need to create an object of parent class at all. Such a parent class whose object can never be created is called as abstract class. Abstract classes are discussed in detail in section 14.14.

## 14.6 Multi-level Inheritance: Calculator

As an example of multi-level inheritance, let us create a C++ program to design different types of calculators. The requirement is to design three types of calculators:

- 1. **Basic calculator**: This calculator provides only arithmetic functions like addition, subtraction, multiplication and division with two variables.
- 2. **Trigonometric calculator**: This calculator provides all the features of basic calculator along with the additional functions to calculate sine, cosine, and tangent of an angle. Since, the trigonometric calculator is required to provide all the features of basic calculator, instead of rewriting them in the Trigonometric class, we will create the Trigonometric calculator class as a child class of class Basic. This way we will only have to define the specialized functions (to compute sine, cosine, and tangent) in the Trigonometric class because the functions of Basic will be anyways inherited.
- 3. **Scientific calculator**: This calculator provides all the features of Basic and Trigonometric class along with the additional functions to calculate natural logarithm and log to the base 10. Although the Scientific calculator needs the functions of both Basic as well as Trigonometric, it is sufficient to create Scientific calculator as a child class of Trigonometric alone. This is because the Trigonometric calculator anyways inherits the features of Basic calculator which will be passed on to Scientific calculator. Hence we just create the Scientific calculator class as a child class of Trigonometric calculator. This way, the Scientific calculator is only required to define required logarithmic functionalities and the functionalities of Basic and Trigonometric calculator will be inherited. Required hierarchy of classes is as shown in Figure 14.36.
