
```text
Output:
    Authors
1.  William Shakespeare
2.  William Stallings
3.  Chetan Bhagat

Select an Author:
1

    Books by William Shakespeare
1.  Romeo and Juliet
2.  The Merchant of Venice
3.  The Comedy of Errors

Enter your choice:
2
You have selected The Merchant of Venice by William Shakespeare
```

在清单 17 中，你可以看到程序首先提示你选择作者，并根据 switch 语句的分支情况显示书籍列表。然后程序提示你从列表中选择一本书。

理解条件语句之后，让我们继续讨论各种迭代语句。

## 2.3 使用迭代语句

迭代语句或循环会根据条件反复执行一段代码，只要该条件求值为 true。一旦条件表达式的求值为 false，循环就会退出。之后，控制权转移到循环后面的下一条语句。以下是 C++ 支持的迭代语句：

- while 循环
- do-while 循环
- for 循环

现在让我们详细讨论这些语句中的每一个。

### 使用 while 循环

只要 while 循环中的条件求值为 true，while 循环就会执行语句。一旦条件变为 false，循环就会终止。以下是 while 循环的语法：

```cpp
while (conditional_expression)
{
    Statements to be executed;
}
```

在前面的语法中，首先测试 `conditional_expression`。如果 `conditional_expression` 为 true，则执行 `while` 循环体内的语句。这些语句会反复执行，直到 `conditional_expression` 为 true。每当 `conditional_expression` 求值为 false 时，循环就会终止。清单 18 展示了 `while` 循环的用法（你可以在光盘的 `code\chapter2` 文件夹中的 `whileloop.cpp` 文件中找到此示例）：

**▶ 清单 18：使用 `while` 循环**

```cpp
#include<iostream.h>

int main()
{
    int value,factorial,temp;
    factorial=1;
    cout<<"Enter a number"<<endl;
    cin>>value;
    temp=value;

    while(temp>0)
    {
        factorial*=temp--;
    }
    cout<<value<<"!="<<factorial<<endl;
    return 0;
}
```

**输出：**

```text
Enter a number
4
4!=24
```

在清单 18 中，`while` 循环内的语句会一直执行，直到存储在 `temp` 变量中的值变为零。当存储在 `temp` 变量中的值变为零时，`while` 循环退出并显示数字（4）的阶乘。

`while` 循环也可以不使用花括号来编写。不带花括号的 `while` 循环只能执行紧跟在循环后面的语句。要执行多条语句，`while` 循环中需要使用花括号。清单 19 展示了简单的 `while` 循环（你可以在光盘的 `code\chapter2` 文件夹中的 `whileloop2.cpp` 文件中找到此示例）：

**▶ 清单 19：使用不带花括号的 `while` 循环**

```cpp
#include<iostream.h>

void main()
{
    int num=10;

    while (num>=0)
        cout<<num--<<endl;
}
```

**输出：**

```text
10
9
8
7
6
5
4
3
2
1
0
```

在清单 19 中，你可以看到 while 循环执行紧跟在循环后面的语句，并显示存储在 num 变量中的值。while 循环会一直执行，直到存储在 num 变量中的值变为零。

### 测试你的知识

**Q5.** 编写一个程序，要求用户输入一个整数，然后打印出它的所有因子。

**答案。**

```cpp
//Program to factorize a given number

#include<iostream.h>
void main()
{
    int No,i,d;
    cout<<"\nGive the required number:-";
    cin>>No;
    d=No;
    i=1;
    while((d>0)&&(i<=No))
    {
        i++;
        if(d%i==0)
        {
            cout<<"\n";
            d/=i;
            i=1;
        }
    }
}
```

**输出：**

```text
Give the required number:-9999

3
3
11
101
```

### 创建嵌套 while 循环

嵌套 while 循环是指在一个 while 循环的循环体中包含另一个 while 循环。清单 20 展示了嵌套 while 循环（你可以在光盘的 `code\chapter2` 文件夹中的 `whileloop3.cpp` 文件中找到此示例）：

**清单 20：创建嵌套 while 循环**

```cpp
#include<iostream.h>

void main()
{
    int num1=1, num2, num3;
    cout<< "Enter a number from 1 to 10: ";
    cin>>num3;
    while(num1<=num3)
    {
        num2 = 1;
        while (num2<=num1)
        {
            cout<<num2<<"\t";
            num2++;
        }
        cout<<"\n";
        num1++;
    }
}
```

