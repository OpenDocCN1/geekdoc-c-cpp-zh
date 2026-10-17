
# C 示例：50 多个示例 (C 教程书籍 1)

![](img/c2ccd27e9fcde6057069b8c0a6bb628d_0_0.png)

# 作者的话

非常感谢你的购买，以及你对学习奇妙编程语言的兴趣。“C示例”包含了超过 30 个功能完全、易于使用且独特的示例。不需要具备先前的编程知识，不过有之前的知识大有裨益。唯一的要求是耐心、投入和对学习的热情。不过，为了不让你对学习 C 产生望步，我将解释如何创建、编译和运行一个“c”源文件。

为了创建一个可编辑的“c”源文件，你首先需要选择一个文本编辑器，我将使用 `emacs`。所以要创建一个“c”源文件，在你的终端输入以下命令：

```
emacs SourceFile.c
```

然后使用以下命令进行编译：

```bash
gcc -o SourceFile SourceFile.c
```

然后使用以下命令运行你的文件：

```bash
./SourceFile
```

本书以易于理解的方式介绍新话题，然后使用新话题以及之前讨论的话题来编写程序，以便在复习的同时学习新材料。这有助于你最大化地学习一门新语言。有很多东西需要学习，熟能生巧。让我们开始吧。

谢谢

```c
#include <stdio.h> // 头文件，包含了输入和输出
// 这样我们可以在下面使用 printf
// 如何设置 .c 文件。这只是为了测试
// 确保你的环境已正确设置。
int main() { // 运行程序时发生了什么
    printf("Hello World!\n"); // \n 是换行符，它将内容置于新行
    return 0; // 表示无错误
}
```

输出: Hello World!

```c
#include <stdio.h>
/* C语言中可用的数据类型。
注意 sizeof() 函数，它返回数据类型的大小（字节）。%lu 是一个存储无符号长整型的占位符。这里列出了许多类型：char, int, float 和 double。 */
```

输出: char 的存储大小: 1 字节

int 的存储大小: 4 字节

float 的存储大小: 4 字节

long 的存储大小: 8 字节

```c
#include <stdio.h>
/* 显示如何声明和初始化变量。多次声明是合法的，只需分行即可。你可以对相似的数据类型执行操作。将变量初始化为某个值。 */
int main(){
    char x; // 变量声明
    x = 't'; // 初始化变量
    // 注意这里有 printf
    int x, y, z; // 同一行的多个声明
    x = 3;
    y = 2;
    z = x+y;
    printf("z: %d\n", z);
    return 0;
}
```

输出: z: 5

```c
#include <stdio.h>
/* C 中的基础运算符。当你执行操作时，运算符必须是相同的数据类型。运算符包括算术、关系和赋值运算符。这些都是我们需要的。 */
int main() {
    int x, y;
    x = 2;
    y = 2;

    /* 算术运算符*/
    printf("2 + 2: %d\n", x+y);
    printf("2 - 2: %d\n", x-y);
    printf("2 * 2: %d\n", x*y);
    printf("2 / 2: %d\n", x/y);
    x++; // 同于 x + 1
    printf("++: %d\n", x);
    y--; // 同于 y - 1
    printf("--: %d\n", y);
    int m = 3%2;// 返回余数
    printf("modulus: %d\n", m);

    /* 关系运算符*/
    // 0（表示假）或 1（表示真）
    printf("2 == 2: %d\n", x==y);//不是赋值，是比较
    printf("2 != 1: %d\n", x!=y);//感叹运算符
    printf("2 > 2: %d\n", x>y);//将返回 0
    printf("2 >= 2: %d\n", x>=y);
    printf("2 < 2: %d\n", x<y);
    printf("2 <= 2: %d\n", x<=y);

    /* 赋值运算符*/
    printf("x += y: %d\n", x+=y);//x = x+y
    printf("x: %d\n", x);//x=4
    printf("x -= y: %d\n", x-=y);//x = x-y x:2
    printf("x: %d\n", x);//x=2
    printf("x *= y: %d\n", x*=y);//x = x*y x:4
    printf("x: %d\n", x);//x=4
    printf("x /= y: %d\n", x/=y);//x = x/y x:2
    printf("x: %d\n", x);//x=2
    printf("x %%= y: %d\n", x%=y);//x = x%y
    // 需要两个符号来打印 %
    printf("x: %d\n", x);

    return 0;
}
```

输出:

2 + 2 : 4

2 - 2 : 0

2 * 2 : 4

2 / 2 : 1

++ : 3

-- : 1

modulus : 1

2 == 2 : 1

2 != 2 : 0

2 > 2 : 0

2 >= 2 : 1

2 < 2 : 0

2 <= 2 : 1

x += y: 4
x: 4
x -= y: 2
x: 2
x *= y: 4
x: 4
x /= y: 2
x: 2
x %= y: 0
x: 0

```c
#include <stdio.h>
/* 演示 if 语句和决策。if 语句控制程序的流程（决定运行哪些代码）。 */
int main() {
    int x = 1;
    int y = 2;

    if(x==y) { // 如果语句通过
        printf("Passed the if statement\n");
    } else if(x!=y) { // 如果此通过且之前的失败
        printf("x was changed...\n");
    } else{ // 如果全部失败
        printf("in else statement\n");
    }

    printf("x: %d\n",x);

    return 0;
}
```

```c
#include<stdio.h>
#include<stdlib.h>
#include<time.h>
/*
作者 | 邮箱 | 日期
CoinFlip: 通过随机数生成模拟抛硬币。随机数生成使用时间，因此我们需要导入 time.h 和 stdlib.h。随机数让你的程序更有趣。
*/
int main() {

    srand(time(0));
    int r = rand()%2 + 1;//给了我们一个 [1,2] 的范围

    if (r == 1) 
        printf("Heads\n");
    else
        printf("Tails\n");

    return 0;
}
```

