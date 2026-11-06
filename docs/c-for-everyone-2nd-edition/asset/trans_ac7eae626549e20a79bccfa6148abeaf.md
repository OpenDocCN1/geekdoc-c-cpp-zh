

```
r = q; ⑧
r = s; ⑨
s = p; ⑩
s = q; ⑪
s = r; ⑫
}
```

**R7.19** 如果忘记删除从堆中获得的对象，会发生什么？如果删除两次，会发生什么？

**R7.20** 编写一个程序，访问已删除的指针、未初始化的指针和 NULL 指针。运行程序时会发生什么？

**R7.21** 找出以下代码中的错误。并非所有行都包含错误。每一行都依赖于前面的行。注意未初始化的指针、NULL 指针、指向已删除对象的指针，以及将指针与对象混淆的问题。

```
1  int* p = new int;
2  p = 5;
3  *p = *p + 5;
4  string s = "Harry";
5  *s = "Sally";
6  delete &s;
7  int* a = new int[10];
8  *a = 5;
9  a[10] = 5;
10 delete a;
11 int* q;
12 *q = 5;
13 q = p;
14 delete q;
15 delete p;
```

**R7.22** 如何仅使用 vector（而不是数组或指针）来定义三角二维数组？

**R7.23** 重写 7.7.3 节中的语句，使街道地址和员工结构分配到堆上。

**R7.24** 设计一个结构类型 Person，包含一个人的姓名以及指向其父亲和母亲的指针。编写语句，为你自己和你的父母定义结构值，并正确建立指针链接。（父母的父母使用 NULL。）

**R7.25** 画出显示习题 P7.4 中调用 maximum 函数结果的图。

**R7.26** 画出读取几行后习题 P7.13 中 lines 数组里的指针图。

**R7.27** 7.6 节描述了一种安排：每个物品都有一个指针，指向借出该物品的用户。这使得很难找出某个特定用户借出了哪些物品。为解决这个问题，设置一个字符串数组 `user_names` 和一个并行数组 `loaned_items`。`loaned_items[i]` 指向一个 `char*` 指针数组，其中每个指针都是第 i 个用户借出的一个物品名称。如果第 i 个用户没有借出任何物品，则 `loaned_items[i]` 为 `NULL`。画出这种安排的图。

以及一个列车指示器，其值为 0（空）、+1（列车顺时针行驶）或 −1（列车逆时针行驶）。在系统中随机路段放置四列列车，每个方向两列。在每一步显示轨道和列车，如下所示：

```
 +---------->--+\
 |  x  x  x  x  |\
 |<----------- |\
 |             |\
 >--<----------|\
 |  x  x  x  x  |\
 +------------+
```

两个矩形表示轨道。每个允许列车在外轨和内轨之间切换的道岔都用 x 表示。每列列车画成 > 或 <，表示其当前方向。程序应显示五十轮。在每一轮中，所有列车都移动一次。

## 自测题答案

- 1. 1
   2
- 2. 2 2
- 3. 30
- 4. 25
- 5. 15，后面是变量 a 的内存地址。该地址可能因程序运行而异。
- 6. 2 0 5
- 7. 2 3 0
- 8. 2 3 5
- 9. 4 5
- 10. `void squares(int n, int* result)`
- 11. 15: `'H''e''l''l''o', ... 'w''o''r''l''d''\n'\0`
- 12. 14. 空终止符不计数，而 '\n' 算作单个字符。
- 13. `char* p = "Hello";`
- 14. 该语句可以编译，但会产生灾难性后果。"Agent" 的类型是 char*。向 char* 加一个整数是合法的。结果是一个指向数组起始位置之后七个字符处的指针。该数组只包含 6 个字符，因此结果指向内存的其他部分。标题字符串将用在那里找到的任意字符构造，直到遇到零为止。结果不可预测。
- 15. `int number = atoi(input.c_str());`
- 16. 3
- 17. 0 1 4
- 18. 访问 p[10] 是非法的；返回的数组元素索引为 0 … 9。
- 19. p 指向一个大小为 10 的数组，元素为 2, 3, 5, 7, 11, 0, 0, 0, 0, 0。
- 20. 当返回的指针不再需要后，对它调用 delete[]。

