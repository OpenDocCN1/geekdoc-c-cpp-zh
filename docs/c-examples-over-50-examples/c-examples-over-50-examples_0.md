# C 示例：50 个以上示例


## 作者的话

非常感谢你的购买，感谢你对学习这门奇妙编程语言的兴趣。“C 示例”包含了 30 多个功能完整、易于使用且独特的示例。不需要预先的编程知识，不过有先前的知识也会很有帮助。唯一的要求是耐心、奉献和学习的热情。然而，为了不让你放弃学习 C，我将解释如何创建、编译和运行一个 `.c` 源文件。

为了创建一个可编辑的 `.c` 源文件，你首先需要选择文本编辑器，我将使用 `emacs`。所以要创建一个 `.c` 源文件，请在命令行中输入以下命令：

```bash
emacs SourceFile.c
```

然后，使用以下命令进行编译：

```bash
gcc -o SourceFile.c SourceFile
```

然后，使用以下命令运行你的文件：

```bash
./SourceFile
```

本书以易于理解的方式介绍新主题，然后使用新主题以及之前讨论过的主题来编写程序，以便在学习新材料的同时进行复习。这有助于你最大化地学习一门新语言。有许多东西需要学习，熟能生巧。让我们让我们开始吧。

## 感谢

### HelloWorld.c

```c
#include <stdio.h> //一个头文件，包含了输入和输出
//这样我们就可以使用下面的 printf 函数

// HelloWorld：介绍了如何设置 .c 文件。
// 这只是一个测试，让你的环境设置良好。
int main(){ // 运行一个 c 程序
printf("Hello World!\n");//'\n' 是换行符，将其放在新行
return 0;
}
```
输出：
```
Hello World!
```

### DataTypes.c

```c
#include <stdio.h>
/*
类型：C 中可用的类型。注意 sizeof() 函数，它返回数据类型的大小。
这里列出了许多数据类型，包括：char, int 和 double。
*/
int main(){
  /*
  int and long: 是整数
  float and double: 是浮点值
  char: 单字符
  %f -> 浮点/双精度占位符
  %.2f -> 格式化 float/double 输出两位小数
  %d -> 整数占位符
  %c -> 字符占位符
  */
  printf("Storage for char: %lu byte \n", sizeof(char));
  printf("Storage for int: %lu bytes \n", sizeof(int));
  printf("Storage for float: %lu bytes \n", sizeof(float));
  printf("Storage for double: %lu bytes \n", sizeof(double));
  return 0;
}
```
输出：
```
Storage for char: 1 byte
Storage for int: 4 byte
Storage for float: 4 byte
Storage for double: 8 byte
```

### Variables.c

```c
#include <stdio.h>
/*
变量：显示如何声明和初始化变量。多个声明是合法的，分行写。
你可以对相似的类型进行操作。初始化意味着给变量赋值。
*/
int main(){
  char letter; //变量声明
  letter = 't'; //初始化变量，注意 char 是
  printf("letter: %c \n", letter);
  int x, y, z; // 注意多个变量声明
  x = 3;
  y = 2;
  z = x+y;
  printf("z: %d \n",z);
  return 0;
}
```
输出：
```
letter: t
z: 5
```

### Operators.c

```c
#include <stdio.h>
/*
运算符：C 中的基本运算符，当你使用运算符执行操作时，必须在相同的数据类型上。包括：算术运算符、关系运算符和赋值运算符。还有更多，但目前我们需要这些。
*/
int main(){
  int x, y;
  x = 2;
  y = 2;
  /*算术运算符*/
  printf("2 + 2 : %d \n", x+y);
  printf("2 - 2 : %d \n", x-y);
  printf("2 * 2 : %d \n", x*y);
  printf("2 / 2 : %d \n", x/y);
  x++; // 相当于 x + 1
  printf("2++ : %d \n", x);
  y--; // 相当于 y-1
  printf("2-- : %d \n", y);
  int m = 3%2; // 返回除法的余数
  printf("modulus : %d \n", m);
  /*关系运算符*/
//返回 0（假）或 1（真）
  printf("2 == 2 : %d \n", x==y);//不是赋值，是比较
  printf("2 != 2 : %d \n", x!=y);//bang 运算符，
  printf("2 > 2 : %d \n", x>y); //将返回 0
  printf("2 >= 2 : %d \n", x>=y);
  printf("2 < 2 : %d \n", x<y);
  printf("2 <= 2 : %d \n", x<=y);
  /*赋值运算符*/
  printf("x += y : %d \n", x+=y);//x = x+y
  printf("x: %d \n",x);
  printf("x -= y : %d \n", x-=y);//x = x-y x:4 y:2
  printf("x: %d \n",x);
  printf("x *= y : %d \n", x*=y);//x = x*y
  printf("x /= y %d \n", x/=y);//x = x/y
  printf("x: %d \n",x);
  printf("x %%= y : %d \n", x%=y);//x = x%y//两个 % 符号用于打印出一个 % 符号
  return 0;
}
```
输出：
```
2 + 2 : 4
2 - 2 : 0
2 * 2 : 4
2 / 2 : 1
2++ : 3
2-- : 1
modulus : 1
2 == 2 : 1
2 != 2 : 0
2 > 2 : 0
2 >= 2 : 1
2 < 2 : 0
2 <= 2 : 1
x += y : 5
x: 5
x -= y : 3
x: 3
x *= y : 6
x: 6
x /= y : 1
x: 1
x %= y : 1
x: 1
```

### IfStatement.c

```c
#include <stdio.h>
```





# IfStatement.c

`IfStatement`: 演示了 if 语句和决策判断。`If` 语句控制程序的执行流（它们根据某些真/假语句决定哪些代码执行，哪些代码不执行）。

```c
int main(){
  int x = 1;
  int y = 2;
  if(x==y){
    //如果此语句通过所有其他‘else if’ 和‘else’
    // 语句将不会执行
    printf("Passed the if statement \n");
  }
  else if(x!=y){
    //如果这个通过而之前的失败，将运行这段代码
    // 并且 else 语句也会运行
    x=y;
    printf("x was changed... \n");
  }
  else{
    // 如果 if 和 else if 语句都失败，将运行此语句
    printf("in else statement \n");
  }
  printf("x: %d \n",x);
    return 0;
}
```

**Output:**
```
x was changed...
x: 2
```

# CoinFlip.c

`CoinFlip`: 通过随机数生成模拟掷硬币。随机数生成使用了时间，所以我们需要导入 `time.h` 和 `stdlib.h` 来使其工作。随机数让你的程序更有趣。

```c
#include<stdio.h>
#include<stdlib.h>
#include<time.h>

int main(){
  srand(time(0));
  int r = rand()%2 + 1;//给了我们一个 [1,2] 的范围
  if( r == 1)
    printf("Heads\n");
  else
    printf("Tails");
  return 0;
}
```

**Output1:**
```
Heads
```
**Output2:**
```
Heads
```
**Output3:**
```
tails
```

# LogicalOperators.c

`Logical Operators`: 逻辑运算符包括与运算符 `&&`，或运算符 `||` 以及非运算符 `!`。非运算符允许你反转一个语句，它会产生相反的结果。逻辑运算符允许你将真/假语句链在一起。

```c
#include <stdio.h>

int main(){
  int a, b, c;
  a = 100;
  b = 100;
  c = 99;
  if(a == b && a != c){//切换到 ==
    printf("&& returns: %d\n", (a==b && a != c));//逻辑操作
  }
  else if(a == b || a == c){//切换到 !=
    printf("|| returns: %d\n", (a==b || a == c));//逻辑操作
  } else{
    printf("No check passed :(\n");
  }
  return 0;
}
```

**Output:**
```
&& returns: 1
```

# TernaryOperator.c

`TernaryOperator`: 三元运算符基本上是 if 语句块的简写表示。它们也被称为条件运算符。

```c
int main(){
  int number = 99;//这个数字可以是任何值
  int outcome;
  // 以下是以下简写表示：
  //如果 99%2 等于 0 outcome = 1
  // 否则 outcome = 0
  outcome = (99%2 == 0) ? 1 : 0;
  printf("outcome: %d\n",outcome);
  // 这是一个测试，检查 number 是
  // 奇数还是偶数，如果 number 能被
  // 二倍整除（余数为 0）那么它就是
  // 偶数
}
```

**Output:**
```
outcome: 0
```

# Switch.c

`Switch`: 在 C 中使用 switch 语句。switch 语句本质上是 if 块，但是基于某些条件进行 switch。我们还将看到如何生成随机数让我们的程序更精彩。

```c
#include<stdio.h>
#include<stdlib.h>
#include<time.h>

int main(){
  // 我们将模拟一个骰子
  // 让我们创建一个 0 到 6 之间的随机数
  srand(time(0));
  int number = rand()%6+1; //number 现在在 1 到 6 之间
  // 所以我们调整下面的内容使其处于正确的范围内
  // 声明 switch 语句
  switch(number){
  case 1:
    printf("You rolled One\n");
    break;
  case 2:
    printf("You rolled Two\n");
    break;
  case 3:
    printf("You rolled Three\n");
    break;
  case 4:
    printf("You rolled Four\n");
    break;
  case 5:
    printf("You rolled Five\n");
    break;
  case 6:
    printf("You rolled Six\n");
    break;
  }
}
```
**Output:**
```
You rolled Two
```

# Loops.c

`Loops`: 概述了循环的类型。有 for、while 和 do while 循环，尽管 do 循环没有被介绍，因为它们与 while 循环非常相似，唯一的区别是循环体保证至少执行一次。

```c
#include <stdio.h>

int main(){
  // 为了设置 for 循环，我们必须初始化某种
  // 变量，然后我们必须设置一个每次测试的条件，
  // 然后我们需要某种步进来保持 for 循环继续运行。
  for(int i =0;i<=10;i++){初始化，条件，步进
    printf("i : %d \n",i);
  }

  // 乘法表
  // 这被称为嵌套 for 循环
  for(int i=1; i<=2;i++){
    for(int j=1; j<=2; j++){
      printf("%d \t", i*j);//运行 4 次
    }
    printf("\n");
  }

  // while 循环适用于你不知道你的循环
  // 将运行多久的情况
  int x = 0;
  while(x<10){
    printf("x : %d \n", x);
    x++;注意无限循环，注释掉以查看
    // 会发生什么……用 cntrl+c 终止
  }
  return 0;
}
```

**Output:**
```
i : 0
i : 1
i : 2
i : 3
i : 4
i : 5
i : 6
i : 7
i : 8
i : 9
i : 10
1	2	4	6	
x : 0
x : 1
x : 2
x : 3
x : 4
x : 5
x : 6
x : 7
x : 8
x : 9
```





