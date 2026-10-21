

- switch 语句计算表达式然后在 case 常量中查找其值。
- 如果值与 case 常量匹配，则执行该特定 case 语句。如果不匹配，则执行 default。
- Switch、case 和 default 是保留关键字。
- switch() 中使用的 break 语句将控制权传递到 switch() 块之外。错误地，如果没有给出 break 语句，则其后的所有 case 都会被执行。

```
/*PROG 3.35 DEMO OF SWITCH-CASE VER 1*/

#include<iostream.h>
void main()
{
int num;
cout<<"Enter 0,1,or 2\n";
cin>>num;
switch(num)
{
case 0 :
    cout<<"U entered zero\n";
    break;
case 1 :
    cout<<"U entered one\n";
    break;
case 2 :
    cout<<" U entered two\n";
    break;
default :
    cout<<"other than 0,1,or 2\n";
}
}
OUTPUT :
Enter 0,1,or 2
1
U entered one
```

![](img/ad5299318df8d4d7c6df5eaa86590ea3_108_0.png)

Figure 3.36. Output screen of program.

**EXPLANATION :**

要检查的条件放在 switch 内部，用括号括起来。不同要检查的值使用 case 语句给出。在第一个 case 中，值被检查为 0。这类似于写 if (num == 0)。case 值后的冒号 (:) 将其与要执行的语句分开。同样，如果 num 的值为零，则第一个 case 匹配，并且该 case 下的所有语句都会被执行。同样，如果 num 的值为 1，则执行第二个 case，其余 case 语句也适用。需要 break 语句来忽略其余的 case 语句，并在找到匹配项时退出 switch 块。如果没有任何 case 匹配，则执行 default。编写 default 是可选的。

```
/*PROG 3.36 DEMO OF SWITCH-CASE VER 2*/

#include<iostream.h>
void main()
{
int num;
cout<<"Enter 0,1 or 2\n";
cin>>num;
switch(num)
{
case 0 : cout<<"U entered zero\n";
break;
case 1 : cout<<"U entered one \n";
case 2 : cout<<"U entered two\n";
break;
default :cout<<"Other than 0,1,or2\n";
}
}
OUTPUT :
Enter 0,1 or 2
2
U entered two
```

![](img/ad5299318df8d4d7c6df5eaa86590ea3_109_0.png)

**EXPLANATION :**

case 1 中没有 break 语句，因此 case 2 也会被执行。事实上，由于第一个 case 缺少 break 语句，其余语句被视为第一个 case 的一部分，直到找到 break 为止。case 2 中的 break 导致控制退出 switch。如果 case 2 中也没有 break，则 default 也会被执行。

```
/*PROG 3.37 TO CHECK GIVEN CHARACTER IS VOWEL OR NOT USING SWITCH CASE VER 3*/

#include <iostream.h>
#include <ctype.h>
void main()
{
char ch;
cout<<"Enter any character \n";
cin>>ch;
ch=tolower(ch);
switch(ch)
{
default :
    cout<<"Not a vowel\n";
    break;
case 'a' :
case 'e' :
case 'i' :
case 'o' :
case 'u' :
    cout<<"It's a vowel\n";
}
}
OUTPUT :
Enter any character
e
It's a vowel
```

![](img/ad5299318df8d4d7c6df5eaa86590ea3_110_0.png)

Figure 3.38. Output screen of program.

**EXPLANATION :**

我们使用了内置函数 tolower 将字符从大写转换为小写。这随后存储回 ch。需要包含头文件 ctype.h。现在无论你输入元音是大写还是小写，它都会以小写形式传递到 switch 块并检查是否属于五个元音之一。

## 3.6 UNCONDITIONAL BRANCHING USING GOTO

goto 语句用于将程序的控制从一个点转移到另一个点。事实上，它使程序控制跳转到标签指定的语句。这种使用 **goto** 的 **无条件转移控制称为分支。** 标签必须在 **goto** 使用的同一函数中。一般的 goto 语句语法如下：

```
goto label;
```

我们通过一个程序来理解 **goto** 的使用。

```
/*PROG 3.38 DEMO OF GOTO VER 1*/

#include <iostream.h>
#include <math.h>
void main()
{
int x;
start :
cout << "Enter a +ve number\n";
cin >> x;
if(x < 0)
goto start;
cout << "sqrt of number is" << sqrt(x) << endl;
}
OUTPUT :
Enter a +ve number
-30
Enter a +ve number
40
sqrt of number is 6.32456
```

