

# 附录 O：奇数复习题答案

- 15. value
- 17. local
- 19. global
- 21. local
- 23. return
- 25. last
- 27. reference
- 29. reference
- 31. parameter lists

```cpp
33. double half(double num)
{
    return num / 2;
}
```

```cpp
35. void timesTen(int num)
{
    cout << (num * 10) << endl;
}
37. void getNumber(int &num)
{
    cout << "Enter a number in the range 1 - 100 : ";
    cin >> num;
    while (num < 1 || num > 100)
    {
        cout << "That number is out of range.\n";
        cout << "Enter a number in the range 1 - 100 : ";
        cin >> num;
    }
}
```

- 39. False
- 41. True
- 43. True
- 45. False
- 47. True
- 49. True
- 51. True
- 53. False
- 55. True

57. 赋值语句应该是：

```cpp
average = (value1 + value2 + value3) / 3.0;
```

该函数定义为 double 但没有返回任何值。

59. 参数应该定义为：

```cpp
int &value
cin >> value;
```

# 第 7 章

- 1. 尺寸声明符（size declarator）用于数组的定义，用指示数组拥有的元素数量。下标（subscript）用于访问数组中的特定元素。
- 2. 因为仅凭数组，函数没有办法确定它包含的元素数量。
- 5. 通过提供初始化列表。数组的大小设置为容纳列表中数值的数量。
- 7. 因为不带括号和下标的数组名代表数组的起始内存地址。所示的语句试图将 array2 的地址赋值给 array1，这是不允许的。
- 9. 通过引用（By reference）。
- 11. 通过对每个数组使用相同的下标值。
- 13. 第二尺寸声明符，用于列数。
- 15. 尺寸声明符 (size declarator)
- 17. 下标 (subscript)
- 19. 尺寸声明符, 下标
- 21. 初始化 (initialization)
- 23. 初始化列表 (initialization list)
- 25. =
- 27. 地址或名称 (address, or name)
- 29. 行、列 (rows, columns)
- 31. 大括号 (braces)
- 33. 标准模板库（或 STL）
- 35. 序列 (sequence)
- 37. push_back
- 41. for (int i = 0; i < 20; i++)
    cout << names[i] << endl;

```cpp
43. const int SIZE = 10;
int id[SIZE]; // 用于存储 ID 号
double weeklyPay[SIZE]; // 用于存储周薪
// 显示每个员工的周总薪。
for (int i = 0; i < SIZE; i++)
{
    cout << "The pay for employee "
    << id[i] << " is $" 
    << showpoint << setprecision(2)
    << weeklyPay[i] << endl;
}
```

```cpp
47. numberArray[0][0] = 15;
numberArray[8][10] = 18;
const int NUM_COLS = 5;
const int row, col; // 循环计数器
total; // 累加器
// 显示每行的和。
for (row = 0; row < NUM_ROWS; row++)
{
    // 设置累加器。
    total = 0;
    // 求行和。
    for (col = 0; col < NUM_COLS; col++)
        total += days[row][col];
    // 显示行的总数。
    cout << "The total for row " << row
    << " is " << total << endl;
}
```

```cpp
// 显示每列的和。
for (col = 0; col < NUM_COLS; col++)
{
    // 设置累加器。
    total = 0;
    // 求列和。
    for (row = 0; row < NUM_ROWS; row++)
        total += days[row][col];
    // 显示列的总数。
    cout << "The total for column " << col
    << " is " << total << endl;
}
```

- 51. True
- 53. False
- 55. False
- 57. True
- 59. True
- 61. False
- 63. False
- 65. True
- 67. True
- 69. True
- 73. False
- 75. False
- 77. True
- 79. True
- 81. 尺寸声明符不能为负数。
- 83. 初始化列表必须括在大括号内。
- 85. 隐式尺寸数组必须是初始化列表。
- 87. 赋值运算符不能将一个数组的内容赋值给另一个数组，这是一个语句。
- 89. 参数必须指定列数而不是行数。

# 第 8 章

- 1. 因为它使用循环遍历数组，从第一个元素开始，与搜索值进行比较，当找到该值或遇到数组结束时停止。
- 3. N/2 次
- 5. 十
- 7. 选择排序的交换次数较少，因为它直接将项目移动到它们的最终位置。
- 9. 二分 (binary)
- 11. 二分 (binary)
- 13. 降序 (descending)
- 15. False
- 17. False

