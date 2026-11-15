

请注意，引用 *(ptr+k) 需要使用括号以按正确顺序执行运算；k 被加到 ptr 中的地址上，然后使用间接运算符来引用 *ptr+k 所指向的值。引用 *ptr+k 将被计算为 *(ptr+k)，因为一元运算符的优先级高于二元运算符。

在第 7 章关于数组的讨论中，我们看到数组名是第一个元素的地址。因此，以下两条语句是等价的：

```
ptr = &x[0];
ptr = x;
```

同样，引用 *(ptr+k) 也等价于 *(x+k)。因此，对数组 x 求和的语句可以简化为以下内容：

```
// Declare and initialize objects.
double x[6], sum = 0;
...
// Sum the values in the array x.
for (int k=0; k<=5; ++k)
{
   sum += *(x+k);
}
```

此示例说明了将数组名用作地址的用法。数组名可以在大多数语句中代替指针使用，但不能用于赋值语句的左侧，因为其值不能更改。

## 练习 9.3

假设数组 g 通过以下语句定义：

```
int g[] = {2, 4, 5, 8, 10, 32, 78};
int *ptr1(g), *ptr2(&g[3]);
```

给出一个内存快照（包括数组值。同时指明相对于数组初始值的偏移值。使用此信息，给出以下引用的值：

- 1. *g
- 2. *(g+1)
- 3. *g+1
- 4. *(g+5)
- 5. *ptr1
- 6. *ptr2
- 7. *(ptr1 + 1)
- 8. *(ptr2 + 2)

## 字符串

回顾第 7 章，字符数组是各个元素以字符形式存储的数组。C 风格字符串是最后一个元素为空字符的字符数组。字符串在许多工程应用中被使用，包括密码学和模式识别。通过指向字符串的指针来操作字符串通常很方便。第 6 章介绍的头文件 cstring 中的许多字符函数都需要将字符串指针作为参数，并且许多函数返回字符串指针。在本节中，我们将探讨使用指针引用 C 风格字符串所需的语法。

头文件 cstring 中包含的函数之一是名为 strstr() 的函数。函数 strstr(ps,pt) 以指向字符串 s 的指针和指向字符串 t 的指针作为参数，并返回字符串 t 在字符串 s 中起始位置的指针。如果 t 在 s 中未出现，则返回空指针。我们将在下一个示例中使用此函数。

假设我们想统计一个字符串在另一个字符串中出现的次数。例如，假设我们想统计字符串 "bb" 在字符串 "abcfgwdibbw" 中出现的次数。strstr() 函数将返回 "bb" 在 "abcfgwdibbw" 中首次出现位置的指针，如果未找到 "bb"，则返回空指针。在此示例中，strstr() 函数将返回指向 "bb" 首次出现位置开头的指针，如下所示：

![](img/0235a4ea835dc4575bd036e024a533b3_515_0.png)

要查找字符串 "bb" 的下一次出现，我们需要搜索紧随 "bb" 首次出现位置之后的字符串部分。然后 strstr() 函数将返回字符串新部分中 "bb" 首次出现位置开头的指针，如下所示：

![](img/0235a4ea835dc4575bd036e024a533b3_515_1.png)

我们重复此过程，直到 strstr() 函数返回空值。实现此过程的完整程序如下：

```
/*------------------------------------------------------------*/
/* Program chapter9_4                                         */
/*                                                            */
/* This program counts and prints the number of               */
/* times one string appears within another string.            */
/*                                                            */
#include <iostream> //Required for cout
#include <cstring> //Required for strstr
using namespace std;

int main()
{
// Declare and initialize objects.
int count = 0;
char strg1[] = "abcfgwdibbw", strg2[] = "bb";
char *ptr1(strg1), *ptr2(strg2);
```

```
// Count number of occurrences of strg2 in strg1.
// While function strstr does not return a null pointer
// increment count and move ptr1 to next section
// of strg1.
while ((ptr1 = strstr(ptr1, ptr2)) != nullptr)
{
    count++;
    ptr1++;
}
// Print the number of occurrences.
cout << "Count: " << count << endl;
return 0;
/*--------------------------------------------------*/
```

