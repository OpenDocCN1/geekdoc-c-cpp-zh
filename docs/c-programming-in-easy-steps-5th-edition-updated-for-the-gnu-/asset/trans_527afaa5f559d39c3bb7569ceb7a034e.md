
## 声明程序常量

当程序需要使用一个永远不会改变的固定常量数据值时，它应与变量以相同的方式声明，但要在声明中包含 const 关键字。例如，表示不变的整数值一百万的常量可以像这样声明并初始化：

```
const int MILLION = 1000000 ;
```

![](img/db19f3858a1e321646bf2590afd29547_58_0.png)

常量声明必须始终使用其将包含的数据值初始化常量对象。程序永远无法从其初始值更改常量的值。这可防止常量值被意外更改，因为如果程序尝试随后更改初始值，编译器会报告错误。

常量名须遵守与变量名相同的命名约定（此处描述），但传统上使用大写字符作为常量名，以便在阅读源代码时易于将其与变量名区分开。

如果程序永远不会更改其所有初始元素值，也可以在数组声明中使用 const 关键字。

- 1. 使用预处理指令开始一个新程序以包含标准输入/输出库函数

  ```
  #include <stdio.h>
  ```

![](img/db19f3858a1e321646bf2590afd29547_59_0.png)

constant.c

- 2. 添加一个 main 函数，声明一个近似数学值 Pi 的常量值

  ```
  int main()
  {
      const float PI = 3.141593 ;
  }
  ```

- 3. 接下来，在 main 函数块中，插入声明四个变量的语句

  ```
  float diameter ;
  float radius ;
  float circ ;
  float area ;
  ```

- 4. 现在，插入请求用户输入以分配给变量的语句

  ```
  printf("Enter the diameter of a circle in millimeters: ");
  scanf("%f", &diameter );
  ```

- 5. 接下来，添加使用常量值和用户输入计算其他三个变量值的语句

  ```
  circ = PI * diameter ;
  radius = diameter / 2 ;
  area = PI * ( radius * radius ) ;
  ```

- 6. 现在，插入将计算值格式化为两位小数输出的语句

  ```
  printf("Circumference is %.2f mm", circ );
  printf("And the area is %.2f sq.mm\n", area );
  ```

- 7. 在 main 函数块末尾，返回零整数值，如函数声明所要求

  ```
  return 0 ;
  ```

- 8. 保存程序文件，然后编译并执行程序，在需要时输入数据以查看计算输出

```
C:\MyPrograms>gcc constant.c -o constant.exe
C:\MyPrograms>constant
Enter the diameter of a circle in millimeters: 
```

```
C:\MyPrograms>constant
Enter the diameter of a circle in millimeters: 140
Circumference is 439.82 mm
And the area is 15393.81 sq.mm
C:\MyPrograms>
```

这里星号字符是算术乘法运算符，正斜杠字符是除法运算符。算术运算符将在下一章中完整演示。

请记住，在 scanf() 中必须在变量名前加上 & 取地址运算符，以便将输入分配给变量。

## 枚举常量值

enum 关键字提供了一种简洁的方式来创建整数常量的序列。可选地，声明可以在 enum 关键字后包含序列的名称。常量名作为逗号分隔的列表跟在花括号内。

默认情况下，每个常量的值都比列表中在其前面的常量大一。若未指定，第一个常量的值为零；下一个值为 1；依此类推。

例如，可以使用 `enum{MON,TUE,WED,THU,FRI};` 给命名的工作日常量一个从零开始的整数值序列——在这种情况下，常量 WED 的整数值为 2。

常量可以在声明中被赋予任意单个整数值，但列表中的下一个常量始终会将前一个值递增一，除非它也被赋予了值。例如，要使序列从 1 而不是零开始，使用 `enum{MON=1,TUE,WED,THU,FRI};` 将 1 分配给第一个常量——在这种情况下，常量 WED 的整数值为 3。

枚举常量的列表也称为“枚举集合”，可能包含重复的常量值。例如，值零可以分配给名为 NIL 和 NONE 的常量。

在下面的示例中，枚举集合表示斯诺克游戏中球的分数值，并包含一个可选名称，该名称以大写形式出现，因为它也是常量。

- 1. 使用预处理指令开始一个新程序以包含标准输入/输出库函数

  ```
  #include <stdio.h>
  ```

![](img/db19f3858a1e321646bf2590afd29547_61_0.png)

![](img/db19f3858a1e321646bf2590afd29547_63_0.png)

在本例中给 **BLUE** 常量赋值为 1 会重新开始递增过程——使 **PINK** 常量为 2，**BLACK** 常量为 3。

![](img/db19f3858a1e321646bf2590afd29547_63_1.png)

enum 类型名（在本例中为 **SNOOKER**）是可选的——因此在本例中可以省略。

## 创建常量类型

一旦枚举序列被声明，它就可以被视为一种新的数据类型，具有其指定的常量名及其相关值的属性。

这种 enum 数据类型的变量可以像声明其他数据类型的变量一样声明——使用以下语法：

```
data-type variable-name ;
```

这里的示例创建了一个名为 SNOOKER 的枚举序列，可视为 enum SNOOKER 的数据类型。因此，可以使用声明 enum SNOOKER pair ; 创建该数据类型的名为“pair”的变量，并可存储该类型定义的枚举集合的值。

要显式地将整数值分配给枚举数据类型的变量，C 标准建议使用强制转换将 int 数据类型转换为 enum 数据类型，如下所示：

```
pair = ( enum SNOOKER ) 7 ;
```

然而在实践中这并非必需，因为枚举值始终是整数，因此等同于 int 数据类型。

enum 声明可选择在最后的花括号后指定变量名来同时创建变量。例如，声明 enum BOOLEAN { FALSE , TRUE } flag ; 定义了一个 enum 数据类型并创建了该类型的名为“flag”的变量。

可以使用 typedef 关键字和以下语法定义自定义数据类型：

```
typedef definition type-name ;
```

声明自定义数据类型有助于使程序代码更简洁。例如，如果程序使用多个 unsigned short int 变量，使用以下声明先创建具有这些修饰符的自定义数据类型会很有用：

```
typedef unsigned short int USINT ;
```

然后每个 unsigned short int 变量声明只需使用自定义数据类型名 USINT 代替 unsigned short int。

![](img/db19f3858a1e321646bf2590afd29547_65_0.png)

虽然不是必需的，但使用推荐的强制转换显式地为枚举类型变量赋值可作为其类型的提醒。

constype.c

- 1. 使用预处理指令开始一个新程序以包含标准输入/输出库函数

  ```
  #include <stdio.h>
  ```

- 2. 添加一个 main 函数，声明并初始化一个从 1 开始的枚举常量集合

  ```
  int main()
  {
      enum SNOOKER
      {
          RED=1, YELLOW, GREEN, BROWN, BLUE, PINK, BLACK
      };
  }
  ```

- 3. 接下来，在 main 函数块中，声明并初始化一个定义好的 enum 类型变量，然后显示其值

  ```
  enum SNOOKER pair = RED + BLACK;
  printf("Pair value: %d\n", pair);
  ```

- 4. 现在，添加一条创建自定义数据类型的语句

  ```
  typedef unsigned short int USINT;
  ```

- 5. 然后，声明并初始化一个自定义数据类型变量并显示其值

  ```
  USINT num = 16;
  printf("Unsigned short int value: %d\n", num);
  ```

- 6. 在 main 函数块末尾，返回零整数值，作为

  ```
  return 0;
  ```
