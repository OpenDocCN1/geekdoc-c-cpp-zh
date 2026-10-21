

编译时多态。也可以有运行时多态，这可通过使用虚函数实现（在第 10 章讨论）。

展品 4.3 给出了默认参数和函数重载解决方案的比较。

**展品 4.3 默认参数与函数重载解决方案的比较**

有时，一个问题既可以用默认参数也可以用函数重载来解决。考虑以下示例：

```cpp
bool CheckPassing(int TotalMarks, int PassingMarks = 50)
```

也可以写成两个不同的函数

```cpp
bool CheckPassing(int TotalMarks);
```

和

```cpp
bool CheckPassing(int TotalMarks, int PassingMarks);
```

我们可以看到，在这两种情况下（使用默认参数或重载函数）的函数调用并无不同。

默认参数显然比函数重载更简单的方式。无需编写函数的两个不同版本。然而，有一个重要的区别；在默认参数的情况下，当用户未指定参数时，默认值会被隐式传递，而在函数重载的情况下，只有显式指定的参数才会被传递。

## 4.9 程序可读性与默认参数

使用默认参数时，程序的可读性可能会受到影响。当使用一个参数调用函数 `CheckPass()` 时，读者无法得知有一个第二个参数正在被自动传递。`PassingMarks` 在逻辑上是可理解的，因此在此情况下是可以接受的。如果不是 `PassingMarks`，而是向 `CheckPass()` 传递学生的姓名，并且如果 `CheckPass()` 有时（并非总是）对其执行某些操作，则对读者来说并不明显。

假设我们需要从某个数据库中根据学生的姓名查找其父母，并在学生不及格时给他们发送邮件。这不是常见的情况。通过查看对 `CheckPass()` 的调用，用户将无法知道发生了什么。在这种情况下，最好使用重载函数显式传递学生的姓名。

对于检查学生是否及格，传递分数是一个显而易见的参数，也是默认参数的合理候选，而学生姓名则不是。当需要时，应使用函数的重载版本显式传递学生的姓名。

在大多数情况下，这类情况都是由于设计错误造成的。这样的函数（向学生家长报告学生不及格）应该被显式调用。将姓名作为默认值传递给本应检查学生是否及格的函数是不正确的设计。

> 默认参数在函数调用处不可见；这有时会妨碍程序的可读性。

## 4.10 成员函数与非成员函数

我们已经讨论了一些调用成员函数和非成员函数之间的差异。让我们看一个例子来详细说明差异。

程序 4.9 包含两个执行相同工作——找出传递给它们的 Time 对象之间差值的函数。其中一个 `MemDiffTime()` 是成员函数，而 `Difference()` 是非成员函数。

**程序 4.9 成员函数与非成员函数**

