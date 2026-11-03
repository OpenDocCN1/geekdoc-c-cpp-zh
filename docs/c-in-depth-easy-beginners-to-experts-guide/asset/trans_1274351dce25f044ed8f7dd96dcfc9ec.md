
在 printf() 中更改成员对输出没有影响。

对象可以被赋给另一个对象，但不能用于其他操作。

```c
3 main()
{
    union a
    {
        int i;
        char ch[2];
    };
    union a z=512;
    printf("%d %d",z.ch[0],z.ch[1]);
}
```

输出：0 2 512 的二进制是 (00000010 00000000)

```c
struct emp
{
    char name[20];
    int age;
};
main()
{
    struct emp e = {"matrix", 30};
    f(e);
}
f(struct emp ee)
{
    printf("%s %d",ee.name,ee.age);
}
```

说明：会发生错误，可以通过在函数 f() 的声明之前声明结构体来纠正。

## Question-结构、联合和枚举之间的相似性是什么？

答案：它们都允许我们定义一种新的数据类型。

## Question-以下声明是否有效：

```c
typedef struct s
{
    int a;
    float b;
}s;
```

答案：是

## Question-结构体可以包含指向自身的指针吗：

答案：可以，这样的结构体被称为自引用结构体。

## Question-指出以下代码中的错误（如有）

```c
typedef struct
{
    int data;
    NODEPTR link;
}*NODEPTR;
```

答案：typedef 为类型定义了一个新的名称，在本例中错误在于 typedef 在被定义之前不能使用。在给定的代码片段中，在声明 link 字段时 typedef 声明尚未定义。

## Question: 如何消除上述问题？

答案：为了解决这个问题，首先必须为结构体命名（"struct node"）。然后将 link 字段声明为简单的 struct node *，如下所示：

```c
typedef struct node
{
    int data;
    struct node *link;
}*NODEPTR;
```

另一种消除问题的方法是将 typedef 声明与结构体定义分离，如下所示：

```c
struct node
{
    int data;
    struct node *link;
};

typedef struct node *NODEPTR;
```

另一种消除问题的方法是在结构体声明之前加上 typedef，在这种情况下应在使用 NODEPTR typedef 声明 link 字段时如下所示：

```c
typedef struct node *NODEPTR;
struct node
{
    int data;
    NODEPTR link;
};
```

在这种情况下，即使 struct node 尚未完全定义，你也可以声明一个涉及 struct node 的新的 typedef 名称；这是允许的。

## Question-

```c
void modify(struct emp*);
struct emp
{
    char name[20];
    int age;
};
main()
{
    struct emp e = {"Sanjay", 35};
    modify(&e);
    printf("%s %d", e.name, e.age);
}
void modify(struct emp *p)
{
    strupr(p->name);
    p->age = p->age + 2;
}
```

答案：struct emp 在函数 modify() 的声明中被提及，而结构体的定义尚未完成。为了解决问题，只需在结构体声明之前或之后声明函数，或在原型前加上语句 struct emp 即可。

## Question-以下代码是否有效：

```c
#include<alloc.h>
struct emp
{
    int len;
    char name[1];
};
main()
{
    char newname[] = "Rahul";
    struct emp *p= (struct emp *) malloc(sizeof(struct emp) - 1 +
    strlen(newname)+1);
    p->len=strlen(newname);
    strcpy(p->name, newname);
    printf("%d %s",p->len, p->name);
}
```

答案：是，该程序为结构体分配空间，并调整大小以使 name 字段能够容纳所请求的名字（而不仅仅是结构体声明所建议的一个字符）。

## Question-上述程序是否有更好的写法？

答案：实现该问题的最佳方法是使用字符指针而不是数组，如下所示：

```c
#include<alloc.h>
struct emp
{
    int len;
    char *name;
};
main()
{
    char newname[] = "Rahul";
    struct emp *p= (struct emp *) malloc(sizeof(struct emp));
    
    p->len=strlen(newname);
    p->name = malloc(p->len + 1);
    strcpy(p->name, newname);
    printf("%d %s",p->len, p->name);
}
```

