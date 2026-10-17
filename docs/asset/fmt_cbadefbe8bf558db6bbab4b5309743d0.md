
- 易于维护，因为只有一个位置作为函数的“家”。
- 模块化使代码易于理解和控制。
- 支持抽象，因为可以使用库函数，而无需额外复制整个函数。

C++ 有两种类型的函数：内置函数或程序员定义函数。在程序员定义函数中，用于特定任务的代码块被赋予一个唯一名称，该名称在函数被调用（激活）时使用。

## 函数声明

*函数声明*介绍函数及其在传递必要参数后能够执行的操作。编译器可以了解函数的签名，并在函数被调用时进行验证。

其语法如下：

```cpp
return_type function_name([ arg1_type arg1_name, ... ]) { code }
```

## 向函数传递参数

传递给函数的参数称为实际参数，函数接收的参数称为*形式参数*。

| C | C++ |
|---|---|
| C 是 C++ 的子集。 | C++ 是 C 的超集。 |
| C 不支持多态、封装和继承。 | C++ 支持多态、封装和继承。 |
| C 不支持数据隐藏，并且很容易被操纵。 | C++ 的封装隐藏了数据，以确保数据结构和运算符按预期使用。 |
| 支持内置数据类型。 | C++ 支持内置以及用户定义的数据类型。 |
| C 是一种函数驱动语言，更关注函数。 | C++ 是一种对象驱动语言。 |
| 使用的头文件是 `stdio.h`。 | C++ 中使用 `iostream.h`。 |
| C 不支持函数和运算符重载。它也没有命名空间功能和引用变量功能。 | C++ 支持函数和运算符重载；它具有命名空间功能和引用变量功能。 |
| C 中的函数不是在结构体内部定义的。 | 函数可以在结构体内部定义。 |
| C 不支持引用变量。 | C++ 支持引用变量。 |
| 命名空间功能不可用。 | C++ 提供命名空间。 |
| C 不支持虚函数和友元函数。 | C++ 支持虚函数和友元函数。 |
| 不支持直接异常处理。 | 支持异常处理。 |
| 内存管理通过 `malloc()` 和 `calloc()` 函数进行。 | `new` 和 `delete` 运算符用于内存分配和释放。 |

## 小结

- 字面量常量（literals）是直接在代码中使用的未命名值。
- `iostream` 类可以处理输入和输出流。
- `cin` 是一个 `istream` 类，使用标准输入来获取值。`cout` 是一个 `ostream` 类，写入标准输出。
- C++ 中的运算符类型包括一元运算符（只接受一个操作数）、二元运算符（接受两个操作数）和三元运算符（处理三个操作数）。
- 将值从一种类型转换为另一种类型的过程称为类型转换。
- C++ 保留了 92 个专供自身使用的单词，称为关键字。
- C++ 具有循环结构，例如 `for`、`while` 和 `do while`，用于执行重复任务。
- 函数定义和声明通过签名完成，以便后续调用。
- C++ 是对 C 的改进，尽管两者有基本的相似之处，但也存在许多差异。

## 练习题

### 理论题

1. 比较 C 与 C++。
2. 定义 C++ 中的字面量和常量。
3. 讨论 C++ 中各种类型的运算符。
4. C++ 中如何进行类型转换？
5. 定义 C++ 中所有基于 IO 的流类。
6. 在程序中，`int` 究竟表示什么？
7. `for` 循环和 `while` 循环哪个更好？结合示例讨论你的答案。
8. `do while` 循环比普通的 `while` 循环更高效吗？
9. 定义各种控制语句并给出示例。
10. 使用 `if-else` 还是 `goto` 更好？请用示例支持你的推理。
11. 讨论在 C++ 中使用函数的过程。
12. 为什么你认为模块化编程受到程序员的青睐？

### 选择题

1. 下列哪项功能不是 C 语言提供的？
   a. 指针
   b. 结构体
   c. 引用
   d. 函数
2. 下列哪种类型是 C++ 提供而 C 不提供的？
   a. `int`
   b. `bool`
   c. `float`
   d. `double`
3. 下列哪个是入口控制循环？
   a. `for`
   b. `while`
   c. `do-while`
   d. `while` 和 `for` 都是
4. 下列哪个运算符具有从左到右的结合性？
   a. 一元运算符
   b. 逻辑非
   c. 数组元素访问
   d. 取地址
5. 字符字面量在 C 和 C++ 中的大小分别是多少？
   a. 4 和 1
   b. 1 和 4
   c. 1 和 1
   d. 4 和 4
6. C++ 中的 `std` 是什么？
   a. `std` 是 C++ 中的一个标准类
   b. `std` 是 C++ 中的一个标准命名空间
   c. `std` 是 C++ 中的一个标准头文件
   d. `std` 是 C++ 中一个用于读取文件的标准头文件
