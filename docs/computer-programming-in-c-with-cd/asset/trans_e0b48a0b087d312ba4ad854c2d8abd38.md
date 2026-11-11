
`endl` 操纵符定义在 `iostream.h` 头文件中，而 `setw()`、`setprecision()` 和 `setfill()` 等操纵符定义在 `iomanip.h` 头文件中。下面我们逐一讨论这些操纵符。

### 使用 endl 操纵符

`endl` 操纵符将输出显示在新的一行。`endl` 操纵符向输出流发送一个换行符。清单 6 展示了 `endl` 操纵符的用法（你可以在 CD 的 `code\chapter2` 文件夹中的 `endlManipulator.cpp` 文件里找到这个示例）：

### ▶ 清单 6：使用 endl 操纵符

```cpp
#include<iostream.h>

int main()
{
  cout<<"Hello";
  cout<<"World";
  cout<<endl;
  cout<<"Hello"<<endl;
  cout<<"World";

  return 0;
}
```

**输出：**

```text
HelloWorld
Hello
World
```

在清单 6 的输出中，你可以看到，当 `endl` 操纵符不与 `cout` 对象一起使用时，HelloWorld 字符串会在屏幕上显示为一行；而当 `endl` 操纵符与 `cout` 对象一起使用时，光标会移到下一行，输出会显示在新的一行。

### 使用 setw() 操纵符

`setw()` 操纵符接受一个整数参数，并设置输出流中每一项的宽度。默认情况下，字符在给定宽度内右对齐。一旦使用 `<<` 运算符显示输出，宽度就会重置为 0。清单 7 展示了 `setw()` 操纵符的用法（你可以在 CD 的 `code\chapter2` 文件夹中的 `setwManipulator.cpp` 文件里找到这个示例）：

### ▶ 清单 7：使用 setw() 操纵符

```cpp
#include<iostream.h>
#include<iomanip.h>
```

### ▶ 清单 9：使用 `setfill()` 操纵符

```cpp
#include<iostream.h>
#include<iomanip.h>
int main()
{
  int x;
  int y;
  cout<<"Calculating sum of two numbers"<<endl<<endl;
  cout<<"Enter two numbers"<<endl;
  cin>>x;
  cin>>y;
  cout<<"Output before using setfill():"<<endl;
  cout<<"sum of two numbers"<<endl;
  cout<<setw(6)<<x+y<<endl;
  cout<<endl;
  cout<<"Output after using setfill():"<<endl;
  cout<<"sum of two numbers"<<endl;
  cout<<setw(6)<<setfill('^')<<x+y<<endl;

  return 0;
}
```

### 输出：

```text
Calculating sum of two numbers

Enter two numbers
5
6
Output before using setfill():
sum of two numbers
     11

Output after using setfill():
sum of two numbers
^^^^^11
```

在清单 9 中，程序提示你输入两个数字。这两个数字分别存储在 `x` 和 `y` 变量中。这两个数字的和首先在左侧以空格显示，因为输出没有使用 `setfill()` 操纵符。这个和再次显示，但这次输出用 `^` 字符替换了空格，因为现在输出使用了 `setfill()` 操纵符。`setfill()` 操纵符用 `^` 字符替代空白字符。

> 为了使用 `setfill()` 操纵符，程序中应包含 `iomanip.h` 头文件。

### 创建自定义操纵符

除了所有预定义操纵符之外，你还可以在 C++ 中创建自己的操纵符。清单 10 展示了如何定义自己的操纵符并在程序中使用它（你可以在 CD 的 `code\chapter2` 文件夹中的 `customManipulator.cpp` 文件里找到这个示例）：

### 清单 10：创建自定义操纵符

```cpp
#include<iostream.h>

ostream & greet (ostream & output)
{
    return output <<"Welcome, ";
}

void main()
{
    char x[10];
    cout<<"Enter your name: ";
    cin>>x;
    cout<<greet<<x;
}
```

**输出：**

```text
Enter your name: user
Welcome, user
```

在清单 10 中，你创建了一个名为 `greet` 的自定义操纵符，它返回输出 `Welcome, `。然后创建了一个程序，其中声明了 `x` 变量，该变量最多存储 10 个字符值。执行此程序时，会提示你输入字符串 `Enter your name:`。输入的名字通过 `cin` 对象存储在 `x` 变量中，然后连同 `greet` 操纵符的输出一起显示名字。

