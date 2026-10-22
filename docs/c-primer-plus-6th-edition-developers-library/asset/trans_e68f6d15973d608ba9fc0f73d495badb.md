
你可以为opaque成员使用值1来表示方框不透明，使用值0表示透明。对于show_border成员也可以这样做。对于颜色，你可以使用简单的RGB（红-绿-蓝）表示。这些是混合光的原色。显示器通过混合红色、绿色和蓝色像素来再现不同的颜色。在计算机彩色显示的早期，每个像素要么开要么关，因此你可以用一位来表示三种二进制颜色中每一种的强度。通常的顺序是左边一位表示蓝色强度，中间一位表示绿色强度，右边一位表示红色强度。表15.3显示了八种可能的组合。它们可以用作fill_color和border_color成员的值。最后，你可以选择用0、1、2分别表示实线、点线和虚线样式；它们可以用作border_style成员的值。

**表15.3 简单颜色表示**

| 位模式 | 十进制 | 颜色 |
|---|---|---|
| 000 | 0 | 黑色 |
| 001 | 1 | 红色 |
| 010 | 2 | 绿色 |
| 011 | 3 | 黄色 |
| 100 | 4 | 蓝色 |
| 101 | 5 | 品红色 |
| 110 | 6 | 青色 |
| 111 | 7 | 白色 |

程序清单15.3在简单示例中使用了box_props结构。它使用#define为可能的成员值创建符号常量。注意，原色由单个位为1来表示。其他颜色可以由原色的组合来表示。例如，品红色由蓝色位和红色位同时为1组成，因此可以用组合BLUE | RED来表示。

**程序清单15.3 fields.c程序**

```c
/* fields.c -- define and use fields */
#include <stdio.h>
#include <stdbool.h>   // C99, defines bool, true, false

/* line styles */
#define SOLID  0
#define DOTTED 1
#define DASHED 2
/* primary colors */
#define BLUE   4
#define GREEN 2
#define RED 1
/* mixed colors */
#define BLACK 0
#define YELLOW (RED | GREEN)
#define MAGENTA (RED | BLUE)
#define CYAN (GREEN | BLUE)
#define WHITE (RED | GREEN | BLUE)

const char * colors[8] = {"black", "red", "green", "yellow",
"blue", "magenta", "cyan", "white"};

struct box_props {
    bool opaque : 1; // or unsigned int (pre C99)
    unsigned int fill_color : 4;
    unsigned int show_border : 1; // or unsigned int (pre C99)
    unsigned int border_color : 3;
    unsigned int border_style : 2;
    unsigned int : 2;
};

void show_settings(const struct box_props * pb);

int main(void)
{
    /* create and initialize box_props structure */
    struct box_props box = {true, YELLOW, true, GREEN, DASHED};
    printf("Original box settings:\n");
    show_settings(&box);
    box.opaque = false;
    box.fill_color = WHITE;
    box.border_color = MAGENTA;
    box.border_style = SOLID;
    printf("\nModified box settings:\n");
    show_settings(&box);
    return 0;
}

void show_settings(const struct box_props * pb)
{
    printf("Box is %s.\n",
    pb->opaque == true ? "opaque" : "transparent");
    printf("The fill color is %s.\n", colors[pb->fill_color]);
    printf("Border %s.\n", pb->show_border == true ? "shown" : "not shown");
    printf("The border color is %s.\n", colors[pb->border_color]);
    printf("The border style is ");
    switch(pb->border_style)
    {
        case SOLID  : printf("solid.\n"); break;
        case DOTTED : printf("dotted.\n"); break;
        case DASHED : printf("dashed.\n"); break;
        default     : printf("unknown type.\n");
    }
}
```

下面是输出：

```text
Original box settings:
Box is opaque.
The fill color is yellow.
Border shown.
The border color is green.
The border style is dashed.
```

```text
Modified box settings:
Box is transparent.
The fill color is white.
Border shown.
The border color is magenta.
The border style is solid.
```

有几点需要注意。首先，你可以使用与普通结构相同的语法来初始化位字段结构：

```c
struct box_props box = {true, YELLOW, true, GREEN, DASHED};
```

类似地，你可以给位字段成员赋值：

```c
box.fill_color = WHITE;
```

此外，你可以将位字段成员用作switch语句的值表达式。你甚至可以将位字段成员用作数组索引：

```c
printf("The fill color is %s.\n", colors[pb->fill_color]);
```

注意，colors数组的定义方式是，每个索引值对应于一个字符串，该字符串代表以该索引值为其数值颜色值的颜色名称。例如，索引1对应字符串"red"，而符号常量red的值为1。

