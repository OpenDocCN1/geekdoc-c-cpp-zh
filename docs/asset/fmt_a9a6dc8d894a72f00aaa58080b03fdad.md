
# C++ 入门指南：从控制结构到对象，附录 O：奇数复习题答案

## 附录 O：奇数复习题答案

### 第 1 章

#### 31. 层级结构图：

![](img/3af3ad0d2f1fe20139551695356e239f_1_0.png)

#### 33. 7

#### 35. 365

### 第 2 章

```cpp
{
  cout << "Two mandolins likes creatures in the\n\n\n";
  cout << "dark\n\n\n";
  cout << "Creating the agony of ecstasy.\n\n\n";
  cout << " George Barker\n\n\n";
  return 0;
}
```

B) 4
C) 2
D) 6
E) 1

`ReadCredit;`

显示“输入客户已使用的信誉额度：”

`ReadUsed.`

`availableCredit = maxCredit - creditUsed;`

显示“客户的可用信誉额度为 $”

显示 `availableCredit`.

```cpp
#include <iostream>
using namespace std;

int main() {
  double maxCredit, creditUsed, availableCredit;

  cout << "Enter the customer's maximum amount of credit: ";
  cin >> maxCredit;
  cout << "Enter the amount of credit used by the customer: ";
  cin >> creditUsed;
  availableCredit = maxCredit - creditUsed;
  cout << "The customer's available credit is $";
  cout << endl;
  return 0;
}
```

```cpp
#include <iostream>
using namespace std;

int main() {
  int score1, score2, score3, averageScore;

  cout << "Enter the score for the 1st game: $";
  cin >> score1;
  cout << "Enter the score for the 2nd game: $";
  cin >> score2;
  cout << "Enter the score for the 3rd game: $";
  cin >> score3;
  averageScore = (score1 + score2 + score3) / 3;
  cout << "The average score is: $";
  cout << averageScore << endl;
  return 0;
}
```

`cin >> number1 >> number2;`

赋值语句应该读取：

`quotient = static_cast<float>(number1) / number2;`

最后一条语句缺少分号。

### 第 3 章

`main` 函数头头应该是：

```cpp
int main()
```

复合赋值运算符使用不当。

语句应该是：

```cpp
number1 *= 50;
number2 *= 50;
```

以下语句：

```cpp
getline >> name;
getline(cin, name);
```

#### 35. 6 12

#### 37. 分钟：612000.0000

小时：10200.0332

天：425.0014

月份：13.9726

年：1.1644

### 第 4 章

```cpp
31. if (y == 0)
    x = 100;
```

```cpp
    commission = .10;
    else if (sales <= 15000)
    commission = .15;
    else
        commission = .20;
```

```cpp
    if (amount2 < 100)
        cout << (amount1 > amount2 ? amount1 : amount2);
```

```cpp
37. if (temperature >= -50 && temperature <= 150)
    cout << "The number is valid.";
```

```cpp
39. if (str1 > str2)
    cout << str2;
else
    cout << str1;
```

59. `if/else` 结构应该用大括号括起来。62 `switch` 语句不能测试关系表达式。应该使用 `if-else` 语句。

### 第 5 章

#### 35.
```cpp
int product = 0, num;
while (product < 100)
{
    cin >> num;
    product = num * 10;
}
```

#### 37.
```cpp
for (int row = 0; row < 1000; row++)
    for (int col = 0; col < 15; col++)
        cout << '#';
    cout << endl;
}
```

#### 39.
```cpp
for (int row = 0; row < 1000; row++)
{
    for (int col = 0; col < 15; col++)
        cout << '#';
    cout << endl;
}
```

#### 41.
```cpp
char sure = 'X';
while (sure != 'Y' && sure != 'N')
{
    cout << "Are you sure you want to ";
    cin >> sure;
}
```

#### 43.
```cpp
int x = 50;
while (x > 0)
{
    cout << x << " seconds to go.\n";
    x--;
}
```

#### 45.
```cpp
ifstream inputFile("Numbers.txt");
int number;
while (inputFile >> number)
cout << number << endl;
inputFile.close();
```

47. false
49. false
51. false
53. false
55. false
57. true
59. true
61. false
63. true

67. `while` 语句末尾不应该有分号。可以认为 `bigNum` 应该定义为 `long` 类型。

`count` 应该初始化为 1。

69. `do-while` 循环测试的表达式应该是 `choice == 1` 而不是 `choice = 1`。

### 第 6 章

- 15. `value`
- 17. `local`
- 19. `global`
- 21. `local`
- 23. `return`
- 25. `last`
- 27. `reference`
- 29. `reference`
- 31. `parameter lists`

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

该函数定义为 `double` 但没有返回任何值。

59. 参数应该定义为：

```cpp
int &value
cin >> value;
```

### 第 7 章

- 35. 序列 (`sequence`)
- 37. `push_back`
- 41. `for (int i = 0; i < 20; i++)`

    `cout << names[i] << endl;`

```cpp
43. const int SIZE = 10;
int id[SIZE]; // 用于存储 ID 号
double weeklyPay[SIZE]; // 用于存储周薪
// 显示每个员工的周总薪。
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

- 61. False

### 第 8 章

### 第 9 章

- 17. 拼接 (`concatenate`)

    `strcpy(str, name);`

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

- 43. `isupper` 函数只能用于测试字符，而不是字符串。
- 45. 编译器不会分配足够的空间来容纳两个字符串。

### 第 11 章

`info.lastName = "Smith"`

`info.middleName = "Bart"`

`info.firstName = "William"`

- C) `cout << info.lastName << endl;`

`cout << info.middleName << endl;`

`cout << info.firstName << endl;`

- 7. A) `"Canton"`

B) `"Haywood"`

C) 978

D) 未初始化 (`uninitialized`)

- 11. 0 1 2

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

- 33. `num = 452;`
- 35. `enum Pets(DOGS, CATS, BIRDS, HAMSTERS);`
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
- 67. `x` 和 `y` 不能同时有效使用。

### 第 12 章

- 3. 内容会被擦除。（换句话说，文件被截断）。
- 23. `put`
- 31. `sequential`

```cpp
41. fstream places("places.dat", ios::in | ios::out);
```

```cpp
43. pets.open("pets.dat", ios::in)
fstream open("pets.dat", ios::in);
```

- 51. True

65. 文件应该这样打开：

```cpp
fstream file("info.dat", ios::in | ios::out);
or
fstream file:
file.open("info.dat", ios::in | ios::out);
```

67. 文件访问日志必须用 `fstream` 对象指定。

69. 文件类标志应该是 `ios::in`。此外，`get` 成员函数不能用于读取字符串。

71. 文件类标志应该是 `ios::out`。此外，最后一行应该是：

`dataFile.write(reinterpret_cast<char *>(&dt), sizeof(dt));`

### 第13 章

- 15. 类的职责是类负责知道的事情以及类负责执行的动作。
- 23. 访问修符
- 35. `default`
- 37. `~`
- 39. `default`
- 41. `constructor`, `destructor`

```cpp
43. class Circle
{
    private:
        double radius;
    public:
        void setRadius(double r)
        { radius = r; }
        double getRadius()
        { return radius; }
        double getArea()
        { return 3.14159 * radius * radius; }
}
```
