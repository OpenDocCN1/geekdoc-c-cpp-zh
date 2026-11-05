
```csharp
Console.WriteLine("\n In Outer loop");
for (int cnt2 = 1; cnt2 <= 3; cnt2++)
{
    Console.WriteLine("\n In inner loop");
}
Console.ReadLine();
}
}
```

输入 nil

输出

```
In Outer loop
In inner loop
In inner loop
In inner loop
In Outer loop
In inner loop
In inner loop
In inner loop
In Outer loop
In inner loop
In inner loop
In inner loop
```

/*在上面的程序中，首先外层循环检查 cnt1=1 的条件，结果为 true，因此程序控制进入外层 for 循环，并打印消息 "In Outer loop"。现在它将进入内层 for 循环，内层循环执行 3 次，并打印消息 "In inner loop" 三次。然后控制再次回到外层 for 循环，再次打印消息 "In Outer loop"，并再次执行内层 for 循环 3 次。此过程将持续进行，直到外层 for 循环的条件变为 false。*/

## 4.4 跳转语句

### 概念

- 1. 跳转语句使用户能够有条件或无条件地跳转到代码的另一部分。

### 说明

- 2. 跳转语句主要用于分支，使程序控制立即转移到代码的另一部分。
- 3. 这些语句也用于需要在处理过程中中断任何循环或 switch-case 语句的地方。
- 4. C# 中有五种跳转语句，如下所示，
  - 1. **break**
  - 2. **continue**
  - 3. **goto**
  - 4. **return**
  - 5. **throw**
- 5. 本节将讨论 break、continue 和 goto 语句。return 语句将在 C# 方法部分讨论，throw 语句将在 C# 异常处理部分讨论。

### 4.4.1 break 语句

#### 概念

- 1. break 语句终止封闭的循环或 switch case 语句，程序控制跳转到紧跟在循环或 switch-case 语句之后的语句。

#### 说明

- 2. break 语句流程图

![](img/3005a4307e6d8f3bb7e76eea28a92357_142_0.png)

- 3. break 语句语法

```csharp
break;
```

#### 示例

```csharp
// Illustration of break statement in which a loop breaks after second iteration.
using System;
namespace CSharpJump
{
class breakStatement
{
static void Main()
{
int cnt;
for (cnt = 100; cnt <= 105; cnt++)
{
Console.WriteLine("" + cnt);
if (cnt == 102)
{
break;
}
}
Console.ReadLine();
}
}
}
```

输入 nil

输出

```
100
101
```

### 4.4.2 continue 语句

#### 概念

- 1. continue 语句强制程序控制直接转到条件，然后继续下一次迭代。

#### 说明

- 2. continue 语句停止当前迭代并开始下一次迭代。
- 3. continue 语句流程图

![](img/3005a4307e6d8f3bb7e76eea28a92357_144_0.png)

图 4.4.2 continue 语句

- 4. continue 语句语法

```csharp
continue;
```

#### 示例

```csharp
//illustration of continue statement which stops the third iteration and starts the fourth iteration.
using System;
namespace CSharpJump
{
class continuestatement
{
static void Main()
{
int cnt;
for (cnt = 1; cnt <= 5; cnt++)
{
if (cnt == 3)
{
continue;
}
Console.WriteLine("" + cnt);
}
Console.ReadLine();
}
}
}
```

输入 nil

输出

```
1
2
4
5
```

### 4.4.3 goto 语句

#### 概念

- 1. goto 语句用于跳转到由预定义标签指定的特定代码段。

#### 说明

- 2. goto 语句最常用于存在紧急情况且没有可退出循环的条件路径时。
- 3. 它广泛用于嵌套循环中。
- 4. goto 语句流程图

![](img/3005a4307e6d8f3bb7e76eea28a92357_145_0.png)

- 5. goto 语句语法

```csharp
goto label;
.........
.........
label:
..........
..........
```

#### 示例

