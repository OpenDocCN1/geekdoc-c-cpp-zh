

请注意，您的程序不应依赖于文件重定向，而应使用标准C库提供的I/O函数来设置和使用外部磁盘文件。

请记住，main()函数应作为程序中的第一个函数出现。请务必为程序中使用的每个函数使用函数原型。

程序的输出应同时发送到终端窗口（您的屏幕）以及请求的csis.txt输出文件。请务必阅读关于捕获程序输出的文档。您的全名和Palomar ID号必须作为注释出现在包含main()的源文件中。请务必将csis.txt输出文件包含在zip存档中。

```
test.c

#include <header.h>

#define TOTAL x + y
#define MESSAGE "ON A CLEAR DAY YOU CAN C FOREVER"
#define FORMAT1 "%s\n"
#define FORMAT2 "%d %d\n"

int main(void) {
    int x, y, z, i, sum;

    printf(FORMAT1, MESSAGE);
    printf(NEWLINE);

    sum = ZERO;
    for (i = MIN; i <= MAX; ++i) {
        sum += i;
    }

    x = MAX;
    y = MIN;
    z = TOTAL;
    printf(FORMAT2, sum, z);

    return 0;
}

header.h

#define MAX 30
#define MIN 20
#define ZERO 0
#define NEWLINE "\n"
```

## 枚举

## Typedef语句

- 枚举与Typedef作业

## 枚举

当数据类型将保存有限值列表中的一个值时，您可以选择使用枚举数据类型。枚举类型的变量可以分配其类型中的任何“值”。

```
// enum.c
enum Day { Sat, Sun, Mon, Tues, Wed, Thurs, Fri };
enum Gender { male, female };

int main (void) {
    enum Day today = Wed;
    enum Day tomorrow = Thurs;
    enum Gender student = female;
    ...
}
```

C编译器将枚举值视为常量，并为每个值赋予一个整数值，从0开始。当我们说 today = Wed; 时，值4被分配给today，而不是名称Wed。

具有枚举类型的变量也可以用于布尔表达式：

```
if (student == female) {
    printf("female");
}
```

其他关系运算符也可以使用。请注意，枚举数据类型会自动在元素之间建立顺序：

```
// enum2.c

#include <stdio.h>

enum Day { Sat, Sun, Mon, Tues, Wed, Thurs, Fri };

int main (void) {
    enum Day today;

    for (today = Sat; today <= Fri; ++today) {
        if (today < Mon) {
            printf("Weekend\n");
        } else {
            printf("Weekday\n");
        }
    }
    return 0;
}
```

### 输出：

```
Weekend
Weekend
Weekday
Weekday
Weekday
Weekday
Weekday
Weekday
```

假设您想在遍历`for`循环时输出变量`today`的不同值。您可以尝试这样做。

```
// enum3.c

#include <stdio.h>

enum Day { Sat, Sun, Mon, Tues, Wed, Thurs, Fri };

int main (void) {
    enum Day today;
    for (today = Sat; today <= Fri; ++today) {
        printf("%d\n", today);
    }
    return 0;
}
```

但您的输出将如下所示：

```
0
1
2
3
4
5
6
```

事实证明，枚举类型的值不能直接写入输出。通常使用switch语句来实现所需结果。

```
// enum4.c

#include <stdio.h>

enum Day { Sat, Sun, Mon, Tues, Wed, Thurs, Fri };

int main (void) {
    enum Day today;

    for (today = Sat; today <= Fri; ++today) {
        switch (today) {
            case Sat: puts("Sat"); break;
            case Sun: puts("Sun"); break;
            case Mon: puts("Mon"); break;
            case Tues: puts("Tues"); break;
            case Wed: puts("Wed"); break;
            case Thurs: puts("Thurs"); break;
            case Fri: puts("Fri"); break;
        }
    }

    return 0;
}
```

### 输出：

```
Sat
Sun
Mon
Tues
Wed
Thurs
Fri
```

C中没有布尔（真或假）数据类型。相反，使用整数值0和1。但是，很容易发明我们自己的布尔类型：