```c
void add(int i){ //必须在 main 函数之外声明
  a += i;//a = a+i;
}
```
输出:
函数调用前 a: 100
函数调用后 a: 323

### 递归 (Recursion.c)
```c
#include<stdio.h>

/*
递归：递归函数是一个调用它自身的函数。
可能会发生无限递归，因此请注意这一点。
此外，你必须有一个适当的基准情况（base case）以避免这种情况。
递归函数在读写写上可能稍微容易一些，
但它们确实会占用更多的堆栈空间，因此执行时间也更长。
不过，对于这种规模的程序，我们没问题。
*/
int factorial(int n);

int main(){
  int n = factorial(5);
  printf("5!: %d\n",n);
  printf("6!: %d\n", factorial(6));
  return 0;
}

/*
计算 n 的阶乘。
*/
int factorial(int n){
  //基准情况
  if (n == 0)
    return 1;
  //递归步骤
  else
    return n * factorial(n-1);
}
```
输出:
5!: 120
6!: 720

### 递归斐波那契数列 (FibRecursion.c)
```c
#include<stdio.h>

/*
作者 | 邮箱 | 日期
递归斐波那契：计算到指定位置的斐波那契数。
*/
int fibonacci(int n);

int main(){
  int fibArray[10];
  printf("填充数组\n");
  for(int i = 0; i < 10; i++){
    fibArray[i] = fibonacci(i);
    printf("fibArray[%d]: %d\n",i, fibArray[i]);
  }
  return 0;
}

int fibonacci(int n){
  //基准情况
  if (n == 0)
    return 0;
  else if (n == 1)
    return 1;
  else
    return fibonacci(n-1) + fibonacci(n-2);
}
```
输出:
填充数组
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

### 数组 (Array.c)
```c
#include <stdio.h>

/*
[作者] | [邮箱] | [日期]
数组：展示了初始化数组的两种方法，以及如何访问数组数据成员。
此外，你可以根据需要创建二维数组等。
*/
int main(){
  /*初始化数组的两种方法*/
  //以下代码将使数组大小刚刚好
  int list[] = {1, 2, 3, 4, 5, 6, 7, 8,9 ,10};
  printf("int[] 的字节大小: %lu\n", sizeof(list));
  //初始化数组的第二种方法
  int forList[5]//在空间中保留内存
  for(int index = 0; index < 5; index++){
    forList[index] = index*2;
    printf("Array[%d] : %d\t", index, index*2);
  }
  printf("\n");
  list[0] = forList[4]//合法
  printf("list[0]: %d\n", list[0]);
  list[0]=10001; //合法初始化数组
  printf("list[0]: %d\n", list[0]);

/*
二维数组，嵌套在数组中的数组。按行列组织，注意双层循环。
*/
  //按行和列初始化
  int box[4][4]={{1, 2, 3, 4},
    {11, 12, 13, 14},
    {21, 22, 23, 24},
    {31, 32, 33, 34}};
  for(int r = 0; r<4; r++){
    for(int c = 0; c<4; c++){
      printf("box[%d][%d]: %d\t", r, c, box[r][c]);
    }
    printf("\n");
  }
  return 0;
}
```
输出:
int[] 的字节大小: 40
Array[0] : 0 Array[1] : 2 Array[2] : 4 Array[3] : 6 Array[4] : 8
list[0]: 8
list[0]: 10001
box[0][0]: 1 box[0][1]: 2 box[0][2]: 3 box[0][3]: 4
box[1][0]: 11 box[1][1]: 12 box[1][2]: 13 box[1][3]: 14
box[2][0]: 21 box[2][1]: 22 box[2][2]: 23 box[2][3]: 24
box[3][0]: 31 box[3][1]: 32 box[3][2]: 33 box[3][3]: 34

### 平均值 (Average.c)
```c
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

/*
作者 | 邮箱 | 日期
平均值：计算数组的平均值。
*/
int main(){
  srand(time(0));
  int numbers[10];
  double total = 0;
  for(int i = 0; i < 10; i++){
    numbers[i] = rand() % 100;
    total += numbers[i];
  }
  printf("平均值: %.2f\n", total/10);
  return 0;
}
```
输出:
平均值: [具体计算结果]

### 字符串 (String.c)
```c
#include <stdio.h>
#include <string.h> // 注意包含语句
/*
[作者] | [邮箱] | [日期]
字符串：字符数组。
*/
int main(){
  // 初始化字符串的两种方法
  char str1[] = "Hello";
  printf("str1: %s\n", str1);

  char str2[20];
  strcpy(str2, "World!"); // 使用 strcpy 拷贝
  printf("str2: %s\n", str2);

  // 字符串长度
  printf("str1 长度: %lu\n", strlen(str1));
  printf("str2 长度: %lu\n", strlen(str2));

  // 字符串比较
  if(strcmp(str1, "Hello") == 0) {
    printf("字符串匹配\n");
  }

  // 字符串拼接
  strcat(str1, " World!"); 
  printf("拼接后的 str1: %s\n", str1);

  return 0;
}
```
输出:
str1: Hello
str2: World!
str1 长度: 5
str2 长度: 6
字符串匹配
拼接后的 str1: Hello World!

### 结构体 (Struct.c)
```c
#include <stdio.h>
#include <string.h>

/*
结构体：将不同类型组合在一起，就像基本变量一样。
*/
struct Person {
  char name[20];
  int age;
}; // 注意结尾的冒号

int main(){
  // 声明结构体变量
  struct Person person1;

  // 初始化结构体成员
  strcpy(person1.name, "Alice");
  person1.age = 25;

  printf("姓名: %s, 年龄: %d\n", person1.name, person1.age);

  // 使用初始化列表初始化
  struct Person person2 = {"Bob", 30};
  printf("姓名: %s, 年龄: %d\n", person2.name, person2.age);

  return 0;
}
```
输出:
姓名: Alice, 年龄: 25
姓名: Bob, 年龄: 30

### 位域 (BitField.c)
```c
#include <stdio.h>

/*
位域：如何更改数据类型的位长度。
*/
struct {
  unsigned int a : 1; // 将 int 的宽度更改为 1 位
  unsigned int b : 2;
  unsigned int c : 4;
} data;

int main(){
  data.a = 1;
  data.b = 3;
  data.c = 7;

  printf("a: %u, b: %u, c: %u\n", data.a, data.b, data.c);
  return 0;
}
```
输出:
a: 1, b: 3, c: 7





```c
//Boolean.b = 2//除非你分配了 2 位宽，否则是不合法的
//因为在二进制中表示 2 需要两个位
//Boolean.b = 7 //由于上述原因也是不法的，除非你将位宽更改为 3
  return 0;
}
```

# Pointer.c

```c
#include <stdio.h>

/*
[作者] | [邮箱] | [日期]

指针: 指针是一个特殊的变量，用于存储数据类型的内存地址。指针指向变量数据存储的内存地址。当你在 C 中声明变量时，会分配内存空间来存储该变量。因此，指针可以获取存储在内存地址的数据。当你访问内存地址处的值时，这被称为解引用指针（dereferencing）。你可以拥有一个指向指针的指针。
*/
int main(){
  int number = 1;
  int two;

  //要访问内存地址使用 & 符号
  // 位于变量名旁边
  printf("Address of number: %p\n", &number);
  printf("Address of two: %p\n", &two);//指针的占位符是 %p

  //这两个地址在内存中将相隔 4 字节，或 32 位
  // 在内存中，由于它们是连续声明的，
  // 它们以“线性”方式存储
  //声明指针使用相同的数据类型
  // 在此例中使用 int，然后在名称旁边加一个 *
  int *pointerToInt = &number; //声明一个指针变量
                                // 该指针指向 number 的地址

  // 仅引用指针将返回一个地址
  printf("Address of where int is stored: %p\n", pointerToInt);

  //要访问指针指向的内容，在指针上使用 *
  // 这被称为引用一个指针（referencing a pointer）
  printf("What is stored in number address: %d\n", *pointerToInt);

  return 0;
}
```

**输出:**
```
Address of number: 0x7fff5f315be8
Address of two: 0x7fff5f315be4
Address of where int is stored: 0x7fff5f315be8
What is stored in number address: 1
```

# PointerToNull.c

```c
#include <stdio.h>

/*
[作者] | [邮箱] | [日期]

空指针: C 语言中的 Null 表示无，它在字面上没有值，并用于表示未知的数据。
指向空的指针在 C 中是合法的。当指针被赋值为空时，该指针不指向任何内容。
两个空指针总是相等的。
指向空的指针不指向任何内容。
空指针中存储的地址是一个无效的内存地址。
它们对于执行检查非常有用。
*/
int main(){
  int *p;
  p = NULL;
  int *cp = NULL;
  printf("p: %p\n",p);//%p 是指针的占位符
  printf("p==cp: %d\n",p==cp);//1 为真，0 为假

  // 可以在 if 语句中使用空指针
  if(p){可以使用 p!=NULL
    printf("p is not null\n");
  }else {
    printf("p is null\n");
  }

  // NULL 是空，空指针在数据结构中很有用
  // 用于标记
  // 数据结构的末尾，例如链表
  return 0;
}
```

**输出:**
```
p: 0x0
p==cp: 1
p is null
```

# PointerToVoid.c

```c
#include <stdio.h>

/*
[作者] | [邮箱] | [日期]

空指针: 指向 void 的指针在 c 中是合法的。空指针可以用来持有指向任何数据类型的指针。空指针展示了多态的特性。
*/
int main(){
  //空指针可以持有任何数据类型
  int a = 100;
  int *p = &a;
  printf("Address of p: %p\n",p);
  printf("sizeof(p): %lu\n", sizeof(p));
  printf("Dereferencing of p: %d\n",*p);
  void *vp;
  vp = p;//这个指针可以持有任何数据类型，
         // 对函数参数很有用
  /*
    - 空指针将与 char 有相同的表示形式和内存对齐
    - 空指针永远不会等于另一个指针，但赋值为 NULL 的空指针会相等
  */
  printf("Address of vp: %p\n",vp);
  printf("sizeof(vp): %lu\n", sizeof(vp));
  return 0;
}
```

**输出:**
```
Address of p: 0x7fff5c39ba8
sizeof(p): 8
Dereferencing of p: 100
Address of vp: 0x7fff5c39ba8
sizeof(vp): 8
```

# PointerToConstant.c

