
## ... 继续

4. 现在，插入语句请求用户输入并将其分配给变量。

   ```c
   printf("Enter the diameter of a circle in millimeters: ");
   scanf("%f", &diameter);
   ```

5. 接下来，添加语句使用常量值和用户输入计算其他三个变量的值。

   ```c
   circ = PI * diameter;
   radius = diameter / 2;
   area = PI * (radius * radius);
   ```

![](img/d1dfb0563339ba187decb78799155b7f_42_0.png)

这里 `*` 星号字符是算术乘法运算符，而 `/` 正斜杠字符是除法运算符。算术运算符将在下一章中完整演示。

6. 现在，插入语句以两位小数格式输出计算得到的值。

   ```c
   printf("\n\tCircumference is %.2f mm", circ);
   printf("\n\tAnd the area is %.2f sq.mm\n", area);
   ```

7. 在 main 函数块的末尾，返回零整数值，如函数声明所要求。

   ```c
   return 0;
   ```

8. 保存程序文件，然后编译并执行程序，在需要时输入数据，以查看计算结果。

![](img/d1dfb0563339ba187decb78799155b7f_42_1.png)

![](img/d1dfb0563339ba187decb78799155b7f_42_2.png)

![](img/d1dfb0563339ba187decb78799155b7f_42_3.png)

![](img/d1dfb0563339ba187decb78799155b7f_42_4.png)

请记住，在 scanf() 中，`&` 取地址运算符必须置于变量名前，以便将输入分配给该变量。

## 枚举常量值

enum 关键字提供了一种简洁的方式来创建整数常量的序列。可选地，声明可以在 enum 关键字之后包含序列的名称。常量名称作为逗号分隔的列表放在大括号内。

默认情况下，每个常量的值都比列表中在其前面的常量大一。除非指定，否则第一个常量的值为零；下一个值为 1；以此类推。

例如，可以使用 `enum {MON,TUE,WED,THU,FRI};` 为命名的星期常量指定从零开始的整数值序列——在这种情况下，常量 WED 的整数值为 2。

常量可以在声明中被赋予任意单个整数值，但列表中的下一个常量将始终使前一个值递增一，除非它也被赋予了值。例如，要使序列从 1 而不是零开始，将 1 分配给第一个常量，使用 `enum {MON=1,TUE,WED,THU,FRI};` ——在这种情况下，常量 WED 的整数值为 3。

枚举常量的列表也称为“枚举集合”，可能包含重复的常量值。例如，值零可以分配给名为 NIL 和 NONE 的常量。

在下面的示例中，枚举集合表示斯诺克游戏中球的分数值，并包含一个可选名称，该名称以大写形式出现，因为它也是常量。

![](img/d1dfb0563339ba187decb78799155b7f_43_0.png)

1. 使用预处理器指令开始一个新程序，以包含标准输入/输出库函数

   `#include <stdio.h>`

2. 添加一个 main 函数，该函数声明并初始化从 1 开始的枚举常量集合

   ```c
   int main()
   {
     enum SNOOKER
     { RED=1,YELLOW, GREEN, BROWN, BLUE, PINK, BLACK };
   }
   ```

3. 接下来，在 main 函数块中，声明一个整数变量来存储某些常量值的总和

   `int total ;`

## 创建常量类型

一旦枚举序列被声明，它就可以被视为一种新的数据类型，具有其指定的常量名称及其相关值的属性。

这种 **enum** 数据类型的变量可以像声明其他数据类型的变量一样声明——使用以下语法：

```c
data-type variable-name ;
```

第 42-43 页的示例创建了一个名为 **SNOOKER** 的枚举序列，可视为 **enum SNOOKER** 的数据类型。因此，可以使用声明 **enum SNOOKER pair ;** 创建该数据类型的名为“pair”的变量，并且可以存储该类型定义的枚举集合的值。

要显式地将整数值分配给枚举数据类型的变量，C 标准建议使用强制转换将 **int** 数据类型转换为 **enum** 数据类型，如下所示：

```c
pair = ( enum SNOOKER ) 7 ;
```

