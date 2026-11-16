

else
cout<<"It should be obvious";
}

在这个程序中，输出将是 "It is strange, isn't it?"。这是因为每当 C++ 成功地将值赋给变量时，由于这是一次成功，所以默认为 true，因此 if() 语句内的条件为 true，所以在使用 (==) 和 (=) 时必须小心。

## Switch 语句

顾名思义，switch 语句用于在各种 case 之间切换。请参考以下程序

```
#include<iostream>
using namespace std;
int main()
{
    int num=5;
    switch (num)
    {
        case 1: cout<<"1";
        case 5: cout<<"5";
        case 6: cout<<"6";
        case 7: cout<<"7";
            break;
        case 8: cout<<"8";
        default:
            cout<<"None of the cases matches";
    }
}
```

在上述程序中，switch 语句将变量 num 与每个 case 进行比较，由于 num 与 5 匹配，因此将执行相应 case 中的语句；此外，没有任何东西能阻止它继续执行后续 case，直到遇到 break 语句或退出。所以，输出将是 567

**默认** 也是一个关键字，当没有任何 case 匹配时，相应的语句会自动执行。引入 **默认** 关键字是可选的。

![](img/5340985153962870d4e4a3b9453b9146_64_0.png)

## 循环

循环是一种反复执行任务的方法，不一定是有限次数。
在 C 中使用以下循环

- 1. for 循环
- 2. while 循环
- 3. do...while 循环

除了这三种之外，跳转语句 goto 也在 C 中用作循环。

## for 循环

这是最流行的循环。请参考以下程序：

```
#include<iostream>
using namespace std;
int main()
{
    int i=5;
    for(i=7;i<10;i++)
    cout<<i;
}
```

上述程序将打印 789，这意味着 for 循环中的第一条语句是初始化，
第二条语句是条件。for 循环下的语句块将
一直执行，直到该条件为 true。一旦该条件变为 false，控制权
就会退出循环。第三条语句在 for 循环内每条语句执行后执行。
关于第三条语句的一个惊人事实是，每次它
都在第二条语句之前执行。否则，结果本应是 78910

请参考以下程序

```
#include<iostream>
using namespace std;
int main()
{
    int i=5;
    for(i=11;i<10;i++)
    cout<<i;
}
```

该程序将不打印任何内容，因为第一条语句总是首先执行，然后在进入循环内的语句之前，会检查条件。所以，条件为 false，因此不会打印任何内容。

其他有效的 for 循环格式包括

```
for(i=0,j=5;i<5&&j>3;i++,j=j-5)
{
/*Statements*/
}
```

请仔细观察，我们不能在第二条语句中使用多于一条语句，如果想要这样做，则必须用逻辑运算符将它们连接起来。

请参考以下程序：

```
#include<iostream>
using namespace std;
int main()
{
     int i=5;
     for(i=1;i<10&&i=11;i++)
     cout<<i;
}
```

在这里，我们使用了逻辑运算符，但编译器会将其读作 (i<10&&i)=11，这是一个错误的表达式。因此，它会生成一个错误："value required as left operand of assignment"

现在请参考以下程序

```
#include<iostream>
using namespace std;
int main()
{
     int i=5;
     for(i=5;i<10&&(i=11);i++)
     cout<<i;
}
```

猜猜它的输出。嗯，它的输出将是 11，令人惊叹，不是吗？我已经说过，它会先执行 for 循环内的第一个赋值，即 i=5。现在，它会检查条件，即 i<10&&(i=11)，在这两个条件不可能同时为真，所以它必须是 false。你错了；这是现代计算机能力的一个演示。我们的计算机是多任务的，这并不意味着它们在程序中同时执行多个任务；相反，它们在任务之间跳转得太快，以至于我们无法察觉。但后果体现在结果上。这里，首先 i 与 10 进行比较，语句 i<10 变为 true，因为 i 最初是 5。现在，11 被赋值给 i，这是一个真语句，因为它是一个赋值。因此，两个语句都为真。所以，for 循环后面的语句 cout<<i; 被执行。但是，现在由于 i 中的值是 11，所以显示 11。现在，i 的值增加，其值变为 12，现在语句 i=11 被执行，然后 i<10 变为 false。所以，程序退出。

这将从以下程序中变得更加清晰和有趣：

```
#include<iostream>
using namespace std;
int main()
{
    int i=5;
    for(i=1;i<10&&(i=3);i++)
    cout<<i;
}
```

猜猜它的输出，嗯，它的输出将是：

![](img/5340985153962870d4e4a3b9453b9146_68_0.png)

即一个无限循环。所以，现在你已经理解了，最初先执行第一个赋值，在条件语句中，首先执行第一个语句，然后执行第二个语句，然后比较两个语句的结果。如果最终结果为 true，则执行 for 循环内的语句块。然后执行 for 循环的第三条语句 i++。然后，程序掉头，不执行条件的第一个语句，而是执行条件的第二个语句 i=3，现在执行条件的第一个语句 i<10，这显然是 true。所以，现在再次执行 for 循环内的语句块 cout<<i;，这个过程开始重复，而不是使用 i=1; i<10 和 i++ 和 && 运算符，循环无限运行。

## while 循环

当我们想要在执行循环中的第一条语句之前测试条件时，使用 while 循环。

请参考以下程序

```
#include<iostream>
using namespace std;
int main()
{
    int i=1;
    while(i<5)
    {
    cout<<i;
    i++;
    }
}
```

该程序的输出将是 1234

## do...while 循环

此循环的突出之处在于，在测试第一个 case 之前以及在每次下一次执行之前测试条件，都会先执行第一条语句。请参考以下程序。

```
#include<iostream>
using namespace std;
int main()
{
int i=1;
do
{
cout<<i;
i++;
}while(i>5);
}
```

其输出将是 1。还要注意，do...while 循环后面必须紧跟一个分号，否则会显示编译错误“Expected ‘;’ before ‘}’ token”

## goto 关键字

goto 是一个关键字，用于从程序的一部分突然跳转到另一部分。请参考以下程序：

```
#include<iostream>
using namespace std;
int main()
{
int i=5;
start:
cout<<i;
i++;
goto start;
}
```

在这个程序中，start 是一个标签，我们希望光标跳转到那里。标签名称后需要一个冒号。每当我们想要跳转到任何标签时，只需使用语法 goto label_name; 所以，这个程序会无限次地跳转到 start，这是一个无限过程。所以，你将看到如下输出

![](img/5340985153962870d4e4a3b9453b9146_70_0.png)

请记住，goto 不是循环，它只是一个跳转器。所以，我们不能在 start...goto start; 内部使用 break 和 continue。

## Break 和 Continue

这两个关键字用于有效地控制循环。Break 用于跳出最内层循环，而 continue 用于跳转到循环顶部。

请参考以下程序

```
#include<iostream>
using namespace std;
int main()
{
int i,j;
for(i=1;i<3;i++)
{
for(j=6;j<9;j++)
{
cout<<"j";
if(j==7)
break;
}
cout<<"i";
}
return 0;
}
```

上述程序的输出将是 jijii。因为首先 i 初始化为 1，j 初始化为 6。现在，j 将被打印。现在 j 的值增加到 7，再次打印 j。但现在 j 是 7，所以 break 语句将被执行，控制权跳出最内层 for 循环，并执行 cout<<"i";。现在 i 的值将被递增。然后，内层 for 循环再次执行。这个过程将持续到语句 i<3 变为 false。

请参考以下程序

```
#include<iostream>
using namespace std;
int main()
{
int i;
for(i=1;i<3;i++)
{
cout<<i;
continue;
cout<<"i";
}