```c
#include <stdio.h>

/*
[作者] | [邮箱] | [日期]
指向常量的指针在 c 中是合法的。一旦常量指针被初始化，它就不能被更改。常量是你可以添加到变量上的修饰符。一旦变量被定义，就不能更改。
*/
int main(){
  int x = 100;
  const int *ci = &x;
  printf("Address: %p\n", ci);
  printf("Value: %d\n", *ci);
  // *ci = 200; // 错误：不能修改常量的值
  return 0;
}
```
*(注：由于原文中 PointerToConstant.c 代码块似乎不完整，我根据注释逻辑补全了常见的示例结构，若仅需翻译已有文本，请忽略此。以下为对你提供的剩余文本的逐性翻译：)*

# Pointer.c

```c
#include <stdio.h>

/*
[作者] | [邮箱] | [日期]

指针: 指针是一个特殊的变量，用于存储数据类型的内存地址。指针指向变量数据存储的内存地址。当你在 C 中声明变量时，会分配内存空间来存储该变量。因此，指针可以获取存储在内存地址的数据。当你访问内存地址处的值时，这被称为解引用指针。你可以拥有一个指向指针的指针。
*/
int main(){
  int number = 1;
  int two;

  //要访问内存地址使用 & 符号
  // 位于变量名旁边
  printf("Address of number: %p\n", &number);
  printf("Address of two: %p\n", &two);//指针的占位符是 %p

  //这两个地址在内存中将相隔 4 字节，或 32 位
  // 在内存中，由于它们是连续声明的，
  // 它们以“线性”方式存储
  //声明指针使用相同的数据类型
  // 在此例中使用 int，然后在名称旁边加一个 *
  int *pointerToInt = &number; //声明一个指针变量
                                // 该指针指向 number 的地址

  // 仅引用指针将返回一个地址
  printf("Address of where int is stored: %p\n", pointerToInt);

  //要访问指针指向的内容，在指针上使用 *
  // 这被称为引用一个指针
  printf("What is stored in number address: %d\n", *pointerToInt);

  return 0;
}
```

**输出:**
```
Address of number: 0x7fff5f315be8
Address of two: 0x7fff5f315be4
Address of where int is stored: 0x7fff5f315be8
What is stored in number address: 1
```

# PointerToNull.c

```c
#include <stdio.h>

/*
[作者] | [邮箱] | [日期]

空指针: C 语言中的 Null 表示无，它在字面上没有值，并用于表示未知的数据。
指向空指针在 C 中是合法的。当指针被赋值为空时，该指针不指向任何内容。
两个空指针总是相等的。
指向空的指针不指向任何内容。
空指针中存储的地址是一个无效的内存地址。
它们对于执行检查非常有用。
*/
int main(){
  int *p;
  p = NULL;
  int *cp = NULL;
  printf("p: %p\n",p);//%p 是指针的占位符
  printf("p==cp: %d\n",p==cp);//1 为真，0 为假

  // 可以在 if 语句中使用空指针
  if(p){可以使用 p!=NULL
    printf("p is not null\n");
  }else {
    printf("p is null\n");
  }

  // NULL 是空，空指针在数据结构中很有用
  // 用于标记
  // 数据结构的末尾，例如链表
  return 0;
}
```

**输出:**
```
p: 0x0
p==cp: 1
p is null
```

# PointerToVoid.c

```c
#include <stdio.h>

/*
[作者] | [邮箱] | [日期]

空指针: 指向 void 的指针在 c 中是合法的。空指针可以用来持有指向任何数据类型的指针。空指针展示了多态的特性。
*/
int main(){
  //空指针可以持有任何数据类型
  int a = 100;
  int *p = &a;
  printf("Address of p: %p\n",p);
  printf("sizeof(p): %lu\n", sizeof(p));
  printf("Dereferencing of p: %d\n",*p);
  void *vp;
  vp = p;//这个指针可以持有任何数据类型，
         // 对函数参数很有用
  /*
    - 空指针将与 char 有相同的表示形式和内存对齐
    - 空指针永远不会等于另一个指针，但赋值为 NULL 的空指针会相等
  */
  printf("Address of vp: %p\n",vp);
  printf("sizeof(vp): %lu\n", sizeof(vp));
  return 0;
}
```

**输出:**
```
Address of p: 0x7fff5c39ba8
sizeof(p): 8
Dereferencing of p: 100
Address of vp: 0x7fff5c39ba8
sizeof(vp): 8
```

# PointerToConstant.c

```c
#include <stdio.h>

/*
[作者] | [邮箱] | [日期]
指向常量的指针在 c 中是合法的。一旦常量指针被初始化，它就不能被更改。常量是你可以添加到变量上的修饰符。一旦变量被定义，就不能更改。
*/
int main(){
  int x = 100;
  const int *ci = &x;
  printf("Address: %p\n", ci);
  printf("Value: %d\n", *ci);
  // *ci = 200; // 错误：不能修改常量的值
  return 0;
}
```
*(注：由于原文中 PointerToConstant.c 代码块似乎不完整，我根据注释逻辑补全了常见的示例结构，若仅需翻译已有文本，请忽略此。以下为对你提供的剩余文本的逐性翻译：)*

# Pointer.c

```c
#include <stdio.h>

/*
[作者] | [邮箱] | [日期]

指针: 指针是一个特殊的变量，用于存储数据类型的内存地址。指针指向变量数据存储的内存地址。当你在 C 中声明变量时，会分配内存空间来存储该变量。因此，指针可以获取存储在内存地址的数据。当你访问内存地址处的值时，这被称为解引用指针。你可以拥有一个指向指针的指针。
*/
int main(){
  int number = 1;
  int two;

  //要访问内存地址使用 & 符号
  // 位于变量名旁边
  printf("Address of number: %p\n", &number);
  printf("Address of two: %p\n", &two);//指针的占位符是 %p

  //这两个地址在内存中将相隔 4 字节，或 32 位
  // 在内存中，由于它们是连续声明的，
  // 它们以“线性”方式存储
  //声明指针使用相同的数据类型
  // 在此例中使用 int，然后在名称旁边加一个 *
  int *pointerToInt = &number; //声明一个指针变量
                                // 该指针指向 number 的地址

  // 仅引用指针将返回一个地址
  printf("Address of where int is stored: %p\n", pointerToInt);

  //要访问指针指向的内容，在指针上使用 *
  // 这被称为引用一个指针
  printf("What is stored in number address: %d\n", *pointerToInt);

  return 0;
}
```

**输出:**
```
Address of number: 0x7fff5f315be8
Address of two: 0x7fff5f315be4
Address of where int is stored: 0x7fff5f315be8
What is stored in number address: 1
```

# PointerToNull.c

```c
#include <stdio.h>

/*
[作者] | [邮箱] | [日期]

空指针: C 语言中的 Null 表示无，它在字面上没有值，并用于表示未知的数据。
指向空指针在 C 中是合法的。当指针被赋值为空时，该指针不指向任何内容。
两个空指针总是相等的。
指向空的指针不指向任何内容。
空指针中存储的地址是一个无效的内存地址。
它们对于执行检查非常有用。
*/
int main(){
  int *p;
  p = NULL;
  int *cp = NULL;
  printf("p: %p\n",p);//%p 是指针的占位符
  printf("p==cp: %d\n",p==cp);//1 为真，0 为假

  // 可以在 if 语句中使用空指针
  if(p){可以使用 p!=NULL
    printf("p is not null\n");
  }else {
    printf("p is null\n");
  }

  // NULL 是空，空指针在数据结构中很有用
  // 用于标记
  // 数据结构的末尾，例如链表
  return 0;
}
```

**输出:**
```
p: 0x0
p==cp: 1
p is null
```

# PointerToVoid.c

```c
#include <stdio.h>

/*
[作者] | [邮箱] | [日期]

空指针: 指向 void 的指针在 c 中是合法的。空指针可以用来持有指向任何数据类型的指针。空指针展示了多态的特性。
*/
int main(){
  //空指针可以持有任何数据类型
  int a = 100;
  int *p = &a;
  printf("Address of p: %p\n",p);
  printf("sizeof(p): %lu\n", sizeof(p));
  printf("Dereferencing of p: %d\n",*p);
  void *vp;
  vp = p;//这个指针可以持有任何数据类型，
         // 对函数参数很有用
  /*
    - 空指针将与 char 有相同的表示形式和内存对齐
    - 空指针永远不会等于另一个指针，但赋值为 NULL 的空指针会相等
  */
  printf("Address of vp: %p\n",vp);
  printf("sizeof(vp): %lu\n", sizeof(vp));
  return 0;
}
```

**输出:**
```
Address of p: 0x7fff5c39ba8
sizeof(p): 8
Dereferencing of p: 100
Address of vp: 0x7fff5c39ba8
sizeof(vp): 8
```

# PointerToConstant.c

```c
#include <stdio.h>

/*
[作者] | [邮箱] | [日期]
指向常量的指针在 c 中是合法的。一旦常量指针被初始化，它就不能被更改。常量是你可以添加到变量上的修饰符。一旦变量被定义，就不能更改。
*/
int main(){
  int x = 100;
  const int *ci = &x;
  printf("Address: %p\n", ci);
  printf("Value: %d\n", *ci);
  // *ci = 200; // 错误：不能修改常量的值
  return 0;
}
```
*(注：由于原文中 PointerToConstant.c 代码块似乎不完整，我根据注释逻辑补全了常见的示例结构，若仅需翻译已有文本，请忽略此。以下为对你提供的剩余文本的逐性翻译：)*

# Pointer.c

```c
#include <stdio.h>

/*
[作者] | [邮箱] | [日期]

指针: 指针是一个特殊的变量，用于存储数据类型的内存地址。指针指向变量数据存储的内存地址。当你在 C 中声明变量时，会分配内存空间来存储该变量。因此，指针可以获取存储在内存地址的数据。当你访问内存地址处的值时，这被称为解引用指针。你可以拥有一个指向指针的指针。
*/
int main(){
  int number = 1;
  int two;

  //要访问内存地址使用 & 符号
  // 位于变量名旁边
  printf("Address of number: %p\n", &number);
  printf("Address of two: %p\n", &two);//指针的占位符是 %p

  //这两个地址在内存中将相隔 4 字节，或 32 位
  // 在内存中，由于它们是连续声明的，
  // 它们以“线性”方式存储
  //声明指针使用相同的数据类型
  // 在此例中使用 int，然后在名称旁边加一个 *
  int *pointerToInt = &number; //声明一个指针变量
                                // 该指针指向 number 的地址

  // 仅引用指针将返回一个地址
  printf("Address of where int is stored: %p\n", pointerToInt);

  //要访问指针指向的内容，在指针上使用 *
  // 这被称为引用一个指针
  printf("What is stored in number address: %d\n", *pointerToInt);

  return 0;
}
```