显然，将长度和字符串存储在同一块内存中的“便利性”现在已经丢失，并且释放该结构体的实例需要两次调用 free() 函数。

## Question-如何释放上述问题中分配的内存？

```c
free(p->name);
free(p);
```

## Question- 以下程序的输出是什么？

```c
main()
{
    struct emp
    {
        char *n;
        int age;
    };
    struct emp e1 = {"David", 23};
    struct emp e2 = e1;
    strupr(e2.n);
    printf("%s\n", e1.n);
}
```

答案：David

当结构体被赋值、传递或返回时，复制是整体进行的。这意味着任何指针字段的副本都指向与原始相同的位置。

换句话说，被指向的内容不会被复制。因此，通过 e2.n 更改名称时，e1.n 也会自动更改。

## Question- 指出以下代码中的错误（如有）：

```c
main()
{
    struct emp
    {
        char n[20];
        int age;
    };
    struct emp e1 = {"David", 23};
    struct emp e2 = e1;
    if(e1 == e2)
        printf("The structures are equal");
}
```

结构不能使用内置的 == 和 != 运算符进行比较。这是因为编译器没有单一、良好的方式来实现结构体比较。对结构体中未使用填充位进行逐字节比较（这种填充用于保持后续字段的对齐正确）。逐字段比较可能需要对大型结构体进行不可接受的重复代码量。此外，任何编译器生成的比较都不可能期望用 strcmp 而不是 == 来比较指针字段。

## Question- 如何检查两个结构体变量的内容是否相同？

答案：

```c
struct emp
{
    char n[20];
    int age;
};
main()
{
    struct emp e1 = {"David", 23};
    struct emp e2;
    scanf("%s %d", e2.n, &e2.age);
    if(structcmp(e1, e2) == 0)
        printf("The structures are equal");
    else
        printf("Structures are unequal");
}
structcmp(struct emp x, struct emp y)
{
    if(strcmp(x.n, y.n) == 0)
        if(x.age == y.age)
            return(0);
    return(1);
}
```

简而言之，如果你需要比较两个结构体，你必须编写自己的函数来执行此操作，该函数按字段逐字段进行比较。

## Question-编译器如何实现结构体的传递和返回？

答案：当结构体作为函数参数传递时，整个结构体通常会被压入栈。为了避免这种开销，许多程序员更喜欢传递指向结构体的指针而不是实际的结构体。结构体通常从函数中返回到由编译器提供的额外“隐藏”参数指向的位置。

## Question- 如何从/向数据文件读写结构体？

答案：要写出结构体，我们可以使用 fwrite()，如下所示：

```c
fwrite(&e, sizeof(e), 1, fp);
```

其中 e 是一个结构体变量。相应的 fread() 调用可以从文件中读取结构体。

调用 fwrite() 时，它会从地址 &e 写出 sizeof(e) 字节。然而，使用 fwrite() 以内存映像形式写入的数据文件将不可移植，特别是如果它们包含浮点字段或指针。这是因为结构体的内存布局取决于机器和编译器。

不同的编译器可能会使用不同数量的填充，并且基本类型的大小和字节顺序在不同机器之间会有所不同。因此，以内存映像形式写入的结构体不一定能被在其他机器上运行的程序（甚至由其他编译器编译的程序）读回，如果你写入的数据文件将来会在机器之间交换，这是一个重要问题。

## Question-如果以下结构体使用 fwrite() 写入文件，fread() 能否成功读回？

```c
struct emp
{
    char *n;
    int age;
};
struct emp e = {"Sujay", 15};
FILE *fp;
fwrite(&e, sizeof(e), 1, fp);
```

答案：不能，因为结构体包含一个 char 指针，使用 fwrite() 将结构体写入磁盘时，只会写入指针 n 中存储的值（而不是它指向的字符串）。当该结构体被读回时，地址会被读回，但很不可能在内存的该地址处存在期望的字符串。

## Question-以下程序是否总是输出结构体大小为 7 字节？

```c
struct ex
{
    char ch;
    int i;
    long int a;
};
```

答案：

否，编译器可能会在结构体中留出空洞，通过为结构体中的第一个字符填充另一个字节，以确保其后的整数存储在偶数位置。
