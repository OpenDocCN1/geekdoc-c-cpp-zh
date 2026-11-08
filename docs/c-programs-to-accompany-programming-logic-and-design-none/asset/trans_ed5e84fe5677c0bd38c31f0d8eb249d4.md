

![](img/08ab7b9c5b7606ff5c1616ca55d8b41c_166_0.png)

图8-4 快餐店报告

为本实验提供的学生文件包含必要的变量声明以及输入和输出语句。你需要实现能够识别何时应发生控制中断的代码。你还需要完成控制中断函数。确保累加每日总计和一周所有天的总合计。代码中的注释会告诉你应在何处编写代码。你可以将本章中的 Bookstore 程序作为这个新程序的指南。

- 1. 使用记事本或你选择的文本编辑器打开名为 `HoursWorked.cpp` 的源代码文件。
- 2. 研究预编写的代码，以了解已经完成了哪些工作。
- 3. 在 `main` 函数中编写控制中断代码。
- 4. 编写 `dayChange` 控制中断函数。
- 5. 将此源代码文件保存到你选择的目录中，然后使该目录成为你的工作目录。
- 6. 编译源代码文件 `HoursWorked.cpp`。
- 7. 执行该程序。

使用以下输入值执行此程序：

- 星期一 – 3小时（员工1）
- 星期二 – 4小时（员工1）
- 星期三 – 5小时（员工1）
- 星期四 – 5小时（员工1）
- 星期五 – 3小时（员工1），4小时（员工2）
- 星期六 – 7小时（员工1），8小时（员工2）
- 星期日 – 0小时

程序结果应包括：

- 星期一总共工作3小时。
- 星期二总共工作4小时。
- 星期三总共工作5小时。
- 星期四总共工作5小时。
- 星期五总共工作7小时。
- 星期六总共工作15小时。
- 星期日总共工作0小时。
- 本周工作总合计为39小时。

## 多级控制中断程序

在*《编程逻辑与设计（第五版）》*第8章中，你学习了如何实现多级控制中断程序。在继续学习本章之前，请确保你理解这些内容。

多级控制中断程序会针对多个条件执行特殊处理。在本节中，你将学习 Bookstore 程序的一个修改版本，它使用了多级控制中断。在这个版本中，程序生成一份报告，打印每个城市和每个州售出书籍的摘要。要生成此类摘要报告，当城市名称发生变化时必须发生一次控制中断。当州名称发生变化时必须发生第二次控制中断。

你已了解到，对于单级控制中断程序，输入必须根据预定的控制中断变量进行排序；同样，对于多级控制中断程序，输入必须按多个控制中断变量进行排序。在这种情况下，输入必须按州内的城市排序。

图8-5包含在*《编程逻辑与设计（第五版）》*第8章中开发的修改版 Bookstore 程序的伪代码，图8-6包含该设计的 C++ 代码。

```text
start
    string title
    num price
    string HEADING = "BOOK LIST"
    string FOOTER = "Total number of book titles "
    num GRAND = 2
    num STATE = 1
    num CITY = 0
    num total[3] = 0, 0, 0
    string prev[2]

    print HEADING
    get title, price, city, state
    prev[STATE] = state
    prev[CITY] = city
    while not eof
        if state not = prev[STATE] then
            stateBreak(total, prev, state, city)
        else
            if city not = prev[CITY] then
                cityBreak(total, prev, city)
            endif
        endif
        total[CITY] = total[CITY] + 1
        get title, price, city, state
    endwhile
    stateBreak(total, prev, state, city)
    print FOOTER, total[GRAND]
stop
void cityBreak(num total[], num prev[], string city)
    num GRAND = 2
    num STATE = 1
    num CITY = 0
    print prev[CITY], total[CITY]
    total[STATE] = total[STATE] + total[CITY]
    total[CITY] = 0
    prev[CITY] = city
return
void stateBreak(num total[], num prev[], string state, string city)
    num GRAND = 2
    num STATE = 1
    num CITY = 0
    string EXPLANATION = "Total for "
    cityBreak(total, prev, city)
    print EXPLANATION, prev[STATE], total[STATE]
    total[GRAND] = total[GRAND] + total[STATE]
    total[STATE] = 0
    prev[STATE] = state
return
```

**图8-5** 修改版 Bookstore 程序伪代码

