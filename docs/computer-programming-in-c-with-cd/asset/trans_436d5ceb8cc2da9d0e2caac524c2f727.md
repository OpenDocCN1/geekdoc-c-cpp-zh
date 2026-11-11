
## 测试你的知识

- Q4. 编写一个程序，读取两个浮点数，并检验它们保留两位小数后是否相同。

答案。

```cpp
#include<iostream.h>
#include<string.h>
#include<math.h>

void main()
{
    float a,b;
    long int c,d;
    cout<<"\nGive two numbers:-";
    cin>>a>>b;
    c=100*a;d=100*b;
    if(c==d)
    cout<<"\nThe numbers "<<a<<" and "<<b<<" are equal to two places.";
    else
    cout<<"\nThe numbers "<<a<<" and "<<b<<" are not equal to two places.";
}
```

**输出：**

```text
Give two numbers:-12.34
15.34

The numbers 12.34 and 15.34 are not equal to two places.
```

## 创建嵌套 if 语句

当 if 语句中包含其他 if 语句时，就称这些 if 语句是嵌套的。当外层 if 语句求值为真时，程序的控制权进入内层 if 语句。以下是创建嵌套 if 语句的语法：

```cpp
if(conditional expression1)
{
    // Statement1 to be executed in case the conditional expression1 is true;
    if(conditional expression2)
    {
        // Statement2 to be executed in case the conditional expression2 is true;
    }
}
```

在前面的语法中，首先测试条件表达式1，如果其求值为真，则执行语句1，程序控制权传递给内层 if 语句。如果内层 if 语句的条件表达式2为真，则执行语句2。清单13展示了如何创建嵌套 if 语句（你可以在 CD 的 code\chapter2 文件夹中的 ifStatement2.cpp 文件里找到此示例）：

### 清单13：创建嵌套 if 语句

```cpp
#include<iostream.h>

int main()
{
    double num;
    cout<<"Enter a number"<<endl;
    cin>>num;
    if(num!=0)
    {
        if(num>0)
            cout<<"The result="<<(1/num)<<endl;
        else
            cout<<"The result="<<(-1/num)<<endl;
    }

    return 0;
}
```

**输出：**

```text
Enter a number
3
The result=0.333333
```

在清单13中，外层 if 语句判断运行时提供的值是否等于零。如果运行时提供的值不为零，则外层 if 语句求值为真，程序控制权转到内层 if 语句。然后内层 if 语句进一步判断该数字是否大于零。如果该数字大于零，则显示用1除以该数字的结果。然而，如果该数字小于零，则控制权转到 else 子句，并在控制台屏幕上显示用-1除以该数字的结果。

你也可以在 if 语句中定义多条语句。清单14展示了如何在 if 语句中定义多条语句（你可以在 CD 的 code\chapter2 文件夹中的 ifStatement3.cpp 文件里找到此示例）：

### 清单14：在 `if` 语句中显示多条语句

```cpp
#include<iostream.h>
void main()
{
    int num;
    cout<<"Enter number: ";
    cin>>num;
    if(num<50)
    {
        int less=50-num;
        cout<<"The number is less than 50"<<endl;
        cout<<"You have to increase the number by " <<less<< " to make it 50";
    }
}
```

**输出：**

```text
Enter number: 40
The number is less than 50
You have to increase the number by 10 to make it 50
```

在清单14中，程序提示你输入一个数字。if 语句验证条件表达式。如果条件为真，则执行花括号内的语句。

如果不使用花括号，并且 if 条件为真，那么 C++ 编译器将只执行紧跟在 if 语句之后的下一条语句。

## 使用 if-else 阶梯

一连串 `if-else` 语句一个接一个地出现，称为 `if-else` 阶梯。清单15演示了 `if-else` 阶梯如何工作（你可以在 CD 的 code\chapter2 文件夹中的 `if-elseStatement2.cpp` 文件里找到此示例）：

### 清单15：使用 `if-else` 阶梯

```cpp
#include<iostream.h>
int main()
{
    char alphbt;
    cout<<"Enter an alphabet"<<endl;
    cin>>alphbt;
    if(alphbt=='a')
        cout<<"It is a vowel"<<endl;
    else if(alphbt=='e')
        cout<<"It is a vowel"<<endl;
    else if(alphbt=='i')
        cout<<"It is a vowel"<<endl;
    else if(alphbt=='o')
        cout<<"It is a vowel"<<endl;
    else if(alphbt=='u')
        cout<<"It is a vowel"<<endl;
    else
        cout<<"It is not a vowel"<<endl;
    return 0;
}
```