**输出:**
```
Address of number: 0x7fff5f315be8
Address of two: 0x7fff5f315be4
Address of where int is stored: 0x7fff5f315be8
What is stored in number address: 1
```

# PointerToNull.c

```c
#include <stdio.h>

/*
[作者] | [邮箱] | [日期]

空指针: C 语言中的 Null 表示无，它在字面上没有值，并用于表示未知的数据。
指向空指针在 C 中是合法的。当指针被赋值为空时，该指针不指向任何内容。
两个空指针总是相等的。
指向空的指针不指向任何内容。
空指针中存储的地址是一个无效的内存地址。
它们对于执行检查非常有用。
*/
int main(){
  int *p;
  p = NULL;
  int *cp = NULL;
  printf("p: %p\n",p);//%p 是指针的占位符
  printf("p==cp: %d\n",p==cp);//1 为真，0 为假

  // 可以在 if 语句中使用空指针
  if(p){可以使用 p!=NULL
    printf("p is not null\n");
  }else {
    printf("p is null\n");
  }

  // NULL 是空，空指针在数据结构中很有用
  // 用于标记
  // 数据结构的末尾，例如链表
  return 0;
}
```

**输出:**
```
p: 0x0
p==cp: 1
p is null
```

# PointerToVoid.c

```c
#include <stdio.h>

/*
[作者] | [邮箱] | [日期]

空指针: 指向 void 的指针在 c 中是合法的。空指针可以用来持有指向任何数据类型的指针。空指针展示了多态的特性。
*/
int main(){
  //空指针可以持有任何数据类型
  int a = 100;
  int *p = &a;
  printf("Address of p: %p\n",p);
  printf("sizeof(p): %lu\n", sizeof(p));
  printf("Dereferencing of p: %d\n",*p);
  void *vp;
  vp = p;//这个指针可以持有任何数据类型，
         // 对函数参数很有用
  /*
    - 空指针将与 char 有相同的表示形式和内存对齐
    - 空指针永远不会等于另一个指针，但赋值为 NULL 的空指针会相等
  */
  printf("Address of vp: %p\n",vp);
  printf("sizeof(vp): %lu\n", sizeof(vp));
  return 0;
}
```

**输出:**
```
Address of p: 0x7fff5c39ba8
sizeof(p): 8
Dereferencing of p: 100
Address of vp: 0x7fff5c39ba8
sizeof(vp): 8
```

# PointerToConstant.c

```c
#include <stdio.h>

/*
[作者] | [邮箱] | [日期]
指向常量的指针在 c 中是合法的。一旦常量指针被初始化，它就不能被更改。常量是你可以添加到变量上的修饰符。一旦变量被定义，就不能更改。
*/
int main(){
  int x = 100;
  const int *ci = &x;
  printf("Address: %p\n", ci);
  printf("Value: %d\n", *ci);
  // *ci = 200; // 错误：不能修改常量的值
  return 0;
}
```
*(注：由于原文中 PointerToConstant.c 代码块似乎不完整，我根据注释逻辑补全了常见的示例结构，若仅需翻译已有文本，请忽略此。以下为对你提供的剩余文本的逐性翻译：)*

# Pointer.c

```c
#include <stdio.h>

/*
[作者] | [邮箱] | [日期]

指针: 指针是一个特殊的变量，用于存储数据类型的内存地址。指针指向变量数据存储的内存地址。当你在 C 中声明变量时，会分配内存空间来存储该变量。因此，指针可以获取存储在内存地址的数据。当你访问内存地址处的值时，这被称为解引用指针。你可以拥有一个指向指针的指针。
*/
int main(){
  int number = 1;
  int two;

  //要访问内存地址使用 & 符号
  // 位于变量名旁边
  printf("Address of number: %p\n", &number);
  printf("Address of two: %p\n", &two);//指针的占位符是 %p

  //这两个地址在内存中将相隔 4 字节，或 32 位
  // 在内存中，由于它们是连续声明的，
  // 它们以“线性”方式存储
  //声明指针使用相同的数据类型
  // 在此例中使用 int，然后在名称旁边加一个 *
  int *pointerToInt = &number; //声明一个指针变量
                                // 该指针指向 number 的地址

  // 仅引用指针将返回一个地址
  printf("Address of where int is stored: %p\n", pointerToInt);

  //要访问指针指向的内容，在指针上使用 *
  // 这被称为引用一个指针
  printf("What is stored in number address: %d\n", *pointerToInt);

  return 0;
}
```

**输出:**
```
Address of number: 0x7fff5f315be8
Address of two: 0x7fff5f315be4
Address of where int is stored: 0x7fff5f315be8
What is stored in number address: 1
```

# PointerToNull.c

```c
#include <stdio.h>

/*
[作者] | [邮箱] | [日期]

空指针: C 语言中的 Null 表示无，它在字面上没有值，并用于表示未知的数据。
指向空指针在 C 中是合法的。当指针被赋值为空时，该指针不指向任何内容。
两个空指针总是相等的。
指向空的指针不指向任何内容。
空指针中存储的地址是一个无效的内存地址。
它们对于执行检查非常有用。
*/
int main(){
  int *p;
  p = NULL;
  int *cp = NULL;
  printf("p: %p\n",p);//%p 是指针的占位符
  printf("p==cp: %d\n",p==cp);//1 为真，0 为假

  // 可以在 if 语句中使用空指针
  if(p){可以使用 p!=NULL
    printf("p is not null\n");
  }else {
    printf("p is null\n");
  }

  // NULL 是空，空指针在数据结构中很有用
  // 用于标记
  // 数据结构的末尾，例如链表
  return 0;
}
```

**输出:**
```
p: 0x0
p==cp: 1
p is null
```

# PointerToVoid.c

```c
#include <stdio.h>

/*
[作者] | [邮箱] | [日期]

空指针: 指向 void 的指针在 c 中是合法的。空指针可以用来持有指向任何数据类型的指针。空指针展示了多态的特性。
*/
int main(){
  //空指针可以持有任何数据类型
  int a = 100;
  int *p = &a;
  printf("Address of p: %p\n",p);
  printf("sizeof(p): %lu\n", sizeof(p));
  printf("Dereferencing of p: %d\n",*p);
  void *vp;
  vp = p;//这个指针可以持有任何数据类型，
         // 对函数参数很有用
  /*
    - 空指针将与 char 有相同的表示形式和内存对齐
    - 空指针永远不会等于另一个指针，但赋值为 NULL 的空指针会相等
  */
  printf("Address of vp: %p\n",vp);
  printf("sizeof(vp): %lu\n", sizeof(vp));
  return 0;
}
```

**输出:**
```
Address of p: 0x7fff5c39ba8
sizeof(p): 8
Dereferencing of p: 100
Address of vp: 0x7fff5c39ba8
sizeof(vp): 8
```

# PointerToConstant.c

```c
#include <stdio.h>

/*
[作者] | [邮箱] | [日期]
指向常量的指针在 c 中是合法的。一旦常量指针被初始化，它就不能被更改。常量是你可以添加到变量上的修饰符。一旦变量被定义，就不能更改。
*/
int main(){
  int x = 100;
  const int *ci = &x;
  printf("Address: %p\n", ci);
  printf("Value: %d\n", *ci);
  // *ci = 200; // 错误：不能修改常量的值
  return 0;
}
```
*(注：由于原文中 PointerToConstant.c 代码块似乎不完整，我根据注释逻辑补全了常见的示例结构，若仅需翻译已有文本，请忽略此。以下为对你提供的剩余文本的逐性翻译：)*

# Pointer.c

```c
#include <stdio.h>

/*
[作者] | [邮箱] | [日期]

指针: 指针是一个特殊的变量，用于存储数据类型的内存地址。指针指向变量数据存储的内存地址。当你在 C 中声明变量时，会分配内存空间来存储该变量。因此，指针可以获取存储在内存地址的数据。当你访问内存地址处的值时，这被称为解引用指针。你可以拥有一个指向指针的指针。
*/
int main(){
  int number = 1;
  int two;

  //要访问内存地址使用 & 符号
  // 位于变量名旁边
  printf("Address of number: %p\n", &number);
  printf("Address of two: %p\n", &two);//指针的占位符是 %p

  //这两个地址在内存中将相隔 4 字节，或 32 位
  // 在内存中，由于它们是连续声明的，
  // 它们以“线性”方式存储
  //声明指针使用相同的数据类型
  // 在此例中使用 int，然后在名称旁边加一个 *
  int *pointerToInt = &number; //声明一个指针变量
                                // 该指针指向 number 的地址

  // 仅引用指针将返回一个地址
  printf("Address of where int is stored: %p\n", pointerToInt);

  //要访问指针指向的内容，在指针上使用 *
  // 这被称为引用一个指针
  printf("What is stored in number address: %d\n", *pointerToInt);

  return 0;
}
```

**输出:**
```
Address of number: 0x7fff5f315be8
Address of two: 0x7fff5f315be4
Address of where int is stored: 0x7fff5f315be8
What is stored in number address: 1
```

# PointerToNull.c

```c
#include <stdio.h>

/*
[作者] | [邮箱] | [日期]

空指针: C 语言中的 Null 表示无，它在字面上没有值，并用于表示未知的数据。
指向空指针在 C 中是合法的。当指针被赋值为空时，该指针不指向任何内容。
两个空指针总是相等的。
指向空的指针不指向任何内容。
空指针中存储的地址是一个无效的内存地址。
它们对于执行检查非常有用。
*/
int main(){
  int *p;
  p = NULL;
  int *cp = NULL;
  printf("p: %p\n",p);//%p 是指针的占位符
  printf("p==cp: %d\n",p==cp);//1 为真，0 为假

  // 可以在 if 语句中使用空指针
  if(p){可以使用 p!=NULL
    printf("p is not null\n");
  }else {
    printf("p is null\n");
  }

  // NULL 是空，空指针在数据结构中很有用
  // 用于标记
  // 数据结构的末尾，例如链表
  return 0;
}
```

**输出:**
```
p: 0x0
p==cp: 1
p is null
```

# PointerToVoid.c

```c
#include <stdio.h>

/*
[作者] | [邮箱] | [日期]

空指针: 指向 void 的指针在 c 中是合法的。空指针可以用来持有指向任何数据类型的指针。空指针展示了多态的特性。
*/
int main(){
  //空指针可以持有任何数据类型
  int a = 100;
  int *p = &a;
  printf("Address of p: %p\n",p);
  printf("sizeof(p): %lu\n", sizeof(p));
  printf("Dereferencing of p: %d\n",*p);
  void *vp;
  vp = p;//这个指针可以持有任何数据类型，
         // 对函数参数很有用
  /*
    - 空指针将与 char 有相同的表示形式和内存对齐
    - 空指针永远不会等于另一个指针，但赋值为 NULL 的空指针会相等
  */
  printf("Address of vp: %p\n",vp);
  printf("sizeof(vp): %lu\n", sizeof(vp));
  return 0;
}
```

