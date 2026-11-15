

```cpp
#include <iostream> //Required for cout
#include <cctype> //Required for toupper()
using namespace std;
//Function prototypes.
void stringupper(char*);
int countchar(const char*, char);
int main()
{
   // Declare and initialize objects.
   char strg1[] = "abbcfgwdibbw";
   char *ptr_strg1 = strg1, ch='B';
// Convert string to uppercase.
stringupper(ptr_strg1);
cout << "The letter " << ch << " appears "
     << countchar(ptr_strg1, ch) << " times in the string "
     << ptr_strg1 << endl;
return 0;
}
```

/**
*----------------------------------------------------------------------*/
/*
*
* This function counts the number of times the character ch *
* appears in the string pointed to by ptr_strg.              *
*                                                          *
*/
int countchar(const char * ptr_strg, char ch)
{
   // Declare and initialize local objects.
   int cnt(0);
// While not end of string.
while(*ptr_strg)
{
   // Look for ch and increment cnt.
   if( *ptr_strg == ch)
      cnt++;
// Move pointer to next character
   ptr_strg++;
}
   return cnt;
}
/**----------------------------------------------------------------------*/

该程序生成以下输出：

字母 B 在字符串 ABCCFGWDBIBBW 中出现 5 次

函数 countchar() 不能修改 ptr_str 所指向的对象。例如，如果我们在 if 语句中犯了常见错误，即使用赋值运算符而不是相等运算符，如下所示：

```
if ( *ptr_str == ch );
```

编译器会将其标记为错误。

const 修饰符也可用于定义指针的类型声明语句中，如下面的语句所示：

```
const char *cptr = "abbcfqwdbibbw";
```

*指向常量的指针*

在上述语句中，cptr 被定义为指向常量的指针。需要注意的是，指针 cptr 本身不是常量，但 cptr 所指向的内容被视为常量。因此，可以重新赋值给 cptr，但不能使用 cptr 来修改对象。以下代码段说明了 const 修饰符的这种用法：

```
// Declare and initialize objects.
int x(5), y(10), *ptr1(&x);
const int *cptr(&y);

// Print values.
cout << *ptr1 <<',' << *cptr << endl;
cout << x << ', ' << y << endl;

// Increment x.
(*ptr1)++;

// Print values.
cout << *ptr1 <<',' << *cptr << endl;
cout << x << ', ' << y << endl;

// Reassign both pointers.
ptr1 = &y;
cptr = &x;

// Increment y.
(*ptr1)++;

// Print values.
cout << *ptr1 <<',' << *cptr << endl;
cout << x << ', ' << y << endl;
```

此代码段生成的输出如下所示：

5,10
5,10
6,10
6,10
11,6
6,11

*常量指针*

常量指针可以在类型声明语句中声明，如语句 `char *const cptr = "A standard message.";` 所示。使用此语法，`cptr` 的值不能被重新赋值，但 `cptr` 所指向的对象可以被修改。

## 练习 9.4

假设对象已通过以下语句定义：
`int i[5], j[10];`
`int *iptr[6];`
`const int *cptr[6];`
`int *const jptr[6];`
确定以下语句是有效还是无效。

- 1. `cptr = jptr;`
- 2. `jptr = cptr;`
- 3. `*cptr = *jptr;`
- 4. `*cptr = *jptr;`
- 5. `*jptr = *cptr;`
- 6. `iptr = cptr;`

## 9.3 应用问题求解：厄尔尼诺-南方涛动数据

在章节开头的讨论中，我们讨论了海面温度。特别是，赤道沿线的正常海面温度在太平洋西部较暖，在太平洋东部较冷。在一种周期性现象中，暖流导致太平洋东部（沿加利福尼亚州、墨西哥和南美洲西海岸）的海水温度升高多达 18°F。这种现象常发生在圣诞节附近，因此常被称为厄尔尼诺。（在西班牙语中，El Niño 意为男孩。）一种逆向现象也会发生，即太平洋西部的海水温度变得更冷，这被称为拉尼娜。（在西班牙语中，La Niña 意为女孩。）这些条件与暖流和东西向大气压力变化之间的南方涛动相关。ENSO（厄尔尼诺-南方涛动）指数是一个指标，它由多个变量计算得出，包括大气压力、风和海水温度。当 ENSO 指数为正时，海水温度代表厄尔尼诺条件；当 ENSO 指数为负时，海水温度代表拉尼娜条件。指数越大，温度与正常值的偏差越大。编写一个程序，读取包含一段时间内年份、季度和 ENSO 指数的数据文件。程序应确定并打印具有最强厄尔尼诺条件的年份和季度。

