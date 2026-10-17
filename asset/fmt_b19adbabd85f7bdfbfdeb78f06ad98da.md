
# 程序 18-9

```cpp
// // 此程序演示了如何使用一个栈来
// // 实现非递归快速排序。
#include <stack>
#include <iostream>
#include <fstream>
#include <algorithm> // 需要 swap 函数
using namespace std;

// // 函数原型
void qsort(int a [], int size);
void outputArray(int a [], int size);
void partition(int a [], int start, int end);

// // Range 类用于表示数组中
// // 待排序的段
class Range
{
    // // 将 qsort 设置为友元
    friend void qsort(int a [], int start, int end);
    int start;
    int end;
public:
    Range(int s, int e)
    {
        start = s;
        end = e;
    }
};

const int MAX = 100;
int main()
{
    ifstream inputFile;
    string filename = "sort.dat";
    int array[MAX];
    int size;
    inputFile.open(filename.data());
    if (!inputFile)
    {
        cout << "文件 " << filename << "无法被"
             << "打开...";
        exit(1);
    }

// // 读取文件以及文件中的项数
// // 注意不要超出数组范围
size = 0;
while (inputFile >> array[size])
{
    size++;
    if (size == MAX)
        break;
}
```

（程序继续）

## 18.7 重点关注问题解决与程序设计：消除递归

```cpp
程序 18-9（继续）
// 打印输入数组
cout << "原始数组为：" << endl;
outputArray(array, size);

// 执行排序并输出结果
qSort(array, size);
cout << "排序后的数组为：" << endl;
outputArray(array, size);
return 0;
}
***************************************************
// qSort 对给定大小的数组 [] 
// 执行非递归的快速排序
***************************************************
void qSort(int arr [], int size) {
    // qStack 处理数组中尚未排序的段
    stack<Range> qStack;
    int pivot, start, end;
    qStack.push(Range(0, size-1));
    // 只要栈中还有待排序的范围
    // 就将其从栈中取出，进行分区，然后
    // 将生成的较小范围放入栈中
    while (!qStack.empty()) {
        Range currentRange = qStack.top();
        qStack.pop();
        start = currentRange.start;
        end = currentRange.end;
        if (start < end) {
            pivot = partition(arr, start, end);
            // 存储生成的较小范围以便
            // 处理
            qStack.push(Range(start, pivot-1));
            qStack.push(Range(pivot + 1, end));
        }
    }
// partition 重新排列从 start 到 end 的数组项
// 所有大于等于 pivot 的值都在 pivot 右侧
// 所有小于 pivot 的值都在 pivot 左侧。
```

（程序继续）

## 第18章 栈与队列

```cpp
程序 18-9（继续）
int partition(int arr[], int start, int end)
{
  // pivot 元素被用作分区子范围的起始元素
  int pivotValue = arr[start];
  int pivotPosition = start;

  // 重新排列数组的其余元素
  for (int pos = start + 1; pos <= end; pos++)
  {
    if (arr[pos] < pivotValue)
    {
      // scan 是“当前”项。
      // 将当前项与 pivot 元素
      // 右项交换
      swap(arr[pivotPosition + 1], arr[pos]);
      // 将当前项与 pivot 元素交换
      swap(arr[pivotPosition], arr[pivotPosition + 1]);
      // 调整 pivot 位置
      pivotPosition++;
    }
  }
  return pivotPosition;
}

/**
 * 输出数组元素。
 */
void outputArray(const int arr [], int size)
{
  for (int k = 0; k < size; k++)
    cout << arr[k] << " ";
  cout << endl;
}
```

程序输出

原始数组为：

34 45 78 32 90

排序后的数组为：

45 32 34 78 90

> 注意：应谨慎使用友元（`friend`）概念，因为它绕过了通过类私有成员提供的保护。在我们的案例中，`Range`类的`start`和`end`成员并未被`qsort`函数修改。

## 18.8 整合一切：将后缀表达式转换为中缀表达式

