

# 678 结构

```c
float   unitcost;
float   totcost;
}parts[10];
```

这两个声明是等价的。在两种情况下，数组变量 `parts[10]` 都是一个包含 10 个相同异构数据类型元素的数组。当未指定结构标签时，必须在结构声明中同时声明数组，因为没有设置存储模板。

当结构已经赋予了一个数据类型名称时，可以在结构声明之后，通过单独的声明语句来声明数组。以下代码展示了在单独语句中声明结构变量。

```c
struct gadgetpart {
    char    partname[10];
    int     count;
    float   unitcost;
    float   totalcost;
};
```

struct gadgetpart parts[10];

注意，首先声明了结构，然后在结构声明之后的单独语句中声明了数组。要像所示那样在单独语句中声明结构变量，必须在结构声明中包含结构标签。

为结构数组 `parts[10]` 分配的存储如下：

| | partname | count | unitcost | totalcost |
|---|---|---|---|---|
| parts[0] | 10 bytes | 4 bytes | 4 bytes | 4 bytes |
| parts[1] | | | | |
| parts[3] | | | | |
| parts[4] | | | | |
| parts[9] | | | | |

一旦数组分配了存储，成员的值就可以像单个变量一样进行存储和操作。可以使用成员运算符或结构变量指针来访问结构变量的成员。结构数组的操作方式也是相同的。

## 11.1.3 结构成员运算符和指针运算符

在使用其他方式之前，必须访问结构变量成员并对其进行初始化。结构变量成员可以在声明时初始化，也可以通过赋值语句或数据输入进行初始化。以下演示了使用成员运算符和结构变量指针访问结构成员。

### 结构成员运算符 使用成员运算符（.）可以访问结构变量的成员。以下代码展示了成员运算符的使用。

```c
struct gadgetpart {
    char pname[10];
    int count;
    float unitcost;
    float totalcost;
};

struct gadgetpart part;
part.partname
part.count
part.unitcost
part.totalcost
```

存储分配如下：

| | pname | count | unitcost | totalcost |
|---|---|---|---|---|
| part | 10 bytes | 4 bytes | 4 bytes | 4 bytes |

注意，变量名后是成员运算符，然后是结构成员名。每一个 `part.partname`、`part.count`、`part.unitcost` 和 `part.totalcost` 都像单个变量一样被使用。唯一的区别是每个结构成员都被识别为属于结构变量 `part`。

以下示例展示了如何使用成员运算符为结构变量成员赋值。

```c
strcpy(part.partname, "bolt");
part.count = 20;
part.unitcost = 0.25;
part.totalcost = part.count * part.unitcost;
```

注意，在每个赋值语句中，左侧都由结构变量 `part` 的成员和成员运算符（.）组成。由于 `name` 是字符字符串数组，不能直接向其赋值字符串；而是使用字符串拷贝函数 `strcpy` 将字符串 "bolt" 拷贝到字符串成员 `name` 中。成员 `count`、`unitcost` 和 `totalcost` 是数值；使用赋值语句为它们分配数值。

存储值如下：

| part.name | part.count | part.unitcost | part.totalcost |
| --- | --- | --- | --- |
| bolt | 20 | 0.25 | 5.00 |
| 10 bytes | 4 bytes | 4 bytes | 4 bytes |

结构变量也可以在声明时按所示初始化：
`struct gadgetpart part1 = {"bolt", 20, 0.25, 5.0};`

### 变量指针 指向结构变量的指针包含分配给它的存储内存地址。指针的值是分配给结构变量存储第一个字节的地址。结构变量和结构指针都可以在结构声明之后声明。以下代码展示了结构变量和结构指针的声明。

结构声明：

```c
struct gadgetpart {
    char partname[10];
    int count;
    float unitcost;
    float totalcost;
};
```

结构变量声明：

```c
struct gadgetpart part1, part2, part3, part4[10];
```

结构指针声明：

```c
struct gadgetpart *ptr1, *ptr2, *ptr3, *ptr4;
```

其中 `ptr1`、`ptr2`、`ptr3` 和 `ptr4` 是指向 `gadgetpart` 类型结构变量的指针。结构变量 `part1`、`part2` 和 `part4[10]` 的地址可以分别赋予结构指针 `ptr1`、`ptr2`、`ptr3` 和 `ptr4`。以下代码展示将结构变量 `part1` 的地址赋值给 `ptr1`。

```c
ptr1 = &part1;
```

结构变量 `part1` 的存储及其指针访问如下：

![](img/8356e6c3bfe3b10)

| | partname | count | unitcost | totalcost |
|---|---|---|---|---|
| part1 | bolt | 20 | 0.25 | 5.00 |
| | 10 bytes | 4 bytes | 4 bytes | 4 bytes |

（注：此处原文表格似乎似乎存在混乱，翻译根据语意调整）