![](img/ad5299318df8d4d7c6df5eaa86590ea3_111_0.png)

Figure 3.39. Output screen of program.

**EXPLANATION :**

start: 被称为标签。start 是标签名，后面必须跟冒号 (:)。任何有效的标识符名都可以作为标签名。当输入 -ve 数字时，如果条件返回 true，控制会使用 goto start; 语句转回 start。在程序中跳转是向后的；这里控制被转移到 goto start; 语句之前的语句，因此它是向后跳转。如果它在 goto start; 语句之后，则将是向前跳转。

```
/*PROG 3.39 LOOP CREATION USING GOTO STATEMENT*/

#include <iostream.h>
void main()
{
    int n=0;
    cout<<"Loop starts\n";
    loop :
        n++;
        cout<<"n="<<n<<endl;
        if(n<5)
            goto loop;
    cout<<"Loop Ends\n";
}
OUTPUT :
Loop starts
n=1
n=2
n=3
n=4
n=5
Loop Ends
```

![](img/ad5299318df8d4d7c6df5eaa86590ea3_112_0.png)

Figure 3.40. Output screen of program.

**EXPLANATION :**

n 的初始值为 0。它在标签 loop 处递增然后打印。使用 if 检查 n 的值是否小于 5。如果 n<5，则控制转移回 loop 标签，即同一组语句会重复执行有限次数（这里次数为 5）。这就是循环，我们使用 goto 和 if 实现的。

## 3.7 INTRODUCTION TO LOOPING

循环是一个过程，其中一组语句会重复执行有限或无限次数。C 提供了三种执行循环的方式，提供三种不同类型的循环。循环可以同义地称为迭代或重复。循环是几乎所有编程语言如 C、C++、Java、VB、C#、Delphi 等中最重要的一部分。

在我们的实际生活中，我们看到很多需要执行重复任务的例子，比如查找班级学生成绩的平均分、查找一组员工的最大薪水、计数数字等。

循环是一块语句，只要满足特定条件就会一遍又一遍地执行。C 提供了三种循环来执行重复操作：

- 1. while
- 2. for
- 3. do-while

要使用任何类型的循环，必须执行三件事：

- 循环控制变量及其初始化。
- 控制循环的条件。
- 控制变量的递增/递减。

### 3.7.1 The While Loop

while 循环的语法很简单：

```
while (condition)
{
    Statements;
    Statements;
    ....................;
}
```

{ } 内的语句称为 while 循环的主体。如果没有大括号，则 while 之后的第一条语句被视为 while 循环的主体。主体内的所有语句都会重复执行，直到 while 中括号内指定的条件满足为止。一旦条件变为 false，主体将被跳过，控制转移到循环外的下一条语句。while 后面不应有分号。我们将看到如果这样做会发生什么。

```
/*PROG 3.40 DEMO OF WHILE LOOP (PRINTING NUMBER 1 TO 10) VER 1*/
#include <iostream.h>
void main( )
{
    int t = 1;
    while(t <= 10)
    {
        cout << "t= " << t << endl;
        t++;
    }
}
OUTPUT :
t = 1
t = 2
t = 3
t = 4
t = 5
t = 6
t = 7
t = 8
t = 9
t = 10
```

![](img/ad5299318df8d4d7c6df5eaa86590ea3_114_0.png)

**Figure 3.41.** *Output screen of program.*

**EXPLANATION :**

在 **while** 循环中，我们声明了条件 **t <= 10**。**t** 被称为循环控制变量。最初 **t 的值为 1**。该 **t** 值与 10 比较，为真，因此控制进入 while 循环，循环内的 cout 语句执行，打印 **t** 的值。然后 **t** 增加 **1**，*即* 变为 **2**。控制回到 while 循环的条件，为真。此过程继续。当 **t** 的值变为 **11** 时，while 循环中的条件变为 false，控制退出循环。由于循环外没有语句，程序终止。

```
/*PROG 3.41 MAXIMUM OF N ELEMENTS */

#include <iostream.h>
void main()
{
    int n,max,t=1,m;
    cout << "Enter how many numbers\n";
    cin >> n;
    cout << "Enter the number\n";
    cin >> m;
    max = m;
    while(t <= n-1)
    {
        cout << "Enter the number\n";
        cin >> m;
        if(max < m)
            max = m;
        t++;
    }
    cout << "Maximum element is" << max << endl;
}
OUTPUT :
Enter how many numbers
3
Enter the number
10
Enter the number
20
Enter the number
30
Maximum element is 30
```