栈可以用于求值后缀表达式。让我们看看如何实现。我们限制为包含数字和二元运算符（`+`, `*`, `/`）的后缀表达式。回顾第14章，后缀表达式要么是一个数字，要么是两个后缀表达式后跟一个运算符。单个数字的求值很简单：只需返回数字。对于简单的情况，必须按顺序处理两个后缀表达式并保存它们的值。遇到运算符时，取出保存的值并应用运算符。

为了查看该方法如何工作，考虑示例

`2 - 5`

因为 `2` 和 `5` 是单个数字表达式，我们将它们的值保存备用。当我们遇到减运算符时，取出两个保存的值并应用运算符作为整个表达式的值。通常，任何后缀表达式都可以通过从左到右读取来求值。当遇到值时，它被推入栈中等待后续阶段的应用。每当遇到运算符时，栈中弹出两个操作数并产生值。当读取完输入表达式后，过程结束。此时，栈中应该只有一个值。这个值就是后缀表达式的值。

这种思想可以将后缀表达式转换为中缀。同样，我们从左到右读取输入。这次我们使用字符串栈而不是整数。读取的任何数字必须是一个操作数：将其转换为字符串并推入栈。如果遇到运算符，弹出栈顶的两个字符串，并在它们之间放置运算符，然后在生成的字符串周围加上括号，例如，上面的输入会导致如下入栈序列：

`"2"`

`"5"`

`"(2 - 5)"`

这些思想用于程序 `18-10`。

## 程序 18-10

```cpp
// 此程序将后缀表达式转换为中缀。
#include <stdio.h>
#include <cstring>
#include <string>
#include <iostream>
```

（程序继续）

### 程序 18-10（继续）

```cpp
#include <sstream>
#include <stack>

using namespace std;

string postfixExpr(istream& inputStream);

int main() {
    string input;
    cout << "输入要转换为中缀的后缀表达式," << endl;
    cout << "或输入空行退出程序：" << endl;
    getline(cin, input);
    while (input.size() != 0) {
        // 将字符串转换为字符串流
        stringstream inputExpr(input);
        cout << "中缀等价于" << endl;
        cout << postfixExpr(inputExpr) << endl;
        cout << "输入另一个后缀表达式：" << endl;
        getline(cin, input);
    }
    return 0;
}

***************************************************
* 读取后缀表达式 p 的 istream
* 并返回表示 p 中缀的字符串
***************************************************
string postfixExpr(istream& in) {
    // 存储计算中的中间值
    stack<string> infixStack;
    // 用于读取表达式中的字符
    char ch;
    int number;
    // 用于从栈中移除中缀表达式
    string lExpr, rExpr;
    ch = in.peek();
    while (ch != EOF) {
        // 如果是空白字符，跳过它并
        // 继续循环的下一次迭代
        if (isspace(ch)) {
            ch = in.get();
            ch = in.peek();
            continue; // 回到循环顶部
        }
        
        // 非空格字符是输入流中的下一个
        // 如果下一个字符是数字，读取它，
        // 转换为字符串，将字符串推入中缀栈
        if (isdigit(ch)) {
            in >> number;
            // 用于将数字转换为字符串
            string numberStr;
            // 使用流将数字转换为字符串
            numberStr = to_string(number);
            // 将表达式推入栈
            infixStack.push(numberStr.c_str());
            ch = in.peek();
            continue;
        }
        // 如果遇到运算符运算符
        // 弹出栈中存储的两个中缀表达式
        // 在两个中缀表达式之间放置运算符，
        //并将结果推入栈
        rExpr = infixStack.top();
        infixStack.pop();
        lExpr = infixStack.top();
        infixStack.pop();
        if (ch == '-' || ch == '*' || ch == '/') {
            infixStack.push("(" + lExpr + " " + ch + " " + rExpr + ")");
        } else {
            cout << "输入表达式错误" << endl;
            exit(1);
        }
        ch = in.get(); // 实际读取运算符字符
        ch = in.peek(); // 准备下一次迭代
    }
    return infixStack.top();
}
```