**输出：**

```text
Enter a number from 1 to 10: 6
1
1  2
1  2  3
1  2  3  4
1  2  3  4  5
1  2  3  4  5  6
```

在清单 20 中，你可以看到外层 while 循环跟踪输入的数字，内层 while 循环显示存储在 `num2` 变量中的数字。

### 使用 do-while 循环

只要指定的条件为 true，`do-while` 循环就会执行一组语句。如果条件变为 false，执行流程就会退出 `do-while` 循环。如你所知，`while` 循环用于先检查条件，然后执行循环体。`do-while` 循环用于先执行循环体，然后检查条件。以下是 `do-while` 循环的语法：

```cpp
do
{
    statements;
} while(conditional_expression);
```

在前面的语法中，`statements` 语句后面是 `while` 关键字和一个要求值布尔值的条件表达式。如果求值返回 true，控制权会回到 `do` 关键字，并继续执行，直到求值变为 false。清单 21 展示了 `do-while` 循环的用法（你可以在光盘的 `code\chapter2` 文件夹中的 `do-whileloop.cpp` 文件中找到此示例）：

**▶ 清单 21：使用 do-while 循环**

```cpp
#include<iostream.h>

int main()
{
    int num;
    do{
        cout<<"Enter a number"<<endl;
        cin>>num;
    }
    while(num%2!=0);
    cout<<"It is an even number"<<endl;
    return 0;
}
```

**输出：**

```text
Enter a number
3
Enter a number
5
Enter a number
4
It is an even number
```

在清单 21 中，程序提示你输入一个数字，该数字会存储在 `num` 变量中。程序会判断存储在变量中的值是否为偶数。如果求值返回 true，控制权会回到 `do` 关键字，并继续执行 do-while 循环，直到求值变为 false。

`do-while` 循环也可以不使用花括号来编写。不带花括号的简单 `do-while` 循环只能执行紧跟在循环后面的语句。要执行多条语句，`while` 循环中需要使用花括号。清单 22 展示了简单的 `do-while` 循环（你可以在光盘的 `code\chapter2` 文件夹中的 `do-whileloop2.cpp` 文件中找到此示例）：

**▶ 清单 22：使用不带花括号的 `do-while` 循环**

```cpp
#include<iostream.h>

int main()
{
    int num=0;
    do
        cout<<num++<<endl;
    while(num<=10);
    return 0;
}
```

**输出：**

```text
0
1
2
3
4
5
6
7
8
9
10
```

在清单 22 中，程序显示 `num` 变量的值，并递增该变量的值，直到 `do-while` 循环的条件求值为 false。如果求值返回 true，控制权会回到 `do` 关键字，并继续执行 `do-while` 循环体，直到条件满足。

### 测试你的知识

**Q6.** 将下面的“do”循环改写为“while”循环。

```cpp
int n=1;
float x=0;
float s;
do
{
  s=1.0/(n*n);
  x=x+s;
  n++;
}
while(s>0.01);
```

**答案。** 为将“do”循环转换为“while”循环，进行了以下更改：

```cpp
int n=1;
float x=0;
float s=1.0;
while(s>0.01)
{
  s=1.0/(n*n);
  x=x+s;
  n++;
}
```

### 使用 for 循环

for 循环会迭代固定次数，由三个部分组成，例如初始化、条件表达式和后置表达式。以下是 for 循环的语法：

```cpp
for(initialization;conditional_expression;post_expression)
```

在前面的语法中，初始化会用值初始化变量。初始化部分只发生一次，其后是条件表达式。如果条件表达式的求值为 false，则执行 for 循环后面的语句。如果 `conditional_expression` 的求值为 true，则执行 for 循环的循环体。`post_expression` 用于递增或递减控制循环的计数器变量。for 循环会一直执行，直到 `conditional_expression` 求值为 false。清单 23 展示了 for 循环的用法（你可以在光盘的 `code\chapter2` 文件夹中的 `forloop.cpp` 文件中找到此示例）：

**▶ 清单 23：使用 for 循环**

```cpp
#include<iostream.h>
```