输出1: Heads

Output2: Heads

Output3: tails

```c
#include <stdio.h>
/* DoEasy | 邮箱]|[日期]
逻辑运算符: 逻辑运算符包括与运算符 `&&`。或运算符 `||`，以及感叹/非运算符 `!`。感叹运算符允许你反转一个语句，它产生相反的结果。逻辑运算符允许你将真/假语句链在一起。
*/
int main(){
    int a, b, c;
    a = 100;
    b = 100;
    c = 99;
    if (a == b && a != c){ // 如果此通过
        printf("&& returns: %d\n", (a==b && a != c));
    }
    else if(a == b || a == c){ // 如果此通过且之前的失败
        printf("|| returns: %d\n", (a==b || a == c));
    }else{ // 如果全部失败
        printf("No check passed :\n");
    }

    return 0;
}
```

/*

作者 | 邮箱 | 日期

TernaryOperator: 三元运算符基本上是 if 块的简写。它们也被称为运算符。

*/

```c
int main() {

int number = 99;//这个数字可以是任何值

int outcome;
//以下是代码的简写：
//if 99%2 等于 0 outcome = 1
//else outcome = 0
outcome = (99%2 == 0) ? 1 : 0;
printf("outcome: %d\n",outcome);
// 这是一个测试，用于检查 number 是
//奇数还是偶数，如果 number 能被
// 2 整除（余数为 0）那么它就是
//偶数

}
```

# 输出:

outcome: 0

```c
#include<stdio.h>
#include<stdlib.h>
#include<time.h>
/*
Switch: 如何在 C 中使用 switch 语句。
switch 语句本质上是 if 块，
但它们根据某些条件进行切换。我们还将
学习如何生成随机数来
让我们的程序更加生动。
*/

```c

int main(){

//我们将模拟掷骰子

//让我们在 0 & 6 之间创建一个随机数

rand(time(0));

int number = rand()%6+1;

//number 现在介于 1 和 6 之间

//所以我们必须调整下面的内容使其处于正确的范围内

//让我们声明 switch 语句

switch(number){

case 1:

printf("You rolled a One!\n");

break;

case 2:

printf("You rolled a Two\n");

break;

case 3:

printf("You rolled a Three\n");

break;

case 4:

printf("You rolled a Four\n");

break;

case 5:

printf("You rolled a Five\n");

break;

case 6:

printf("You rolled a Six\n");

break;

}

}

```

# 输出:

You rolled a Two


```c

#include <stdio.h>

/*

[作者] | [邮箱] | [日期]

Loops: 概述循环的类型。有 for、while 和 do while 循环，虽然没有介绍 do while 循环，因为它们与 while 循环非常相似，唯一的例外是，

循环

体被保证

至少执行一次。

*/

```c
int main(){
}
```

```c
/*为了设置一个循环，我们必须初始化某种计数器
变量，然后我们必须设置一个条件在每次运行时进行测试，
然后我们需要某种步进方式来让 for 循环继续运行。
*/
for(int i=0; i<=10;i++){//初始化，条件，步进
printf("i : %d \n",i);
}
```

```c
//乘法表
//这被称为嵌套循环
for(int i=1; i<=12;i++){
for(int j=1; j<=12; j++) {
printf("%d \n",i*j);//将运行 144 次
}
printf("\n");
}
```

```c
//while 循环适用于你不知道循环
//将运行多长时间
int x = 0;
while(x<10){
printf("xx : %d \n", x);
x //注意无限循环，注释掉以查看
//会发生什么...用 ctrl+c 终止
}
return 0;
}
```

# 输出:

i: 0

i: 1

i: 2

i: 3

i: 4

i: 5

i: 6

i: 7

i: 8

i: 9

i: 10

1 2 3 4 5 6 7 8 9 10 11 12

2 4 6 8 10 12 14 16 18 20 22 24

3 6 9 12 15 18 21 24 27 30 33 36

4 8 12 16 20 24 28 32 36 40 44 48

5 10 15 20 25 30 35 40 45 50 55 60

6 12 18 24 30 36 42 48 54 60 66 72

7 14 21 28 35 42 49 56 63 70 77 84

8 16 24 32 40 48 56 64 72 80 88 96

9 18 27 36 45 54 63 72 81 90 99 108

10 20 30 40 50 60 70 80 90 100 110 120

11 22 33 44 55 66 77 88 99 110 121 132

12 24 36 48 60 72 84 96 108 120 132 144

x: 0

x: 1

x: 2

x: 3

x: 4

x: 5

x: 6

x: 7

x: 8

x: 9

```c
#include <stdio.h>
/*
[作者] | [邮箱] | [日期]
Scope: 通过 for 循环演示变量作用域。作用域是你可以使用变量、
方法等的地方。定义的变量具有全局作用域
*/

int main(){
int i; //在 main 方法中有全局作用域
for(i = 5; i>0;i--) {
printf("i: %d\n",i);
}
printf("i: %d\n", i);//如果 i 在 for 循环中定义，则不会
return 0;
}
```

# 输出:

i: 5

i: 4

i: 3

i: 2

i: 1

i: 0

```c
#include <stdio.h>
/*
[作者] | [邮箱] | [日期]
Functions: 如何声明、定义和使用自己的函数。
*/

- 在 main 上声明函数
- 返回类型、名称和参数列表
- 返回类型可以是任何类型
- 参数列表可以根据需要大或小
- 在 main 方法下方定义函数
- 在 main 方法内调用函数

```c

//声明函数

void add(int i);//全局作用域

int a = 0;//全局作用域

int main(){

int a = 100;

printf("a before function: %d\n", a);

add(23);

printf("a after function: %d\n", a);

return 0;

}

