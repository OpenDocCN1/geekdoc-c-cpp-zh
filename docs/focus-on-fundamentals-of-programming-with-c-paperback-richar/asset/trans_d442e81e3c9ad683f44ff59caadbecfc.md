

## 嵌套结构

C 允许我们嵌套结构，即在其他结构中定义结构。
例如，假设我们想要记录房子中各个房间的尺寸。我们可以先按如下方式定义一个 `Distance` 结构体：

```
// nestingStructs1.c
typedef struct {
    int feet;
    float inches;
} Distance;
```

我们现在可以定义一个 `Room` 结构体，它包含作为其组件的 `Distance` 变量：

```
// nestingStructs2.c
typedef struct {
    Distance length, width;
} Room;
```

我们现在初始化结构体变量的每个字段：

```
// nestingStructs3.c
int main(void) {
    Room bedroom, kitchen;

    bedroom.length.feet = 25;
    bedroom.length.inches = 6;
    bedroom.width.feet = 20;
    bedroom.width.inches = 8.5;

    kitchen.length.feet = 15;
    kitchen.length.inches = 3.25;
    kitchen.width.feet = 10;
    kitchen.width.inches = 6;

    return 0;
}
```

下面是另一个示例。假设我们需要设置一个在特定日期和时间发生的事件列表。我们希望将日期和时间关联在一个单一实体中。

首先我们定义一个 `Date` 结构体和一个 `Time` 结构体：

```
// nestingStructs4.c
typedef struct {
    int month;
    int day;
    int year;
} Date;
typedef struct {
    int hour;
    int minute;
    int second;
} Time;
```

我们现在可以按如下方式定义一个 `DateTime` 结构体：

```
// nestingStructs5.c
typedef struct {
    Date eventDate;
    Time eventTime;
} DateTime;
```

让我们现在创建一个 `DateTime` 变量并初始化其组件：

```
// nestingStructs6.c

int main(void) {
    DateTime appt;
    appt.eventDate.month = 8;
    appt.eventDate.day = 23;
    appt.eventDate.year = 2013;
    appt.eventTime.hour = 11;
    appt.eventTime.minute = 30;
    appt.eventTime.second = 45;
    return 0;
}
```

如果我们正在实现一个日历程序，可能需要许多 `DateTime` 变量。因此，让我们创建一个 `DateTime` 结构体数组：

```
// nestingStructs7.c

DateTime event[1000];
```

我们现在可以按如下方式初始化数组的一个元素：

```
// nestingStructs8.c

event[35].eventDate.month = 7;
event[35].eventDate.day = 14;
event[35].eventDate.year = 2015;
event[35].eventTime.hour = 2;
event[35].eventTime.minute = 15;
event[35].eventTime.second = 00;
```

## 结构体作业

1. 编写代码以完成以下每项任务：

- a) 使用 typedef 声明一个名为 Automobile 的结构体，包含以下成员：

model - 最多 25 个字符的字符串
year – 整数
mpg – 整数

- b) 声明类型为 Automobile 的变量 car。

- c) 将以下信息分配给变量 car 的相应字段：

> 2012 款英菲尼迪每加仑可行驶 25 英里。

- d) 声明一个包含 500 个 Automobile 的数组 vehicle。

- e) 将变量 car 赋值给数组的第 5 个元素。

- f) 输出数组第 5 个位置中的 Automobile 信息。显示输出。

- g) 声明变量 p 为指向 Automobile 结构体的指针。

- h) 将数组第 5 个位置的地址赋值给变量 p。

- i) 使用变量 p，输出数组第 5 个位置中的 Automobile 信息。显示输出。

- j) 声明变量 q 为指向 Automobile 结构体的指针。

- k) 将数组第一个位置的地址赋值给变量 q。

- l) 使用变量 q，输出数组第 5 个位置中的 Automobile 信息。显示输出。

## 数据库实验

本实验将重点介绍结构体的使用和操作。实验的每个部分都应在其自身的函数中设计，根据需要传递参数。你需要构建一个 C 程序 `database.c`，用于检索和操作公司的工资单数据库 `payfile.txt`。每个员工的数据应读入包含以下字段标识符的 `struct` 中：

| 字段 | 描述 |
| :--- | :--- |
| first | 最多 7 个字符 |
| initial | 最多 1 个字符 |
| last | 最多 9 个字符 |
| street | 最多 16 个字符 |
| city | 最多 11 个字符 |
| state | 最多 2 个字符 |
| zip | 最多 5 个字符 |
| age | 整数 |
| sex | 最多 1 个字符 (M/F) |
| tenure | 表示受雇年数的整数 |
| salary | 表示周薪的双精度浮点数 |

你的程序应执行下面指示的每个操作。请务必为每个部分清晰地标记输出。请记住，实验的每个部分都应在其自身的函数中设计，根据需要传递参数。