![](img/23fb3582e93ebc95909e1de029c3d388_376_0.png)

![](img/23fb3582e93ebc95909e1de029c3d388_376_1.png)

![](img/23fb3582e93ebc95909e1de029c3d388_376_2.png)

```
31. StreetAddress state_dept;
    state_dept.house_number = 2201;
    state_dept.street_name = "C Street NW";
```

```
32. StreetAddress* state_dept = new StreetAddress;
    state_dept->house_number = 2201;
    state_dept->street_name = "C Street NW";
```

```
33. struct Date
{
    string month; // It is also OK to define month as an int
    int day;
};
```

```
34. Date independence_day;
    independence_day.month = "July";
    independence_day.day = 4;
```

```
35. cout << harry.office->house_number << " " << harry.office->street_name;
```

注意，必须使用箭头，因为 office 是一个指针。

始终为流使用引用参数。

注意，下面代码中 `process_name` 函数的 `in_file` 参数变量是一个引用参数。读取或写入会修改流变量。流变量会监视到目前为止已读取或写入了多少个字符。任何读取或写入操作都会改变该数据。因此，必须始终将流参数变量设为引用参数。

完整程序如下所示。如你所见，从文件读取与从键盘输入读取一样简单。

看一下程序输出。值得注意的是，仅 69 个男孩名字和 153 个女孩名字就占了所有出生人口的一半。对于那些从事个性化小饰品生产的人来说，这是个好消息。习题 P8.10 要求你研究这种分布多年来是如何变化的。

## ch08/babynames.cpp

```cpp
#include <iostream>
#include <fstream>
#include <string>

using namespace std;

/**
   Reads name information, prints the name if total >= 0, and adjusts the total.
   @param in_file the input stream
   @param total the total percentage that should still be processed
*/
void process_name(ifstream& in_file, double& total)
{
   string name;
   int count;
   double percent;
   in_file >> name >> count >> percent;

   if (in_file.fail()) { return; } // Check for failure after each input
   if (total > 0) { cout << name << " "; }
   total = total - percent;
}

int main()
{
   ifstream in_file;
   in_file.open("babynames.txt");
   if (in_file.fail()) { return 0; } // Check for failure after opening

   double boy_total = 50;
   double girl_total = 50;

   while (boy_total > 0 || girl_total > 0)
   {
      int rank;
      in_file >> rank;
      if (in_file.fail()) { return 0; }

      cout << rank << " ";

      process_name(in_file, boy_total);
      process_name(in_file, girl_total);
44        cout << endl;
45    }
46
47    return 0;
48 }
```

## 程序运行结果

```
1 Michael Jessica
2 Christopher Ashley
3 Matthew Emily
4 Joshua Sarah
5 Jacob Samantha
6 Nicholas Amanda
7 Andrew Brittany
8 Daniel Elizabeth
9 Tyler Taylor
10 Joseph Megan
...
68 Dustin Gabrielle
69 Noah Katie
70 Caitlin
71 Lindsey
...
150 Hayley
151 Rebekah
152 Jocelyn
153 Cassidy
```

![](img/23fb3582e93ebc95909e1de029c3d388_384_0.png)

- 1. 如果调用 in_file.open("") 会发生什么？
- 2. 以下代码有什么问题？
  ```
  ifstream out_file;
  out_file.open("output.txt");
  out_file << "Hello, World!" << endl;
  ```
- 3. 以下函数有什么问题？
  ```
  double sum(ifstream in)
  {
      double total = 0;
      double input;
      while (in >> input) { total = total + input; }
      return total;
  }
  ```
- 4. 如何修改 babynames.cpp 程序，以便得到占总人口 10% 的最常见名字？
- 5. 如何修改 babynames.cpp 程序，使程序输出保存到文件 00 中？

**练习一下** 现在可以尝试本章末尾的这些习题：R8.3、R8.6、P8.1。

