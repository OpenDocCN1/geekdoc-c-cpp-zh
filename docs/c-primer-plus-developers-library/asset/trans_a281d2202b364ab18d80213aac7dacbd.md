
数组的地址不传达有关数组大小的任何信息，通常将数组大小作为单独参数传递。或者，可以传递指向数组开头和末尾之后一个位置的指针来表示一个范围，就像 STL 中的算法所做的那样。

C++ 提供三种表示 C 风格字符串的方式：使用字符数组、字符串常量或指向字符串的指针。它们都是 `char*` 类型（指向 char 的指针），因此它们作为 `char*` 类型参数传递给函数。C++ 使用空字符（\0）终止字符串，字符串函数会测试空字符以确定它们正在处理的任何字符串的结尾。

C++ 还提供 `string` 类来表示字符串。函数可以接受 `string` 对象作为参数，并使用 `string` 对象作为返回值。`string` 类的 `size()` 方法可用于确定所存储字符串的长度。

C++ 将结构与基本类型同等对待，这意味着你可以按值传递它们，并将它们用作函数返回类型。然而，如果结构很大，传递指向该结构的指针并让函数处理原始数据可能更高效。这些同样的考虑也适用于类对象。

C++ 函数可以是递归的；也就是说，特定函数的代码可以包含对自身的调用。

C++ 函数的名称充当该函数的地址。通过使用指向函数的指针作为函数参数，可以将你希望第一个函数调用的第二个函数的名称传递给该函数。

## 章节复习

- 1. 使用函数有哪三个步骤？

- 2. 构造与以下描述匹配的函数原型：
  - a. `igor()` 不接受参数，也没有返回值。
  - b. `tofu()` 接受一个 `int` 参数并返回一个 `float`。
  - c. `mpg()` 接受两个 `double` 类型参数并返回一个 `double`。
  - d. `summation()` 接受一个 long 数组的名称和一个数组大小作为值，并返回一个 long 值。
  - e. `doctor()` 接受一个字符串参数（该字符串不应被修改）并返回一个 double 值。
  - f. `ofcourse()` 接受一个 boss 结构作为参数，且不返回任何内容。
  - g. `plot()` 接受一个指向 map 结构的指针作为参数，并返回一个字符串。

- 3. 编写一个函数，接受三个参数：一个 `int` 数组的名称、数组大小和一个 `int` 值。让该函数将数组的每个元素设置为该 `int` 值。

- 4. 编写一个函数，接受三个参数：指向数组中某个范围第一个元素的指针、指向该范围末尾之后元素的指针，以及一个 `int` 值。让该函数将数组的每个元素设置为该 `int` 值。

- 5. 编写一个函数，接受一个 double 数组和一个数组大小作为参数，并返回该数组中的最大值。注意，该函数不应改变数组的内容。

- 6. 为什么不对属于基本类型的函数参数使用 `const` 限定符？

- 7. C 风格字符串在 C++ 程序中可以采取哪三种形式？

- 8. 编写一个具有以下原型的函数：

```cpp
int replace(char * str, char c1, char c2);
```

让该函数将字符串 str 中每次出现的 c1 替换为 c2，并让该函数返回它所做的替换次数。

- 9. 表达式 `*"pizza"` 是什么意思？`"taco"[2]` 呢？

- 10. C++ 使你可以按值传递结构，也允许传递结构的地址。如果 `glitz` 是一个结构变量，你会如何按值传递它？你会如何传递它的地址？这两种方法各有什么取舍？

- 11. 函数 `judge()` 的返回类型为 `int`。它接受一个函数的地址作为参数。其地址被传递的函数又接受一个指向 `const char` 的指针作为参数，并返回一个 `int`。编写该函数原型。

- 12. 假设有如下结构声明：

```cpp
struct applicant {
    char name[30];
    int credit_ratings[3];
};
```

  - a. 编写一个函数，接受一个 applicant 结构作为参数并显示其内容。
  - b. 编写一个函数，接受一个 applicant 结构的地址作为参数，并显示所指向结构的内容。

- 13. 假设函数 `f1()` 和 `f2()` 具有以下原型：

```cpp
void f1(applicant * a);
const char * f2(const applicant * a1, const applicant * a2);
```

这里所述示例的中奖概率是：从 47 个中正确选出 5 个的概率乘以从 27 个中正确选出 1 个的概率。修改程序清单 7.4 以计算赢得这种彩票的概率。

- 5. 定义一个递归函数，接受一个整数参数并返回该参数的阶乘。回想一下，3 的阶乘写作 3!，等于 3 × 2!，依此类推，且 0! 定义为 1。一般来说，如果 n 大于零，则 n! = n * (n − 1)!。在一个程序中使用循环让用户输入各种值，程序报告这些值的阶乘，以此测试你的函数。

- 6. 编写一个使用以下函数的程序：

`Fill_array()` 接受一个 double 值数组的名称和一个数组大小作为参数。它提示用户输入要输入到数组中的 double 值。当数组已满或用户输入非数字输入时，它停止接收输入，并返回实际输入的条目数。

`Show_array()` 接受一个 double 值数组的名称和一个数组大小作为参数，并显示数组的内容。

`Reverse_array()` 接受一个 double 值数组的名称和一个数组大小作为参数，并反转数组中存储值的顺序。

该程序应使用这些函数填充一个数组，显示该数组，反转该数组，显示该数组，反转除数组第一个和最后一个元素之外的所有元素，然后显示该数组。

- 7. 重做程序清单 7.7，修改三个数组处理函数，使它们各自使用两个指针参数来表示一个范围。`Fill_array()` 函数不返回实际读取的项数，而应返回指向最后一个填充位置之后位置的指针；其他函数可以将该指针用作第二个参数来标识数据的结尾。

- 8. 在不使用 array 类的情况下重做程序清单 7.15。做两个版本：

  - a. 使用一个由 `const char *` 组成的普通数组来表示季节名称的字符串，并使用一个 double 的普通数组表示开支。
  - b. 使用一个由 `const char *` 组成的普通数组来表示季节名称的字符串，并使用一个其唯一成员为 double 普通数组的结构来表示开支。（这种设计类似于 array 类的基本设计。）

- 9. 本练习提供编写处理数组和结构的函数的练习。以下是一个程序骨架。通过提供所描述的函数来完成它：

```cpp
#include <iostream>
using namespace std;

const int SLEN = 30;
struct student {
    char fullname[SLEN];
    char hobby[SLEN];
    int ooplevel;
};
// getinfo() has two arguments: a pointer to the first element of
// an array of student structures and an int representing the
// number of elements of the array. The function solicits and
// stores data about students. It terminates input upon filling
// the array or upon encountering a blank line for the student
// name. The function returns the actual number of array elements
// filled.
int getinfo(student pa[], int n);

// display1() takes a student structure as an argument
// and displays its contents
void display1(student st);

// display2() takes the address of student structure as an
// argument and displays the structure’s contents
void display2(const student * ps);

// display3() takes the address of the first element of an array
// of student structures and the number of array elements as
// arguments and displays the contents of the structures
void display3(const student pa[], int n);

int main()
{
    cout << "Enter class size: ";
    int class_size;
    cin >> class_size;
    while (cin.get() != '\n')
        continue;

    student * ptr_stu = new student[class_size];
    int entered = getinfo(ptr_stu, class_size);
    for (int i = 0; i < entered; i++)
    {
        display1(ptr_stu[i]);
        display2(&ptr_stu[i]);
    }
    display3(ptr_stu, entered);
    delete [] ptr_stu;
    cout << "Done\n";
    return 0;
}
```