此程序的输出为：
count: 2

## 作为函数参数的指针

当指针作为参数传递给函数时，指针可以按值传递或按引用传递。如果指针按值传递，则可以使用该指针修改其指向的对象，但函数不能修改指针的值。如果指针按引用传递，则可以使用该指针修改其指向的对象，并且也可以修改指针的值。

考虑以下程序，它调用一个函数将字符串转换为大写：

```
/*--------------------------------------------------*/
/* Program chapter9_5 */
/* */
/* This program converts a string to all uppercase. */
/* */
/* Include <iostream> //Required for cout */
/* Include <cctype> //Required for toupper() */
using namespace std;
// Function prototypes
void stringupper(char*);

int main()
{
    // Declare and initialize objects.
    char strg1[] = "aBcFgWdHbIbw";
    char *ptr_strg1(strg1);

    // Ouput string before and after call to function.
    cout << ptr_strg1 << endl;
```

```
stringupper(ptr_strg1);
cout << ptr_strg1 << endl;

return 0;
/***********************************************************************/
/*
/*
/* This function converts each character in
/* the string pointed to by ptr_strg to uppercase.
/*
void stringupper(char* ptr_strg)
{
    // While not end of string (while character is not null).
    while(*ptr_strg)
    {
        // Convert character to uppercase
        *ptr_strg = toupper(*ptr_strg);

        // Mover pointer to next character
        ptr_strg++;
    }
/***********************************************************************/
```

在此示例中，指针 ptr_strg1 被传递给函数 stringupper()，ptr_strg1 指向的字符串被转换为大写。形式参数 ptr_strg 在函数中被递增以遍历字符串，但 main 中的实参未发生任何更改，因为 ptr_strg1 是按值传递的。此程序的输出为

abbcfgwdibbw
ABCBCFGWDIBBW

下一个程序将程序 9_5 中的函数修改为使用按引用传递而不是按值传递：

```
/***********************************************************************/
/* Program chapter9_6
/*
/* This program converts a string to all uppercase.
/*
#include <iostream> //Required for cout
#include <ctype> //Required for toupper
using namespace std;

//Function prototypes
void stringupper(char*&);

int main()
{
    // Declare and initialize objects.
    char strg1[] = "abbcfgwdibbw";
    char *ptr_strg1 = strg1;
```

```
// Ouput string before and after call to function.
cout << ptr_strg1 << endl;
stringupper (ptr_strg1);
cout << ptr_strg1 << endl;
return 0;
}
/* -------------------------------------------------------------------*/
/*                                                                     */
/*                                                                     */
/*    This function converts each character in the string              */
/*    pointed to by ptr_strg to uppercase.                             */
/*                                                                     */
/*-------------------------------------------------------------------*/
void stringupper(char*& ptr_strg)
{
    // While not end of string.
    while(*ptr_strg)
    {
        // Convert character to uppercase
        /*ptr_strg = toupper(*ptr_strg);*/

        // Mover pointer to next character
        ptr_strg++;
    }
/*-------------------------------------------------------------------*/
```

> 请注意函数原型和函数头中运算符的顺序。按引用传递指针时，地址运算符必须跟在解引用运算符之后。

在此版本的程序中，字符串与程序 chapter9_6 中一样被转换为大写。但是，在此版本中，函数中递增形式参数会更改 main 中的实参，因为使用了按引用传递。在调用函数 stringupper() 之后，指针 ptr_strg1 指向字符串末尾的空字符。因此，大写字符串不会被打印。此程序的示例输出为

```
abbcfgwdbbibw
```

在两个示例中，函数 stringupper() 都能够修改形式参数所指向的字符串。

有时，将指针作为参数传递给函数，并确保函数不会意外修改被指向的对象是可取的。我们可以在函数原型和函数头中使用 const 修饰符来保护被指向的对象，如下一个示例所示。此示例中未包含函数 stringupper() 的定义：

```
/* -------------------------------------------------------------------*/
/*                                                                     */
/*    Program chapter9_7                                             */
/*                                                                     */
/*    This program counts the number of times a specified             */
/*    letter appears in an uppercase string.                          */
/*                                                                     */
/*-------------------------------------------------------------------*/