## 测试你的知识

- Q3. 编写一个程序，创建一个自定义操纵符，每次使用该操纵符时都显示 `$` 符号。

答案。

```cpp
#include<iostream.h>

ostream & dollar (ostream & output)
{
    return output <<"$ ";
}

void main()
{
    int amt;
    cout<<"Enter amount: ";
    cin>>amt;
    cout<<"You have entered "<<dollar<<amt;
}
```

**输出：**

```text
Enter amount: 1000
You have entered $ 1000
```

> 简要说明操纵符（孟买大学，2008 年 12 月）

现在，我们来看看如何使用条件语句在程序中检查条件。

## 2.2 使用条件语句

条件语句是一种控制语句，允许你在程序中的两条或多条执行路径之间进行选择。条件语句使程序在计算给定条件表达式后执行一个代码块。如果条件表达式结果为真，则执行相应的代码块；否则，跳过该代码块。以下是 C++ 支持的条件语句列表：

- if 语句
- if-else 语句
- 嵌套 if 语句
- if-else 阶梯
- switch 语句
- 嵌套 switch 语句

现在让我们详细讨论这些语句。

### 使用 if 语句

`if` 语句根据表达式为真还是为假来执行代码。只有当 `if` 语句中的表达式求值为真时，才会执行条件表达式后面的代码；否则，程序控制会传递到下一条语句。

以下是 `if` 语句的语法：

```cpp
if(conditional expression)
<Statements to be executed when conditional expression evaluated to true>;
```

当条件表达式返回假值时，程序控制会跳过当前语句（该语句本应在条件表达式返回真值时执行），转到下一条语句。清单 11 展示了一个使用 `if` 语句的示例（你可以在 CD 的 `code\chapter2` 文件夹中的 `ifStatement.cpp` 文件里找到这个示例）：

### 清单 11：使用 `if` 语句

```cpp
#include<iostream.h>

int main()
{
  int age;
    cout<<"Enter your age"<<endl;
    cin>>age;
  if(age<18)
    cout<<"You are not eligible to vote"<<endl;
  if(age>=18)
    cout<<"You are eligible to vote"<<endl;

  return 0;
}
```

### 输出 1：当提供的值小于 18 时

```text
Enter your age
17
You are not eligible to vote
```

### 输出 2：当提供的值大于或等于 18 时

```text
Enter your age
24
You are eligible to vote
```

在清单 11 中，运行时提供的值被设置到名为 `age` 的变量中。当条件表达式（`age<18`）求值为真时，会执行第一个 `if` 语句后面的语句（输出 1）。如果运行时提供的年龄大于或等于 18，则执行第二个 `if` 语句后面的语句（输出 2）。

### 使用 if-else 语句

使用 `if-else` 语句，如果条件为真，则执行一个代码块；如果条件为假，则执行另一个代码块。这意味着当条件为真时执行 `if` 子句，当条件为假时执行 `else` 子句。以下是 `if-else` 语句的语法：

```cpp
if (conditional expression)
//Statement1 to be executed in case conditional expression is true;

else
//Statement2 to be executed in case conditional expression is false;
```

在前面的语法中，当 `if` 语句后指定的条件为真时，执行语句 1；否则，执行语句 2。

清单 12 展示了使用 `if-else` 语句作为比使用多个 if 语句更好的替代方案（你可以在 CD 的 `code\chapter2` 文件夹中的 `if-elseStatement.cpp` 文件里找到这个示例）：

### ▶ 清单 12：使用 `if-else` 语句

```cpp
#include<iostream.h>
int main()
{
    int age;
    cout<<"Enter your age"<<endl;
    cin>>age;
    if(age<18)
        cout<<"You are not eligible to vote"<<endl;
    else
        cout<<"You are eligible to vote"<<endl;
    return 0;
}
```

### 输出 1：当提供的值小于 18 时

```text
Enter your age
17
You are not eligible to vote
```

### 输出 2：当提供的值大于或等于 18 时

```text
Enter your age
24
You are eligible to vote
```

在清单 12 中，运行时提供的值被设置到名为 age 的变量中。当条件表达式（age<18）求值为真时，执行 `if` 语句后面的语句。如果条件表达式（age<18）求值为假，则执行 `else` 子句后面的语句。
