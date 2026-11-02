

## 7.9.2 指针/索引表示法

指针可以像数组一样被索引。如果 `bPtr` 的值为 `b`，则表达式 `bPtr[1]` 引用数组元素 `b[1]`。这称为指针/索引表示法。

## 7.9.3 不能用指针算术修改数组名

记住，数组名始终指向数组的开头，因此数组名就像常量指针。因此，表达式

```c
b += 3
```

无效，因为它试图用指针算术修改数组名的值。

> **常见编程错误 7.10**
> *试图用指针算术修改数组名的值是一种编译错误。*

## 7.9.4 演示指针索引和偏移量

图7.20使用我们讨论过的四种引用数组元素的方法——数组索引、以数组名作为指针的指针/偏移量、指针索引，以及使用指针的指针/偏移量——来打印整型数组 `b` 的四个元素。

```c
// Fig. 7.20: fig07_20.cpp
// Using indexing and pointer notations with arrays.
#include <stdio.h>
#define ARRAY_SIZE 4

int main(void)
{
    int b[] = {10, 20, 30, 40}; // create and initialize array b
    int *bPtr = b; // create bPtr and point it to array b

    // output array b using array index notation
    puts("Array b printed with:\nArray index notation");

    // loop through array b
    for (size_t i = 0; i < ARRAY_SIZE; ++i) {
        printf("b[%zu] = %d\n", i, b[i]);
    }

    // output array b using array name and pointer/offset notation
    puts("\nPointer/offset notation where\n"
        "the pointer is the array name");

    // loop through array b
    for (size_t offset = 0; offset < ARRAY_SIZE; ++offset) {
        printf("*(b + %zu) = %d\n", offset, *(b + offset));
    }

    // output array b using bPtr and array index notation
    puts("\nPointer index notation");

    // loop through array
    for (size_t i = 0; i < ARRAY_SIZE; ++i) {
        printf("bPtr[%zu] = %d\n", i, bPtr[i]);
    }

    // output array b using bPtr and pointer/offset notation
    puts("\nPointer/offset notation");

    // loop through array b
    for (size_t offset = 0; offset < ARRAY_SIZE; ++offset) {
        printf("*(bPtr + %zu) = %d\n", offset, *(bPtr + offset));
    }
}
```

```
Array b printed with:
Array index notation
b[0] = 10
b[1] = 20
b[2] = 30
b[3] = 40

Pointer/offset notation where
the pointer is the array name
*(b + 0) = 10
*(b + 1) = 20
*(b + 2) = 30
*(b + 3) = 40

Pointer index notation
bPtr[0] = 10
bPtr[1] = 20
bPtr[2] = 30
bPtr[3] = 40

Pointer/offset notation
*(bPtr + 0) = 10
*(bPtr + 1) = 20
*(bPtr + 2) = 30
*(bPtr + 3) = 40
```

**图 7.20** | 使用索引和指针表示法处理数组。

## 7.9.5 用数组和指针复制字符串

为了进一步说明数组和指针的可互换性，让我们看看图7.21程序中的两个字符串复制函数——`copy1`和`copy2`。两个函数都将字符串复制到字符数组中。比较`copy1`和`copy2`的函数原型后，这两个函数看起来完全相同。它们完成相同的任务，但实现方式不同。

```c
// Fig. 7.21: fig07_21.c
// Copying a string using array notation and pointer notation.
#include <stdio.h>
#define SIZE 10

void copy1(char * const s1, const char * const s2); // prototype
void copy2(char *s1, const char *s2); // prototype

int main(void)
{
    char string1[SIZE]; // create array string1
    char *string2 = "Hello"; // create a pointer to a string

    copy1(string1, string2);
    printf("string1 = %s\n", string1);

    char string3[SIZE]; // create array string3
    char string4[] = "Good Bye"; // create an array containing a string

    copy2(string3, string4);
    printf("string3 = %s\n", string3);
}

// copy s2 to s1 using array notation
void copy1(char * const s1, const char * const s2)
{
    // loop through strings
    for (size_t i = 0; (s1[i] = s2[i]) != '\0'; ++i) {
        ; // do nothing in body
    }
}

// copy s2 to s1 using pointer notation
void copy2(char *s1, const char *s2)
{
    // loop through strings
    for ( ; (*s1 = *s2) != '\0'; ++s1, ++s2) {
        ; // do nothing in body
    }
}
```

