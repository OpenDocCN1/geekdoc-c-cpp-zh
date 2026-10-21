

```
cout << "Designation is " << Designation << "\n";
}
/* Now member functions of the following class can access private variables of this class */
friend CollectionEmp;
/* If forward declaration is not provided, this statement will give an error */
};
class CollectionEmp
{
private:
    employee ColEmp[10];
    /* The collection is in the array form; it can even be a linked list */
    int Index;
public:
    void InitIndex()
    {
        Index = 0;
    }

    bool operator +(employee Emp)
    {
        if(Index < 9)
        {
            ColEmp[Index] = Emp;
            Index++;
            return true;
        }
        else
        {
            return false;
        }
    }

    void ListDeptWise()
    {
        string TempDeptName;
        cout << "Enter the department of the university:";
        cin >> TempDeptName;
        cout << "\n";

        for(int i = 0; i < 10; ++i)
        {
            if(ColEmp[i].DeptName == TempDeptName)
            {
                ColEmp[i].DisplayDetails();
            }
        }
    }
};
void main()
{
    CollectionEmp UniEmpCol;
    UniEmpCol.InitIndex();
    employee UniEmployee[10];

    UniEmployee[1].Init(1,"Lara", "Exam", "Professor");
    UniEmployee[2].Init(2, "Ponting", "Marksheet", "Clerk");
    UniEmployee[3].Init(3, "Laxman", "Accounts", "Head Clerk");
```
```
UniEmployee[4].Init(4, "Flintoff", "Exam", "Clerk");
UniEmployee[5].Init(5, "Muralidharan", "Accounts", "CAO");
UniEmployee[6].Init(6, "Sarfaraz", "Exam", "Informer");
UniEmployee[7].Init(7, "Dean Jones", "Exam", "Invigilator");
UniEmployee[8].Init(8, "Madugalle", "Exam", "Examiner");
UniEmployee[9].Init(9, "Ganguly", "Marksheet", "Repeater");
UniEmployee[0].Init(10, "Nafees", "Accounts", "Clerk");
for(int i = 0; i < 10; ++i)
{
    UniEmpCol + UniEmployee[i];
    /* Placing the employees in the collection object */
}
UniEmpCol.ListDeptWise();
/* This is a member function now, not a dummy one though! */
}
```

## Output

Enter the department of the university: Exam

Details of employee number 1
Name is Lara
Department is Exam
Designation is Professor

Details of employee number 4
Name is Flintoff
Department is Exam
Designation is Clerk

Details of employee number 6
Name is Sarfaraz
Department is Exam
Designation is Informer

Details of employee number 7
Name is Dean Jones
Department is Exam
Designation is Sleeper

Details of employee number 8
Name is Madugalle
Department is Exam
Designation is Examiner

## How the Program Works

定义和调用时的差异 请看第4章中的程序4.14与本程序之间的差异。只是机械上的差异而已。令人惊讶的是，两个程序中只有两行不同，即定义函数头的那一行和调用函数的那一行。以下是更改内容：

- 1. bool AddToCol() 改为 bool operator +()。
- 2. UniEmpCol.AddToCol(UniEmployee[i]) 改为 UniEmpCol + UniEmployee[i]。

运算符重载的步骤 这表明运算符重载可以使用简单的技术来简化。首先编写一个执行任务的函数，并测试其是否正常工作。然后，只需在程序中的少数地方进行两个机械更改即可。

- 1. 将函数名更改为 operator <operator_symbol>（例如 operator +），在函数定义处进行。
- 2. 在程序中 wherever 函数调用被作出时，将该运算符用作隐式函数调用。因此，Object1.function (Object2) 被更改为 Object1 <Operator> Object2。

> 注意 过度使用重载运算符可能会降低可读性，而适度使用则会提高可读性。为不明显的操作重载运算符，例如使用 '+' 来减去参数，是糟糕的编程。

## Overloading Operators for a Purpose

程序 6.3 显示了如何为目的而重载 +。这里使用了前面讨论过的同一个 Time 类，并重载了 + 来相加两个时间。这里唯一的额外特性是使用同一个运算符处理两个以上的参数。也可以在此注意到构造函数的用途。

## PROGRAM 6.3 Operator overloading for a purpose