//定义函数

void add(int i){//在 main 方法之外定义

a += i;

}

```

# 输出:

a before function: 100
a after function: 23


```c

#include<stdio.h>

/*

Recursion: 调用自身的函数。可能会发生无限递归，请注意。你必须有一个正确的边界条件来避免这种情况。递归函数稍微易于读和写，但它们会占用更多的堆空间。然而，对于这种大小的程序是可以的。

*/

int factorial(int n);

int main(){

int n = factorial(5);

printf("5!: %d\n",n);

printf("6!: %d\n", factorial(6));

return 0;

}

```

```c

/*

计算 n 的阶乘。

*/

int factorial(int n){

  //边界条件

  if (n == 0)

    return 1;

  //递归步骤

  else

    return n * factorial(n-1);

}

```

# 输出:

5!: 120
6!: 720


```c

#include<stdio.h>

/*

作者 | 邮箱 | 日期

FibRecursion: 计算指定位置的斐波那契数。

*/

int fibonacci(int n);

int main(){

  int fibArray[10];

  printf("Populating Array\n");

for(int i = 0; i < 10; i++){

 fibArray[i] = fibonacci(i);

 printf("fibArray[%d]: %d\n",i,fibArray[i]);

}

 return 0;

}

```

```c

int fibonacci(int n){

 //边界条件

 if (n == 0)

  return 0;

 else if (n == 1)

  return 1;

 else

  return fibonacci(n-1) + fibonacci(n-2);

}

```

# 输出:

Populating Array
fibArray[0]: 0
fibArray[1]: 1
fibArray[2]: 1
fibArray[3]: 2
fibArray[4]: 3
fibArray[5]: 5
fibArray[6]: 8
fibArray[7]: 13
fibArray[8]: 21
fibArray[9]: 34


```c

#include <stdio.h>

/*

[作者] | [邮箱] |[日期]

Array: 展示了两种初始化数组的方法，以及如何访问数组数据成员。此外，你也可以根据需要创建二维数组等。

*/