- a) 将员工数据读入结构体数组。
- b) 将每个结构体的内容以易于阅读的格式输出，格式类似于输入文件。
- c) 输出工资单上所有男性的名和姓。
- d) 输出工资单上薪酬最高的女性的名和姓。
- e) 输出工资单上薪酬最低的男性的名和姓。
- f) 输出所有员工的平均薪水。
- g) 输出所有收入低于平均薪水的女性的名和姓。
- h) 以三位小数输出平均薪水以上男性人数与平均薪水以下男性人数的比率。
- i) 输出所有年收入超过 35,000 美元、在公司工作至少 5 年且年龄超过 30 岁的员工的名和姓。
- j) 给所有周收入低于 350.00 美元的员工涨薪 10%，并输出每位获得加薪员工的名、姓和新薪水。
- k) (额外学分) 按邮政编码对结构体进行排序，并输出每位员工的名、姓和邮政编码。

下面是一个 C 函数 `strsub()`，它从字符串 `buf` 中根据字符串内的 `start` 和 `end` 索引提取子字符串 `sub`。

```
void strsub(char buf[], char sub[], int start, int end) {
    int i, j;

    for (j=0, i=start; i<=end; i++, j++) {
        sub[j] = buf[i];
    }
    sub[j] = '\0';
}
```

当你从文件中读取一行数据并需要从该行数据中提取不同信息以放入结构体字段时，此函数可能很有用。请记住，数组使用基于零的索引。

```
while (!feof(fp)) {
    fgets(buf, MAX, fp);
    strsub(buf, workers[i].first, 0, 6);
    strsub(buf, workers[i].initial, 8, 8);
    strsub(buf, workers[i].last, 10, 18);
    ...
    ...
}
```

你可以假设有以下声明：

```
#define MAX 100
```

C 库 stdlib.h 和 string.h 中的以下三个函数可能对本实验有用：

```
atoi() - converts a string to an integer
atof() - converts a string to a float
strcmp() - compares two strings
```

对于实验的额外学分部分，你需要修改我们之前学习的排序算法，使其适用于结构体。

payfile.txt 的内容如下：

| ADA | A AUGUSTA | 33 | BABBAGE ROAD | LOVELACE | GB | 19569 | 28 | F | 2 | 350.50 |
|---|---|---|---|---|---|---|---|---|---|---|
| ISAAC | A ASIMOV | 99 | FICTION WAY | AMHERST | MA | 63948 | 58 | M | 6 | 423.88 |
| HUMPHREY | R BOGART | 71 | SAM STREET | HOLLYWOOD | CA | 48482 | 56 | M | 5 | 366.00 |
| ALBERT | G EINSTEIN | 94 | ENERGY WAY | PRINCETON | NJ | 47474 | 67 | M | 8 | 780.00 |
| EMMYLOU | L HARRIS | 66 | COUNTRY ROAD | NASHVILLE | TN | 72647 | 38 | F | 2 | 767.42 |
| JAMES | T KIRK | 11 | SPACE STREET | VULCAN | CA | 82828 | 46 | M | 1 | 235.70 |
| TED | L KOPPLE | 55 | ABC PLACE | WASHINGTON | DC | 37376 | 48 | M | 9 | 909.44 |
| DAVID | T LETTERMAN | 14 | WNBC AVENUE | NEW YORK | NY | 19338 | 47 | M | 5 | 445.65 |
| STEVIE | R NICKS | 31 | MUSIC ROAD | CHICAGO | IL | 23459 | 38 | F | 8 | 460.88 |
| MONTY | P PYTHON | 76 | SILLY STREET | LONDON | GB | 80939 | 44 | M | 2 | 320.50 |
| ROGER | R RABBIT | 15 | LOONEY TOONS | HOLLYWOOD | CA | 91343 | 24 | M | 4 | 259.53 |
| SALLY | W RIDE | 21 | COLUMBIA WAY | HOUSTON | TX | 91123 | 30 | F | 9 | 707.80 |
| ROD | Q SERLING | 11 | TWILIGHT ZONE | SAN DIEGO | CA | 93939 | 56 | M | 1 | 440.00 |
| LUKE | R SKYWALKER | 43 | MILKY WAY | NEW YORK | NY | 12343 | 35 | M | 5 | 660.00 |

请记住，main() 函数应作为程序中的第一个函数出现。请务必为程序中使用的每个函数使用函数原型。

程序的输出应发送到终端窗口（您的屏幕）以及请求的 .cis.txt 输出文件。请务必阅读关于捕获程序输出的文档。你的全名和 Palomar ID 号必须作为注释出现在包含 main() 的源文件中。请务必将 .cis.txt 输出文件包含在 zip 压缩包中。

