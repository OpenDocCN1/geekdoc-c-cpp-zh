
int `numbers[SIZE] = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};`

`file.write(reinterpret_cast<char *>(numbers), sizeof(numbers));`

在该函数执行后，`numbers` 数组的内容将被写入二进制文件。以下代码显示从文件中读取值并存储到 `numbers` 数组中：

```cpp
const int SIZE = 10;

int numbers[SIZE];

file.read(reinterpret_cast<char *>(numbers), sizeof(numbers));
```

程序 12-14 展示了将一个 `int` 数组写入文件，然后将数据从文件读回内存。

# 程序 12-14

```cpp
1 // 此程序使用了 write 和 read 函数。
2 #include <iostream>
3 #include <fstream>
4 using namespace std;
5
6 int main() {
7     const int SIZE = 10;
8     fstream file;
9     int numbers[SIZE] = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
10    // 以二进制模式打开文件用于输出。
11    file.open("numbers.dat", ios::out | ios::binary);
12
13    // 将数组的内容写入文件。
14    cout << "Writing the data to the file.\n";
15    file.write(reinterpret_cast<char *>(numbers), sizeof(numbers));
16
17    // 关闭文件。
18    file.close();
19
20    // 以二进制模式打开文件用于输入。
21    file.open("numbers.dat", ios::in | ios::binary);
22
22    // 将文件内容读入数组。
23    cout << "Reading the data back into memory.\n";
24    file.read(reinterpret_cast<char *>(numbers), sizeof(numbers));
25
26    // 显示数组的内容。
27    for (int count = 0; count < SIZE; count++)
28        cout << numbers[count] << " ";
29    cout << endl;
30
31    // 关闭文件。
32    file.close();
33    return 0;
34 }
```

# 12.8 结构体记录

## 程序输出

```
Writing the data to the file.
Reading the data back into memory.
```

## 结构体记录

**概念：** 结构体可以将固定长度的记录存储到文件中。

在本章早期介绍了字段（fields）和记录（records）的概念。字段是关于单个项的数据。记录由字段组成，是关于单个项的完整数据集。例如，一个人的姓名、地址和电话号码。所有属于一个人的字段共同构成记录。

在 C++ 中，结构体提供了将数据组织成字段和记录的方便方法。例如，可以使用以下代码创建一个包含信息的记录：

```cpp
const int NAME_SIZE = 51, ADDR_SIZE = 51, PHONE_SIZE = 14;

struct Info {
    char name[NAME_SIZE];
    int age;
    char address1[ADDR_SIZE];
    char address2[ADDR_SIZE];
    char phone[PHONE_SIZE];
};
```

除了提供数据的组织结构，结构体还将数据封装成单个单元。例如，假设结构体变量定义为 `Info person;`，一旦 `person` 的成员（或字段）填充了数据，可以使用以下函数将整个变量写入文件：

```cpp
file.write(reinterpret_cast<char*>(&person), sizeof(person));
```

第一个参数是 `person` 的地址。`reinterpret_cast` 运算符将地址转换为 `char` 指针。第二个参数是以 `person` 为参数的 `sizeof` 运算符。它返回 `person` 结构体使用的字节数。程序 12-15 展示了这种技术。

> **注意：** 由于结构体可以包含混合数据类型，打开文件存储它们时应始终使用 `ios::binary` 模式。

# 程序 12-15

```cpp
1  // 此程序使用结构体变量将记录写入文件。
2  #include <iostream>
3  #include <fstream>
4  using namespace std;
5
6  // 数组大小
7  const int NAME_SIZE = 51, ADDR_SIZE = 51, PHONE_SIZE = 14;
8
9  // 声明记录的结构体。
10 struct Info
11 {
12     char name[NAME_SIZE];
13     int age;
14     char address1[ADDR_SIZE];
15     char address2[ADDR_SIZE];
16     char phone[PHONE_SIZE];
17 };
18
19 int main()
20 {
21     Info person; // 用于存储人的信息
22     char again;  // 用于存储 Y 或 N
23
24     // 以二进制输出模式打开文件。
25     fstream people("people.dat", ios::binary);
26
27     do
28     {
29         // 获取人的数据。
30         cout << "Entering the data about a "
31              << "person:\n";
32         cout << "Name: ";
33         cin.getline(person.name, NAME_SIZE);
34         cout << "Age: ";
35         cin >> person.age;
36         cin.ignore(); // 跳过剩余的换行符。
37         cout << "Address line 1: ";
38         cin.getline(person.address1, ADDR_SIZE);
39         cout << "Address line 2: ";
40         cin.getline(person.address2, ADDR_SIZE);
41         cout << "Phone: ";
42         cin.getline(person.phone, PHONE_SIZE);
43
44         // 将 person 结构体的内容写入文件。
45         people.write(reinterpret_cast<char*>(&person),
46                      sizeof(person));
47
48         // 判断用户是否想写入另一个记录。
49         cout << "Do you want to enter another record? ";
50         cin >> again;
51         cin.ignore(); // 跳过剩余的换行符。
52     } while (again == 'Y' || again == 'y');
53
54     // 关闭文件。
55     people.close();
56     return 0;
57 }
```