```
string1 = Hello
string3 = Good Bye
```

**图 7.21** | 使用数组表示法和指针表示法复制字符串。

### 使用数组索引表示法复制

函数`copy1`使用数组索引表示法将`s2`中的字符串复制到字符数组`s1`。该函数将计数器变量`i`定义为数组索引。`for`语句头（第28行）执行整个复制操作——其循环体是空语句。语句头指定`i`初始化为零，并在循环的每次迭代中加一。表达式`s1[i] = s2[i]`从`s2`复制一个字符到`s1`。当在`s2`中遇到空字符时，它被赋给`s1`，而赋值表达式的值变成赋给左操作数（`s1`）的值。当空字符从`s2`赋给`s1`时（假），循环终止。

### 使用指针和指针算术复制

函数`copy2`使用指针和指针算术将`s2`中的字符串复制到字符数组`s1`。同样，`for`语句头（第37行）执行整个复制操作。该语句头不包含任何变量初始化。与函数`copy1`一样，表达式`(*s1 = *s2)`执行复制操作。指针`s2`被解引用，得到的字符被赋给解引用后的指针`s1`。在条件中赋值之后，两个指针分别递增，以指向数组`s1`中的下一个字符和字符串`s2`中的下一个字符。当在`s2`中遇到空字符时，它被赋给解引用后的指针`s1`，循环终止。

### 关于函数 copy1 和 copy2 的说明

*`copy1`和`copy2`的第一个实参必须是一个足够大的数组，以容纳第二个实参中的字符串。* 否则，当试图写入不属于该数组的内存位置时，可能会发生错误。此外，每个函数的第二个形参都声明为`const char * const`（一个常量字符串）。在这两个函数中，第二个实参被复制到第一个实参中——一次从中读取一个字符，但从不修改这些字符。因此，第二个形参被声明为指向常量值，以便强制执行最小权限原则——这两个函数都不需要修改第二个实参中字符串的能力。

## 7.10 指针数组

数组可以包含指针。指针数组的一种常见用途是构成字符串数组，简称为字符串数组。数组中的每一项都是一个字符串，但在C中，字符串本质上是指向其第一个字符的指针。因此，字符串数组中的每一项实际上是指向某个字符串第一个字符的指针。考虑字符串数组`suit`的定义，它在表示一副扑克牌时可能有用。

```c
const char *suit[4] = {"Hearts", "Diamonds", "Clubs", "Spades"};
```

定义中的`suit[4]`部分表示一个包含4个元素的数组。声明中的`char *`部分表示数组`suit`的每个元素都是“指向char的指针”类型。限定符`const`表示每个元素所指向的字符串不会被修改。要放入数组的四个值是`"Hearts"`、`"Diamonds"`、`"Clubs"`和`"Spades"`。每个值在内存中都存储为*以空字符结尾的字符串*，它比引号之间的字符数多一个字符。这四个字符串的长度分别为7、9、6和7个字符。尽管看起来这些字符串被放入了`suit`数组，但实际上数组中只存储了指针（图7.22）。每个指针指向其对应字符串的第一个字符。因此，尽管`suit`数组的*大小固定*，它却提供了对*任意长度*字符的访问。这种灵活性是C强大的数据结构能力的一个例子。

这些花色本可以放在一个二维数组中，其中每一行表示一种花色，每一列表示花色名称中的一个字母。这样的数据结构每行必须有固定的列数，而这个数量