```cpp
1    // Bookstore2.cpp - This program creates a report that lists
2    // all of the books sold in each city and each state.
3    // Input:  Interactive
4    // Output: Report
5    #include <iostream>
6    #include <string>
7    using namespace std;
8    void cityBreak(int total[], string prev[], string city);
9    void stateBreak(int total[], string prev[], string state, string city);
10   int main()
11   {
12       double price;
13       string title, city = "", state = "";
14       const string HEADING = "Book List";
15       const string FOOTER = "Total number of book titles ";
16       const string SENTINEL = "done";
17       const int GRAND = 2;
18       const int STATE = 1;
19       const int CITY = 0;
20       int total[] = {0, 0, 0};
21       string prev[2];
22       bool notDone = true;
23
24       cout << "\t\t\t\t\t" << HEADING << endl;
25       cout << "Enter a book title or done to quit: ";
26       cin >> title;
27       if(title == SENTINEL)
28       {
29           notDone = false;
30       }
31       else
32       {
33           cout << "Enter the book's price: ";
34           cin >> price;
35           cout << "Enter the city: ";
36           cin >> city;
37           cout << "Enter the state: ";
38           cin >> state;
39           prev[STATE] = state;
40           prev[CITY] = city;
41       }
42       while(notDone == true)
43       {
44           if(state != prev[STATE])
45               stateBreak(total, prev, state, city);
46           else if(city != prev[CITY])
47               cityBreak(total, prev, city);
48           total[CITY]++;
49           cout << "Enter a book title or done to quit: ";
50           cin >> title;
51           if(title == SENTINEL)
52           {
53               notDone = false;
54           }
55           else
56           {
57               cout << "Enter the book's price: ";
58               cin >> price;
59               cout << "Enter the city: ";
60               cin >> city;
61               cout << "Enter the state: ";
62               cin >> state;
63           }
64       }
65       stateBreak(total, prev, state, city);
66       cout << "\t\t\t\t\t" << FOOTER << total[GRAND] << endl;
67       return 0;
68   } // End of main function

70   void cityBreak(int total[], string prev[], string city)
71   {
72       const int GRAND = 2;
73       const int STATE = 1;
74       const int CITY = 0;

76       cout << "\t\t\t\t" << prev[CITY] << " " << total[CITY] << endl;
77       total[STATE] += total[CITY];
78       total[CITY] = 0;
79       prev[CITY] = city;
80   } // End of cityBreak function

81   void stateBreak(int total[], string prev[], string state, string city)
82   {
83       const int GRAND = 2;
84       const int STATE = 1;
85       const int CITY = 0;
86       const string EXPLANATION = "Total for ";

88       cityBreak(total, prev, city);
89       cout << "\t\t\t\t\t" << EXPLANATION << prev[STATE]
90            << " " << total[STATE] << endl;
91       total[GRAND] += total[STATE];
92       total[STATE] = 0;
93       prev[STATE] = state;
94   } // End of stateBreak function
```

**图8-6** 用 C++ 编写的修改版 Bookstore 程序

如图8-6所示，C++ 程序以注释（第1行到第4行）开始，这些注释描述了：1）程序做什么；以及2）程序的输入和输出。接下来是第5行和第6行的两个预处理器指令、第7行的 `using namespace std;` 语句，以及第8行和第9行的 `cityBreak` 和 `stateBreak` 函数声明。注意，`cityBreak` 函数不返回任何内容（`void`），并接受三个参数：一个 `int` 数组、一个 `string` 数组和一个 `string`。另外，注意 `stateBreak` 函数不返回任何内容（`void`），并接受四个参数：一个 `int` 数组、一个 `string` 数组和两个 `string`。开始 `main` 函数的 C++ 代码位于第10行。

在 `main` 函数内的第12行到第24行中，变量和常量被声明并在适当时初始化，同时打印报告标题。注意，所声明的变量中有两个是数组：一个名为 `total` 的 `int` 数组和一个名为 `prev` 的 `string` 数组。`total` 数组用于存储城市总计、州总计和总合计，而 `prev` 数组用于存储前一个城市和州的名称。常量 `CITY`、`STATE` 和 `GRAND` 用作索引值，以访问 `total` 数组的元素，常量 `CITY` 和 `STATE` 用于访问存储在 `prev` 数组中的前一个城市和前一个州的名称。名为 `city` 和 `state` 的变量用作控制中断变量，以处理此程序中的两个控制中断。

使用与原始 Bookstore 程序相同的技术，预读（第25行到第38行）获取第一条输入记录。在此程序版本中，一条输入记录现在由单本书的书名、价格、城市和州组成。如果用户尚未完成记录输入，程序还会在第39行和第40行将 `state` 的值赋给 `prev[STATE]`，并将 `city` 的值赋给 `prev[CITY]`。

只要 `bool` 变量 `notDone` 的值为 true，第42行的 `while` 循环就会继续执行。在 `while` 循环体内，`if` 语句测试第一个控制中断变量 `state`（第44行），以确定当前正在处理的记录是否与前一条记录具有相同的州。如果不同，我们就知道遇到了一个新的州。在这种情况下，程序调用 `stateBreak` 函数（第45行），它是……之一