# 第 9 章

- 1. 解引用指针，允许代码操作指针指向。
- 3. 乘法运算符、指针变量定义和间接运算符（indirection operator）。
- 5. 将 ptr 存储的地址增加 int 的 4 倍。
- 7. 为了动态分配内存。

- 5. string
- 7. string
- 9. isupper
- 11. isdigit
- 13. toupper
- 15. cctype
- 17. 拼接 (concatenate)
- 19. strcpy
- 21. strncmp
- 23. atoi
- 27. if (toupper(choice) == 'Y')
- 29. if (strlen(name) <= 9)
    strcpy(str, name);

```cpp
31. int wCount(char *str)
{
    int num = 0;
    while (*str != '\0')
    {
        if (*str == 'W')
            num++;
    }
    return num;
}
```

- 33. False
- 35. False
- 37. True
- 39. False
- 41. True
- 43. isupper 函数只能用于测试字符，而不是字符串。
- 45. 编译器不会分配足够的空间来容纳两个字符串。

# 第 11 章

- 1. C++ 语言内置的数据类型，如 int, char, float 等。
- 3. 数组的元素必须是相同类型。结构体的成员可以是不同的类型。
- 5. FullName info;
   info.lastName = "Smith"
   info.middleName = "Bart"
   info.firstName = "William"

- C) cout << info.lastName << endl;
cout << info.middleName << endl;
cout << info.firstName << endl;
- 7. A) "Canton"
B) "Haywood"
C) 978
D) 未初始化 (uninitialized)
- 9. 联合体（union）的所有成员占用同一块内存，而结构体（structure）的成员有自己的内存位置。
- 11. 0 1 2
- 13. 已声明 (declared)
- 15. 成员 (members)
- 17. 标签 (tag)
- 19. Car hotRod = {"Ford", "Mustang", 1997, 2000};
- 21. Car forSale[35] = {"Ford", "Taurus", 1997, 21000, "Honda", "Accord", 1992, 11000, "Lamborghini", "Countach", 1997, 20000};

```cpp
23. struct TempScale {
    double fahrenheit;
    double centigrade;
};
struct Reading {
    int windSpeed;
    double humidity;
    TempScale temperature;
};
```

```cpp
25. void showReading(Reading values)
{
    cout << "Wind speed: " << values.windSpeed << endl;
    cout << "Humidity: " << values.humidity << endl;
    cout << "Fahrenheit temperature: " << values.temperature.fahrenheit << endl;
    cout << "Centigrade temperature: " << values.temperature.centigrade << endl;
}
```

```cpp
27. getReading() {
    Reading local;
    cout << "Enter the following values:\n";
    cout << "Wind speed: ";
    cin >> local.windSpeed;
    cout << "Humidity: ";
    cin >> local.humidity;
    cout << "Fahrenheit temperature: ";
    cin >> local.temperature.fahrenheit;
}
```

```cpp
cout << "Centigrade temperature: ";
cin >> local.temperature.centigrade;
return local;
}
```

- 29. rptr->WindSpeed = 50;

```cpp
31. union Items
{
    char alpha;
    int num;
    long bigNum;
    float real;
};
Items x;
```

- 33. num = 452;
- 35. enum Pets(DOGS, CATS, BIRDS, HAMSTERS);
- 37. True
- 39. False
- 41. False
- 43. True
- 45. True
- 47. True
- 49. False
- 51. False
- 53. True
- 55. True
- 57. 结构声明没有标签。
- 59. 没有声明结构体变量。TwoVals 是结构标签。
- 61.  的初始化列表必须括在大括号内。
- 63. 结构成员不能在结构定义中初始化。
- 65. 函数必须定义一个 TwoVals 结构变量。然后，该变量应用于赋值语句。
- 67. x 和 y 不能同时有效使用。

# 第 12 章

- 1. 最快的数据类型允许读取和写入，而 istream 数据类型只允许读取，而 ofstream 数据类型只允许写入。
- 3. 内容会被擦除。（换句话说，文件被截断）。
- 5. 因为引用文件流对象的内部状态在大多数操作中都会发生变化。它们应该始终传递给函数以确保内部一致性。
- 7. 当遇到文件末尾时，eof 成员函数会报告该位的状态。

