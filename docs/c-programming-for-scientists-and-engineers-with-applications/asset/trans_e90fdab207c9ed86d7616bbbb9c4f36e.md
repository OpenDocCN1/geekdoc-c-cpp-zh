
```c
/* room1 - 结构变量 */
/* 调用者： */
/*  main  */
/* 使用的文件： */
/*  outfile.dat - 输出数据文件 */
/* *************************************************** */
void funoutput(CUBICLE room1[])
{
    FILE *outptr;
    int i;
    outptr = fopen("outfile.dat", "w");

    for(i = 0; i < ENTRIES; i++) {
        fprintf(outptr, "Room: %d\n", i+1);
        fprintf(outptr,
            "length: %5.2f width: %5.2f height: %5.2f\n\n",
            room1[i].length, room1[i].width, room1[i].height);
        fprintf(outptr,"total wall area: %6.2f\n\n",
            room1[i].areewall);
        fprintf(outptr,"cost to paint walls: %6.2f\n\n",
            room1[i].paintcost);
    }
    fprintf(outptr, "\n\n");

    close(outptr);
    return;
}
```

# 输入与输出

输入数据文件："infile.dat"
20.5 16.5 10.0
30.6 25.4 8.0
45.5 30.0 9.5
16.5 12.8 8.0

输出数据文件："outfile.dat"
Room: 1
length: 20.50 width: 16.50 height: 10.00
total wall area: 740.00
cost to paint walls: 1850.00

Room: 2
length: 30.60 width: 25.40 height: 8.00
total wall area: 896.00
cost to paint walls: 2240.00

Room: 3
length: 45.50 width: 30.00 height: 9.50
total wall area: 1434.50
cost to paint walls: 3586.25

Room: 4
length: 16.50 width: 12.80 height: 8.00
total wall area: 468.80
cost to paint walls: 1172.00

# 章节总结

结构是一种派生数据类型，用于以异构记录的形式存储和处理相关数据。结构可以带标签（tag）或不带标签进行声明，以便为要分配的存储设置模板。标签充当唯一分配给结构的数据类型。一旦声明了结构，就可以声明结构变量来为结构变量的成员分配存储。结构声明的一般形式如下：

```c
struct tagname {
    structure data members;
};
```

结构变量的声明如下：

`struct tagname variable1,variable2,..., variableN;`

一旦声明了结构变量，就会根据结构声明模板为它们分配存储。

结构变量数据成员的值可以通过初始化、赋值、输入或计算来定义。可以使用成员运算符（点符号 `.`）或通过结构变量指针使用解引用和成员运算符（`->`）来访问结构变量的数据成员。可以在结构变量的数值成员上执行所有的算运算。

可以使用 `typedef` 构造为结构数据类型定义别名。实现方法如下：

```c
typedef struct student_record
{
    structure members;
} STUDENT;
```

在这种情况下，STUDENT 是 `struct student_record` 的别名。可以使用别名 STUDENT 代替 `struct student_record` 来声明结构变量。下面的示例显示了这种声明。

`struct student_record var1, var2;`

等于

`STUDENT var1, var2;`

其中 var1 和 var2 是结构变量。

如果两个结构变量具有相同的数据类型，可以将一个结构变量的值赋予另一个结构变量；否则必须逐个成员赋值。

结构变量可以通过值或指针传递给函数。结构变量可以通过返回语句或参数和参数从函数返回。

结构可以嵌套在另一个结构内部。必须先声明嵌套结构，然后声明包含它的外部结构。

结构成员可以是指向相同结构数据类型变量的指针。此类结构被称为自引用结构。它们对于实现链表非常有用。

联合体（union）是一种用于优化存储使用的构造。在这种构造中，联合体只有一个成员是激活的并分配存储的。枚举（Enumeration）用于只能有一少量固定值的数据，例如每个月的名称、原色等。

# 732 结构

# 练习题

1. 使用以下结构编写一个 C 程序，描述圆柱的轴、圆形截面和圆柱。给定长度和半径，计算圆形截面的面积、圆柱的表面积以及圆柱的体积。
```c
struct shape {
    float length;
    float radius;
    float area;
    float volume;
};
```

