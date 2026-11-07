
## 问题分析与算法设计

**输出** 最高 GPA 以及所有与该最高 GPA 关联的姓名。例如，对于上述数据，最高 GPA 是 3.8，而具有该 GPA 的学生是 Ron 和 Mickey。

我们读取第一个 GPA 和学生姓名。由于该数据是读取的第一个条目，因此它是到目前为止的最高 GPA。接下来，我们读取第二个 GPA 和学生姓名。然后，我们将这个（第二个）GPA 与到目前为止的最高 GPA 进行比较。会出现三种情况：

- 1. 新的 GPA 大于到目前为止的最高 GPA。在这种情况下，我们：
  - a. 更新到目前为止的最高 GPA 的值。
  - b. 初始化栈——即从栈中移除学生姓名。
  - c. 将到目前为止具有最高 GPA 的学生姓名保存到栈中。
- 2. 新的 GPA 等于到目前为止的最高 GPA。在这种情况下，我们将新学生的姓名添加到栈中。
- 3. 新的 GPA 小于到目前为止的最高 GPA。在这种情况下，我们丢弃具有该成绩的学生姓名。

然后，我们读取下一个 GPA 和学生姓名，并重复步骤 1 到 3。我们继续此过程，直到到达输入文件的末尾。

从上述讨论可以清楚地看出，我们需要以下变量：

```cpp
double GPA;             //variable to hold the current GPA
double highestGPA;      //variable to hold the highest GPA
string name;            //variable to hold the name of the student
stackType<string> stack(100); //object to implement the stack
```

前面的讨论可转化为以下算法：

- 1. 声明变量并初始化 stack。
- 2. 打开输入文件。
- 3. 如果输入文件不存在，则退出程序。
- 4. 将浮点数的输出设置为带小数点和尾随零的固定小数格式。同时，将精度设置为两位小数。
- 5. 读取 GPA 和学生姓名。
- 6. `highestGPA = GPA;`
- 7. `while`（未到文件末尾）
  {
  7.1. `if`（GPA > highestGPA）
  {
  7.1.1. `clearStack(stack);`
  7.1.2. `push(stack, student name);`
  7.1.3. `highestGPA = GPA;`
  }
  7.2. `else`
  `if`（GPA 等于 highestGPA）
  `push(stack, student name);`
  7.3. 读取 GPA 和学生姓名；
  }
- 8. 输出最高 GPA。
- 9. 输出具有最高 GPA 的学生姓名。

## 程序清单

```cpp
/************************************************************
// Author: D.S. Malik
//
// This program uses the class myStack to determine the
// highest GPA from a list of students with their GPA.
// The program also outputs the names of the students
// who received the highest GPA.
************************************************************/

#include <iostream>
#include <iomanip>
#include <fstream>
#include <string>

#include "myStack.h"

using namespace std;

int main()
{
        //Step 1
        double GPA;
        double highestGPA;
        string name;

        stackType<string> stack(100);

        ifstream infile;

        infile.open("HighestGPAData.txt");                 //Step 2

        if (!infile)                                      //Step 3
        {
            cout << "The input file does not exist. "
                 << "Program terminates!"
                 << endl;
            return 1;
        }

        cout << fixed << showpoint;                       //Step 4
        cout << setprecision(2);                          //Step 4

        infile >> GPA >> name;                            //Step 5

        highestGPA = GPA;                                 //Step 6

        while (infile)                                    //Step 7
        {
            if (GPA > highestGPA)                         //Step 7.1
            {
                stack.initializeStack();                 //Step 7.1.1

                if (!stack.isFullStack())                //Step 7.1.2
                    stack.push(name);

                highestGPA = GPA;                         //Step 7.1.3
            }
            else if (GPA == highestGPA)                   //Step 7.2
                if (!stack.isFullStack())
                    stack.push(name);
                else
                {
                    cout << "Stack overflows. "
                         << "Program terminates!"
                         << endl;
                    return 1; //exit program
                }

            infile >> GPA >> name;                        //Step 7.3
        }

        cout << "Highest GPA = " << highestGPA
             << endl;                                     //Step 8
        cout << "The students holding the "
             << "highest GPA are:" << endl;

        while (!stack.isEmptyStack())                     //Step 9
        {
            cout << stack.top() << endl;
            stack.pop();
        }

        cout << endl;

        return 0;
}
```