## 12.8 使用结构体创建记录

## 粗体显示的示例输入对应的程序输出

输入以下关于个人的数据：
姓名：Charlie Baxter
年龄：42
地址行 1：67 Kennedy Blvd.
地址行 2：Perth, SC 38754
电话：(803)555-1234
你想输入另一个记录吗？Y
输入以下关于个人的数据：
姓名：Meredith Murney
年龄：22
地址行 1：487 Lindsay Lane
地址行 2：Hazel, NC 28737
电话：(828)555-9999
你想输入另一个记录吗？N

程序 12-15 允许你通过填充 `person` 变量的成员来构建文件，然后将变量写入文件。程序 12-16 打开文件并将每个记录读取到 `person` 变量中，然后在屏幕上显示这些数据。

## 程序 12-16

```cpp
1  // 此程序使用结构体变量从文件中读取记录。
2  #include <iostream>
3  #include <fstream>
4  using namespace std;
5
6  const int NAME_SIZE = 51, ADDR_SIZE = 51, PHONE_SIZE = 14;
7
8  // 为记录声明结构体。
9  struct Info
10 {
11     char name[NAME_SIZE];
12     int age;
13     char address1[ADDR_SIZE];
14     char address2[ADDR_SIZE];
15     char phone[PHONE_SIZE];
16 };
17
18 int main()
19 {
20     Info person; // 用于存储个人信息
21     char again;  // 用于存储 Y 或 N
22     fstream people; // 文件对象
23
24     // 以二进制模式打开输入文件。
25     people.open("person.dat", ios::in | ios::binary);
26
27     // 检查错误。
28     if (!people)
29     {
30         cout << "打开文件错误。程序终止。\n";
31         return 0;
32     }
33
34     cout << "文件中的人员有：\n";
35     // 从文件中读取第一个记录。
36     people.read(reinterpret_cast<char*>(&person),
37                 sizeof(person));
38
39     // 当未到达文件末尾时，显示记录。
40     while (!people.eof())
41     {
42         // 显示记录。
43         cout << "Name: ";
44         cout << person.name << endl;
45         cout << "Age: ";
46         cout << person.age << endl;
47         cout << "Address line 1: ";
48         cout << person.address1 << endl;
49         cout << "Address line 2: ";
50         cout << person.address2 << endl;
51         cout << "Phone: ";
52         cout << person.phone << endl;
53
54         // 等待用户按回车键。
55         cout << "\n按回车键查看下一个记录。\n";
56         cin.get(again);
57
58         // 从文件中读取下一个记录。
59         people.read(reinterpret_cast<char*>(&person),
60                     sizeof(person));
61     }
62
63     cout << "这就是文件中的所有数据！\n";
64     people.close();
65     return 0;
66 }
```

## 程序输出（使用程序 12-15 创建的文件作为输入）

文件中的人员有：

姓名：Charlie Baxter
年龄：42
地址行 1：67 Kennedy Blvd.
地址行 2：Perth, SC 38754
电话：(803)555-1234

按回车键查看记录。
姓名：Meredith Murney
年龄：22
地址行 1：487 Lindsay Lane
地址行 2：Hazel, NC 28737
电话：(828)555-9999
这就是文件中的所有数据！

# 12.9 随机访问文件

## 随机访问文件

**概念：** 随机访问意味着非顺序地访问文件中的数据。到为止所有的程序都是顺序访问。当打开文件时，读取或写入的位置位于文件开头（除非使用 `ios::app` 模式，会将数据写入末尾）。如果以输出模式打开，数据在之后写入。如果以输入模式打开，从第一个字节读取数据。随着读取或写入的继续，文件流的位置在文件中移动。顺序访问的问题在于，为了读取文件的特定字节，必须读取其之前的所有字节。例如，如果程序需要文件的数百字节处，它必须读取前 99 个字节。要到达末尾，必须快进。没有办法直接跳转到该字节。虽然顺序访问在很多情况下很有用，但它会减慢程序速度。如果文件很大，定位其中的数据可能花费很长时间。相反，C++ 允许程序执行随机访问。在随机访问中，程序可以直接跳转到文件的任何字节，而无需先读取前面的字节。顺序访问与随机访问的区别就像磁带与光盘的区别。听 CD 时，不需要快进，只需跳转到你想听的曲目。如图 12-8 所示。