```
//AddTime.cpp
#include <iostream>
using namespace std;

class Time
{
public:
    int Hours;
    int Minutes;
    int Seconds;

    void ShowTime()
    {
        cout << "Time is" << Hours << " hours : " << Minutes << " minutes : and " << Seconds << " seconds \n";
    }

    Time(int TempHours = 0, int TempMinutes = 0, int TempSeconds = 0)
    {
        Hours = TempHours;
        Minutes = TempMinutes;
        Seconds = TempSeconds;
    } // It can serve as default constructor as well

    Time operator +(Time Time2)
    {
        int TempHours, TempMinutes, TempSeconds;
        TempHours = Hours + Time2.Hours;
        TempMinutes = Minutes + Time2.Minutes;
        TempSeconds = Seconds + Time2.Seconds;
        TempMinutes += TempSeconds / 60;
        TempSeconds %= 60;
        TempHours += TempMinutes / 60;
        TempMinutes %= 60;
        return Time(TempHours, TempMinutes, TempSeconds);
    }
};
void main()
{
    Time Time1(12, 15, 15);
```
```
cout << "The first value \n";
Time1 ShowTime();
Time Time2(10, 30, 30);
cout << "The second value \n";
Time2.ShowTime();
Time Time3;
Time3 = Time1 + Time2;
cout << "And the result is \n";
Time3.ShowTime();
Time Time4 = Time1 + Time2 + Time3; // Adding three times
Time4.ShowTime();

/* The following will work and would be the same as Time3.ShowTime(). We are not defining a temporary object; the compiler will do that for us here. */
(Time1 + Time2).ShowTime();
}
```

## Output

The first value
Time is 12 hours : 15 minutes : and 15 seconds

The second value
Time is 10 hours : 30 minutes : and 30 seconds

And the result is
Time is 22 hours : 45 minutes : and 45 seconds
Time is 45 hours : 31 minutes : and 30 seconds

## How the Program Works

看语句

```
Time Time4 = Time1 + Time2 + Time3;
```

我们在这里尝试相加三个时间。它类似于语句

```
Time1.operator + (Time2.operator + (Time 3));
```

需要注意的是，这并不是重载的 '+' 具有两个以上参数的情况。重载的 '+' 无论为哪个类重载，始终只有两个参数。

> 注意 我们不能使用重载的 '+' 来相加三项。这是因为当我们重载一个运算符时，必须遵守使用该运算符的原始构造。'+' 设计为使用两个操作数（二元运算符），因此必须遵守这一点。

另一个有趣的语句是

```
(Time1 + Time2).ShowTime();
```

编译器从表达式 Time1 + Time2 生成一个临时对象，并为该对象调用成员函数 ShowTime()。该语句是以下内容的简写表示：

```
Time Temporary = Time1 + Time2; Temporary.ShowTime();
```

## 6.4 SITUATIONS WHERE OPERATOR OVERLOADING IS USEFUL

当我们开发一个将由其他用户使用的类库时，运算符重载很重要。在这种情况下，适当的运算符重载会更有优势。用户无需记住函数名称，拼写错误的可能性也非常小。

## 236 Programming with ANSI C++

当运算符重载为作为团队一部分开发的类提供时，类的使用和可读性在很大程度上取决于运算符定义的直观性。考虑链表的情况。如果为将节点对象添加到链表对象提供重载的 +，它是有意义的，并且可读性强且歧义较少。

```
Like LinkedList, L, Newlist;
Node N;
L = L + N; // Adding a node to a list
Newlist = L + N; // New list from old list and adding a node
```

还需要注意的是，程序 6.2 中的重载 + 不一定返回相同类型的对象。在其原始形式中，+ 运算符始终返回相同对象类型的对象；相加两个整数返回一个整数，相加两个浮点数返回一个浮点数，等等。然而，在程序 6.2 中，它返回一个布尔值。在链表示例中，它相加两种不同类型的对象并返回第一个操作数的类型。C++ 提供了这种灵活性，这使得运算符重载极其有用。

并非所有运算符都享有重载的灵活性。运算符 new、delete 和 -> 有限制，它们只能返回与原始运算符相同类型的对象。

运算符可分为一元运算符（有一个参数）和二元运算符（有两个参数）。应记住，不可能重载唯一的 ternary 运算符。

## 6.5 OVERLOADING UNARY OPERATORS

具有单个参数的运算符称为一元运算符。当这些运算符作为成员函数重载时，不必显式传递任何参数。指向调用对象的 this 指针作为隐式参数传递。

```
//UnaryOp.cpp
#include <iostream>
using namespace std;
class Matrix
{
	int Element[3][3];
public:
	Matrix() {} // Default constructor
	Matrix(int TempMatrix[3][3])
	{
		for(int i = 0; i < 3; i++)
			for(int j = 0; j < 3; j++)
				Element[i][j] = TempMatrix[i][j];
	}
	void Read()
	{
		for(int i = 0; i < 3; i++)
			for(int j = 0; j < 3; j++)
				cin >> Element[i][j];
	}
}
```