```csharp
// Illustration of goto statement in which control is transferred to the 'stop' label in the fourth iteration of the loop
using System;
namespace CSharpJump
{
class gotostatement
{
    static void Main()
    {
        int cnt;
        for (cnt = 1; cnt <= 5; cnt++)
        {
            Console.WriteLine("" + cnt);
            if (cnt%4 == 0)
            {
                goto stop;
            }
        }

        stop:
        Console.WriteLine("Loop Stops");
        Console.ReadLine();
    }
}
}
```

输入 nil

输出

```
1
2
3
4

Loop Stops
```

## 4.5 其他语句

### 4.5.1 块语句

#### 概念

- 1. 块语句用于将逻辑相关的多个程序段组合在一起。

#### 说明

- 2. 块语句语法

```csharp
{
}
```

#### 示例

```csharp
//illustration of block statement
namespace CSharpStatements
{ //Begin Statement
    class BlockStatement
    { // Begin Statement
        static void Main(string[] args)
        { //Begin Statement
            int num, power;
            num = 5;
            power = num * num;
            Console.WriteLine(power);
            Console.ReadLine();
        } // End Statement
    } // End Statement
} // End Statement
```

输入 nil

输出

25

### 4.5.2 空语句

#### 概念

- 1. 空语句用于通常需要语句但无需执行操作的情况。

#### 说明

- 2. 它只是将控制转移到语句的终点。
- 3. 它便于用于具有空循环体和标签语句的 while 循环。
- 4. 空语句语法

```csharp
{
    ;
}
```

#### 示例

```csharp
//Illustration of empty statement
namespace CSharpStatements
{
    class EmptyStatement
    {
        public bool print()
        {
            Console.WriteLine("India");
            return false;
        }
        static void Main(string[] args)
        {
            int cnt = 0;
            EmptyStatement es = new EmptyStatement();
            while (es.print())
            {
                ;//Empty Statement
            }
            Console.WriteLine("cnt = {0}", cnt);
            Console.ReadLine();
        }
    }
}
```

输入 Nil

输出

```text
India
```

### 4.5.3 using 语句

#### 概念

- 1. using 语句用于在程序中添加一个或多个资源。

#### 说明

- 2. using 语句获取一个或多个资源，执行它们，然后释放对象或资源。
- 3. using 语句用于每个 C# 程序中，以添加所需的命名空间和类的内置集合。它广泛用于通过 C# 进行数据库连接。
- 4. using 语句语法

```csharp
using Mynamespace;
```

#### 示例

```csharp
using System;
using System.Text;

namespace CSharpStatements
{
class Use_using
{
    public void Display()
    {
        Console.WriteLine("Execute Two");
    }
}

class UsingStatement
{
    static void Main(string[] args)
    {
        using (Use_using c = new Use_using())
        {
            Console.WriteLine("Executes One");
            c.Display();
        }
        Console.WriteLine("Execute Three");
        Console.ReadLine();
    }
}
}
```

输入 nil

输出

```
Execute One
Execute Two
Execute Three
```

## 两分题及答案

Q.1 如果要在代码中替换多个 if-else 语句，你会使用哪个语句？

答：在 Visual Basic 中，我们可以使用 Select-Case 语句来替换多个 If-Else 语句。在 C# 中，我们应该使用 Switch-Case 语句来替换多个 If-Else 语句。

Q.2 在 C# 语言中实现多重选择的两种不同方式是什么？

答：if-else 和 switch 是在 C# 中实现多重选择的两种方式。

Q.3 给出以下程序的输出。

```c
#include <stdio.h>
int i;
int main()
{
    if(i);
    else
        printf("Else");
    return 0;
}
```

在上面的程序中，执行了 else 块。由于 i 是全局定义的，它被初始化为默认值 0。由于 if 中的表达式求值为 FALSE，因此执行 Else 块。请注意，空块等价于分号（;）。因此，语句 if (i); 和 if (i) {} 是等价的。

Q.4 在下面的程序中，'C# - is too sharp' 将被打印多少次？

```c
#include <stdio.h>

int main()
{
    int i = 1024;
    for (; i >= 1)
        printf("C# - is too sharp");
    return 0;
}
```

上面的程序将打印该语句 11 次。在 for 循环中，表达式是可选的。