7. `\a` 转义码表示什么？
   a. 警报
   b. 反斜杠
   c. 制表符
   d. 换页
8. `\t` 转义码表示什么？
   a. 警报
   b. 反斜杠
   c. 制表符
   d. 换页
9. 下列哪个不是 C++ 中的关键字？
   a. `int`
   b. `break`
   c. `object`
   d. `void`
10. 哪种方式会产生永久性更改？
    a. 按值传递
    b. 按引用传递
    c. 传递地址
    d. b 和 c 都是

### 实践题

1. 编写一个 C++ 程序来实现运算符。
2. 编写一个 C++ 程序，在不同行上打印你的爱好。
3. 编写一个 C++ 程序，打印三个数的和。
4. 编写一个 C++ 程序，对用户输入的两个数进行加、乘、减运算。
5. 编写一个 C++ 程序，根据用户输入的所有尺寸计算圆柱体的体积。
6. 编写一个 C++ 程序，计算矩形、正方形和圆形的面积与周长，所有尺寸由用户输入。
7. 编写一个 C++ 程序，使用函数交换两个数。
8. 编写一个 C++ 程序，将温度从摄氏度转换为华氏度。
9. 编写一个 C++ 程序，找出用户输入的五个数中的最大值。
10. 编写一个 C++ 程序，计算用户输入的四个数的总和和平均值。

### 选择题答案

| 答案表 |
| --- |
| 1. (c) |
| 2. (b) |
| 3. (d) |
| 4. (c) |
| 5. (a) |
| 6. (b) |
| 7. (a) |
| 8. (c) |
| 9. (c) |
| 10. (d) |

### 参考资料

#### 书籍

- B. Stroustrup，*The C++ Programming Language*（第4版），（Addison-Wesley Professional，2013年）。
- K. R. Venugopal，*Mastering C++*（第2版），（McGraw Hill Education，2017年7月）。
- Y. Kanetkar，*Let Us C++*，（BPB Publications，2020年9月）。

#### 网站

- Learn CPP，访问于2022年5月，`https://www.learncpp.com`
- Geeks For Geeks，访问于2022年5月，`https://www.geeksforgeeks.org`
- WordPress，访问于2022年5月，`https://wordpress.com`
- Code 2 Flow，访问于2022年5月，`https://code2flow.com`
- Silly Codes，访问于2022年5月，`https://sillycodes.com`

# 数组与字符串

## 3.1 什么是数组？

*数组*就像一个存储设施：它允许你将相似的数据类型保存在同一个“屋檐”下，并用一个名称来标识。存储在数组中的项可以是整数、字符和字符串。无论你想把什么分组在一起，都可以使用数组。让我们看看如何声明和初始化它们。

### 3.1.1 声明数组的方式

- `Datatype array_name[array_size];` 通过给定大小来声明
- `Datatype array_name[]={element1, ele2..};` 通过初始化元素来声明
- `Datatype array_name[array_size]={element1, ele2..};` 通过初始化元素和大小来声明
- `Datatype array_name[array_index]= ele3;` 将元素赋值给特定索引

这里，使用了 `[ ]` 下标运算符，以便编译器知道这是一个数组；其后是相同类型的元素，索引从 0 开始（即任何数组的第一个元素总是被赋给索引 0，即 `arr[0]`，数组的最后一个索引是 `n-1`，其中 `n` 表示元素总数）。让我们看一个例子。尝试将数组想象成一列旅客列车，有三节车厢，依次排列，票号从 0 到 2。名为 `Train` 的数组有三个车厢，索引如图 3.1 所示。

![](img/4d9a4ae4efedabe01be6e6c44bad2dc1_60_0.png)

### 3.1.2 访问数组成员的方式

- 存储在连续内存位置中的数组元素也按顺序访问。
- 索引对于提取特定元素很重要。
- 索引为 0 的元素也可以说是数组名称的*指针*。
- 如果你使用静态/固定数组，则使用 `index[n-1]` 提取最后一个元素。
- 对于动态数组，大小在运行时确定，因此使用 `array.length()` 方法来确定确切的大小和索引。

**代码：列车和车厢数组示例**

```cpp
#include <iostream>
int main()
{
        int train[3]={10,11}; // 声明三节车厢
        train[2]= 12;
        std::cout << "\nElements in Train are\n";
        std::cout << "Elements 1: "<<train[0];
        std::cout << "\nElements 2:"<<train[1];
        std::cout << "\nElements 3: "<<train[2];
        return 0;
}
```

**输出：**

```text
Elements in Train are
Elements 1: 10
Elements 2: 11
Elements 3: 12
```