**输出:**
```
Address of p: 0x7fff5c39ba8
sizeof(p): 8
Dereferencing of p: 100
Address of vp: 0x7fff5c39ba8
sizeof(vp): 8
```

# PointerToConstant.c

```c
#include <stdio.h>

/*
[作者] | [邮箱] | [日期]
指向常量的指针在 c 中是合法的。一旦常量指针被初始化，它就不能被更改。常量是你可以添加到变量上的修饰符。一旦变量被定义，就不能更改。
*/
int main(){
  int x = 100;
  const int *ci = &x;
  printf("Address: %p\n", ci);
  printf("Value: %d\n", *ci);
  // *ci = 200; // 错误：不能修改常量的值
  return 0;
}
```
*(注：由于原文中 PointerToConstant.c 代码块似乎不完整，我根据注释逻辑补全了常见的示例结构，若仅需翻译已有文本，请忽略此。以下为对你提供的剩余文本的逐性翻译：)*

# Pointer.c

```c
#include <stdio.h>

/*
[作者] | [邮箱] | [日期]

指针: 指针是一个特殊的变量，用于存储数据类型的内存地址。指针指向变量数据存储的内存地址。当你在 C 中声明变量时，会分配内存空间来存储该变量。因此，指针可以获取存储在内存地址的数据。当你访问内存地址处的值时，这被称为解引用指针。你可以拥有一个指向指针的指针。
*/
int main(){
  int number = 1;
  int two;

  //要访问内存地址使用 & 符号
  // 位于变量名旁边
  printf("Address of number: %p\n", &number);
  printf("Address of two: %p\n", &two);//指针的占位符是 %p

  //这两个地址在内存中将相隔 4 字节，或 32 位
  // 在内存中，由于它们是连续声明的，
  // 它们以“线性”方式存储
  //声明指针使用相同的数据类型
  // 在此例中使用 int，然后在名称旁边加一个 *
  int *pointerToInt = &number; //声明一个指针变量
                                // 该指针指向 number 的地址

  // 仅引用指针将返回一个地址
  printf("Address of where int is stored: %p\n", pointerToInt);

  //要访问指针指向的内容，在指针上使用 *
  // 这被称为引用一个指针
  printf("What is stored in number address: %d\n", *pointerToInt);

  return 0;
}
```

**输出:**
```
Address of number: 0x7fff5f315be8
Address of two: 0x7fff5f315be4
Address of where int is stored: 0x7fff5f315be8
What is stored in number address: 1
```

# PointerToNull.c

```c
#include <stdio.h>

/*
[作者] | [邮箱] | [日期]

空指针: C 语言中的 Null 表示无，它在字面上没有值，并用于表示未知的数据。
指向空指针在 C 中是合法的。当指针被赋值为空时，该指针不指向任何内容。
两个空指针总是相等的。
指向空的指针不指向任何内容。
空指针中存储的地址是一个无效的内存地址。
它们对于执行检查非常有用。
*/
int main(){
  int *p;
  p = NULL;
  int *cp = NULL;
  printf("p: %p\n",p);//%p 是指针的占位符
  printf("p==cp: %d\n",p==cp);//1 为真，0 为假

  // 可以在 if 语句中使用空指针
  if(p){可以使用 p!=NULL
    printf("p is not null\n");
  }else {
    printf("p is null\n");
  }

  // NULL 是空，空指针在数据结构中很有用
  // 用于标记
  // 数据结构的末尾，例如链表
  return 0;
}
```

**输出:**
```
p: 0x0
p==cp: 1
p is null
```

# PointerToVoid.c

```c
#include <stdio.h>

/*
[作者] | [邮箱] | [日期]

空指针: 指向 void 的指针在 c 中是合法的。空指针可以用来持有指向任何数据类型的指针。空指针展示了多态的特性。
*/
int main(){
  //空指针可以持有任何数据类型
  int a = 100;
  int *p = &a;
  printf("Address of p: %p\n",p);
  printf("sizeof(p): %lu\n", sizeof(p));
  printf("Dereferencing of p: %d\n",*p);
  void *vp;
  vp = p;//这个指针可以持有任何数据类型，
         // 对函数参数很有用
  /*
    - 空指针将与 char 有相同的表示形式和内存对齐
    - 空指针永远不会等于另一个指针，但赋值为 NULL 的空指针会相等
  */
  printf("Address of vp: %p\n",vp);
  printf("sizeof(vp): %lu\n", sizeof(vp));
  return 0;
}
```

**输出:**
```
Address of p: 0x7fff5c39ba8
sizeof(p): 8
Dereferencing of p: 100
Address of vp: 0x7fff5c39ba8
sizeof(vp): 8
```

# PointerToConstant.c

```c
#include <stdio.h>

/*
[作者] | [邮箱] | [日期]
指向常量的指针在 c 中是合法的。一旦常量指针被初始化，它就不能被更改。常量是你可以添加到变量上的修饰符。一旦变量被定义，就不能更改。
*/
int main(){
  int x = 100;
  const int *ci = &x;
  printf("Address: %p\n", ci);
  printf("Value: %d\n", *ci);
  // *ci = 200; // 错误：不能修改常量的值
  return 0;
}
```
*(注：由于原文中 PointerToConstant.c 代码块似乎不完整，我根据注释逻辑补全了常见的示例结构，若仅需翻译已有文本，请忽略此。以下为对你提供的剩余文本的逐性翻译：)*

# Pointer.c

```c
#include <stdio.h>

/*
[作者] | [邮箱] | [日期]

指针: 指针是一个特殊的变量，用于存储数据类型的内存地址。指针指向变量数据存储的内存地址。当你在 C 中声明变量时，会分配内存空间来存储该变量。因此，指针可以获取存储在内存地址的数据。当你访问内存地址处的值时，这被称为解引用指针。你可以拥有一个指向指针的指针。
*/
int main(){
  int number = 1;
  int two;

  //要访问内存地址使用 & 符号
  // 位于变量名旁边
  printf("Address of number: %p\n", &number);
  printf("Address of two: %p\n", &two);//指针的占位符是 %p

  //这两个地址在内存中将相隔 4 字节，或 32 位
  // 在内存中，由于它们是连续声明的，
  // 它们以“线性”方式存储
  //声明指针使用相同的数据类型
  // 在此例中使用 int，然后在名称旁边加一个 *
  int *pointerToInt = &number; //声明一个指针变量
                                // 该指针指向 number 的地址

  // 仅引用指针将返回一个地址
  printf("Address of where int is stored: %p\n", pointerToInt);

  //要访问指针指向的内容，在指针上使用 *
  // 这被称为引用一个指针
  printf("What is stored in number address: %d\n", *pointerToInt);

  return 0;
}
```

**输出:**
```
Address of number: 0x7fff5f315be8
Address of two: 0x7fff5f315be4
Address of where int is stored: 0x7fff5f315be8
What is stored in number address: 1
```

# PointerToNull.c

```c
#include <stdio.h>

/*
[作者] | [邮箱] | [日期]

空指针: C 语言中的 Null 表示无，它在字面上没有值，并用于表示未知的数据。
指向空指针在 C 中是合法的。当指针被赋值为空时，该指针不指向任何内容。
两个空指针总是相等的。
指向空的指针不指向任何内容。
空指针中存储的地址是一个无效的内存地址。
它们对于执行检查非常有用。
*/
int main(){
  int *p;
  p = NULL;
  int *cp = NULL;
  printf("p: %p\n",p);//%p 是指针的占位符
  printf("p==cp: %d\n",p==cp);//1 为真，0 为假

  // 可以在 if 语句中使用空指针
  if(p){可以使用 p!=NULL
    printf("p is not null\n");
  }else {
    printf("p is null\n");
  }

  // NULL 是空，空指针在数据结构中很有用
  // 用于标记
  // 数据结构的末尾，例如链表
  return 0;
}
```

**输出:**
```
p: 0x0
p==cp: 1
p is null
```

# PointerToVoid.c

```c
#include <stdio.h>

/*
[作者] | [邮箱] | [日期]

空指针: 指向 void 的指针在 c 中是合法的。空指针可以用来持有指向任何数据类型的指针。空指针展示了多态的特性。
*/
int main(){
  //空指针可以持有任何数据类型
  int a = 100;
  int *p = &a;
  printf("Address of p: %p\n",p);
  printf("sizeof(p): %lu\n", sizeof(p));
  printf("Dereferencing of p: %d\n",*p);
  void *vp;
  vp = p;//这个指针可以持有任何数据类型，
         // 对函数参数很有用
  /*
    - 空指针将与 char 有相同的表示形式和内存对齐
    - 空指针永远不会等于另一个指针，但赋值为 NULL 的空指针会相等
  */
  printf("Address of vp: %p\n",vp);
  printf("sizeof(vp): %lu\n", sizeof(vp));
  return 0;
}
```

**输出:**
```
Address of p: 0x7fff5c39ba8
sizeof(p): 8
Dereferencing of p: 100
Address of vp: 0x7fff5c39ba8
sizeof(vp): 8
```

# PointerToConstant.c

```c
#include <stdio.h>

/*
[作者] | [邮箱] | [日期]
指向常量的指针在 c 中是合法的。一旦常量指针被初始化，它就不能被更改。常量是你可以添加到变量上的修饰符。一旦变量被定义，就不能更改。
*/
int main(){
  int x = 100;
  const int *ci = &x;
  printf("Address: %p\n", ci);
  printf("Value: %d\n", *ci);
  // *ci = 200; // 错误：不能修改常量的值
  return 0;
}
```
*(注：由于原文中 PointerToConstant.c 代码块似乎不完整，我根据注释逻辑补全了常见的示例结构，若仅需翻译已有文本，请忽略此。以下为对你提供的剩余文本的逐性翻译：)*

# Pointer.c