## seekp 和 seekg 成员函数

文件流对象拥有成员函数，用于将读/写位置移动到文件的任何字节。`seekp` 函数用于输出模式打开的文件，`seekg` 用于输入模式打开的文件（如果你记住“p”代表“put”（写入），“g”代表“get”（读取），这就有意义）。`seekp` 用于写入数据的文件，`seekg` 用于读取数据的文件。

以下是 `seekp` 的用法示例：

```cpp
file.seekp(20L, ios::beg);
```

第一个参数是表示文件偏移的长整型。这是你想移动的字节数。在此示例中使用 `20L`（记住 L 强制编译器将数字视为长整型）。该语句将文件的写入位置移动到字节 20 处（编号从 0 开始，因此字节 20 实际上是第 21 个字节）。第二个参数是模式，指定从哪里计算偏移。标志 `ios::beg` 表示从文件开头计算偏移。或者，偏移也可以从文件末尾或文件的当前位置计算。表 12-6 列出了所有随机访问模式的标志。

## 表 12-6 偏移模式

| 模式标志 | 说明 |
|---|---|
| `ios::beg` | 偏移从文件开头计算 |
| `ios::end` | 偏移从文件末尾计算 |
| `ios::cur` | 偏移从当前位置计算 |

表 12-7 显示了使用各种模式标志的 `seekp` 和 `seekg` 示例。注意表 12-7 中的示例使用了负偏移。负偏移会导致读或写位置向后移动，而正偏移会导致向前移动。

假设 `file.txt` 包含以下数据：

`abcdefghijklmnopqrstuvwxyz`

程序 12-17 使用 `seek` 函数在文件的不同位置之间跳转，每次停止后检索一个字符。

## 表 12-7 模式示例

| 语句 | 对读/写位置的影响 |
|---|---|
| `file.seekp(32L, ios::beg)` | 将写入位置设置为文件开头的第 33 个字节（字节 32）。 |
| `file.seekp(-10L, ios::end)` | 将写入位置设置为文件末尾倒数第 10 个字节。 |
| `file.seekp(20L, ios::cur)` | 将写入位置设置为当前位置后的第 21 个字节（字节 20）。 |
| `file.seekg(2L, ios::beg)` | 将读取位置设置为文件开头的第 3 个字节（字节 2）。 |
| `file.seekg(-100L, ios::end)` | 将读取位置设置为文件末尾倒数第 100 个字节。 |
| `file.seekg(0L, ios::end)` | 将读取位置设置为文件末尾。 |

![图 12-8 顺序访问与随机访问](img/191adf3284699566a7b1008cebdb5_731_0.png)

## 程序 12-17

```cpp
// 此程序演示 seekg 函数。
#include <iostream>
#include <fstream>
using namespace std;

int main() {
    char ch;
    fstream file("file.txt", ios::in | ios::binary);

    // 移动到第 5 个字节（从 0 开始）
    file.seekg(5L, ios::beg);
    file.get(ch);
    cout << "从开始第 5 个字节：" << ch << endl;

    // 移动到倒数第 10 个字节
    file.seekg(-10L, ios::end);
    file.get(ch);
    cout << "从结束第 10 个字节：" << ch << endl;

    // 移动到当前位置后第 3 个字节
    file.seekg(3L, ios::cur);
    file.get(ch);
    cout << "从当前第 3 个字节：" << ch << endl;

    file.close();
    return 0;
}
```

## 程序屏幕输出

```
从开始第 5 个字节：f
从结束第 10 个字节：q
从当前第 3 个字节：u
```

程序 12-18 展示了 `seekg` 函数的一个更健壮的示例。它打开由程序 12-15 创建的 `people.dat` 文件。该文件包含两条记录。程序 12-18 首先显示记录 1（第二个记录），然后显示记录 0。

`main` 函数之外有两个重要的函数。第一个函数 `byteNum` 接收记录数作为参数，并返回该记录的起始字节。它通过将记录数乘以 `Info` 结构体的大小来计算记录的起始字节。这返回了该记录从文件开始的偏移量。第二个函数 `showRec` 接收 `Info` 结构体作为参数，并将其内容显示在屏幕上。

# 程序 12-18

```cpp
// 此程序从文件中随机读取一条数据记录。
#include <iostream>
#include <fstream>
using namespace std;

const int NAME_SIZE = 51, ADDR_SIZE = 51, PHONE_SIZE = 14;

// 声明记录结构体。
struct Info {
    char name[NAME_SIZE];
    int age;
    char address1[ADDR_SIZE];
    char address2[ADDR_SIZE];
    char phone[PHONE_SIZE];
};

// 函数原型
long byteNum(int);
void showRec(Info);

int main() {
```