### 3.1.3 遍历一维数组

这里，*1D* 指的是一维数组，你可以使用 `for` 和 `while` 循环语句轻松遍历它以访问和获取数组元素，并允许用户在特定索引处输入数组元素。

**代码：创建一维数组**

```cpp
#include <iostream>
using namespace std;
int main() {

    int num_array[6];
    cout << "Enter six numbers: " << endl;
    for (int i = 0; i < 6; ++i)
    {
        cin >> num_array[i];//从用户处获取元素
    }
    cout << "The numbers are: ";
    for (int j = 0; j < 6; ++j) {
        cout << num_array[j] << " ";// 显示用户数组
    }

    return 0;
}
```

**输出：**

```text
Enter six numbers:
12
79
45
33
11
23
The numbers are: 12  79  45  33  11  23
```

## 3.2 数组上的操作

### 3.2.1 将数组传递给函数

函数非常有用，但你可以传递不需要的数组元素，这会产生一个问题：想象一下传递数千个这样的元素！你可以通过只传递数组名称来避免这种情况，数组名称充当指向第一个元素和整个数组的指针。确保函数签名通过以下方式之一表明它是一个数组非常重要：

- `int func(int array_name[]){ //函数体 }`
- `int func(int array_name[array_size]){ //函数体 }`
- `int func(int *array_name){ //函数体 }`

**代码：传递数组**

```cpp
#include <iostream>

int coach (int train[], int s)
{
int i,price=0;
for( i = 0; i < s; i++)
price += train [i];
return price;
}
int main ( )
{
int price,s;
int train[3]={1050,1100};

std::cout << "How many passengers ";
std::cin >> s;
price = coach (train, s);
std::cout << "\nYour bill is:"<<price;
return 0;
}
```

**输出：**

```text
How many passengers 3

Your bill is: 2150
```

### 3.2.2 查找长度

确定用户输入的动态数组的确切长度非常重要，因为大小可能在程序中途发生变化。

### 3.2.4 搜索

按索引访问数组中的每一个元素（称为*遍历*）对于大型数组来说效率不高，因此我们应该使用一种算法来查找我们想要的元素。以下便是这些搜索方法。

#### 线性搜索

在线性搜索中，我们通过遍历数组并检查搜索元素是否与数组元素匹配，来顺序查找所需的元素。

##### 线性搜索算法

1. 开始。
2. 如果未给定数组，则从用户处获取大小和元素输入。
3. 从用户处输入搜索元素。
4. 初始化 `for` 循环，从 `i=0` 到索引 `size-1`。
5. 使用嵌套 `if` 循环判断搜索元素是否等于 `array[i]`。
6. 如果结果为真，则找到匹配项；跳出循环。
7. 如果结果为假，则执行代码的 `else` 部分。
8. 停止。

##### 代码：线性搜索示例

```cpp
#include<iostream>
using namespace std;
int main()
{
    int size,e,flag=0;
    cout<<"\nGive the size of the array "<<endl;
    cin>>size;
    int array[size];
    cout<<"Enter the elements of the array "<<endl;
    for(int i=0;i<size;i++)
    {
        cin>>array[i];
    }
    cout<<"What do you wish to search for"<<endl;
    cin>>e;
    for(int i=0;i<size;i++)//traverse array
    {
        if(array[i]==e)//check with element to match
        {
            flag=i;
            break;
        }
    }
    if(flag)
        cout<<"Element "<<e<<" is at index "<<flag;
    else
        cout<<"Element "<<e<<" is not present\n";
    return 0;
}
```

##### 输出

```text
Give the size of the array
4
Enter the elements of the array
11
23
66
77
What do you wish to search for
88
Element 88 is not present
```

你还可以通过设置一个初始为 false 的标志，并在 `if` 语句内将 `i` 的值赋给它，来轻松找到搜索元素所在的索引。

#### 二分搜索

在该搜索算法中，我们获得一个按从小到大顺序排列的有序数组。然后，通过找到中点将工作分成两半，并基于中点继续寻找下一半。程序检查搜索元素是大于还是小于中间元素，并重复此过程，直到数组为空并找到匹配的元素。

##### 二分搜索算法

1. 开始。
2. 如果未给定数组，则从用户处获取大小和元素输入。
3. 从用户处输入搜索元素。
4. 调用二分搜索函数，并传入数组、`firstindex`、`lastindex` 和搜索元素。
5. 执行嵌套 `if` 循环，判断搜索元素是等于 `array[mid]`、小于 `array[mid]` 还是大于 `array[mid]`。
6. 如果结果为真，则找到匹配项，返回 `mid`。
7. 如果结果为假，则返回 0 并退出循环。
8. 停止。

##### 代码：二分搜索示例