```cpp
// MemNonMem.cpp
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
        cout << "Time is " << Hours << " hours : " << Minutes << " minutes : and " << Seconds << " seconds \n";
    }

    void SetTime(int TempHours, int TempMinutes, int TempSeconds)
    {
        Hours = TempHours;
        Minutes = TempMinutes;
        Seconds = TempSeconds;
    }

    /* The following is a member function doing the same job as a non-member Difference()
       (standalone) function */
    void MemDiffTime(Time Time2)
    {
        /* Only one argument Time2 is passed; this is treated as the second argument. The first
           is an implicit argument, pointer to the calling object (the 'this' pointer), that is,
           pointer to Time4 in our example */
        {
            Seconds = Seconds - Time2.Seconds;
            /* Seconds or hours can now be used without the object.member format, that is, in
               our case, Time4.Seconds */
            if (Seconds < 0)
            {
                Seconds += 60;
                Minutes--;
                if (Minutes < 0)
                {
                    Minutes = 59;
                    Hours--;
                }
            }
        }

        Minutes = Minutes - Time2.Minutes;
        if (Minutes < 0)
        {
            Minutes += 60;
            Hours--;
        }

        Hours = Hours - Time2.Hours;
        if (Hours < 0)
        {
            Hours = 0;
            Minutes = 0;
            Seconds = 0;
            // To indicate erroneous input
        }

        /* There is no return statement. The object pointer is implicitly passed.
           It points to the changed object, so we do not need any return statement now */
    }
};

void main()
{
    Time Difference(Time, Time);
    /* Prototype for our non-member function */
    Time Time1, Time2;
    Time1.SetTime(12, 15, 15);
    cout << "The first value \n";
    Time1.ShowTime();
    Time2.SetTime(10, 30, 30);
    cout << "The second value \n";
    Time2.ShowTime();

    Time Time3;
    Time3 = Difference(Time1, Time2);
    cout << "The difference using a non-member function is \n";
    Time3.ShowTime();

    Time Time4 = Time1;
    Time4.MemDiffTime(Time2);
    cout << "The difference using a member function is \n";
    Time4.ShowTime();
}

Time Difference(Time T1, Time T2)
{
    Time DifferenceTime;
    DifferenceTime.Seconds = T1.Seconds - T2.Seconds;
    if (DifferenceTime.Seconds < 0)
    {
        DifferenceTime.Seconds += 60;
        T1.Minutes--;
        if (T1.Minutes < 0)
        {
            T1.Minutes = 59;
            T1.Hours--;
        }
    }

    DifferenceTime.Minutes = T1.Minutes - T2.Minutes;
    if (DifferenceTime.Minutes < 0)
    {
        DifferenceTime.Minutes += 60;
        T1.Hours--;
    }

    DifferenceTime.Hours = T1.Hours - T2.Hours;
    if (DifferenceTime.Hours < 0)
    {
        DifferenceTime.Hours = 0;
        DifferenceTime.Minutes = 0;
        DifferenceTime.Seconds = 0; // To indicate erroneous input
    }

    return DifferenceTime;
}
```

**输出**

The first value  
Time is 12 hours : 15 minutes : and 15 seconds

The second value  
Time is 10 hours : 30 minutes : and 30 seconds

The difference using a non-member function is  
Time is 1 hours : 44 minutes : and 45 seconds

The difference using a member function is  
Time is 1 hours : 44 minutes : and 45 seconds

**程序如何工作**

查看 `MemDiffTime()` 和 `Difference()` 函数并观察两者之间的差异。虽然它们的目的相同，但在某些地方有所不同。让我们详细查看每一个。

1. 使用成员函数时，只需传递一个参数而不是两个参数。第一个参数是隐式传递的。不能选择第一个参数；它始终是指向调用该函数的对象的指针。在非成员情况下，`Difference(Time1, Time2)` 或 `Difference(Time2, Time1)` 都是可能的。使用 `Time4.MemDiffTime(Time2)` 则绝对不可能，指针指向 `Time4` 将始终是第一个参数。在 `Time2.MemDiffTime(Time4)` 中，指针指向 `Time2` 将始终是第一个参数。我们将在讨论使用友元成员函数进行运算符重载时再次重访这个问题。

2. 我们在成员函数中使用成员变量而不指定其调用对象，例如，不是写 `T1.Seconds`，我们只写 `Seconds`。这里再次假设了调用对象，写 `Seconds` 等同于写 `this->Seconds`。

3. 另一个区别与访问的成员变量的访问说明符有关。`Difference()` 能工作是因为 `Seconds`、`Minutes` 和 `Hours` 都是公有变量。如果它们是私有变量，只有 `MemDiffTime()` 会工作而 `Difference()` 不会工作。如果 `Difference()` 函数需要在这些变量定义为私有时仍然工作，则应将其设为类 `Time` 的友元。我们将在第 4.11 节讨论友元。

4. 使用成员函数时不需要显式的 return 语句。自动传递的 `this` 指针（指向调用对象）已负责此事。`this` 指针实际上会使函数对实际对象操作（因为传递了指向它的指针），因此我们不需要任何返回值。非成员函数在临时副本上操作，需要返回它。

### 4.10.1 决定将函数设为成员还是非成员

这是一个设计相关的问题。在程序 4.9 这样的情况下，我们应该定义独立函数还是成员函数？经验法则是，如果它自然是成员，就使用成员函数。为什么？

