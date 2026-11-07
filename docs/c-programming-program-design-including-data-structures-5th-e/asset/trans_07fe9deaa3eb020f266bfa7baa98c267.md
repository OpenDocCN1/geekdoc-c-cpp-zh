
```cpp
while (!dummyStack.isEmptyStack())  //print dummyStack
{
    cout << dummyStack.top() << " ";
    dummyStack.pop();
}
cout << endl;

return 0;
}

void testCopyConstructor(stackType<int> otherStack)
{
    if (!otherStack.isEmptyStack())
        cout << "otherStack is not empty. " << endl
             << "The top element of otherStack: "
             << otherStack.top() << endl;
}
```

### 示例运行：

```
The elements of copyStack: 38 45 23
otherStack is not empty.
The top element of otherStack: 38
The original stack is not empty.
The top element of the original stack: 38
The elements of dummyStack: 38 45 23
```

建议你对这个程序进行一次走查。

## 编程示例：最高 GPA

在这个示例中，我们编写一个 C++ 程序，它读取一个数据文件，该文件由每个学生的 GPA 及其后的学生姓名组成。然后，程序打印最高 GPA 以及所有获得该 GPA 的学生的姓名。程序只扫描输入文件一次。此外，我们假设班级中最多有 100 名学生。

**输入** 程序读取一个输入文件，该文件由每个学生的 GPA 及其后的学生姓名组成。示例数据为：

```
3.5 Bill
3.6 John
2.7 Lisa
3.9 Kathy
3.4 Jason
3.9 David
3.4 Jack
```

### 输出

最高 GPA 以及与最高 GPA 关联的所有姓名。例如，对于上述数据，最高 GPA 是 3.9，具有该 GPA 的学生是 Kathy 和 David。

### 问题分析与算法设计

我们读取第一个 GPA 和学生姓名。由于这个数据是读取的第一项，所以它是目前为止最高的 GPA。接下来，我们读取第二个 GPA 和学生姓名。然后我们将这个（第二个）GPA 与目前为止最高的 GPA 进行比较。会出现三种情况：

- 1. 新的 GPA 大于目前为止最高的 GPA。在这种情况下，我们：
    - a. 更新目前为止最高 GPA 的值。
    - b. 初始化栈——即从栈中移除学生的姓名。
    - c. 将目前为止具有最高 GPA 的学生的姓名保存到栈中。
- 2. 新的 GPA 等于目前为止最高的 GPA。在这种情况下，我们将新学生的姓名添加到栈中。
- 3. 新的 GPA 小于目前为止最高的 GPA。在这种情况下，我们丢弃具有该成绩的学生的姓名。

然后我们读取下一个 GPA 和学生姓名，并重复步骤 1 到 3。我们继续这个过程，直到到达输入文件的末尾。

从上述讨论可以清楚地看出，我们需要以下变量：

```
double GPA;               //variable to hold the current GPA
double highestGPA;        //variable to hold the highest GPA
string name;              //variable to hold the name of the student
stackType<string> stack(100); //object to implement the stack
```

前面的讨论可转化为以下算法：

- 1. 声明变量并初始化栈。
- 2. 打开输入文件。
- 3. 如果输入文件不存在，则退出程序。
- 4. 将浮点数的输出设置为固定的小数格式，带小数点和尾随零。同时，将精度设置为两位小数。
- 5. 读取 GPA 和学生姓名。
- 6. `highestGPA = GPA;`
- 7. `while`（未到文件末尾）
    ```
    {
        7.1. `if` (GPA > highestGPA)
        {
            7.1.1. clearStack(stack);
            7.1.2. push(stack, student name);
            7.1.3. highestGPA = GPA;
        }
        7.2. `else`
            `if` (GPA is equal to highestGPA)
                push(stack, student name);
        7.3. Read GPA and student name;
    }
    ```
- 8. 输出最高 GPA。
- 9. 输出具有最高 GPA 的学生的姓名。

### 程序清单

```cpp
/******************************************************
// Author: D.S. Malik
//
// This program uses the class myStack to determine the
// highest GPA from a list of students with their GPA.
// The program also outputs the names of the students
// who received the highest GPA.
//******************************************************

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

if (!infile)                                         //Step 3
{
    cout << "The input file does not "
         << "exist. Program terminates!"
         << endl;
    return 1;
}

cout << fixed << showpoint;                          //Step 4
cout << setprecision(2);                             //Step 4

infile >> GPA >> name;                               //Step 5

highestGPA = GPA;                                    //Step 6

while (infile)                                       //Step 7
{
    if (GPA > highestGPA)                            //Step 7.1
    {
        stack.initializeStack();                    //Step 7.1.1

        if (!stack.isFullStack())                    //Step 7.1.2
            stack.push(name);

        highestGPA = GPA;                            //Step 7.1.3
    }
    else if (GPA == highestGPA)                      //Step 7.2
    {
        if (!stack.isFullStack())
            stack.push(name);
        else
        {
            cout << "Stack overflows. "
                 << "Program terminates!"
                 << endl;
            return 1;   //exit program
        }
    }
    infile >> GPA >> name;                           //Step 7.3
}

cout << "Highest GPA = " << highestGPA                 //Step 8
     << endl;
cout << "The students holding the "
     << "highest GPA are:" << endl;

while (!stack.isEmptyStack())                         //Step 9
{
    cout << stack.top() << endl;
    stack.pop();
}

cout << endl;

return 0;
}
```

### 示例运行：

### 输入文件（HighestGPAData.txt）

```
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
```

### 输出

```
Highest GPA = 3.90
The students holding the highest GPA are:
Vinay
Minnie
Andy
```

请注意，具有最高 GPA 的学生的姓名是按相反顺序输出的，相对于它们在输入中出现的顺序，这是因为栈顶元素是最后添加到栈中的元素。

## 栈的链式实现

由于数组大小是固定的，在栈的数组（线性）表示中，只能将固定数量的元素压入栈。如果在程序中要压入的元素数量超过数组大小，程序可能会因错误而终止。我们必须克服这些问题。

我们已经看到，通过使用指针变量，我们可以动态分配和释放内存；通过使用链表，我们可以动态组织数据（例如有序表）。接下来，我们将使用这些概念来动态实现栈。

回想一下，在栈的线性表示中，stackTop 的值表示栈中元素的数量，而 stackTop − 1 的值指向栈顶项。借助 stackTop，我们可以做几件事：找到栈顶元素、检查栈是否为空，等等。

与线性表示类似，在链式表示中，stackTop 用于定位栈中的栈顶元素。但是，有一个细微差别。在前一种情况下，stackTop 给出数组的索引。在后一种情况下，stackTop 给出栈顶元素的地址（内存位置）。

下面的类实现了抽象类 stackADT 的功能。

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
    //               otherwise returns false.

    bool isFullStack() const;
    //Function to determine whether the stack is full.
    //Postcondition: Returns false.

    void initializeStack();
    //Function to initialize the stack to an empty state.
    //Postcondition: The stack elements are removed;
    //               stackTop = NULL;

    void push(const Type& newItem);
    //Function to add newItem to the stack.
    //Precondition: The stack exists and is not full.
    //Postcondition: The stack is changed and newItem
    //               is added to the top of the stack.
```