### 位字段与按位运算符

位字段和按位运算符是解决同一类编程问题的两种可选方法。也就是说，通常你可以使用其中任何一种方法。例如，前面的示例使用了一个与unsigned int大小相同的结构来保存图形框的信息。相反，你可以使用一个unsigned int变量来保存相同的信息。然后，你可以使用按位运算符来访问不同部分，而不是使用结构成员表示法。通常，这样做会更麻烦一些。让我们看一个同时采用这两种方法的示例，以说明它们之间的差异，而不是建议同时采用两种方法是个好主意！

你可以使用联合作为将结构方法与按位方法结合起来的手段。给定现有的struct box_props类型声明，你可以声明以下联合：

```c
union Views /* look at data as struct or as unsigned short */
{
    struct box_props st_view;
    unsigned short us_view;
};
```

在某些系统上，unsigned int和box_props结构都占用16位内存。在其他系统上，例如我们的系统，unsigned int和box_props是32位。无论哪种情况，使用这个联合，你可以使用st_view成员将该内存视为结构，或者使用us_view成员将同一块内存视为unsigned short。结构的哪些位字段对应于unsigned short中的哪些位？这取决于实现和硬件。下面的示例假设结构从字节的低位端到高位端加载到内存中。也就是说，结构中的第一个位字段进入字的位0。（为简单起见，图15.3用16位单元说明了这一概念。）

程序清单15.4使用Views联合来比较位字段方法和按位方法。其中，box是一个Views联合，因此box.st_view是使用位字段的box_props结构，而box.us_view是将相同数据视为unsigned short的视图。回想一下，联合可以初始化其第一个成员，因此初始化值与结构视图匹配。程序使用基于结构视图的函数以及基于unsigned short视图的函数来显示框属性。两种方法都可以访问数据，但技术不同。程序还使用本章前面定义的itobs()函数将数据显示为二进制字符串，以便你可以看到哪些位为1，哪些位为0。

```text
box.us_view
the box union seen as an integer
bit 15
bit 0

box.st_view
the box union seen as a structure
num_prtrs
gameio
num_comcds
num_drives
vid_setup
mother_bd
has_drive
```

**图15.3 联合作为整数和结构。**

**程序清单15.4 dualview.c程序**

```c
/* dualview.c -- bit fields and bitwise operators */
#include <stdio.h>
#include <stdbool.h>
#include <limits.h>
/* BIT-FIELD CONSTANTS */
/* line styles */
#define SOLID 0
#define DOTTED 1
#define DASHED 2
/* primary colors */
#define BLUE 4
#define GREEN 2
#define RED 1
/* mixed colors */
#define BLACK 0
#define YELLOW (RED | GREEN)
#define MAGENTA (RED | BLUE)
#define CYAN (GREEN | BLUE)
#define WHITE (RED | GREEN | BLUE)

/* BITWISE CONSTANTS */
#define OPAQUE 0x1
#define FILL_BLUE 0x8
#define FILL_GREEN 0x4
#define FILL_RED 0x2
#define FILL_MASK    0xE
#define BORDER       0x100
#define BORDER_BLUE  0x800
#define BORDER_GREEN 0x400
#define BORDER_RED   0x200
#define BORDER_MASK  0xE00
#define B_SOLID      0
#define B_DOTTED     0x1000
#define B_DASHED     0x2000
#define STYLE_MASK   0x3000

const char * colors[8] = {"black", "red", "green", "yellow",
    "blue", "magenta", "cyan", "white"};
struct box_props {
    bool opaque           : 1;
    unsigned int fill_color : 3;
    unsigned int           : 4;
    bool show_border      : 1;
    unsigned int border_color : 3;
    unsigned int border_style : 2;
    unsigned int           : 2;
};

union Views    /* look at data as struct or as unsigned short */
{
    struct box_props st_view;
    unsigned short us_view;
};

void show_settings(const struct box_props * pb);
void show_settings1(unsigned short);
char * itobs(int n, char * ps);

int main(void)
{
    /* create Views object, initialize struct box view */
    union Views box = {{true, YELLOW, true, GREEN, DASHED}};
    char bin_str[8 * sizeof(unsigned int) + 1];

    printf("Original box settings:\n");
    show_settings(&box.st_view);
    printf("\nBox settings using unsigned int view:\n");
    show_settings1(box.us_view);

    printf("bits are %s\n",
        itobs(box.us_view, bin_str));
    box.us_view &= ~FILL_MASK;      /* clear fill bits */
```
