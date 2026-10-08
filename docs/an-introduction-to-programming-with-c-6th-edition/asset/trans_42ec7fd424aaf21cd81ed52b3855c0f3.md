

# 主函数
IPO 图表信息
C++ 指令

输入
菜单选择
int choice = 0;

处理
无

输出
无

```
Algorithm
repeat
  call the getChoice function
  to display the menu and get the
  menu choice
  if (choice is 1)
    call the addRecords function
  else
    if (choice is 2)
      call the displayTotal()
  end if
until (menu choice is not 3)

choice = getChoice();
if (choice == 1) {
  addRecords();
} else {
  if (choice == 2) {
    displayTotal();
  }
} // // end if
```

# getChoice 函数
IPO 图表信息
C++ 指令

输入
无
int menuChoice = 0;

处理
无

输出
菜单选择

- Algorithm
1. 显示菜单
cout << endl << "Menu Options" << endl;
cout << "1 Add Records" << endl;
cout << "2 Display Total Sales" << endl;
cout << "3 Exit the program" << endl;
2. 获取菜单选择
cout << "Choice (1, 2, or 3)?" ;
cin >> menuChoice;
cin.ignore(100, '\n');
cout << endl;
3. 返回 menuChoice
return menuChoice;

图 14-17 主函数和 getChoice 函数的 IPO 图表信息和 C++ 指令

| addRecords 函数 | C++ 指令 |
| --- | --- |
| 输入 | |
| 销售员姓名 | string name = ""; |
| 额 | int sales = 0; |
| 处理 | |
| 无 | |
| 输出 | |
| sales.txt 文件（顺序访问） | ofstream outFile; |
| 算法 | |
| 1. 以追加模式打开 sales.txt 文件 | outFile.open("sales.txt", ios::app); |
| 2. 如果（sales.txt 文件已成功打开） | if (outFile.is_open()) { |
| 输入销售员姓名 | cout << "Salesperson's name\n(X to stop):"; |
| getline(cin, name); } |

图 14-18 addRecords 函数的 IPO 图表信息和 C++ 指令（续）

（续）

| repeat while（当销售员姓名不是 "X" 或 "x"） | while (name != "X" && name != "x") |
| --- | --- |
| 输入销售额 | cout << "Sales:"; |
| cin << sales; | |
| cin.ignore(100, '\n'); | |
| 将销售员姓名和销售额写入 sales.txt 文件 | outFile << name << '#' << sales << endl; |
| 获取另一个销售员姓名 | cout << "Salesperson's name (X to stop):"; |
| getline(cin, name); | |
| //end while | |
| outFile.close(); } | |
| 结束 repeat 关闭 sales.txt 文件 | |
| else | |
| 显示“无法打开文件”消息 | cout << "File could not be opened." << endl; |
// //end if | |
| 结束 if | |

图 14-18 addRecords 函数的 IPO 图表和 C++ 指令

最后，14-19 显示了 displayTotal 函数的 IPO 图表和 C++ 指令。它创建了一个输入文件对象并使用该对象通过 open 函数在 if 函数中打开 sales.txt 进行输入。if 子句中的条件决定了 sales.txt 文件是否成功打开。如果条件为假，则 displayTotal 函数显示适当的错误消息并结束函数。相反，如果条件为真，则处理 if 语句中真路径的指令。真路径中的指令从 sales.txt 文件中读取记录，将其赋值给 name 变量并赋值给 sales 变量。真路径中的 while 告诉计算机，只要文件指针不在文件末尾，就重复执行循环体指令。循环体中的第一条语句将销售额加到累加变量变量，该变量命名为 total。循环体中的剩余指令从文件中读取另一条记录。当指针位于 sales.txt 文件的末尾时会发生这种情况，if 语句真路径的最后两条语句关闭 sales.txt 文件，然后在屏幕上显示总销售额。在显示总销售额后，displayTotal 函数结束。

# 第 14 章 顺序访问文件

| displayTotal 函数 | IPO 图表信息 | C++ 指令 |
| --- | --- | --- |
| 输入 | sales.txt（顺序访问） | ifstream inFile; |
| 处理 | 销售员姓名和销售额 | string name = ""; |
| int sales = 0; | | |
| 输出 | 总销售额（累加器） | int total = 0; |
| 算法 | | |
| 1. 以输入模式打开 sales.txt 文件 | inFile.open("sales.txt"); |
| 2. 如果（sales.txt 文件已成功打开） | if (inFile.is_open()) { |
| 从 sales.txt 读取销售员姓名和销售额 | getline(inFile, name); |
| inFile >> sales; | | |
| inFile.ignore(); | | |
| repeat（当指针不在文件末尾时） | while (!inFile.eof()) { |
| 将销售额加到累加变量 | total += sales; |
| 从文件中读取另一条记录 | getline(inFile, name); |
| 当指针位于 sales.txt 文件末尾时 | | |
| if 语句真路径的最后两条语句关闭 sales.txt 文件 | inFile.close(); |
| 然后在屏幕上显示总销售额 | cout << "Total sales: $" << total << endl; |
| } | |
| else | |
| 显示“无法打开文件”消息 | cout << "File could not be opened." << endl; |
// //end if | |
| 结束 if | |

图 14-19 displayTotal 函数的 IPO 图表和 C++ 指令

