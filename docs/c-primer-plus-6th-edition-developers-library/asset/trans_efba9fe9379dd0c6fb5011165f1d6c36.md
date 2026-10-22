

```
box.us_view |= (FILL_BLUE | FILL_GREEN); /* reset fill */
box.us_view ^= OPAQUE;                 /* toggle opacity */
box.us_view |= BORDER_RED;            /* wrong approach */
box.us_view &= ~STYLE_MASK;           /* clear style bits */
box.us_view |= B_DOTTED;              /* set style to dotted */
printf("\nModified box settings:\n");
show_settings(&box.st_view);
printf("\nBox settings using unsigned int view:\n");
show_settings1(box.us_view);
printf("bits are %s\n", itobs(box.us_view,bin_str));

return 0;
}

void show_settings(const struct box_props * pb)
{
    printf("Box is %s.\n", pb->opaque == true ? "opaque": "transparent");
    printf("The fill color is %s.\n", colors[pb->fill_color]);
    printf("Border %s.\n", pb->show_border == true ? "shown" : "not shown");
    printf("The border color is %s.\n", colors[pb->border_color]);
    printf ("The border style is ");
    switch(pb->border_style)
    {
        case SOLID  : printf("solid.\n"); break;
        case DOTTED : printf("dotted.\n"); break;
        case DASHED : printf("dashed.\n"); break;
        default     : printf("unknown type.\n");
    }
}

void show_settings1(unsigned short us)
{
    printf("box is %s.\n", (us & OPAQUE) == OPAQUE? "opaque": "transparent");
    printf("The fill color is %s.\n", colors[(us >> 1) & 07]);
    printf("Border %s.\n", (us & BORDER) == BORDER? "shown" : "not shown");
    printf ("The border style is ");
    switch(us & STYLE_MASK)
    {
        case B_SOLID  : printf("solid.\n"); break;
        case B_DOTTED : printf("dotted.\n"); break;
        case B_DASHED : printf("dashed.\n"); break;
default : printf("unknown type.\n");
}
printf("The border color is %s.\n", colors[(us >> 9) & 07]);
}

char * itobs(int n, char * ps)
{
    int i;
    const static int size = CHAR_BIT * sizeof(int);

    for (i = size - 1; i >= 0; i--, n >>= 1)
        ps[i] = (01 & n) + '0';
    ps[size] = '\0';

    return ps;
}
```

以下是输出：

Original box settings:
Box is opaque.
The fill color is yellow.
Border shown.
The border color is green.
The border style is dashed.

Box settings using unsigned int view:
box is opaque.
The fill color is yellow.
Border shown.
The border style is dashed.
The border color is green.
bits are 00000000000000001001010000111

Modified box settings:
Box is transparent.
The fill color is cyan.
Border shown.
The border color is yellow.
The border style is dotted.

Box settings using unsigned int view:
box is transparent.
The fill color is cyan.
Border not shown.

The border style is dotted.
The border color is yellow.
bits are 0000000000000000001011100001100

有几个要点需要讨论。位域和按位视图之间的一个区别是，按位视图需要位置信息。例如，我们使用 BLUE 来表示蓝色颜色。该常量具有数值 4。但由于数据在结构中的排列方式，实际保存填充颜色蓝色设置的位是位 3（记住编号从 0 开始——参见图 15.1），而保存边框颜色蓝色设置的位是位 11。因此，程序定义了一些新的常量：

```
#define FILL_BLUE    0x8
#define BORDER_BLUE   0x800
```

这里，0x8 是仅位 3 置为 1 时的值，0x800 是仅位 11 置为 1 时的值。你可以使用第一个常量来设置填充颜色的蓝色位，使用第二个常量来设置边框颜色的蓝色位。使用十六进制表示法更容易看出涉及哪些位。回想一下，每个十六进制数字代表四位。因此，0x800 与 0x8 具有相同的位模式，只是后面加上了八个 0 位。这种关系用 2048 和 8，即十进制等价物，就远不那么明显。

如果值是 2 的幂，可以使用左移运算符来提供值。例如，你可以用以下内容替换最后的 #define 语句：

```
#define FILL_BLUE    1<<3
#define BORDER_BLUE   1<<11
```

这里，第二操作数是与 2 配合使用的幂。即，0x8 是 2³，0x800 是 2¹¹。等价地，表达式 1<<n 是整数中仅第 n 位设为 1 的值。像 1<<11 这样的表达式是常量表达式，并在编译时求值。

你可以使用枚举而不是 #define 来创建符号常量。例如，可以这样做：