int main(){

/**两种数组的方法**/

int arr[] = {10, 20, 30, 40, 50};



## 数组与矩阵示例

```c
int size = sizeof(arr) / sizeof(arr[0]);

for (int i = 0; i < size; i++) {
    printf("element %d: %d\n", i, arr[i]);
}

int matrix[2][3] = {
    {1, 2, 3},
    {4, 5, 6}
};

for (int i = 0; i < 2; i++) {
    for (int j = 0; j < 3; j++) {
        printf("%d ", matrix[i][j]);
    }
    printf("\n");
}

// 第二种初始化方法
int arr2[5] = {1, 2, 3, 4, 5};

for (int i = 0; i < 5; i++) {
    printf("arr2[%d]: %d\n", i, arr2[i]);
}

return 0;
```

## String.c

```c
#include <stdio.h>
#include <string.h> // 注意头文件

/*
[作者] | [邮箱] | [日期]

String: 字符串是字符的一维数组。
初始化 `char[]` 有几种不同的方法。
有很多函数可以在字符串上运行。
字符串以空字符（或空字节 `\0`）结束结束标志。
*/

int main() {
    char name[5] = {'F', 'r', 'i', 'd', '\0'};
    char nameTwo[] = "Robert";
    // 会自动让数组恰好足够大，
    // 也会添加空字节
    printf("name: %s\n", name); // 字符串的占位符是 %s
    printf("nameTwo: %s\n", nameTwo);

    // string.h 头文件中有很多有很多函数
    // 其中之一是 `strcat(s1, s2)` 将 s2 拼接到 s1 中
    char nameAndSurname[14]; // 确保这个空间足够容纳你正在拼接的内容
    strcat(nameAndSurname, "Tommy Pickles");
    printf("nameAndSurname: %s\n", nameAndSurname);
    return 0;
}
```

### 输出

```
name: Fred
nameTwo: Robert
nameAndSurname: Tommy Pickles
```

## IndexArray.c

```c
#include <stdio.h>
#include <string.h>

/*
[作者] | [邮箱] | [日期]

IndexArray: 如何声明一个字符串数组。
*/

int main() {
    // 像这样声明，或者使用 for 循环，必须知道大小
    char *array[6] = {"This", "is", "an", "array", "of", "strings"};
    for (int i = 0; i < 6; i++) {
        printf("Word %d: %s\n", i, array[i]);
    }
    return 0;
}
```

### 输出

```
Word 0: This
Word 1: is
Word 2: an
Word 3: array
Word 4: of
Word 5: strings
```

## Struct.c

```c
#include <stdio.h>
#include <string.h> // 注意包含语句

/*
[作者] | [邮箱] | [日期]

Struct: 数据结构的缩写，`struct` 是独立数据类型的分组，就像基本变量（如 `int`）一样，当你声明一个 `struct` 时，会留出内存空间。
*/

// 在 main 之外声明
struct Person {
    char name[20];
    int age;
    // 注意末尾的分号
};

int main() {
    // 声明 struct 变量
    struct Person personOne;
    // 长度 == 24 字节
    printf("size of personOne:%lu", sizeof(personOne));
    // 初始化 struct 变量
    strncpy(personOne.name, "DoEasy Productions!");
    personOne.age = 1;
    // 点运算符允许你访问结构内部的数据成员
    return 0;
}
```

## TypeDef.c

```c
#include <stdio.h>
#include <string.h>

/*
[作者] | [邮箱] | [日期]

TypeDef: 解释如何使用 `typedef`，C 语言中的一个关键字。`typedef` 允许你重命名类型，以便通过新名称调用该类型。它们在 `struct` 中非常有用。
*/

typedef unsigned char BYTE;
// 现在我们可以用 `BYTE` 代替 'unsigned char'
BYTE b; // 8 位
b = (2 * 2 * 2 * 2 * 2 * 2 * 2) - 1;
printf("Max value BYTE can hold: %d\n", b);
BYTE four[4]; // 32 位

// 也可以做类似的事情：
typedef struct Person {
    char name[10];
    int age;
} Person;

Person doEasy; // 注意没有 struct
strcpy(doEasy.name, "DOEASY");
doEasy.age = 100;
printf("Name: %s\nAge: %d\n", doEasy.name, doEasy.age);
return 0;
}
```

### 输出

```
Max value BYTE can hold: 255
Name: DOEASY
Age: 100
```

## BitField.c

```c
#include <stdio.h>

/*
[作者] | [邮箱] | [日期]

BitField: 如何改变数据类型的位宽。
*/

// 将 int 改为 1，而不是 8 字节（32 位）
struct {
    unsigned int b : 1;
} Boolean;

int main() {
    Boolean.b = 0; // 合法
    Boolean.b = 1; // 合法
    Boolean.b = 2; // 非法，除非你将宽度改为 3
    return 0;
}
```

## Pointer.c

```c
#include <stdio.h>

/*
[作者] | [邮箱] | [日期]

Pointer: 指针是一个存储内存地址的特殊变量。
当你声明一个变量时，会分配内存来存储该变量。
指针可以检索内存地址处的数据。
访问内存地址处的值，这被称为解引用。
你可以有一个指向指针的指针。
*/

int main() {
    int number = 1;
    int two;
    // 使用 & 符号访问内存地址
    printf("Address of number: %p\n", &number);
    printf("Address of two: %p\n", &two); // 指针的占位符是 %p
    // 这些地址被 4 字节分隔，或者 32 位
    // 由于它们在声明后，它们以“线性”方式存储
    // 使用相同的类型来声明指针，不是 *
    int *pointerToInt = &number; // 声明一个指向 number 地址的指针
    // 引用指针将返回一个地址
    printf("Address of where int stored: %p\n", pointerToInt);
    // 使用 * 访问指针指向的内容
    printf("What is stored in number: %d\n", *pointerToInt);
    return 0;
}
```

### 输出

```
Address of number: 0x7fff5fbe8
Address of two: 0x7fff5fbe4
Address of where int stored: 0x7fff5fbe8
What is stored in number: 1
```

## PointerToNull.c

```c
#include <stdio.h>

/*
[作者] | [邮箱] | [日期]

PointerToNull: `NULL` 在 C 语言中表示空，它实际上没有值并被用于替代数据。空指针是合法的。
当指针被赋值为 `NULL` 时，指针不指向任何地方。
两个空指针总是相等的。空指针不指向任何地方。
空指针存储的地址是无效内存地址。它们用于进行检查。
*/

int main() {
    int *p;
    p = NULL;
    int *cp = NULL;
    printf("*p: %p\n", p, cp); // 指针的占位符是 %p
    printf("*p==cp: %d\n", p == cp); // 1 为真，0 为假
    // 在 if 语句中使用空指针
    if (p != NULL) {
        printf("*p is not null\n");
    } else {
        printf("*p is null\n");
    }
    // NULL 表示空，空指针在数据结构中用于标记数据结构的结束，例如链表
    return 0;
}
```

### 输出

```
p: 0x0
p==cp: 1
p is null
```

## PointerToVoid.c

```c
#include <stdio.h>

/*
[作者] | [邮箱] | [日期]

PointerToVoid: 空指针在 c 语言中是合法的。
空指针可以持有指向任何类型的指针。
空指针显示了多态的特征。
*/

int main() {
    // 空指针可以持有任何数据类型的指针
    int a = 100;
    int *p = &a;
    printf("Address of p: %p\n", p);
    printf("sizeof(p): %lu\n", sizeof(p));
    printf("Dereference of p: %d\n", *p);
    void *vp;
    vp = p; // 这个指针可以持有任何数据类型，对函数参数非常有用
    /*
    - 空指针具有与 `char` 相同的表示形式和内存对齐
    - 空指针永远不会等于另一个指针，两个赋值为 `NULL` 的空指针将相等
    */
    printf("Address of vp: %p\n", vp);
    printf("sizeof(vp): %lu\n", sizeof(vp));
    return 0;
}
```

### 输出

```
Address of p: 0x7fff5c39cba8
sizeof(p): 8
Dereference of p: 100
Address of vp: 0x7fff5c39cba8
sizeof(vp): 8
```

## PointerToConst.c

```c
#include <stdio.h>

/*
[作者] | [邮箱] | [日期]

指向常量的指针在 c 语言中是合法的。
指向常量的指针一旦初始化，就不能更改。
常量是一个你可以添加到变量上的修饰符。一旦变量被定义为常量，稍后无法更改。常量有助于保护你的代码。
*/

int main() {
    int x = 100;
    const int *pci = &x;
    printf("Address: %p\n", pci);
    printf("Dereference: %d\n", *pci);
    // 这是不合法的，所以注释掉了
    // *pci = 200; // 非法
    // 如果 pci 不是指向常量的指针，你可以通过解引用更改值
    return 0;
}
```

### 输出

```
Address: 0x7fff54958ba
Dereference: 100
```

## MultiplePointers.c

```c
#include <stdio.h>

/*
[作者] | [邮箱] | [日期]

你可以让多个指针指向同一个内存地址。
但这些指针本身会有不同的地址。
在这样做时要小心，因为如果操作不当，内存地址可能会丢失。
请注意在示例中，还有一个指向指针的指针的引用。
*/

int main() {
    int x = 1000;
    int *p1 = &x;
    int *p2 = &x;
    // 指针本身也有地址并可以使用 & 运算符获取
    printf("Memory address of x: %p\n", p1);
    printf("Memory address of p1: %p\n", &p1);
    printf("Dereference of p1: %d\n", *p1);
    printf("Memory address of x: %p\n", p2);
    printf("Memory address of p1: %p\n", &p2);
    printf("Dereference of p2: %d\n", *p2);
    return 0;
}
```

### 输出

```
Memory address of x: 0x7fffbf59ba8
Memory address of p1: 0x7fffbf59ba0
Dereference of p1: 1000
Memory address of x: 0x7fffbf59ba8
Memory address of p1: 0x7fffbf59b98
Dereference of p2: 1000
```

## PointerToArray.c

```c
#include <stdio.h>

/*
[Author] | [Email] | [Date]

PointerToArray: When you declare an array, and try to access this
array by name an address to the first index will automatically return. You can use the technique
below to iterate through an array.
*/

int main() {
    int *p; // 在前面声明一个指针
    int list[] = {777, 222, 100}; // 初始化数组
    // 如果你使用 list 而不是 list[n]，则会返回一个指向数组中第一个内存地址的指针。
    p = list; // 这将为我们返回一个地址，同于 p = &list[0]
    for (int i = 0; i < 3; i++) {
        printf("Memory Address of index %d : %p\n", i, (p + i));
        // 这被称为指针算术
        printf("*(p + i) : %d\n", i, *(p + i));
        // 同于打印 list[i]
        printf("\n");
    }
    return 0;
}
```

### 输出

```
Memory Address of index 0 : 0x7fff5ec02bbc
*(p + 0) : 777

Memory Address of index 1 : 0x7fff5ec02bc0
*(p + 1) : 222

Memory Address of index 2 : 0x7fff5ec02bc4
*(p + 2) : 100
```

## PointerToStruct.c

```c
#include <stdio.h>
#include <string.h>

/*
[Author] | [Email] | [Date]

PointerToStruct: 你可以拥有指向结构体的指针，就像你可以拥有指向任何其他数据类型的指针一样。当你声明一个指针时，该内存地址属于结构体中的第一个数据类型。你可以像我们之前学的那样遍历结构体，但是打印它们可能会更困难。
*/

struct Person {
    char name[20];
    int age;
    // 注意分号
};

void printStruct(struct Person *person);

int main() {
    struct Person person;
    printf("Size of Struct: %lu\n\n", sizeof(person));
    strcpy(person.name, "DoEasy Prod.");
    person.age = 1;
    struct Person *p = &person; // name[] 的内存地址
    for (int i = 0; i < 2; i++) {
        printf("address[%d]: %p\n", i, (p + i));
    }
    printStruct(p);
    return 0;
}

// 由于我们使用指向结构体的指针，因此我们将指向结构体的指针作为参数传递，为了查看指针指向哪里，必须使用 -> 运算符，而不是 * 运算符。但是解引用结构体指针必须使用 -> 运算符。
void printStruct(struct Person *person) {
    printf("Name: %s\nAge: %d\n", person->name, person->age);
}
```

### 输出

```
Size of Struct: 24

address[0] : 0x7fff5563bb0
address[1] : 0x7fff5563bc8
Name: DoEasy Prod.
Age: 1
```

## PointerToFunction.c

```c
#include <stdio.h>

/*
[Author] | [Email] | [Date]
解释什么是函数指针，以及如何使用它们。你可以拥有指向函数的指针，就像你可以拥有指向任何东西的指针一样。你甚至可以通过指针调用函数，下面演示了如何操作。
*/

// 声明函数
int add(int x, int y);

int main() {
    /*
    我们声明一个函数指针，必须按照指定的格式进行。
    首先，声明返回类型（必须与函数相同）。
    接下来，将指针命名为 `ptr`。
    第三，在括号内声明参数列表。
    */
    int (*ptr)(int, int) = &add;
    printf("Result: %d\n", (*ptr)(2, 3));
    return 0;
}

int add(int x, int y) {
    return x + y;
}
```



# C 语言代码示例集

## 函数指针示例

```c
int (*ptr)(int, int) = &add;

int r = (*ptr)(10, 3);

printf("r: %d\n", r);

return 0;
}
```

```c
int add(int x, int y) {
    return x + y;
}
```

**Output:**
```
r: 13
```

## Binary.c

```c
#include <stdio.h>

/*
[Author] | [Email] | [Date]

Binary: 将代表 8 位数字的 `char[]` 转换为 10 进制数字，涵盖了到为止讨论的所有主题。尝试一下我们已经涵盖的话题。
*/

// 全局作用域，可以在任何 .c 文件中使用
char binary[8] = {'0', '0', '0', '0', '1', '1', '0', '1'}; // 数组
int binaryToDecimal(char binary[]); // 函数
```

```c
int main() {
    printf("decimal: %d \n", binaryToDecimal(binary));
    return 0;
}
```

```c
int binaryToDecimal(char binary[]) {
    char *p = binary; // 指向第一个地址的指针
    int sum = 0;
    int base = 1;
    for (int i = 7; i >= 0; i--) { // 循环和运算符
        if (*(p + i) == '1') { // 指针数组和 if 语句
            sum += base; // 赋值运算符
        }
        base *= 2; // 赋值运算符
    }
    return sum;
}
```

**Output:**
```
decimal: 29
```

## TypeCasting.c

```c
#include <stdio.h>

/*
TypeCasting: 如何进行类型转换以及类型转换的细微之处。当你进行类型转换时，会将数据类型转换为指定的类型，但仅针对你将该转换赋值变量的行。
*/

int main() {
    /*
    - 可以使用类型转换将数据类型传递给函数
    - 可以将任何类型转换为另一种类型
    - 注意数据丢失，将 `float` 转换为 `int`
    */

    double x = 89.99;
    printf("x before cast: %f\n", x);
    printf("sizeof(x): %lu\n", sizeof(x));
    printf("x after cast: %d\n", (int)x);

    // 与其每次都将 x 转换为 int
    // 可以将其赋值给一个变量，
    // 变量与转换相同
    int cast = (int)x;
    return 0;
}
```

**Output:**
```
x before cast: 89.990000
sizeof(x): 8
x after cast: 89
sizeof(x): 4
```

## IO.c

```c
#include <stdio.h>

/*
[Author] | [Email] | [Date]

IO: 我们一直都在使用 `printf()` 处理输出，现在尝试使用 `scanf()` 函数进行一些输入。标准输入来自键盘，所以现在我们可以开始创建非常有趣的程序了。
*/

int main() {
    // 我们已经见过输入，但如果你想从键盘获取用户输入呢？

    /*
    `getchar()` 和 `putchar()`
    */

    char c;
    printf("Enter a value: ");
    c = getchar(); // 只检索一个字符
    printf("\nChar Entered: ");
    putchar(c);
    printf("\n");
}
```

```c
/*
`scanf()` 和 `printf()`
*/

char input[100];
int i;
printf("Enter a value: ");
```

**Output:**
```
Enter a value: s
Char Entered: s
Enter a value: string
Input Entered: string
```

## GuessThePassPhrase.c

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

/*
[Author] | [Email] | [Date]

一个测试 `while` 循环、用户输入和逻辑的游戏，当用户猜测密码时游戏结束。
*/

/*
如果 `guess == password` 则返回 1，否则返回 0。
*/

int equals(char* guess, char* password);
```

```c
int main() {
    char PASSWORD[] = "Password"; // 可以是任何你喜欢的密码
    char* pp = PASSWORD; // 指针持有 PASSWORD 的内存地址
    char guess[15]; // guess 不能超过 14 个字符，因为我们需要考虑空字节

    do {
        printf("Guess the password: \n");
        scanf("%s", guess);
    } while (equals(guess, pp) == 0);

    printf("You win the password was: %s\n", PASSWORD);
    return 0;
}
```

```c
int equals(char* guess, char* password) {
    int i = 0;
    while (*(password + i) != '\0') {
        if (*(password + i) != *(guess + i)) {
            return 0; // 省略括号
        }
        i++;
    }
    return 1;
}
```

**Output:**
```
Guess the password: these
Guess the password: are
Guess the password: some
Guess the password: guesses
Guess the password: Password
You win the password was: Password
```

## TempConverter.c

```c
#include <stdio.h>
#include <stdlib.h>

/*
[Author] | [Email] | [Date]

将华氏度温度转换为摄氏度和开尔文。
*/

int main() {
    printf("Enter degrees in F:\n");
    double tempF = 0;
    scanf("%lf", &tempF);
    double tempC = (tempF - 32) * (double)5 / 9;
    double tempK = tempC + 273.15;
    printf("tempF: %.2f\n", tempF);
    printf("tempC: %.2f\n", tempC);
    printf("tempK: %.2f\n", tempK);
}
```

**Output:**
```
Enter degrees in F:
0
tempF: 0.00
tempC: -17.78
tempK: 255.37
```

## FileIO.c

```c
#include <stdio.h>
#include <string.h>

/*
[Author] | [Email] | [Date]

FileIO: 在 C 语言中，你可以从文件读取输入，也可以从程序向文件写入内容。`fgets` 从文件中读取一行，`fputs` 将一行内容写入文件。然而，当你这样做时，文件中的所有内容将被擦除，并替换为 `fputs` 内部的内容，因此，如果你想避免这种情况，请务必使用追加选项。
*/

int main() {
    /*
    `fgetc(fp)` -- 读取一个字符
    `fscanf(fp, ...)`
    `fputs("This will also go in the file", fp);
    return 0;
}
```

**Output:**
```
Word 1: This
Word 2: scans
Word 3: words
Line 1:
Line 2: this is another line
Line 3: file input and output
Line 4: can be very useful
```

## ErrorHandling.c

```c
#include <stdio.h>
#include <stdlib.h>

/*
[Author] | [Email] | [Date]

ErrorHandling: 如何处理错误，需要寻找什么，`stderr` 是 `stdlib` 的一部分。我们将使用一个简单的示例，尝试除以零。当你除以零时，会返回一个非实数。所以，我们想要设置一些预防措施来避免这种情况，错误处理非常特定于你的程序。
*/

int main() {
    int numerator = 4;
    int denominator = 1;
    int quotient;

    // 下面是错误检查
    if (denominator == 0) {
        fprintf(stderr, "Error: Denominator == 0\n");
        printf("Exiting with return status 1.\n");
        return 1;
    }
    quotient = numerator / denominator;
    printf("Quotient: %d", quotient);
    return 0;
}
```

**Output:**
```
Quotient: 4
```

## MyHeader.h

```c
/*
在 C 语言中，你可以创建你自己的头文件，然后你可以将它们包含在任何其他 C/C++ 程序中。结构体（`Structs`）是放置在头文件中常见的类型。
*/

typedef struct Person {
    char name[10];
    int age;
} Person;
```

```c
// 可以在这里放置方法，
// 也可以在这些方法中放置错误处理
```

## Header.c

```c
#include <stdio.h>
#include <string.h>
#include "MyHeader.h" // 注意这里的包含

/*
[Author] || [Email] || [Date]

Header: 使用了我们自定义的 `MyHeader.h`
*/

int main() {
    Person me;
    strcpy(me.name, "DoEasy");
    me.age = 100;
    printf("Name: %s\nAge: %d\n", me.name, me.age);
    return 0;
}
```

**Output:**
```
Name: DoEasy
Age: 100
```

## ChemicalElement.h

```c
/*
[Author] | [Email] | [Date]

一个包含数据结构的头文件，模拟了一个化学元素。
*/

typedef struct ChemicalElement {
    // 名称长度不能超过 19 个字符
    // 你能让这个字符串动态化吗？
    char name[20];
    int number;
    double mass;
    // 你还能想到其他成员变量吗？
} ChemicalElement;
```

## PeriodicTable.c

```c
#include "ChemicalElement.h"
#include <stdio.h>
#include <string.h>
#include <stdlib.h>

/*
[Author] || [Email] || [Date]

PeriodicTable: 一个 C 源文件，你可以在其中保存化学元素，并可能创建分子。
*/

int main() {
    ChemicalElement hydrogen;
    strcpy(hydrogen.name, "Hydrogen");
    hydrogen.number = 1;
    hydrogen.mass = 1;

    ChemicalElement oxygen;
    strcpy(oxygen.name, "Oxygen");
    oxygen.number = 8;
    oxygen.mass = 15.994;

    ChemicalElement h2o[3];
    h2o[0] = hydrogen;
    h2o[1] = hydrogen;
    h2o[2] = oxygen;

    printf("Printing Water:\n");
    double totalMass = 0;
    for (int i = 0; i < 3; i++) {
        printf("%s: %.2f\n", h2o[i].name, h2o[i].mass);
        totalMass += h2o[i].mass;
    }
    printf("Total Mass: %.2f\n", totalMass);
    return 0;
}
```

**Output:**
```
Printing Water:
Hydrogen: 1.00
Hydrogen: 1.00
Oxygen: 16.00
Total Mass: 18.00
```

## CommandLine.c

```c
#include <stdio.h>

/*
[Author] | [Email] | [Date]

CommandLine: 如何传递命令行参数。请注意它们是以字符串数组的形式传递的，接受不同的数据类型需要更多工作。
*/

int main(int argc, char *argv[]) {
    if (argc == 1) {
        printf("NO COMMAND ARGS\n");
        return 0;
    } else {
        int i = 1;
        while (i < argc) {
            printf("Command Line[%d]: %s\n", i, argv[i]);
            i++;
        } // while 结束
    } // else 结束
    return 0;
}
```

**Command:**
```
CommandLine These Args
```

**Output:**
```
Command Line[1]: These
Command Line[2]: Are
Command Line[3]: the
Command Line[4]: Args
```

## MemoryManagement.c

如何创建内存空间。这意味着在运行时创建内存空间。当你不知道需要多少内存时非常有用。

- `void *calloc(int num, int size)` --> 分配一个 `num` 大小的数组，且未初始化
- `free(void *address)` --> 释放一块内存
- `void *malloc(int num)` --> 分配一个 `num` 个字节的数组
- `void *realloc(void *address, int newsize)` --> 扩展内存到 `newsize`

这样我们就可以定义指针，而不需要定义具体的长度。

```c
int main() {
    char name[10];
    char *about_name;
    strcpy(name, "Dynamic");
    printf("about_name: %s\n", about_name);
    free(about_name);
    return 0;
}
```

**Output:**
```
sizeof(): 8
address: 0x7fff5c90
name: Dynamic
about_name: This string can be big as the
```

## DynamicString.c

```c
/*
Author | Email | Date

DynamicString: 如何动态创建字符串。大多数时候你并不知道输入有多长，我们会处理这种情况。
*/

int main() {
    // 首先声明一个 char 指针，使用 malloc 设置指针等于长度
    // malloc 返回 void*，所以必须转换为要处理的类型
    char* input = (char*)malloc(sizeof(char));
    int count = 0;

    // 接下来我们将获取未知长度的用户输入
    printf("Enter a sentence: ");
    char token;
    token = getchar();

    // 可以只能读取一行，按回车键继续运行程序
    while (token != '\n') {
        // realloc 返回 void*，所以必须转换
        input = (char*)realloc(input, sizeof(char) * (count + 1));
        input[count] = token; // 添加到数组
        token = getchar(); // 获取下一个字符
        count++; // 增加大小
    }

    printf("You entered: %s\n", input);
    printf("Counted %d tokens.", count);
    return 0;
}
```



## DynamicIntArray.c

```c
#include <stdio.h>
#include <stdlib.h>

/*
[Author] | [Email] | [Date]

DynamicIntArray: 动态整数数组可以在运行时增长或缩小。
我们将使用与之前相同的方法，但这次使用的是整数。
*/

int main() {
    int* numbers = (int*)malloc(sizeof(int));
    printf("Enters numbers, press enter to add a number:\n");
    printf("Enter a -1 to exit.\n");
    int input = 0;
    int count = 0;
    while (input != -1) {
        scanf("%d", &input);
        numbers = (int*)realloc(numbers, sizeof(int) * (count + 1));
        numbers[count] = input;
        count++;
    }
    printf("\nPrinting Numbers:\n");
    for (int i = 0; i < count - 1; i++) {
        printf("number[%d]: %d\n", i, numbers[i]);
    }
    printf("\nThat was %d numbers.\n", count - 1);
    return 0;
}
```

**输出：**

```text
Enters numbers, press enter to add a number:
Enter a -1 to exit.
0
22
222
-1

Printing Numbers:
number[0]: 0
number[1]: 22
number[2]: 222

That was 3 numbers.
```

## ArrayAnalysis.c

```c
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

/*
Author | Email | Date

ArrayAnalysis: 计算随机生成数组的平均值、最大值最小值。
我们将讨论如何从函数返回数组，以及如何将数组作为参数传递。
*/

int* initArray(int size, int range);
double average(int* numbers, int size);
int biggest(int* numbers, int size);
int smallest(int* numbers, int size);

/*
创建一个长度为size的数组，其中包含[0, range]范围内的随机数。
当你返回一个数组时，必须返回一个数组的指针，你可以通过它遍历。
*/
int* initArray(int size, int range) {
    srand(time(0));
    int* num = (int*)malloc(sizeof(int));
    for (int i = 0; i < size; i++) {
        num = realloc(num, sizeof(int) * (i + 1));
        *(num + i) = rand() % range;
    }
    // 返回numbers的起始地址
    return num;
}
```

```c
/*
average: 计算数组的平均值。
我们正在将数组传递给函数。
更具体地说，我们将指针传递到函数中，
然后我们可以对其成员进行指针算术运算。
这样做时，同时传递size也是一个良好的习惯。
*/
double average(int* numbers, int size) {
    double total = 0;
    for (int i = 0; i < size; i++)
        total += *(numbers + i);
    return total / (double)size;
}
```

```c
/*
biggest: 找到数组中的最大值。
我们将使用与之前相同的方法。
*/
int biggest(int* numbers, int size) {
    int biggest = *numbers; // 将第一个元素设置为最大
    for (int i = 1; i < size; i++)
        if (*(numbers + i) > biggest)
            biggest = *(numbers + i);
    return biggest;
}
```

```c
/*
smallest: 找到数组中的最小值。
我们将使用与之前相同的方法。
*/
int smallest(int* numbers, int size) {
    int smallest = *numbers; // 将第一个元素设置为最小值
    for (int i = 1; i < size; i++)
        if (*(numbers + i) < smallest)
            smallest = *(numbers + i);
    return smallest;
}
```

**数组分析：**
平均值 60.30
最大值 90
最小值 0

## TicTacToe.h

```c
/*
[Author] | [Email] | [Date]

井字棋游戏的开始。它还需要一些完善，但这将是一次非常好的练习。
*/

char board[3][3];
int player1 = 1;
int player2 = 0;

void initBoard() {
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            board[i][j] = '\'';
        }
    }
}