### 1. 问题描述

确定具有最强厄尔尼诺条件的年份和季度。

### 2. 输入/输出描述

I/O 图显示数据文件作为输入，年份和季度作为输出。

![](img/0235a4ea835dc4575bd036e024a533b3_522_0.png)

### 3. 手动示例

假设数据文件包含以下数据：

| 年份 | 季度 | ENSO 指数 |
|------|---------|------------|
| 1990 | 1 | 0.6 |
| 1991 | 1 | 0.2 |
| 1992 | 1 | 1.1 |
| 1993 | 1 | 0.5 |
| 1994 | 1 | 0.1 |
| 1995 | 1 | 1.2 |
| 1996 | 1 | -0.3 |
| 1997 | 1 | -0.1 |
| 1998 | 1 | 2.2 |
| 1999 | 1 | -0.7 |
| 2000 | 1 | -1.1 |

相应的输出将是以下报告：

```
Maximum El Nino Conditions in Data file
Year: 1998, Quarter: 1
```

### 4. 算法开发

我们首先开发分解大纲，因为它将解决方案分解为一组顺序步骤。

*分解大纲*

- 1. 将 ENSO 数据读入数组并确定最大正指数。

- 2. 打印与最大强度对应的年份和季度。

伪代码的细化如下：

### 伪代码细化

```
main: if file cannot be opened
   print error message

else
   read data and determine maximum intensity
   print the year and quarter that go with maximum intensity
```

伪代码中的步骤现在足够详细，可以转换为 C++。

```
/*
/* Program chapter 9.2
/* This program reads a data file of ENSO index values and
/* determines the maximum El Nino condition in the file.
/* ------------------------------------------------------------------*/
#include<iostream> //Required for cout
#include<fstream> //Required for ifstream

const int MAX_SIZE(1000);

using namespace std;

int main()
{
//Declare variables
int k(0), year[MAX_SIZE], qtr[MAX_SIZE], maxK(0);
double index[MAX_SIZE];
ifstream fin("ENSO1.txt");
if(fin.fail())
{
   cerr <<"Could not open file ENSO1.txt" <<endl;
   exit(1);
}
fin >> *year, *qtr, *index;
while(fin)
{
   if(*(index+k) > *(index+maxK))
      maxK = k;
   k++;
}
fin >> *(year+k) >> *(qtr+k) >> *(index+k);
//end while

/* Print data for maximum El Nino condition.
cout << "Maximum El Nino conditions in Data File \n";
cout << "Year: " << *(year+maxK) << " Quarter:"
     << *(qtr+maxK) << endl;
return 0;
}
/*------------------------------------------------------------*/
```

### 5. 测试

使用手动示例数据的程序输出如下：

```
Maximum El Nino conditions in Data File
Year: 1998 Quarter: 1
```

## 修改 9.2

- 1. 修改程序以查找并打印最大拉尼娜条件。
- 2. 修改程序以查找最接近零的条件。这些将是最接近正常条件的条件。
- 3. 修改程序，以便打印所有具有厄尔尼诺条件的年份和季度。
- 4. 修改程序，以便统计具有厄尔尼诺条件的年份数量和具有拉尼娜条件的年份数量。打印这两个值。
- 5. 修改程序，以便计算并打印具有厄尔尼诺条件的年份的平均强度。

## 9.4 动态内存分配

动态内存分配允许程序在程序执行期间为对象分配内存，而不是在编译程序时确定内存需求。当程序使用的数组大小无法在程序执行前确定时，这一点非常重要；如果没有动态内存分配，程序就必须指定数组预期的最大大小。对于内存有限的系统，如果所有数组都必须指定为预期的最大大小，可能没有足够的内存来运行程序。动态内存从称为程序堆的可用内存区域分配。动态内存使用 new 运算符在堆上分配，并使用 delete 运算符返回到堆。

堆

### new 运算符

动态内存分配使用关键字 new 指定，后跟类型说明符以指示要分配的对象的数据类型。new 运算符返回所分配对象的地址