然而在实践中这并非必需，因为枚举值始终是整数，因此等同于 **int** 数据类型。

**enum** 声明可选择性地通过在最后一个大括号后指定变量名来创建变量。例如，声明 **enum BOOLEAN { FALSE , TRUE } flag ;** 定义了一个 **enum** 数据类型并创建了该类型的名为“flag”的变量。

可以使用 **typedef** 关键字和以下语法定义自定义数据类型：

```c
typedef definition type-name ;
```

声明自定义数据类型可以帮助使程序代码更简洁。例如，如果程序使用多个 **unsigned short int** 变量，则最好先使用以下声明创建具有这些修饰符的自定义数据类型：

```c
typedef unsigned short int USINT ;
```

然后，每个 **unsigned short int** 变量声明只需使用自定义数据类型名称 **USINT** 代替 **unsigned short int**。

![](img/d1dfb0563339ba187decb78799155b7f_45_0.png)

> 虽然不是必需的，但使用推荐的强制转换显式地为枚举类型变量赋值可作为其类型的提醒。

1. 使用预处理器指令开始一个新程序，以包含标准输入/输出库函数

   ```c
   #include <stdio.h>
   ```

2. 添加一个 main 函数，该函数声明并初始化从 1 开始的枚举常量集合

   ```c
   int main()
   {
       enum SNOOKER
       { RED=1,YELLOW, GREEN, BROWN, BLUE, PINK, BLACK };
   }
   ```

3. 接下来，在 main 函数块中，声明并初始化一个已定义 enum 类型变量，然后显示其值

   ```c
   enum SNOOKER pair = RED + BLACK ;
   printf( "Pair value: %d \n", pair );
   ```

4. 现在，添加语句创建自定义数据类型

   ```c
   typedef unsigned short int USINT ;
   ```

5. 然后，声明并初始化自定义数据类型的变量并显示其值

   ```c
   USINT num = 16 ;
   printf( "Unsigned short int value: %d \n", num );
   ```

6. 在 main 函数块的末尾，返回零整数值，如函数声明所要求

   ```c
   return 0 ;
   ```

7. 保存程序文件，然后编译并执行程序，以查看分配给枚举类型变量和自定义数据类型的数值

![](img/d1dfb0563339ba187decb78799155b7f_46_0.png)

![](img/d1dfb0563339ba187decb78799155b7f_46_1.png)

```text
C:\MyPrograms>gcc constype.c -o constype.exe
C:\MyPrograms>constype
Pair value: 8
Unsigned short int value: 16
C:\MyPrograms>
```

## 定义常量

预处理器 `#define` 指令可用于指定可在程序中使用的常量文本值，语法如下：

```c
#define CONSTANT-NAME "text-string"
```

与 `#include` 指令类似，这些指令应出现在程序代码的最开始。程序代码中指定的常量名称的任何出现都将在编译前由预处理器替换为相关的文本字符串。

条件预处理器 `#ifdef` 指令也可以用来评估定义是否当前存在。根据评估结果，其后可能跟随 `#define` 指令以指定常量文本值。此预处理器例程称为“宏”，每个宏必须以 `#endif` 指令结束。

有用的是，预处理器宏可以检查编译器定义的常量以确定主机操作系统。这些常量因机器而异，但在 Windows 平台上通常会有一个名为 `__WIN32` 的常量，而在 Linux 平台上通常会有一个 `linux` 常量。`#ifdef` 预处理器指令可以应用适当的文本字符串来标识主机平台。

![](img/d1dfb0563339ba187decb78799155b7f_47_0.png)

1. 使用预处理器指令开始一个新程序，以包含标准输入/输出库函数

   ```c
   #include <stdio.h>
   ```

2. 添加三个进一步的预处理器指令，指定用于在源代码中替换的文本字符串

   ```c
   #define LINE ""
   #define TITLE "C Programming in easy steps"
   #define AUTHOR "Mike McGrath"
   ```

3. 接下来，添加一个条件宏，指定用于标识 Windows 主机平台的文本字符串

   ```c
   #ifdef __WIN32
   #define SYSTEM "Windows"
   #endif
   ```