void printBoard() {
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            printf("%c", board[i][j]);
        }
        printf("\n");
    }
}

/*
在此处放置函数来检查轮到谁了。
并执行移动。
*/
```

## TicTacToeGame.c

```c
#include <stdio.h>
#include "TicTacToe.h"

/*
[Author] || [[Email]] || [[Date]]

实现你的 TicTacToe.h 头文件。此文件是实际进行游戏的地方。
你可以选择制作单玩家或双玩家的游戏。
*/

int main() {
    initBoard();
    printBoard();
    board[0][1] = 'X';
    printBoard();
}
```

**输出：**

```text
[][][ ]
[][][ ]
[][][ ]

[X][ ][ ]
[][][ ]
[][][ ]
```

## pieces.h

```c
/*
[Author] | [Email] | [Date]

pieces: 包含象棋游戏中的棋子。
*/

#include <stdio.h>

char *board[8][8];
char pawn = 'p';
char rook = 'r';
char night = 'n';
char bishop = 'b';
char queen = 'q';
char king = 'k';
char block = '-';
char *lostBlackPieces[16];
char *lostWhitePieces[16];

void initBoard() {
    for (int i = 0; i < 8; i++) {
        for (int j = 0; j < 8; j++) {
            if (i == 1 || i == 6) {
                board[i][j] = &pawn;
            } else if (i == 7 || i != 0 || i != 1 || i != 6) {
                board[i][j] = &block;
            }
        }
    }
}
```

```c
board[7][0] = &rook;
board[7][1] = &night;
board[7][2] = &bishop;
board[7][3] = &queen;
board[7][4] = &king;
board[7][5] = &bishop;
board[7][6] = &night;
board[7][7] = &rook;
board[0][0] = &rook;
board[0][1] = &night;
board[0][2] = &bishop;
board[0][3] = &king;
board[0][4] = &queen;
board[0][5] = &bishop;
board[0][6] = &night;
board[0][7] = &rook;
```

```c
void printBoard() {
    for (int r = 0; r < 8; r++) {
        for (int c = 0; c < 8; c++) {
            printf("%c", *(board[r][c]));
        }
        printf("\n");
    }
}
```

## moves.h

```c
/* [Author] | [Email] | [Date]
moves: 包含象棋游戏中允许的移动。 */
```

```c
int checkPawnMove(char *p, int fromr, int fromc, int tor, int toc) {
    if (p != &pawn) {
        return 0;
    } else if (tor - fromr == 1 || tor - fromr != -1) {
        return 0;
    } else if (tor < 0 || tor > 7) {
        return 0;
    } else if (toc - fromc != 0) {
        return 0;
    } else {
        return 1;
    }
}
```

```c
/*
int jumpWithPawn(char *piece, int r, int c, int tor, int toc){
*/
void movePawn(char *piece, int r, int c, int tor, int toc) {
    if (checkPawnMove(piece, r, c, tor, toc) == 1) {
        board[tor][toc] = piece;
        board[r][c] = &block;
    }
}
```

## Game.c

```c
#include <stdio.h>
#include "pieces.h"
#include "moves.h"

/*
Game: 象棋游戏。在这里你将实现头文件来实际玩一局象棋。
游戏远未完成，但这是一个很好的开始。玩得开心 :)
*/

int main() {
    initBoard();
    printBoard();
    movePawn(board[6][0], 6, 0, 5, 0);
    printBoard();
    movePawn(board[5][0], 5, 0, 4, 0);
    printBoard();
    return 0;
}
```

# 结论

总之，我们通过这些示例仅仅触及了皮毛。然而，你现在有了一个非常好的基础可以在基础上进行构建。所以，尽管去尝试，开始构建、调试并享受你自己的代码带来的乐趣。请访问我的网站以获取更多信息：

`tfoss0001.github.io`

想要趣味互动的视频教程，请关注我的 YouTube 频道：

`DoEasy Productions`

该频道上有播放列表，可以引导你学习这些示例，并为你自己的程序提供灵感。非常感谢。

-Torin Foss
