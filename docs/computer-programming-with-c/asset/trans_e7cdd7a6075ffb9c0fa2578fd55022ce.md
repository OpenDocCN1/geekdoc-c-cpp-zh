

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

`main()` 函数中的第一条语句

```cpp
Student s1;
```

创建一个名为 s1 的 Student 类对象。这个对象可以存储现实世界中一个 Student 的数据。由于 Student 是 Person 的子类，s1 的对象内存将包含从 Person 继承的成员 name、dob 和 gender，以及专门的成员变量（roll_no 和 marks），如图 14.34 所示。注意，如前所述，Date 对象将是 s1 对象内存的一部分。成员函数 inputPerson()、outputPerson() 和 calculateAge() 也将被 Student 类继承，并且由于它们在 Person 中被定义为公有函数，因此可以在子类中直接访问。因此，可以正确地想象 Student 类总共有五个函数（inputStudent()、

![](img/57c0d966bb33c67a5a188e6bf39e4e02_815_0.png)

图 14.35：从用户处获取 s1 成员的过程

将 Student 对象的所有成员值打印到计算机屏幕上。这个执行流程可以用与我们解释输入逻辑类似的方式来理解。函数 outputStudent() 调用 outputPerson() 打印姓名和性别，然后调用 calculateAge() 打印学生的年龄。calculateAge() 调用 Date 类中的 getDateDiff() 函数，该函数给出当前日期与出生日期之间的差值。

与我们对 Student 对象所做的类似，以下语句

```cpp
Professor p1;
p1.inputProf();
p1.outputProf();
```

创建一个名为 p1 的 Professor 类对象，输入 p1 的成员变量并将详细信息打印到计算机屏幕上。

> **在计算机内存中，我们如何表示既不是学生也不是教授的人？**
>
> 对于现实世界中的这样的人，我们不能创建 Student 类的对象，因为他/她不是学生；也不能创建 Professor 类的对象，因为他/她不是教授。为了存储不属于任何子类别的对象的数据，我们必须在程序中创建一个父类的对象。这是因为我们知道现实世界的对象仅属于一般类别，而不属于任何专门类别。在这种情况下，我们知道现实世界的对象是一个人，但他/她既不是大学的学生，也不是教授。这个对象可能是图书管理员、职员或大学其他工作人员。在这种情况下，由于我们没有可以表示该对象的正确子类，我们应该使用下面的语句创建一个一般类（Person）的对象来存储其数据。
>
> Person p1;
>
> 然而，由于 p1 只包含 name、dob 和 gender 三个成员，对于任何既不是 Student 也不是 Professor 的其他对象，我们只能存储这些信息。如果需要存储任何额外信息，建议你创建 Person 类的另一个子类来表示该类别。例如，Clerk 类可以表示所有职员，Accountant 类可以表示所有会计师等。请记住，如前所述，只有当类之间存在相当大的属性差异，且仅使用广义类无法完整表示对象时，才应将类插入继承层次结构中。
>
> 在某些情况下，业务逻辑强制要求所有对象必须映射到至少一个子类。这意味着业务中不能存在对象不属于任何子类别的情况。在这种情况下，你的继承树必须是完整的，并且应创建子类来表示业务范围内所有可能的对象。这样，就完全不需要创建父类的对象。这种永远无法创建对象的父类称为抽象类。抽象类将在 14.14 节中详细讨论。

## 14.6 多级继承：计算器

作为多级继承的一个例子，让我们创建一个 C++ 程序来设计不同类型的计算器。要求设计三种类型的计算器：

- 1. **基本计算器**：该计算器仅提供算术功能，如两个变量的加法、减法、乘法和除法。
- 2. **三角函数计算器**：该计算器提供基本计算器的所有功能，以及计算角度的正弦、余弦和正切的额外功能。由于三角函数计算器需要提供基本计算器的所有功能，我们不会在 Trigonometric 类中重写它们，而是将 Trigonometric 计算器类创建为 Basic 类的子类。这样，我们只需在 Trigonometric 类中定义专门的功能（计算正弦、余弦和正切），因为 Basic 的功能无论如何都会被继承。
- 3. **科学计算器**：该计算器提供 Basic 和 Trigonometric 类的所有功能，以及计算自然对数和以 10 为底的对数的额外功能。虽然 Scientific 计算器需要 Basic 和 Trigonometric 两者的功能，但仅将 Scientific 计算器创建为 Trigonometric 的子类就足够了。这是因为 Trigonometric 计算器无论如何都会继承 Basic 计算器的功能，这些功能将传递给 Scientific 计算器。因此，我们只需将 Scientific 计算器类创建为 Trigonometric 计算器的子类。这样，Scientific 计算器只需定义所需的对数功能，而 Basic 和 Trigonometric 计算器的功能将被继承。所需的类层次结构如图 14.36 所示。

