
递增指针以指向数组中的下一个位置。以下任一语句

```
--vPtr;
vPtr--;
```

递减指针以指向数组的上一元素。

### 7.8.6 从另一个指针中减去一个指针

指针变量可以相互相减。例如，如果 vPtr 包含位置 3000，而 v2Ptr 包含地址 3008，则语句

```
x = v2Ptr - vPtr;
```

会将从 vPtr 到 v2Ptr 的数组元素个数赋给 x，在本例中为 2（不是 8）。除非在数组上执行，否则指针算术是未定义的。我们不能假设同一类型的两个变量在内存中是连续存储的，除非它们是数组的相邻元素。

**常见编程错误 7.6**
减去不引用同一数组元素的两个指针。

### 7.8.7 指针之间的赋值

如果两者具有相同的类型，则可以将一个指针赋给另一个指针。此规则的例外是 void 指针（即 void *），它是一种通用指针，可以表示任何指针类型。所有指针类型都可以赋给 void 指针，而 void 指针可以赋给任何类型的指针（包括另一个 void 指针）。在这两种情况下，都不需要强制类型转换操作。

### 7.8.8 void 指针

void 指针不能被解引用。考虑以下情况：编译器知道在具有 4 字节整数的机器上，指向 int 的指针引用 4 字节内存，但 void 指针仅包含未知数据类型的内存位置——指针所引用的确切字节数编译器并不知晓。编译器必须知道数据类型才能确定引用值所代表的字节数。

**常见编程错误 7.7**
如果两者都不是 void * 类型，将一种类型的指针赋给另一种类型的指针是语法错误。

**常见编程错误 7.8**
解引用 void * 指针是语法错误。

### 7.8.9 比较指针

指针可以使用相等和关系运算符进行比较，但除非指针指向同一数组的元素，否则此类比较毫无意义。指针比较比较指针中存储的地址。对指向同一数组中元素的两个指针进行比较可以显示，例如，一个指针指向的数组元素编号高于另一个指针。指针比较的常见用途是确定指针是否为 NULL。

![](img/bf54db922e6fa8319cba11069e785521_324_0.png)

> 常见编程错误 7.9
> 比较不引用同一数组元素的两个指针。

## 7.9 指针与数组的关系

在 C 语言中，数组和指针密切相关，通常可以互换使用。数组名可以被视为一个常量指针。指针可用于执行涉及数组索引的任何操作。

假设以下定义：

```
int b[5];
int *bPtr;
```

由于数组名 b（不带索引）是指向数组第一个元素的指针，因此我们可以使用语句将 bPtr 设置为数组 b 第一个元素的地址

```
bPtr = b;
```

此语句等效于按如下方式获取数组 b 第一个元素的地址：

```
bPtr = &b[0];
```

### 7.9.1 指针/偏移量表示法

数组元素 b[3] 可以通过指针表达式另行引用

```
*(bPtr + 3)
```

表达式中的 3 是指针的偏移量。当 bPtr 指向数组的第一个元素时，偏移量指示要引用的数组元素，并且偏移量值与数组索引相同。这种表示法称为指针/偏移量表示法。括号是必要的，因为 * 的优先级高于 +。如果没有括号，上面的表达式将向表达式 *bPtr 的值添加 3（即，如果 bPtr 指向数组开头，则向 b[0] 添加 3）。与数组元素可以用指针表达式引用一样，地址

```
&b[3]
```

可以用指针表达式写成

```
bPtr + 3
```

数组本身可以被视为指针并用于指针算术。例如，表达式

```
*(b + 3)
```

也引用数组元素 b[3]。一般来说，所有带索引的数组表达式都可以用指针和偏移量来写。在这种情况下，使用数组名作为指针使用了指针/偏移量表示法。前面的语句不会以任何方式修改数组名；b 仍然指向数组中的第一个元素。

### 7.9.2 指针/索引表示法

指针可以像数组一样进行索引。如果 bPtr 的值为 b，则表达式

```
bPtr[1]
```

引用数组元素 b[1]。这称为指针/索引表示法。

### 7.9.3 不能使用指针算术修改数组名

请记住，数组名始终指向数组的开头——因此数组名就像一个常量指针。因此，表达式