示例运行：

```text
Input File (HighestGPAData.txt)

3.4 Randy
3.2 Kathy
2.5 Colt
3.4 Tom
3.8 Ron
3.8 Mickey
3.6 Peter
3.5 Donald
3.8 Cindy
3.7 Dome
3.9 Andy
3.8 Fox
3.9 Minnie
2.7 Gilda
3.9 Vinay
3.4 Danny

Output

Highest GPA = 3.90
The students holding the highest GPA are:
Vinay
Minnie
Andy
```

请注意，具有最高 GPA 的学生姓名是相对于它们在输入中出现的顺序按相反顺序输出的，这是因为栈顶元素是最后添加到栈中的元素。

## 栈的链式实现

由于数组大小是固定的，在栈的数组（线性）表示中，只能将固定数量的元素压入栈。如果在程序中要压入的元素数量超过数组大小，程序可能因错误而终止。我们必须克服这些问题。

我们已经看到，通过使用指针变量，可以动态分配和释放内存；通过使用链表，可以动态组织数据（例如有序表）。接下来，我们将使用这些概念来动态实现栈。

回想一下，在栈的线性表示中，`stackTop` 的值表示栈中元素的数量，而 `stackTop − 1` 的值指向栈顶项。借助 `stackTop`，我们可以做几件事：找到栈顶元素、检查栈是否为空，等等。

与线性表示类似，在链式表示中，`stackTop` 用于定位栈顶元素。然而，有一个细微差别。在前一种情况下，`stackTop` 给出数组的索引。在后一种情况下，`stackTop` 给出栈顶元素的地址（内存位置）。

以下类实现了抽象类 `stackADT` 的函数：

```cpp
//Definition of the node
template <class Type>
struct nodeType
{
        Type info;
        nodeType<Type> *link;
};

template <class Type>
class linkedStackType: public stackADT<Type>
{
public:
        const linkedStackType<Type>& operator=
                                      (const linkedStackType<Type>&);
                //Overload the assignment operator.

        bool isEmptyStack() const;
                //Function to determine whether the stack is empty.
                //Postcondition: Returns true if the stack is empty;
                //              otherwise returns false.

        bool isFullStack() const;
                //Function to determine whether the stack is full.
                //Postcondition: Returns false.

        void initializeStack();
                //Function to initialize the stack to an empty state.
                //Postcondition: The stack elements are removed.
                //              stackTop = nullptr;

        void push(const Type& newItem);
                //Function to add newItem to the stack.
                //Precondition: The stack exists and is not full.
                //Postcondition: The stack is changed and newItem
                //              is added to the top of the stack.
```

![](img/d0be7fc6d804b63484835c6c8bc67a07_1239_0.png)

![](img/d0be7fc6d804b63484835c6c8bc67a07_1241_0.png)

图 17-12 空链栈与非空链栈

在图 17-12(b) 中，栈顶元素是 C；也就是说，最后压入栈的元素是 C。

接下来，我们讨论实现链栈操作的相关函数定义。

### 默认构造函数

我们考虑的第一个操作是默认构造函数。默认构造函数在声明栈对象时将栈初始化为空状态。因此，该函数将 stackTop 设置为 nullptr。该函数的定义如下：

```cpp
template <class Type>
linkedStackType<Type>::linkedStackType()
{
    stackTop = nullptr;
}
```

### 空栈与满栈

操作 isEmptyStack 和 isFullStack 非常直接。如果 stackTop 为 nullptr，则栈为空。此外，由于栈元素的内存是动态分配和释放的，栈永远不会满。（只有当我们耗尽内存时，栈才会满。）因此，函数 isFullStack 始终返回值 false。实现这些操作的函数定义如下：

```cpp
template <class Type>
bool linkedStackType<Type>::isEmptyStack() const