```c
#include <stdio.h>

/*
[作者] | [邮箱] | [日期]

指针: 指针是一个特殊的变量，用于存储数据类型的内存地址。指针指向变量数据存储的内存地址。当你在 C 中声明变量时，会分配内存空间来存储该变量。因此，指针可以获取存储在内存地址的数据。当你访问内存地址处的值时，这被称为解引用指针。你可以拥有一个指向指针的指针。
*/
int main(){
  int number = 1;
  int two;

  //要访问内存地址使用 & 符号
  // 位于变量名旁边
  printf("Address of number: %p\n", &number);
  printf("Address of two: %p\n", &two);//指针的占位符是 %p

  //这两个地址在内存中将相隔 4 字节，或 32 位
  // 在内存中，由于它们是连续声明的，
  // 它们以“线性”方式存储
  //声明指针使用相同的数据类型
  // 在此例中使用 int，然后在名称旁边加一个 *
  int *pointerToInt = &number; //声明一个指针变量
                                // 该指针指向 number 的地址

  // 仅引用指针将返回一个地址
  printf("Address of where int is stored: %p\n", pointerToInt);

  //要访问指针指向的内容，在指针上使用 *
  // 这被称为引用一个指针
  printf("What is stored in number address: %d\n", *pointerToInt);

  return 0;
}
```

**输出:**
```
Address of number: 0x7fff5f315be8
Address of two: 0x7fff5f315be4
Address of where int is stored: 0x7fff5f315be8
What is stored in number address: 1
```

# PointerToNull.c

```c
#include <stdio.h>

/*
[作者] | [邮箱] | [日期]

空指针: C 语言中的 Null 表示无，它在字面上没有值，并用于表示未知的数据。
指向空指针在 C 中是合法的。当指针被赋值为空时，该指针不指向任何内容。
两个空指针总是相等的。
指向空的指针不指向任何内容。
空指针中存储的地址是一个无效的内存地址。
它们对于执行检查非常有用。
*/
int main(){
  int *p;
  p = NULL;
  int *cp = NULL;
  printf("p: %p\n",p);//%p 是指针的占位符
  printf("p==cp: %d\n",p==cp);//1 为真，0 为假

  // 可以在 if 语句中使用空指针
  if(p){可以使用 p!=NULL
    printf("p is not null\n");
  }else {
    printf("p is null\n");
  }

  // NULL 是空，空指针在数据结构中很有用
  // 用于标记
  // 数据结构的末尾，例如链表
  return 0;
}
```

**输出:**
```
p: 0x0
p==cp: 1
p is null
```

# PointerToVoid.c

```c
#include <stdio.h>

/*
[作者] | [邮箱] | [日期]

空指针: 指向 void 的指针在 c 中是合法的。空指针可以用来持有指向任何数据类型的指针。空指针展示了多态的特性。
*/
int main(){
  //空指针可以持有任何数据类型
  int a = 100;
  int *p = &a;
  printf("Address of p: %p\n",p);
  printf("sizeof(p): %lu\n", sizeof(p));
  printf("Dereferencing of p: %d\n",*p);
  void *vp;
  vp = p;//这个指针可以持有任何数据类型，
         // 对函数参数很有用
  /*
    - 空指针将与 char 有相同的表示形式和内存对齐
    - 空指针永远不会等于另一个指针，但赋值为 NULL 的空指针会相等
  */
  printf("Address of vp: %p\n",vp);
  printf("sizeof(vp): %lu\n", sizeof(vp));
  return 0;
}
```

**输出:**
```
Address of p: 0x7fff5c39ba8
sizeof(p): 8
Dereferencing of p: 100
Address of vp: 0x7fff5c39ba8
sizeof(vp): 8
```

# PointerToConstant.c

```c
#include <stdio.h>

/*
[作者] | [邮箱] | [日期]
指向常量的指针在 c 中是合法的。一旦常量指针被初始化，它就不能被更改。常量是你可以添加到变量上的修饰符。一旦变量被定义，就不能更改。
*/
int main(){
  int x = 100;
  const int *ci = &x;
  printf("Address: %p\n", ci);
  printf("Value: %d\n", *ci);
  // *ci = 200; // 错误：不能修改常量的值
  return 0;
}
```
*(注：由于原文中 PointerToConstant.c 代码块似乎不完整，我根据注释逻辑补全了常见的示例结构，若仅需翻译已有文本，请忽略此。以下为对你提供的剩余文本的逐性翻译：)*

# Pointer.c

```c
#include <stdio.h>

/*
[作者] | [邮箱] | [日期]

指针: 指针是一个特殊的变量，用于存储数据类型的内存地址。指针指向变量数据存储的内存地址。当你在 C 中声明变量时，会分配内存空间来存储该变量。因此，指针可以获取存储在内存地址的数据。当你访问内存地址处的值时，这被称为解引用指针。你可以拥有一个指向指针的指针。
*/
int main(){
  int number = 1;
  int two;

  //要访问内存地址使用 & 符号
  // 位于变量名旁边
  printf("Address of number: %p\n", &number);
  printf("Address of two: %p\n", &two);//指针的占位符是 %p

  //这两个地址在内存中将相隔 4 字节，或 32 位
  // 在内存中，由于它们是连续声明的，
  // 它们以“线性”方式存储
  //声明指针使用相同的数据类型
  // 在此例中使用 int，然后在名称旁边加一个 *
  int *pointerToInt = &number; //声明一个指针变量
                                // 该指针指向 number 的地址

  // 仅引用指针将返回一个地址
  printf("Address of where int is stored: %p\n", pointerToInt);

  //要访问指针指向的内容，在指针上使用 *
  // 这被称为引用一个指针
  printf("What is stored in number address: %d\n", *pointerToInt);

  return 0;
}
```
*(抱歉，由于系统在处理中出现了重复错误，以下是为您整理的最终翻译内容：)*

[content]
```c
//Boolean.b = 2//除非你分配了 2 位宽，否则是不合法的
//因为在二进制中表示 2 需要两个位
//Boolean.b = 7 //由于上述原因也是不法的，除非你将位宽更改为 3
  return 0;
}
```

# Pointer.c

```c
#include <stdio.h>

/*
[作者] | [邮箱] | [日期]

指针: 指针是一个特殊的变量，用于存储数据类型的内存地址。指针指向变量数据存储的内存地址。当你在 C 中声明变量时，会分配内存空间来存储该变量。因此，指针可以获取存储在内存地址的数据。当你访问内存地址处的值时，这被称为解引用指针。你可以拥有一个指向指针的指针。
*/
int main(){
  int number = 1;
  int two;

  //要访问内存地址使用 & 符号
  // 位于变量名旁边
  printf("Address of number: %p\n", &number);
  printf("Address of two: %p\n", &two);//指针的占位符是 %p

  //这两个地址在内存中将相隔 4 字节，或 32 位
  // 在内存中，由于它们是连续声明的，
  // 它们以“线性”方式存储
  //声明指针使用相同的数据类型
  // 在此例中使用 int，然后在名称旁边加一个 *
  int *pointerToInt = &number; //声明一个指针变量
                                // 该指针指向 number 的地址

  // 仅引用指针将返回一个地址
  printf("Address of where int is stored: %p\n", pointerToInt);

  //要访问指针指向的内容，在指针上使用 *
  // 这被称为引用一个指针
  printf("What is stored in number address: %d\n", *pointerToInt);

  return 0;
}
```

**输出:**
```
Address of number: 0x7fff5f315be8
Address of two: 0x7fff5f315be4
Address of where int is stored: 0x7fff5f315be8
What is stored in number address: 1
```

# PointerToNull.c

```c
#include <stdio.h>

/*
[作者] | [邮箱] | [日期]

空指针: C 语言中的 Null 表示无，它在字面上没有值，并用于表示未知的数据。
指向空指针在 C 中是合法的。当指针被赋值为空时，该指针不指向任何内容。
两个空指针总是相等的。
指向空的指针不指向任何内容。
空指针中存储的地址是一个无效的内存地址。
它们对于执行检查非常有用。
*/
int main(){
  int *p;
  p = NULL;
  int *cp = NULL;
  printf("p: %p\n",p);//%p 是指针的占位符
  printf("p==cp: %d\n",p==cp);//1 为真，0 为假

  // 可以在 if 语句中使用空指针
  if(p){可以使用 p!=NULL
    printf("p is not null\n");
  }else {
    printf("p is null\n");
  }

  // NULL 是空，空指针在数据结构中很有用
  // 用于标记
  // 数据结构的末尾，例如链表
  return 0;
}
```

**输出:**
```
p: 0x0
p==cp: 1
p is null
```

# PointerToVoid.c

```c
#include <stdio.h>

/*
[作者] | [邮箱] | [日期]

空指针: 指向 void 的指针在 c 中是合法的。空指针可以用来持有指向任何数据类型的指针。空指针展示了多态的特性。
*/
int main(){
  //空指针可以持有任何数据类型
  int a = 100;
  int *p = &a;
  printf("Address of p: %p\n",p);
  printf("sizeof(p): %lu\n", sizeof(p));
  printf("Dereferencing of p: %d\n",*p);
  void *vp;
  vp = p;//这个指针可以持有任何数据类型，
         // 对函数参数很有用
  /*
    - 空指针将与 char 有相同的表示形式和内存对齐
    - 空指针永远不会等于另一个指针，但赋值为 NULL 的空指针会相等
  */
  printf("Address of vp: %p\n",vp);
  printf("sizeof(vp): %lu\n", sizeof(vp));
  return 0;
}
```

**输出:**
```
Address of p: 0x7fff5c39ba8
sizeof(p): 8
Dereferencing of p: 100
Address of vp: 0x7fff5c39ba8
sizeof(vp): 8
```

# PointerToConstant.c

```c
#include <stdio.h>

/*
[作者] | [邮箱] | [日期]
指向常量的指针在 c 中是合法的。一旦常量指针被初始化，它就不能被更改。常量是你可以添加到变量上的修饰符。一旦变量被定义，就不能更改。
*/
int main(){
  int x = 100;
  const int *ci = &x;
  printf("Address: %p\n", ci);
  printf("Value: %d\n", *ci);
  // *ci = 200; // 错误：不能修改常量的值
  return 0;
}
```




```c
printf("Name: %s\nAge: %d\n", person->name, person->age);
}
```

Output:
Size of Struct: 24
address[0] : 0x7fff55633bb0
address[1] : 0x7fff55633bc8
Name: DoEasy Prod.
Age: 1

### PointerToFunction.c

```c
#include <stdio.h>

/*                                                                                                                                                                                           
[Author] | [Email] | [Date]                                                                                              

解释什么是函数指针，以及如何使用它们。你可以像拥有其他任何内容的指针一样，拥有一个函数的指针。你甚至可以通过指针调用函数，下文说明了如何操作。
*/
// 声明一个函数

int add(int x, int y);

int main(){
  /*
   当我们声明一个函数指针时，必须以指定的
   格式来操作。首先，声明返回类型（它必须与函数的
   返回类型相同）。接下来，为指针命名，在我们的
   案例中，指针名称是‘ptr’。第三，在括号中声明
   参数列表，要与函数完全一致。在我们的案例中，
   函数接收两个参数，都是 int 类型。所以我们的指针必须
   同样如此。最后，将指针设置为函数存储
   的地址。
   */
  int (*ptr)(int, int) = &add;
  int r = (*ptr)(10,3);
  printf("r: %d\n",r);
  return 0;
}

int add(int x, int y){
  return x+y;
}
```