```
b += 3
```

无效，因为它试图使用指针算术修改数组名的值。

> **常见编程错误 7.10**
> 
> *尝试使用指针算术修改数组名的值会导致编译错误。*

### 7.9.4 演示指针索引和偏移量

图 7.20 使用了我们讨论过的四种引用数组元素的方法——数组索引、指针/偏移量（数组名作为指针）、指针索引和指针/偏移量（使用指针）——来打印整数数组 b 的四个元素。

```
1  // Fig. 7.20: fig07_20.cpp
2  // Using indexing and pointer notations with arrays.
3  #include <stdio.h>
4  #define ARRAY_SIZE 4
5
6  int main(void)
7  {
8      int b[] = {10, 20, 30, 40}; // create and initialize array b
9      int *bPtr = b; // create bPtr and point it to array b
10
11     // output array b using array index notation
12     puts("Array b printed with:\nArray index notation");
13
14     // loop through array b
15     for (size_t i = 0; i < ARRAY_SIZE; ++i) {
16         printf("b[%u] = %d\n", i, b[i]);
17     }
18
19     // output array b using array name and pointer/offset notation
20     puts("\nPointer/offset notation where\n" "the pointer is the array name");
21
22     // loop through array b
23     for (size_t offset = 0; offset < ARRAY_SIZE; ++offset) {
24         printf("*(b + %u) = %d\n", offset, *(b + offset));
25     }
26     }
```

```
// output array b using bPtr and array index notation
puts("\nPointer index notation");
// loop through array b
for (size_t i = 0; i < ARRAY_SIZE; ++i) {
    printf("bPtr[%u] = %d\n", i, bPtr[i]);
}
// output array b using bPtr and pointer/offset notation
puts("\nPointer/offset notation");
// loop through array b
for (size_t offset = 0; offset < ARRAY_SIZE; ++offset) {
    printf("*(bPtr + %u) = %d\n", offset, *(bPtr + offset));
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

Fig. 7.20 | Using indexing and pointer notations with arrays. (Part 2 of 2.)

### 7.9.5 使用数组和指针进行字符串复制

为了进一步说明数组和指针的可互换性，让我们看看图 7.21 程序中的两个字符串复制函数——copy1 和 copy2。两个函数都将字符串复制到字符数组中。在比较 copy1 和 copy2 的函数原型后，函数看起来相同。它们完成相同的任务，但实现方式不同。

```
1 // Fig. 7.21: fig07_21.c
2 // Copying a string using array notation and pointer notation.
3 #include <stdio.h>
4 #define SIZE 10
5
6 void copy1(char * const s1, const char * const s2); // prototype
7 void copy2(char *s1, const char *s2); // prototype
8
9 int main(void)
10 {
11     char string1[SIZE]; // create array string1
12     char *string2 = "Hello"; // create a pointer to a string
13
14     copy1(string1, string2);
15     printf("string1 = %s\n", string1);
16
17     char string3[SIZE]; // create array string3
18     char string4[] = "Good Bye"; // create an array containing a string
19
20     copy2(string3, string4);
21     printf("string3 = %s\n", string3);
22 }
23
24 // copy s2 to s1 using array notation
25 void copy1(char * const s1, const char * const s2)
26 {
27     // loop through strings
28     for (size_t i = 0; s1[i] = s2[i] != '\0'; ++i) {
29         ; // do nothing in body
30     }
31 }
32
33 // copy s2 to s1 using pointer notation
34 void copy2(char *s1, const char *s2)
35 {
36     // loop through strings
37     for ( ; (*s1 = *s2) != '\0'; ++s1, ++s2) {
38         ; // do nothing in body
39     }
40 }
```

string1 = Hello
string3 = Good Bye

## Fig. 7.21 | Copying a string using array notation and pointer notation.

## 使用数组索引表示法进行复制

函数 copy1 使用数组索引表示法将 s2 中的字符串复制到字符数组 s1。函数将计数器变量 i 定义为数组索引。for 语句头（第 28 行）执行整个复制操作——其主体为空语句。头指定 i 初始化为零，并在循环的每次迭代中递增一。表达式 s1[i] = s2[i] 将一个字符从 s2 复制到 s1。当空字符
