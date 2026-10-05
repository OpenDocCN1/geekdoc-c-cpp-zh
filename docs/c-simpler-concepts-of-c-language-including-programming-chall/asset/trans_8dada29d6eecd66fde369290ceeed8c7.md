

## 100 简化 C 

(I) i = &a;
(II) f = &b;
(III) c = NULL;

(I) 将指针 i 初始化为变量 a 的地址。
(II) 将指针 f 初始化为变量 b 的地址。
(III) 将指针 c 初始化为值 NULL。

> 任何类型的指针都可以赋值为值 NULL。这种指针被称为空指针（NULL pointer）。

以下图视化了上述声明和初始化。

![](img/5bbdccabcf90cef7ee48b1b48eaa187d_111_0.png)

图 7.1 已初始化指针的行为

在声明时就将指针变量赋值为 `NULL` 始终是一个良好的习惯。如果没有赋值为 `NULL`，那么指针变量将持有内存空间中的一个随机地址，这并不是我们期望的特性。考虑以下声明：

```
int *p;
```

未初始化指针 p 的行为如图 7.2 所示。

![](img/5bbdccabcf90cef7ee48b1b48eaa187d_111_1.png)

图 7.2 未初始化指针的行为

## 未初始化术语的影响

在编程中，未初始化的指针被称为“坏指针”（bad pointer）。这是因为使用此类指针的影响可能是剧性的。它可能会停止程序的执行，甚至可能损坏某些内存地址。因此，请小心使用此类指针。

## 指针

### 访问指针变量的内容

普通变量可以通过其名称直接访问。指针变量通过在前面加一个星号 `*` 来访问。例如（假设声明 `int *p`）`printf("%u",p);` —— 该语句打印指针变量 p 的内容，因为 p 是指针变量，它应该包含一个地址。在打印地址时，可以使用地址说明符 `%u`（用于无符号整数）。

注意：要打印指针变量的内容，请使用 `*`。要打印任何变量的地址，使用 `&`。`*` 也称为取值运算符，而 `&` 是取地址运算符。

以下程序演示了上述指针概念。随程序之后是程序 7.1 的输出。

```
#include<stdio.h>
void main(){
    int var=20;
    int *p=NULL;//指向空；'NULL'指针
    char *c=0;
    float *f=NULL;//指向 var
    p=&var;
    printf("%d (directly printing)",var);
    printf("\n%d (printing using pointer)",*p);
    printf("\naddress of var is %u",&var);
    printf("\naddress of pointer p is %u",&p);
    printf("\naddress of pointer c is %u",&c);
    printf("\naddress of pointer f is %u",&f);
    getch();}
```

## 程序 7.1 间接运算符与引用运算符的使用

```
var=20 (directly printing)
var=20 (printing using pointer)
address of var is 2686784
address of pointer p is 2686784
address of pointer c is 2686780
address of pointer f is 2686776
```

## 输出 7.1

从输出 7.1 可以观察到，指针变量地址之间的差异为 4：这是因为任何类型的指针变量只占用 4 字节。无论是 char、int 还是 float 或 double，这种情况都适用。

## 7.2. 多级间接

人们可以根据指针类型多次应用任何运算符。如果只是简单的指针，则只能使用一个间接运算符。还有其他类型的指针，例如：

- *指向指针的指针（2 级）*
- **指向指针的指针再次指向另一个指针（3 级）**
- 依此类推。

2 级指针使用 2 个 `*`，3 级指针使用 3 个星号。程序 7.2 使用了这两种类型的指针。在查看程序之前，请看下方的图。

![](img/5bbdccabcf90cef7ee48b1b48eaa187d_113_0.png)

图 7.2 多级间接

```
#include<stdio.h>
void main()
{
    int var=20;
    int *p;
    p=&var;
    int **p1;
    p1=&p;
    int ***p2;
    p2=&p1;
    printf("\naddress of var : %u",&var);
    printf("\ncontent of p : %u",*p);
    printf("\naddress of p : %u",&p);
    printf("\ncontent of p1 : %u",*p1);
    printf("\nvar= %d (printing directly)",var);
    printf("\nvar= %d (printing using p1)",**(p1));
    printf("\nvar= %d (printing using p2)",*(*(p2)));
    getch();
}
```

程序 7.2 双级、三级间接运算符

## 指针

address of var : 2686784
content of p : 20
address of p : 2686784
content of p1 : 20
var= 20 (printing directly)
var= 20 (printing using p1)
var= 20 (printing using p2)

## 7.3. 指针之间的兼容性

在编程中，未初始化的指针被称为“坏指针”。这是因为使用此类指针的影响可能是剧性的。它可能会停止程序的执行，甚至可能损坏某些内存地址。因此，请小心使用此类指针。

注意：要打印指针变量的内容，请使用 `*`。要打印任何变量的地址，使用 `&`。`*` 也称为取值运算符，而 `&` 是取地址运算符。

（注：原文中存在大量重复段落，已按要求仅翻译逻辑，未重复输出）