```
enum { OPAQUE = 0x1, FILL_BLUE = 0x8, FILL_GREEN = 0x4, FILL_RED = 0x2,
    FILL_MASK = 0xE, BORDER = 0x100, BORDER_BLUE = 0x800,
    BORDER_GREEN = 0x400, BORDER_RED = 0x200, BORDER_MASK = 0xE00,
    B_DOTTED = 0x1000, B_DASHED = 0x2000, STYLE_MASK = 0x3000};
```

如果你不打算创建枚举变量，就不需要在声明中使用标签。

请注意，使用按位运算符更改设置会更复杂。例如，考虑将填充颜色设置为青色。仅仅打开蓝色位和绿色位是不够的：

```
box.us_view |= (FILL_BLUE | FILL_GREEN); /* reset fill */
```

问题在于颜色还取决于红色位的设置。如果该位已经设置（对于黄色颜色就是如此），此代码会保留红色位并设置蓝色和绿色位，导致颜色变为白色。解决此问题的最简单方法是先关闭所有颜色位，然后再设置新值。即程序使用以下代码：

```
box.us_view &= ~FILL_MASK;        /* clear fill bits */
box.us_view |= (FILL_BLUE | FILL_GREEN); /* reset fill */
```

为了展示如果不先清除相关位会发生什么，程序还执行了以下操作：

```
box.us_view |= BORDER_RED;        /* wrong approach */
```

由于 BORDER_GREEN 位已经设置，结果颜色为 BORDER_GREEN | BORDER_RED，换算为黄色。

在这种情况下，位域版本更简单：

```
box.st_view.fill_color = CYAN;    /*bit-field equivalent */
```

你不需要先清除位。此外，对于位域成员，你可以使用与填充相同的颜色值用于边框，但对于按位运算符方法，你需要使用不同的值（反映实际位位置的值）。

接下来，比较以下两个打印语句：

```
printf("The border color is %s.\n", colors[pb->border_color]);
printf("The border color is %s.\n", colors[(us >> 9) & 07]);
```

在第一个语句中，表达式 pb->border_color 的值在 0–7 范围内，因此可作为 colors 数组的索引。使用按位运算符获得相同信息更复杂。一种方法是使用 ui >> 9 将边框颜色位右移到值中的最右位置（位 0–2），然后将此值与掩码 07 结合，以便关闭除最右三个位之外的所有位。然后剩下的部分在 0–7 范围内，可作为 colors 数组的索引。

## Caution

位字段与位位置之间的对应关系取决于实现。例如，在旧的 Macintosh PowerPC 上运行清单 15.4 产生以下输出：

```
Original box settings:
Box is opaque.
The fill color is yellow.
Border shown.
The border color is green.
The border style is dashed.

Box settings using unsigned int view:
box is transparent.
The fill color is black.
Border not shown.
The border style is solid.
The border color is black.
```

```
bits are 1011000010101000000000000000000

Modified box settings:
Box is opaque.
The fill color is yellow.
Border shown.
The border color is green.
The border style is dashed.

Box settings using unsigned int view:
box is opaque.
The fill color is cyan.
Border shown.
The border style is dotted.
The border color is red.
bits are 1011000010101000001001000001101
```

代码更改了相同的位，但 Macintosh PowerPC 将结构加载到内存中的方式不同。特别是，它将第一个位字段加载到最高有效位而不是最低有效位。因此，结构表示最终位于前 16 位中（顺序与 PC 版本不同），而无符号整数表示最终位于后 16 位中。因此，清单 15.4 对位位置的假设对于 Macintosh 是不正确的，使用按位运算符更改不透明度和填充颜色设置会更改错误的位。

## Alignment Features (C11)

C11 的对齐功能更像是字节操作而不是位操作，但它们也体现了 C 关联硬件事项的能力。对齐在此上下文中是指对象在内存中的定位方式。例如，为了最高效率，系统可能要求类型为 double 的值存储在能被四整除的内存地址上，但允许 char 存储在任何地址。对大多数程序员来说大多数时间，对齐不是问题。但某些情况可能受益于对齐控制，例如从一个硬件位置向另一个硬件位置传输数据或调用同时操作多个数据项的指令。

_Alignof 运算符给出类型的对齐要求。它通过在 _Alignof 关键字后跟带括号的类型来使用：

```
size_t d_align = _Alignof(float);
```

d_align 的值例如为 4 表示 float 对象具有 4 的对齐要求。这意味着 4 是存储该类型值的连续地址之间的字节数。一般来说，对齐值应为非负的 2 的幂。更大