**输出：**

```text
Enter an alphabet
e
It is a vowel
```

在清单15中，可以看到运行时提供的字符会在多个 `if-else` 语句中依次测试，直到找到匹配项。

使用 `if-else` 阶梯创建的程序难以阅读和维护，因为程序变得更复杂、更难理解。C++ 提供了 switch 语句来克服这些困难和理解程序时的复杂性，接下来将讨论这一点。

## 使用 switch 语句

`switch` 语句是一种条件语句，它将一个值与不同的值进行测试。如果值匹配，则执行相应的一组语句。switch 语句以 `switch` 关键字开头，后面括号 () 中是一个值表达式。它由多个 case 标签组合而成，这些 case 标签必须用 `break` 语句分隔。每个 case 标签都包含一个常量值，该常量值与 `switch` 表达式中指定的值进行匹配。如果值匹配，则执行该 case 标签的语句。此外，你还可以指定 `default` 标签，当 `switch` 表达式中指定的值与给定的 case 标签都不匹配时，将执行该标签。使用 switch 语句的语法是：

```cpp
switch(expression)
{
    case value1: statement1;
    break;
    case value2: statement2;
    break;
    case value3: statement3;
    break;
    .
    .
    .
    default: default_statement;
}
```

**输出：**

```text
Enter an alphabet
i
It is a vowel
```

在清单16中，你在运行时提供的值存储在 `alphabet` 变量中。该变量用作 switch 子句的参数，并与 case 标签中的各种常量进行比较。如果某个 case 标签的常量等于 switch 语句中表达式的值，则执行该 case 标签后面的语句。在清单16中，执行了 case `'i'`。如果没有任何 case 标签与 switch 表达式中存储的值匹配，则执行 default 标签。

## 创建嵌套 switch 语句

switch 语句也可以嵌套。这意味着与 if 语句一样，switch 语句也可以定义在其他 switch 语句中。清单17展示了嵌套 switch 语句的示例（你可以在 CD 的 code\chapter2 文件夹中的 `switchStatement2.cpp` 文件里找到此示例）：

### 清单17：嵌套 switch 语句

```cpp
#include<iostream.h>

void main()
{
    int author, book;
    cout<<"\t Authors\n";
    cout<<"1. William Shakespeare\n";
    cout<<"2. William Stallings\n";
    cout<<"3. Chetan Bhagat\n\n";

    cout<<"Select an Author: \n";
    cin>>author;
    switch(author)
    {
    case 1:cout<<"\tBooks by William Shakespeare\n\n";
        cout<<"1. Romeo and Juliet\n";
        cout<<"2. The Merchant of Venice\n";
        cout<<"3. The Comedy of Errors\n\n";

        cout<<"Enter your choice: \n";
        cin>>book;
        switch(book)
        {
            case 1: cout<<"You have selected Romeo and Juliet by William Shakespeare\n";
            break;
            case 2: cout<<"You have selected The Merchant of Venice by William Shakespeare\n";
            break;
            case 3: cout<<"You have selected The Comedy of Errors by William Shakespeare\n";
            break;
            default:cout<<"Wrong choice\n";
            break;
        }
        break;
    case 2 : cout<<"\tBooks by William Stallings\n\n";
        cout<<"1. Business Data Communication\n";
        cout<<"2. Wireless Communications and Networks\n";
        cout<<"3. High Speed Networks and Internets\n\n";

        cout<<"Enter your choice: \n";
        cin>>book;
        switch(book)
        {
            case 1: cout<<"You have selected Business Data Communication by William Stallings\n";
            break;
            case 2: cout<<"You have selected Wireless Communications and Networks by William Stallings\n";
            break;
            case 3: cout<<"You have selected High Speed Networks and Internets by William Stallings\n";
            break;
            default:cout<<"wrong choice";
            break;
        }
        break;
    case 3:cout<<"\tBooks by Chetan Bhagat\n\n";
        cout<<"1. One Night @ Call Center\n";
        cout<<"2. The 3 Mistakes of My Life\n";
        cout<<"3. Five Point Something\n\n";
        cout<<"Enter your choice: \n";
        cin>>book;
        switch(book)
        {
            case 1: cout<<"You have selected One Night @ Call Center by Chetan Bhagat\n";
            break;
            case 2: cout<<"You have selected The 3 Mistakes of My Life by Chetan Bhagat\n";
            break;
            case 3: cout<<"You have selected Five Point Something by Chetan Bhagat\n";
            break;
            default:cout<<"wrong choice\n";
            break;
        }
    default:cout<<"wrong choice\n";
        break;
    }
}
```