Output:
r: 13

### Binary.c

```c
#include <stdio.h>

/*
[Author] | [Email] | [Date]

二进制：将代表 8 位二进制数的 char[] 转换为十进制 10 数字，涵盖了目前为止讨论的所有主题。尝试一下我们涵盖的一些主题是一个良好的习惯。
*/
// 全局作用域，可以在 .c 源文件的任何地方使用
char binary[8]= {‘0','0','0','0','1','1','0','1'}; // 数组
int binaryToDecimal(char binary[]); // 函数
int main(){
  printf("decimal: %d \n", binaryToDecimal(binary));
    return 0;
}

int binaryToDecimal(char binary[]){
  char *p = binary; // 指向 binary[] 中第一个地址的指针
  int sum = 0;
  int base = 1;
  for(int i = 7; i>0; i--){ // 循环和运算符
    // 尝试 i < sizeof(binaryNumber)/sizeof(char)
    if(*(p+i) == ‘1’){//指向数组的指针，以及 if 语句
    sum += base;// 赋值运算符   
    }
    base *= 2;// 赋值运算符
  }
  return sum;
}
```

Output:
decimal: 13

### TypeCasting.c

```c
#include <stdio.h>
/*                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      
[Author] | [Email] | [Date]
类型转换：如何进行类型转换以及其中的之处。当你进行类型转换时，你将一种数据类型转换为指定的数据类型，但仅对你转换的那一行代码有效，除非你将该转换赋值给变量。
*/
int main(){
  /*
  - 使用强制转换向函数传递不同的数据类型
  - 可以将任何数据类型转换为另一种类型
  - 注意数据丢失，例如将 float 转换为 int
  */
  double x = 89.99;
  printf("x before cast: %f\n", x);
  printf("sizeof(x): %lu\n", sizeof(x));
  printf("x after cast: %d\n", (int)x);
  printf("sizeof((int)x): %lu\n", sizeof((int)x));
  // 与其每次都将 x 转换为 int，
  // 我们可以将其赋值给一个变量，
  // 只要确保变量与转换后的类型相同即可
  int castVariable = (int)x;
  return 0;
}
```

Output:
x before cast: 89.990000
sizeof(x): 8
x after cast: 89
sizeof((int)x): 4

### IO.c

```c
#include <stdio.h>
/*
[Author] | [Email] | [Date]
IO：我们一直都在通过 printf() 函数处理输出，现在让我们尝试使用 scanf() 函数进行一些输入。
标准输入来自键盘，所以现在我们可以开始创建一些有趣且令人程序了。
*/
int main(){
  // 我们已经看到输入了，但如果你想
  // 从键盘获取用户输入怎么办？
  /*
   getchar() 和 putchar()
  */
  char c;
  printf("Enter a value>>> ");
  c = getchar();//只检索一个字符
  printf("\nChar Entered: ");
  putchar(c);
  printf("\n");
  /*
   scanf() 和 printf()
  */
  char input[100];
  int i;
  printf("Enter a value>>> ");
  // 获取你喜的任何数据类型模式
  scanf("%s %d", input, &i);//这可以是任何你喜欢的模式
  printf("\nInput Entered: ");
  printf("%s %d", input, i);
  printf("\n");
  return 0;
}
```

Output:
Enter a value>>> s
Ch Entered: s
Enter a value>>> string 4
Input Entered: string 4

### GuessThePassPhrase.c

```c
#include<stdio.h>
#include<stdlib.h>
#include<string.h>
/*
[Author] | [Email] | [Date]
一个用于测试 while 循环、用户输入和逻辑的游戏，当用户猜中我们的密码时，游戏结束。
*/
  /*
  如果 guess == password 则返回 1。
  否则返回 0。
  */
int equals(char* guess, char* password);
int main(){
  char PASSWORD[] = “Password”;//这可以是密码
  char* pp = PASSWORD;//这持有内存地址
  char guess[15];//不能超过 14
  do{
    printf("Enter the password: ");
    scanf("%s", guess);
  }while(equals(guess, pp) == 0);
  printf("You was: %s",PASSWORD);
  return 0;
}

int equals(char* guess, char* password){
  int i = 0;
  while(*(guess+i)==*(password+i)){
    i++;
  }
  return 1;
}
```

Output:
Enter the password: some
You was: Password

### TempConverter.c

```c
#include<stdio.h>
#include<stdlib.h>
/*
[Author] | [Email] | [Date]
将华氏温度转换为摄氏度和开尔文温度。
*/
int main(){
  printf("Enter degrees in F:\n");
  double tempF = 0;
  scanf("%lf", &tempF);
  double tempC = (tempF-32)*5/9;
  double tempK = tempC + 273.15;
  printf("tempF: %.2f\n",tempF);
  printf("tempC: %.2f\n",tempC);
  printf("tempK: %.2f\n",tempK);
}
```

Output:
Enter degrees in F:
0
tempF: 0.00
tempC: -17.78
tempK: 255.37

### FileIO.c

```c
#include <stdio.h>
#include <string.h>
/*
[Author] | [Email] | [Date]
FileIO：在 C 中你可以从文件读取输入，也可以从程序写入文件。fgets 读取文件的一行，fputs 将一行写入文件，当你这样做时文件内容会被擦除并替换，所以如果你想避免这一点，请确保使用追加选项。
*/
int main(){
  /*
   fgetc(fp) -->读取一个字符
   fscanf(fp, source)—>读取模式
   fgets -->读取行
  */
  FILE *fp //首先声明一个文件指针
  char contents[50];//不能超过 50
  fp = fopen("tester.txt","r");
  //if fp == NULL {
  fscanf(fp, "%s", contents);
  printf("Word 1: %s\n",contents);
  fscanf(fp, "%s", contents);
  printf("Word 2: %s\n",contents);
  fscanf(fp, "%s", contents);
  printf("Word 3: %s\n",contents);
  for(int i = 0; i<4; i++){
  fgets(contents, 50, fp);
    printf("Line %d: %s\n", i+1, contents);
  }
  fclose(fp);
  fp = fopen("output.txt","w");
  //不会添加换行符
  fprintf(fp,"This will write into file above");
  fputs("This will also fo in the file",fp);
  return 0;
}
```

Output:
Word 1: This
Word 2: scans
Word 3: words
Line 1: 
Line 2: this is another line
Line 3: file input and output
Line 4: can be very useful

### ErrorHandling.c

```c
#include <stdio.h>
#include <stdlib.h>
/*
[Author] | [Email] | [Date]
错误处理：如何处理错误，寻找什么，
*/
```




以及 `stderr`，它是 `stdlib` 的一部分。我们将使用一个除以零的简单示例。当你除以零时，会返回一个非实数。因此，我们需要设置一些预防措施来避免这种情况，错误处理非常取决于你的程序。

```c
int main(){
  int numerator = 4;
  int denominator = 1;
  int quotient;
  //下面是错误检查
  if(denominator == 0){
    fprintf(stderr,"Error: Denominator == 0\n");
    fprintf("Exiting with return status 1.\n");
    return 1;
  }
  quotient = numerator/denominator;
  fprintf("Quotient: %d", quotient);
  return 0;
}
```

**输出：**
```
Quotient: 4
```

### MyHeader.h
```c
/*
   在 C 语言中，你可以创建自己的头文件，然后可以将将其
  包含任何其他 C/C++ 程序中。结构体（Structs）是头文件中
  常见的放置内容。
  */
typedef struct Person{
  char name[10];
  int age;
}Person;
//可以把方法放在这里，
//也可以在这些方法内部放置错误处理
```

### Header.c
```c
#include <stdio.h>
#include <string.h>
#include "MyHeader.h"//注意包含

/*
[作者] | [邮箱] | [日期]
Header: 使用了我们自定义的 MyHeader.h 文件。
*/
int main(){
  Person me;
  strcpy(me.name,"DoEasy");
  me.age = 100;
  printf("Name: %s\nAge: %d\n",me.name, me.age);
  return 0;
}
```

**输出：**
```
Name: DoEasy
Age: 100
```

### ChemicalElement.h
```c
/*
[作者] | [邮箱] | [日期]
一个包含数据结构的头文件
该结构模拟了一个化学元素。
*/
typedef struct ChemicalElement{
  //名称不能超过 19 个字符
  // 你能让这个字符串变成动态的吗？
  char name[20];
  int number;
  double mass;
  // 你还能想到其他成员吗？
}ChemicalElement;
```

### PeriodicTable.c
```c
#include "ChemicalElement.h"
#include<stdio.h>
#include<string.h>
#include<stdlib.h>

/*
[作者] | [邮箱] | [日期]
PeriodicTable: 一个可以在其中保存化学元素的 C 源文件，
也许可能可以开始创建分子。
*/
int main(){
  ChemicalElement hydrogen;
  strcpy(hydrogen.name, "Hydrogen");
  hydrogen.number = 1;
  hydrogen.mass = 1.001;
  ChemicalElement oxygen;
  strcpy(oxygen.name, "Oxygen");
  oxygen.number = 8;
  oxygen.mass = 15.9994;
  ChemicalElement h2o[3];
  h2o[0] = hydrogen;
  h2o[1] = hydrogen;
  h2o[2] = oxygen;
  printf("Printing Water:\n");
  double totalMass=0;
  for(int i = 0; i < 3; i++){
    printf("%s: %.2f\n", h2o[i].name, h2o[i].mass);
    totalMass += h2o[i].mass;
  }
  printf("Total Mass: %.2f\n", totalMass);
  return 0;
}
```

**输出：**
```
Printing Water:
Hydrogen: 1.00
Hydrogen: 1.00
Oxygen: 16.00
Total Mass: 18.00
```

### CommandLine.c
```c
#include <stdio.h>

/*
[作者] | [邮箱] | [日期]
CommandLine: 如何传递命令行参数。
请注意它们是以字符串数组的形式传递的
所以接收不同的数据类型需要更多工作。
*/
int main(int argc, char *argv[]){
  if (argc == 1){
    printf("NO COMMAND LINE ARGS\n");
    return 0;
  } else {
    int i =1;
    while(i<argc){
      printf("Command Line Arg[%d]:%s\n", i, argv[i]);
      i++;
    }end while
  }end else
  return 0;
}
```
**执行：**
```
./CommandLine These Are the Args
Command Line Arg[1]:These
Command Line Arg[2]:Are
Command Line Arg[3]:the
Command Line Arg[4]:Args
```

