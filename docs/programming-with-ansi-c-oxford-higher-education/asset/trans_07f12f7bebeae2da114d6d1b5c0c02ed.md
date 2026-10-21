

add(Int1);

在第一种情况下，当我们没有向函数传递参数时，它实际上是用参数 100 和 200 分别调用的，因为它们在函数头中被定义为默认参数。因此，输出的数字是 300。在第二种情况下，我们只提供了一个参数。这被认为是第一个参数（显然），而未由调用者明确提供的第二个参数则取自默认值；因此，5 加上 200 得到 205 作为输出。有趣的是，如果用户的意图是只提供第二个参数并将第一个参数作为默认值，如果函数按如下方式调用，则不会得到预期的答案。

add(Int2);

输出是 207，这意味着 Int2 被认为是第一个参数，第二个参数取默认值。

C++ 编译器如何知道 Int2 应该作为第二个参数？是因为它里面包含 2 吗？如果参数是 Balance 和 Interest，这在实际程序中更有可能呢？没有办法向编译器提供此信息。因此，第一个参数被假定为默认值。

第 3 章的程序 3.9 已在程序 4.3 中修改。函数 CheckPass() 已添加到程序中。该函数足够简单易懂。它的主体只有一行并返回一个 bool 值，通过为 true，不通过为 false。返回的值取决于学生的成绩和及格分数的值。

函数 PrintDetails() 也被更改，使其在调用 CheckPass() 函数后还显示学生是否通过。PrintDetails() 使用多种类型的及格分数值进行调用，以展示具有默认参数的函数如何被调用。

## PROGRAM 4.3 Default arguments

```
// DefaultArgument.cpp
#include <iostream>
#include <string>
using namespace std;

bool CheckPass(int TotalMarks, int PassingMarks = 50);
// Default value is specified here for an argument

class student
{
public:
    int RollNumber;
    string Name;
    string Address;
    int TotalMarks;

    void SetDetails(int Roll, string StudentName, string StudentAddress, int StudentMarks)
    {
        RollNumber = Roll;
        Name = StudentName;
        Address = StudentAddress;
        TotalMarks = StudentMarks;
    }

    void PrintDetails()
{
    cout << "Roll number is " << RollNumber << "\n";
    cout << "Name is " << Name << "\n";
    cout << "Address is " << Address << "\n";

    if(CheckPass(TotalMarks))
        // It takes passing marks as 50 here
        cout << "Congratulations! You have passed (passing marks 50)\n";
    if(CheckPass(TotalMarks,40))
        cout << "Congratulations! You have passed (passing marks 40)\n";
    if(CheckPass(TotalMarks, 35))
        cout << "Congratulations! You have passed (passing marks 35)\n";
    else
        cout << "Sorry! Better luck next time\n";
}
};
bool CheckPass(int TotalMarks, int PassingMarks)
/* Notice the default value for an argument is not repeated here,
it is an error if it is done that way */
{
    return(TotalMarks > PassingMarks);
}
void main()
{
    student ArrayOfStudents[3];
    ArrayOfStudents[0].SetDetails(1, "Umesh Yadav", "New Delhi", 75);
    ArrayOfStudents[0].PrintDetails();
    ArrayOfStudents[1].SetDetails(2, "Varon Aaron", "Jharkhand", 87);
    ArrayOfStudents[1].PrintDetails();
    ArrayOfStudents[2].SetDetails(3, "Vinay Kumar", "Tamil Nadu", 37);
    ArrayOfStudents[2].PrintDetails();
}
```

## How the Program Works

查看 CheckPass() 函数的原型。

```
bool CheckPass(int TotalMarks, int PassingMarks = 50);
```

这里，PassingMarks 是一个默认参数，其默认值设为 50。这意味着如果仅用一个参数调用函数 CheckPass()，第二个参数的默认值应取为 50。函数可以用 CheckPass(72) 或 CheckPass(30) 调用，其中及格分数将被视为 50，即第二个参数默认假定为 50。因此，对 CheckPass(72) 的调用等同于调用 CheckPass(72, 50)。应注意，函数也可以用 CheckPass(40, 35) 调用，其中及格分数被明确指定为 35。

在此示例中，默认参数在原型中指定。如果函数在被使用之前定义，则可以省略原型。在这种情况下，函数本身将具有指定的默认参数。如果默认参数已在原型中指定，则不能在函数头中重新定义。因此，如果在调用之前定义函数 CheckPass()，它将具有以下头：

```
bool CheckPass(int TotalMarks, int PassingMarks = 50)
```

而不是

```
bool CheckPass(int TotalMarks, int PassingMarks)
```

并且此时没有原型。

可以有多个默认参数与多个普通参数一起存在。传递这些参数的规则非常简单。所有普通参数必须在参数列表中位于所有默认参数之前。

CheckPass() 函数原型可以重写如下（假设代码已更改以适应其他参数的使用）：

```
CheckPass(int Sub1Marks, int Sub2Marks, int PassingMarks = 50)
```

```
CheckPass(int Sub1Marks, int Sub2Marks, int PassingMarks1 = 50,
int PassingMarks2 = 35);
```

```
CheckPass(int Sub1Marks, int PassingMarks1 = 50, int Sub2Marks,
int PassingMarks2 = 35);
```

```
/* 此语句是错误的，因为 PassingMarks1 是一个在 Sub2Marks 之前编写的默认参数，而 Sub2Marks 不是默认参数。 */
```

## 4.5.1 Using Static Variable as Default Argument to a Function

如果在大多数情况下参数的值保持不变，则带默认参数的函数非常方便。这里有一个有趣的事实需要注意，静态变量也可以用作默认参数值。因此，可以写成

```
Account(AccountNumber = NextNumber)
```

其中 NextNumber 是一个静态变量，并且每次创建新的 Account 对象时都会递增。这是一个例子，展示了如何向程序添加重要功能。只要创建新账户，它就会自动获得唯一的账户号码。这可以用以下程序中的一个简单示例来说明。getNext() 函数会自动接收下一个立即数字。可以观察到静态整数值 Next 被递增并从函数返回。

这种简单的解决方案仅在下一个数字序列从零开始的情况下才可能，如果 getNext() 序列 supposed 从其他数字开始，则不起作用。这样的程序需要一些更改。

```
#include <iostream>
using namespace std;
static int Next;
int getNext(int NextNumber = Next)
{
    Next++;
    return NextNumber;
}
int main()
{
cout << getNext() << endl;
cout << getNext() << endl;
cout << getNext() << endl;
getchar();
```

输出

0

1

2

鼓励读者思考以下问题：

- 1. 为什么所有普通参数必须在所有默认参数之前？
- 2. 编译器如何确定哪个参数对应哪个参数？
- 3. 编译器如何确定某个特定默认参数是否被显式传递？

## 4.5.2 Functions with Objects as Parameters

C++ 中的函数可以像 C 函数一样具有任何有效的数据类型作为参数或返回类型。作为 C++ 中对象可用性的一个明显结果，C++ 中的函数可以传递和返回对象。考虑以下程序。

### Passing an object

函数可以像其他变量一样传递对象。以下程序使用一个非成员函数 PrintValues()，它接受一个 complex 对象作为参数并打印它。

```
// ReturnComplexObject.cpp
#include <iostream>
using namespace std;
class Complex
{
public:
double real;
double imag;
void SetValues(int TempReal, int TempImag)
{
real = TempReal;
imag = TempImag;
}
};
void PrintValues(Complex ComplexNumber)
{
cout << "(" << ComplexNumber.real << "," << ComplexNumber.imag << ")";
}
int main()
{
