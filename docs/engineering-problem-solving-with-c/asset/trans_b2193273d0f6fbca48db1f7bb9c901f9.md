
我们的流程图提供了足够的细节来开发问题的解决方案。

```
/*-------------------------------------------*/
/* Program chapter7_13 */
/* This program runs a simulation to calculate */
/* the probability of drawing 2 red cards, each */
/* with a face value less than 10, from a */
/* shuffled deck of 52 cards. The results are */
/* then compared to analytical results. */
#include<iostream> //Required for cout.
#include "Card.h" //Required for Card.
#include "CardDeck.h" //Required for CardDeck.
using namespace std;

int main()
{
 //Declare objects.
 CardDeck theDeck;
 Card card1, card2;
 double pE, eventCounter = 0;
 int n;
 bool isRed;

 cout << "Enter the analytical result ";
 cin >> pE;
 cout << "Enter number of experiments to run ";
 cin >> n;

 for(int i=0; i<n; ++i)
 {
 theDeck.shuffleDeck();
 card1 = theDeck.draw();
 card2 = theDeck.draw();

 //Check if the event occurred.
 if ( (card1.getSuit() == 'H' || card1.getSuit() == 'D')
 && (card2.getSuit() == 'H' || card2.getSuit() == 'D'))
 {
 isRed = true;
 }
 else
 {
 isRed = false;
 }
 if( isRed && (card1.getRank() < 10 && card2.getRank() < 10) )
 {
 ++eventCounter;
 cout << "Event " << eventCounter << endl;
 card1.displayCard(cout);
 cout << " ";
 card2.displayCard(cout);
 cout << endl;
 }//End if
 }//End for
 cout << "Analytical results: " << pE << endl
 << "Simulated results: " << eventCounter << '/' << n
 << " = " << eventCounter/n << endl;
 return 0;
 }
/*--------------------------------------------------------------*/
```

## 5. 测试

我们将使用少量实验对解决方案进行两次测试，以便查看结果并确保我们正确计数了事件。

### 模拟 1

```
Enter the analytical result 0.0904977
Enter number of experiments to run 97
Event 1
4 of Diamonds 8 of Diamonds
Event 2
5 of Diamonds 2 of Hearts
Event 3
3 of Hearts 2 of Hearts
Event 4
4 of Diamonds 7 of Hearts
Event 5
7 of Hearts 8 of Hearts
Event 6
5 of Hearts 2 of Diamonds
Event 7
8 of Diamonds 4 of Hearts
Event 8
9 of Hearts 8 of Diamonds
Event 9
4 of Diamonds 9 of Hearts
Analytical results: 0.0904977
Simulated results: 9/97 = 0.0927835
```

### 模拟 2

```
Enter the analytical result 0.0904977
Enter number of experiments to run 97
Event 1
6 of Hearts 4 of Hearts
Event 2
8 of Hearts 5 of Hearts
Event 3
8 of Diamonds 2 of Hearts
Event 4
6 of Hearts 5 of Diamonds
Event 5
3 of Diamonds 8 of Hearts
Event 6
4 of Diamonds 3 of Hearts
Event 7
3 of Hearts 4 of Hearts
Analytical results: 0.0904977
Simulated results: 7/97 = 0.0721649
```

为了对较大的 n 值运行模拟，我们将注释掉打印语句以加快执行速度。

### 模拟 3

```
Enter the analytical result 0.0904977
Enter number of experiments to run 101371
Analytical results: 0.0904977
Simulated results: 9171/101371 = 0.0904697
```

### 模拟 4

```
Enter the analytical result 0.0904977
Enter number of experiments to run 101371
Analytical results: 0.0904977
Simulated results: 9101/101371 = 0.0897791
```

### 模拟 5

```
Enter the analytical result 0.0904977
Enter number of experiments to run 1111111
Analytical results: 0.0904977
Simulated results: 100368/1111111 = 0.0903312
```

### 修改 7.11

以下练习需要修改程序 chapter7_13，但无需修改 Card 或 CardDeck。

- 1. 修改程序 chapter7_13 以计算抽取 2 张牌面卡片的概率。
- 2. 修改程序 chapter7_13 以计算抽取 5 张黑色卡片的概率。
- 3. 修改程序 chapter7_13 以计算抽取 4 张 A 牌的概率。

## 总结

### 关键术语