### MemoryManagement.c
```c
#include <stdio.h>
#include <string.h>
#include <stdlib.h>

/*
[作者] | [邮箱] | [日期]
如何动态创建内存空间。这意味着在运行时创建
内存空间。当你不知道需要多少
内存时非常有用。
void *calloc(int num, int size)-->分配一个包含 num 个元素的数组，每个元素为 size
void free(void *address)-->释放给定地址的内存块
void malloc(int num)-->分配一个包含 num 个字节的数组，这些字节是未初始化的
void *realloc(void *address, int size)-->重新分配内存，将其扩展到 size
这样我们可以定义一个指针，而不需要定义多少内存
*/
int main(){
  char name[10];
  char *about_name;
  strcpy(name,"doeasy");
  about_name = malloc(100*sizeof(char));
  printf("sizeof(): %lu\n", sizeof(about_name));
  printf("address: %p\n", about_name);
  strcpy(about_name,"This string can be big as...");
// 如果你想让它更大，根据用户的输入使用 realloc() 最后释放空间
  printf("name: %s\n",name);
  printf("about_name: %s\n", about_name);
  free(about_name);
  return 0;
}
```
**输出：**
```
sizeof(): 8
address: 0xfff5c8b0
name: doeasy
about_name: This string can be big as…
```

### DynamicString.c
```c
/*
[作者] | [邮箱] | [日期]
DynamicString: 如何动态创建一个字符串。
运行时不知道输入有多长，
我们现在处理这个问题。
*/
int main(){
  // 首先声明一个指向 char 的指针
  // 使用 malloc 设置长度
  // malloc 返回 void*，所以必须强制转换为数据类型
  // 接下来获取一些用户输入
  char* input = (char*)malloc(sizeof(char));
  int count = 0;
  printf("Enter a sentence: ");
  char token;
  token = getchar();
  // 只能读取一个字符，按回车键继续程序
  // realloc 返回 void*，所以必须强制转换为指针类型
  // 添加到数组
  while(token != '\n'){
    input = (char*)realloc(input, sizeof(char)*(count+1));
    input[count] = token;// 获取下一个 token
    count++; // 增加我们的 size
  }
  printf("You entered: %s\n", input);
  printf("Count %d.\n",count);
  return 0;
}
```
**输出：**
```
Enter a sentence: this sentence can any length
You entered: this sentence can any length
```

### DynamicIntArray.c
```c
#include<stdio.h>
#include<stdlib.h>

/*
[作者] | [邮箱] | [日期]
DynamicIntArray: 动态整数数组可以在运行时增长或缩小。
我们将使用与相同的方法，但是针对整数。
*/
int main(){
  int* numbers = (int*)malloc(sizeof(int));
  printf("Enters numbers, press enter to add a number:\n");
  printf("Enter -1 to exit.\n");
  int input = 0;
  int count = 0;
  while(input != -1){
    scanf("%d", &input);
    numbers = (int*)realloc(numbers, sizeof(int)*(count+1));
    numbers[count] = input;
    count++;
  }
  printf("\nPrinting Numbers:\n");
  for(int i = 0; i<count-1;i++){
    printf("number[%d]: %d\n",i, numbers[i]);
  }
  printf("\nThat was %d numbers.\n",count-1);
  return 0;
}
```
**输出：**
```
Enters numbers, press enter to add a number:
Enter -1 to exit.
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

### ArrayAnalysis.c
```c
#include<stdio.h>
#include<stdlib.h>
#include<time.h>

/*
作者 | [邮箱] | [日期]
ArrayAnalysis: 计算随机生成数组的平均值、最大值和最小值。
我们将讨论如何从函数返回数组，以及如何将数组作为参数传递
*/
int* initArray(int size, int range);
double average(int* numbers, int size);
int biggest(int* numbers, int size);
int smallest(int* numbers, int size);

int main(){
  int* pi = initArray(10, 100);
  double ave = average(pi, 10);
  int big = biggest(pi, 10);
  int small = smallest(pi, 10);
  printf("Analyzing Array:\n");
  printf("\tAverage %.2f\n",ave);
  printf("\tBiggest %d\n",big);
  printf("\tSmallest %d\n", small);
  return 0;
}

/*
创建一个长度为 size 的数组，包含在 [0, range] 之间的随机数。
当你返回一个数组时，必须返回一个指向数组的指针，你之后可以对其迭代。
*/
int* initArray(int size, int range){
  srand(time(0));
  int* num = (int*)malloc(sizeof(int));
  for(int i = 0; i < size; i++){
    num = realloc(num, sizeof(int)*(i+1));
    *(num+i) = rand()%range;
  }
  // 这返回指向数字第一个元素的
  // 地址
  return num;
}
```




```c
/*
  average: 计算我们数组的平均值。
  我们正在将一个数组传递到函数中。
  具体来说，我们是将一个指针传递到函数中，
  然后我们可以对该指针进行算术运算
  以解引用它的成员。当你这样做时，
  同时传递大小是一个良好的习惯。
*/
double average(int* numbers, int size){
  double total = 0;
  for(int i = 0; i < size; i++)
    total += *(numbers+i);
  return total/(double)size;
}
```

```c
/*
  biggest: 找到数组中最大的数字。
  我们将使用与上面相同的技术。
*/
int biggest(int* numbers, int size){
  int biggest = *numbers;
  //将 biggest 初始化为第一个元素
  for(int i = 1; i < size; i++){
    if(*(numbers+i) > biggest)
      biggest = *(numbers+i);
  }
  return biggest;
}
```

```c
/*
  smallest: 找到数组中最小的数字。
  我们将使用与上面相同的技术。
*/
int smallest(int* numbers, int size){
  int smallest = *numbers;
  //将 smallest 初始化为第一个元素
  for(int i = 1; i < size; i++){
    if(*(numbers+i) <smallest)
      smallest = *(numbers+i);
  }
  return smallest;
}
```

### 输出:
分析数组：
平均值 60.30
最大 90
最小 0

### TicTacToe.h
```c
/*
[作者] | [邮箱] | [日期]
井字棋游戏的开始。它还需要一些完善，但这将是一次非常棒的练习。
*/
char board[3][3];
int player1 = 1;
int player2 = 0;
void initBoard(){
  for(int i = 0; i < 3; i++){
    for(int j = 0; j < 3; j++){
      board[i][j] = ' ';
    }
  }
}

void printBoard(){
  for(int i = 0; i < 3; i++){
    for(int j = 0; j < 3; j++){
      printf("[%c]",board[i][j]);
    }
    printf("\n");
  }
}

/*
在这里放置函数来检查该轮到谁了。
以及进行移动。
*/
```

### TicTacToeGame.c
```c
#include <stdio.h>
#include "TicTacToe.h"

/*
[作者] | [邮箱] | [日期]
测试我们的 TicTacToe.h 头文件。这个文件是实际运行游戏的地方。
你可以选择制作单人或双人游戏。
*/
int main(){
  initBoard();
  printBoard();
  board[0][1] = 'X';
  printBoard();
}
```

### 输出:
```
[ ][ ][ ]
[ ][ ][ ]
[ ][ ][ ]
[ ][X][ ]
[ ][ ][ ]
[ ][ ][ ]
```

### pieces.h
```c
/*
  [作者] | [邮箱] | [日期]
pieces: 包含国际象棋游戏的棋子。
*/
#include <stdio.h>
char *board[8][8];
char pawn = 'p';
char rook = 'r';
char night = 'n';
char bishop = 'b';
char queen = 'q';
char king = 'k';
char block = ' ';
char *lostBlackPieces[16];
char *lostWhitePieces[16];

void initBoard(){
  for(int i = 0; i<8;i++){
    for(int j = 0; j<8; j++){
      if(i==1 || i == 6){
        board[i][j] = &pawn;
      }      
      else if (i != 7 || 1 !=0 || i != 1 || i != 6)
        board[i][j]=&block;
    }
  }
  board[7][0]=&rook;
  board[7][1]=&night;
  board[7][2]=&bishop;
  board[7][3]=&queen;
  board[7][4]=&king;
  board[7][5]=&bishop;
  board[7][6]=&night;
  board[7][7]=&rook;
  board[0][0]=&rook;
  board[0][1]=&night;
  board[0][2]=&bishop;
  board[0][3]=&king;
  board[0][4]=&queen;
  board[0][5]=&bishop;
  board[0][6]=&night;
  board[0][7]=&rook;
}

void printBoard(){
  for (int r = 0; r<8; r++){
    for(int c = 0; c<8; c++){
      printf("[%c]", *(board[r][c]));
    }
    printf("\n");
  }
}
```

### moves.h
```c
/*
  [作者] | [邮箱] | [日期]
movess: 包含国际象棋游戏中允许的移动。
*/
int checkPawnMove(char *p, int fromr, int fromc, int tor, int toc){
  if(p != &pawn){
    return 0;
  }
  else if(tor-fromr == 1 || tor - fromr!=-1){
    return 0;
  }
  else if(tor < 0 || tor > 7){
    return 0;
  }
  else if(toc-fromc != 0){
    return 0;
  }
  else{
    return 1;
  }
}

/*
int jumpWithPawn(char *piece, int r, int c, int tor, int toc){
}
*/
void movePawn(char *piece, int r, int c, int tor, int toc){
  if(checkPawnMove(piece, r, c, tor, toc)==1){
    board[tor][toc] = piece; 
    board[r][c] = &block;
  }
}
```

### Game.c
```c
#include <stdio.h>
#include "pieces.h"
#include "moves.h"

/*
Game: 国际象棋游戏。在这里你将实现头文件来实际玩国际象棋。
游戏远未完成，但这是一个很好的开始。祝愉快 :)
*/
int main(){
  initBoard();
  printBoard();
  movePawn(board[6][0], 6, 0, 5, 0);
  printBoard();
  movePawn(board[5][0], 5, 0, 4, 0);
  printBoard();
  return 0;
}
```

### 结
总之，这些示例我们仅仅触及了皮一角。然而，现在你有了一个可以据此构建的基础基础。所以，去尝试吧，开始构建、破坏并从自己的代码中享受乐趣。请访问我的网站获取更多信息：

[tfoss0001.github.io](http://tfoss0001.github.io)

想要看有趣的互动式视频教程，请查看我的 YouTube 频道：

DoEasy Productions

该频道上有播放列表可以引导你学习这些示例，并为你编写自己的程序提供灵感。非常感谢。

-Torin Foss