2. 使用以下结构编写一个 C 程序，存储长度为 $l$ 的柱的压缩负载 $p$ 和直径 $d$。计算柱中的压缩应力和应变。以正确的格式输出负载、直径、应力和应变。
```c
struct strength {
    float p;
    float d;
    float stress;
    float strain;
}
```
使用使用以下公式计算应力和应变：
$area = (\pi d^2)/4$
$stress = p/area$
其中 $E$ 是弹性模量，值为 $30 \times 10^6$ psi。

3. 编写一个 C 程序计算 10 名机器工的周薪，包括 ID、姓名、工作小时和时薪。计算总薪，并从总薪中扣除 25% 得到净工资。输出 ID、姓名、时薪、总薪、扣款额和净工资。超过 40 小时的加班费为时薪的 1.5 倍。按员工组织数据。

4. 编写一个 C 程序计算三个不同模型的库存。每个模型有一定数量的汽车和每辆汽车的价格。计算每个模型所有汽车的总成本。输出模型名称、汽车数量和总成本。按模型组织数据。# 附录 A

**不可打印字符**

| 十进制 | 十六进制 | 二进制 | 字符 |
|---|---|---|---|
| 0 | 0 | 000000 | NUL—空字符 |
| 1 | 1 | 000001 | SOH—正文 (Start of Header) |
| 2 | 2 | 000010 | STX—正文 (Start of Text) |
| 3 | 3 | 000011 | ETX—文本结束 (End of Text) |
| 4 | 4 | 000100 | EOT—传输结束 (End of Transmission) |
| 5 | 5 | 000101 | ENQ—询问 (Enquiry) |
| 6 | 6 | 000110 | ACK—确认 (Acknowledgment) |
| 7 | 7 | 000111 | BELL—铃声 |
| 8 | 8 | 001000 | BS—退格 (Backspace) |
| 9 | 9 | 001001 | HT—水平制表符 (Horizontal Tab) |
| 10 | a | 001010 | LF—换行 (Line Feed) |
| 11 | b | 001011 | VT—垂直制表符 (Vertical Tab) |
| 12 | c | 001100 | FF—分页符 (Form Feed) |
| 13 | d | 001101 | CR—回车 (Carriage Return) |
| 14 | e | 001110 | SO—移出 (Shift Out) |
| 15 | f | 001111 | SI—移入 (Shift In) |
| 16 | 10 | 010000 | DLE—数据转义 (Data Escape) |
| 17 | 11 | 010001 | DC1—控制 1 |
| 18 | 12 | 010010 | DC2—控制 2 |
| 19 | 13 | 010011 | DC3—控制 3 |
| 20 | 14 | 010100 | DC4—控制 4 |
| 21 | 15 | 010101 | NQ—否定确认 (Negative Acknowledge) |
| 22 | 16 | 010110 | SYN—同步 (Synchronization) |
| 23 | 17 | 010111 | ETB—块结束 (End of Block) |
| 24 | 18 | 011000 | CAN—取消 (Cancel) |
| 25 | 19 | 011001 | EM—媒介结束 (End of Medium) |
| 26 | la | 011010 | SUB—替换 (Substitute) |
| 27 | 1b | 011011 | ESC—转义符 (Escape) |
| 28 | 1c | 011100 | FS—文件分隔符 (File Separator) |
| 29 | 1d | 011101 | GS—分组分隔符 (Group Separator) |
| 30 | 1e | 011110 | RS—记录分隔符 (Record Separator) |
| 31 | 1f | 011111 | US—单元分隔符 (Unit Separator) |
| 127 | 7f | 1111111 | DEL—删除 |

# ASCII 字符

| 十进制 | 十六进制 | 二进制 | 字符 |
|---|---|---|---|
| 32 | 20 | 010000 | 空格 |
| 33 | 21 | 010001 | ! |
| 34 | 22 | 010010 | " |
| 35 | 23 | 010011 | # |
| 36 | 24 | 010100 | $ |
| 37 | 25 | 010101 | % |
| 38 | 26 | 010110 | & |
| 39 | 27 | 010111 | . |
| 40 | 28 | 010100 | ( |
| 41 | 29 | 010101 | ) |
| 42 | 2a | 010110 | * |
| 43 | 2b | 010111 | + |
| 44 | 2c | 011100 | , |
| 45 | 2d | 011101 | - |