- 字母数字字符
- 空字符
- 字符串类
- 数组
- 偏移量
- 下标
- 二分查找
- 一维数组
- 统一建模语言 (UML)
- 事件空间
- 样本空间
- 方差
- C 风格字符串
- 选择排序算法
- 向量类
- 字符串
- 顺序查找
- 空白字符
- 大小
- 排序
- 零交叉
- 均值
- 标准差
- 中位数
- 统计量

### C++ 语句摘要

```
Include C-style string header file
#include<cstring>
Include string class header file
#include<string>
Include vector class header file
#include<vector>
Range-based for Statement
for(declaration:range)
statement;
Array and vector declaration:
int a[5], b[]={2, 3, -1};
char vowels[]={'a', 'e', 'i', 'o', 'u'};
string words[100];
vector<double> time;
```

### 注意事项

- 1. 标识符 i 常用作一维数组的下标。
- 2. 使用符号常量来声明数组的大小，以便于修改。

### 注意事项

- 1. 仅在需要将所有数据保留在内存中时才使用数组。
- 2. 如果在 C 风格字符串末尾打印出意外字符，则字符串中可能缺少空字符。
- 3. 引用数组元素时，小心不要超过最大偏移量值。
- 4. 数组必须声明为大于或等于要存储在其中的最大值数量的大小。
- 5. 因为函数中的数组引用始终是按引用传递，请小心不要意外更改函数中数组的值。

## 习题

### 考试练习！

#### 判断题

请指出以下陈述是正确 (T) 还是错误 (F)。

- 1. 如果初始化序列短于数组，则其余值初始化为零。T F
- 2. 如果在没有大小但带有初始化序列的情况下定义数组，则数组大小是任意的。T F
- 3. 当下标或偏移量的值大于数组的最大有效偏移量时，将始终导致执行错误。T F
- 4. 如果不带偏移量指定数组标识符，则将打印数组的所有值。T F
- 5. 在 ASCII 中，字符串 "Smith" 小于字符串 "Johnson"。T F

#### 选择题

- 6. 数组是
- (a) 一组具有共同对象名且数据类型相同的值。
- (b) 存储在相邻内存位置的不同数据类型元素的集合。
- (c) 包含多个相同数据类型值的对象。
- (d) 内存中存储多个相同数据类型值的位置。
- 7. 数组中的单个元素通过指定来寻址
- (a) 数组名和元素的偏移量。
- (b) 数组名。
- (c) 数组中元素的偏移量，后跟数组名。
- (d) 数组中元素的偏移量。
- 8. 偏移量标识数组中特定元素的 __________。
- (a) 位置
- (b) 值
- (c) 范围
- (d) 名称

#### 内存快照问题

执行以下每组语句后，给出相应的内存快照。使用 ? 表示未初始化的数组元素。

```
9. int t[5];
...
t[0] = 5;
for (int k=0; k<4; k++)
t[k+1] = t[k] + 3;
10. char s[] = "Hello", t[] = {'a', 'e', 'i', 'o', 'u'}, name[10];
strcpy(name, "Sue");
```

### 程序输出

问题 11-13 参照以下语句：

```
string strng1 = "k", strng2 = "265", strng3 = "xyz";
```

- 11. 以下语句的输出是什么？

```
cout << strng1.size() << endl;
```

- 12. 以下语句的输出是什么？

```
strng1 = strng2;
cout << strng1 << endl;
```

- 13. 以下语句的输出是什么？

```
strng1 += strng2;
cout << strng1 << endl;
```

问题 14-16 参照以下语句：

```
double x[] = { 2, 4, 6, 8, 10, 12 }, sum = 0;
```

- 14. 以下语句的输出是什么？

```
for (double k : x)
{
   cout << k << " ";
}
```

- 15. 以下语句的输出是什么？

```
for (double k : x)
   sum += k;
cout << sum << endl;
```

- 16. 以下语句的输出是什么？

```
for (double k : x)
{
   cout << k << " ";
   --k;
   cout << k << endl;
}
```

## 编程练习

### 线性插值。

以下问题引用存储在文件 tunnel.dat 中的风洞测试数据。文件包含一组数据，每行包含飞行路径角（以度为单位）及其对应的升力系数。飞行路径角将按升序排列。

- 17. 编写一个程序，读取风洞测试数据，然后允许用户输入飞行路径角。如果角度在数据集范围内，程序应使用线性插值计算相应的升力系数。（您可能需要参考第 5.6 节中的线性建模部分。）