```
// enum5.c
enum Boolean { false, true };
enum Boolean flag;
flag = true;

or as

enum Boolean { false, true } flag;
flag = false;
```

枚举类型的一个令人恼火的方面是它们不被C输入输出语句识别。例如：

```
// enum6.c
enum direction { north, south, east, west };

direction d1 = south;
printf("%d\n", south);
```

输出的值为1。

如果希望将特定整数值与枚举值关联，则可以在定义数据类型时将整数分配给该值。随后出现在列表中的枚举值将被分配从指定整数值加1开始的顺序值。

例如：

```
// enum7.c
enum direction { up, down, left = 10, right };
```

每个枚举值将具有以下数值：

```
up = 0
down = 1
left = 10
right = 11
```

定义枚举数据类型时可以省略数据类型的名称。定义数据类型时，也可以将变量声明为特定的枚举数据类型：

```
// enum8.c

enum { east, west, south, north } location;
```

请注意，在函数内定义枚举数据类型会将该定义的使用限制在函数内定义的变量上。在程序开头（任何函数之外）定义枚举数据类型，会使类型定义对文件全局。

## Typedef语句

typedef语句使程序员能够为数据类型分配一个替代名称。例如：

```c
// typedef1.c
typedef int COUNTER;
```

定义名称COUNTER等同于C数据类型int。现在可以将变量声明为COUNTER类型：

```c
// typedef2.c
typedef int COUNTER;
COUNTER a, b, c;
```

这为程序提供了更好的可读性。以下是另一个示例：

```c
// typedef3.c
typedef char *STRING_PTR;
```

定义名称STRING_PTR为char指针。现在可以定义STRING_PTR类型的变量：

```c
// typedef4.c
typedef char *STRING_PTR;
STRING_PTR buffer;
```

C编译器将其视为字符指针。

另一个示例：

```
// typedef5.c
typedef char STRING[81];
```

定义一个名为STRING的类型，它是一个包含81个字符的数组。现在可以定义STRING类型的变量，如下所示：

```
// typedef6.c
typedef char STRING[81];
STRING text;
```

这相当于将变量text定义为包含81个字符的字符数组，并等效于：

```
char text[81];
```

### 定义新类型名称的步骤

- 1. 编写语句，仿佛正在定义所需类型的变量。
- 2. 在通常出现已定义变量名称的位置，替换为新类型名称。
- 3. 在最前面放置关键字typedef。

## 枚举与Typedef作业

- 1. a) 声明一个枚举标记，其值代表一周中的七天。
  b) 使用`typedef`为枚举定义一个名称。

- 2. 关于枚举常量的以下哪些陈述是正确的？
  a) 枚举常量可以表示程序员指定的任何整数。
  b) 枚举常量具有与使用`#define`创建的常量完全相同的属性。
  c) 枚举常量默认具有值0、1、2、...。
  d) 枚举中的所有常量必须具有不同的值。
  e) 枚举常量可以在表达式中用作整数。

- 3. 假设`b`和`i`按以下方式声明：
  ```
  enum { FALSE, TRUE } b;
  int i;
  ```
  以下哪些语句是合法的？哪些是“安全”的（始终产生有意义的结果）？
  a) `b = FALSE;`	b) `i = b;`
  c) `b++;`	d) `i = b;`	e) `i = 2 * b + 1;`

- 4. 假设direction变量按以下方式声明：

  ```
  enum { NORTH, SOUTH, EAST, WEST } direction;
  ```

  设x和y为int变量。编写一个switch语句来测试direction的值，如果direction是EAST则递增x，如果direction是WEST则递减x，如果direction是SOUTH则递增y，如果direction是NORTH则递减y。

- 5. 以下各声明中枚举常量的整数值是多少？
  a) enum { NORTH, EAST, SOUTH, WEST };
  b) enum { DIAMONDS = 5, HEARTS, CLUBS, SPADES };
  c) enum { MON = 8, TUES, WED, THURS = 14, FRI };
  d) enum { RED = 5, BLUE, GREEN, YELLOW = 12, BROWN };

