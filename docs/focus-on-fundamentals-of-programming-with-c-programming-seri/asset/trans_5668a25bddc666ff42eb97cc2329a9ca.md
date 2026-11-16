

## 预处理器作业

1. 编写预处理器指令以完成以下每一项：

- a) 定义符号常量 TRUE，其值为 1。
- b) 定义符号常量 FALSE，其值为 0。
- c) 如果已定义符号常量 YES，则取消其定义并将其重新定义为 1。
- d) 定义一个宏 AREA，它接受一个参数并计算正方形的面积。
- e) 定义宏 SUM，用于求两个数的和。
- f) 定义宏 MIN2，用于确定两个数值中的较小值。

2. 编写一个宏，计算 n 除以 4 的余数。

3. 令 DOUBLE 为以下宏：

```
#define DOUBLE(x) 2*x
```

- a) DOUBLE(1+2) 的值是多少？
- b) 4/DOUBLE(2) 的值是多少？
- c) 修复 DOUBLE 的定义。

4. 对于以下每个宏，给出一个说明宏存在问题的示例，并展示如何修复它。

- a) #define AVG(x, y) (x+y) / 2
- b) #define AREA(x, y) (x) * (y)

## 预处理器实验

在本次作业中，我们将构建一个简单的 C 预处理器 pre.c，用于为编译准备 C 程序 test.c。预处理器将解析 test.c 中的源代码，并创建一个包含预处理后代码的输出文件 out.c。out.c 的内容随后应被输出、编译并执行。

预处理器应执行以下操作：

- 从源代码中删除所有注释。
- 识别 #include 预处理器命令，并将指定文件的内容插入到 out.c 中。
- 识别 #define 预处理器命令，并用相应的替换字符串替换所有符号名称。

为了协助处理 #define 命令，我们将使用以下方案：

test.c 中识别出的每个已定义符号及其替换字符串应放置在文件 define.txt 中。从源代码 test.c 读取每个标记时，必须将其与 define.txt 的内容进行比较，以确定该标记是否为预定义符号。如果是，则必须将相应的替换字符串放入 out.c。否则，将标记本身放入 out.c。

为了避免将每个标记与 define.txt 的内容进行比较，我们将使用一个简单的哈希表，每个位置初始化为 0。对于遇到的每个 #defined 符号，我们将获取其哈希值，将哈希表中相应位置的内容设置为 1，并将符号及其替换字符串发送到 define.txt。对于 test.c 中的每个其他标记，我们也必须获取其哈希值并检查哈希表中相应的位置。如果找到 0，则该标记不是预定义符号，应放入 out.c。但是，如果标记哈希到包含 1 的位置，则该标记可能是预定义符号。我们必须在 define.txt 中搜索该标记。如果找到匹配项，则将替换字符串放入 out.c，否则，将标记本身放入 out.c。

请注意，您的程序不应依赖于文件重定向，而应使用标准 C 库提供的 I/O 函数来设置和使用外部磁盘文件。

请记住，`main()` 函数应作为程序中的第一个函数出现。请务必为程序中使用的每个函数使用函数原型。

程序的输出应发送到终端窗口（您的屏幕）以及请求的 `csis.txt` 输出文件。请务必阅读关于捕获程序输出的文档。您的全名必须作为注释出现在包含 `main()` 的源文件中。请务必将 `csis.txt` 输出文件包含在 zip 压缩包中。

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

- 枚举
- typedef 语句
- 枚举 & typedef 作业

## 枚举

当数据类型将保存有限列表中的一个值时，您可以选择使用枚举数据类型。枚举类型的变量可以赋予其类型中的任何“值”。

```
// enum1.c
enum Day { Sat, Sun, Mon, Tues, Wed, Thurs, Fri };
enum Gender { male, female };

int main (void) {
    enum Day today = Wed;
    enum Day tomorrow = Thurs;
    enum Gender student = female;
    ...
}
```

枚举值被 C 编译器视为常量，每个枚举值都被赋予一个整数值，从 0 开始。当我们说 today = Wed; 时，值 4 被赋予 today，而不是名称 Wed。

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
        }
        else {
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

假设您想在遍历 `for` 循环时输出变量 `today` 的不同值。您可以尝试这样做。

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

事实证明，枚举类型的值不能直接写入输出。通常使用 switch 语句来实现所需结果。

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

C 中没有布尔（真或假）数据类型。相反，使用整数值 0 和 1。但是，很容易发明我们自己的布尔类型：

```
// enum5.c
enum Boolean { false, true };
enum Boolean Flag;
flag = true;
or as
enum Boolean { false, true } flag;
flag = false;
```

枚举类型的一个令人烦恼的方面是，它们不被 C 输入输出语句识别。例如：

```
// enum6.c
enum direction { north, south, east, west };
direction d1 = south;
printf("%d\n", south);
```

值 1 被输出。

如果希望将特定整数值与枚举值关联，则可以在定义数据类型时将整数赋给该值。列表中随后出现的枚举值将从指定整数值加 1 开始分配顺序值。

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

请注意，在函数内定义枚举数据类型会将该定义的使用限制在函数内定义的变量上。在程序开头（任何函数之外）定义枚举数据类型，会使该类型定义对文件全局。

