

- 7. 抛出的值随后可能无法在 `catch` 块的异常处理代码中访问。

- 9. 被抛出的对象可以是特定对象，也可以是匿名对象。

- 11. 第 12 行的 `cout` 语句将 `catch` 块与 `try` 块分隔开。因此，`catch` 块没有关联的 `try` 块，而 `try` 块也没有关联的 `catch` 块。第 13 行的 `catch` 块没有参数。正确的代码是：

```cpp
double salary = 78000;                         //Line 1
double raise;                                  //Line 2

try                                            //Line 3
{                                              //Line 4
    cout << "Enter the raise: ";               //Line 5
    cin >> raise;                              //Line 6
    cout << endl;                              //Line 7

    if (raise < 0.0)                           //Line 8
        throw raise;                           //Line 9

    cout << "Salary increase: $"               //Line 10
         << salary * raise / 100 << endl;
    cout << "Exiting the try block." << endl;  //Line 11
}                                              //Line 12
catch (double x)                               //Line 13
{                                              //Line 14
    cout << "Negative raise: " << x << endl;   //Line 15
}                                              //Line 16
```

（在 a 和 b 中，用户输入以阴影标示。）

- a. **输入加薪比例：** `5`

  工资增加：$3900  
  正在退出 try 块。

  **输入加薪比例：** `-4`  
  负的加薪比例：-4

- 13.（以下内容中，用户输入以阴影标示。）

  - a. **输入项目数量：** `25`  
    **输入单个项目的成本：** `5.50`  
    总成本：$137.50

  - b. **输入项目数量：** `-55`  
    项目数量为负：-55  
    项目数量必须为非负数。

  - c. **输入项目数量：** `37`  
    **输入单个项目的成本：** `-4.5`  
    单位成本为负：-4.50  
    单位成本必须为非负数。

  - d. 输入项目数量：`-10`  
    项目数量为负：-10  
    项目数量必须为非负数。

- 15.
  - a. 55
  - b. 正在退出 try 块。
  - c. 异常：除数为 0
  - d. 异常：总分超出范围。

- 17.
  - a. `class out_of_range`
  - b. `class length_error`
  - c. `class runtime_error`

19. 一条 throw 语句。

21.（假设类 `tornadoException` 的定义位于头文件 `tornadoException.h` 中。）

```cpp
#include <iostream>
#include "tornadoException.h"

using namespace std;

int main()
{
    int miles;

    try
    {
        cout << "Enter the miles: ";
        cin >> miles;
        cout << endl;

        if (miles < 5)
            throw tornadoException();
        else
            throw tornadoException(miles);
    }
    catch (tornadoException tE)
    {
        cout << tE.what() << endl;
    }

    return 0;
}
```

23. 函数在函数头中使用 `throw` 子句指定它所抛出的异常。

25. （1）什么也不做；（2）部分处理异常，然后抛出相同的异常或新异常；（3）抛出新异常。

## 第 15 章

- 1. a. 正确；b. 正确；c. 错误；d. 错误；e. 错误；f. 错误；g. 正确；h. 正确

- 3. 一种根据自身较小版本来定义自身的定义。

- 5. 因为基准情形会终止递归。

- 7.
  - a. 第 3 行到第 6 行的语句。
  - b. 第 7 行和第 8 行的语句。
  - c. 这是一个有效调用。`recFunc(58)` 的值为 32。
  - d. 这是一个有效调用。`recFunc(-24)` 的值为 24。
  - e. 这是一个有效调用。`recFunc(0)` 的值为 0。

- 9.
  - a. `8 5 2`
  - b. `7`
  - c. `6 3`
  - d. `-85`

- 11.
  - a. `4 12 28`
  - b. `5 15 34 72 148`
  - c. `2 8 21 47 98`
  - d. 不产生任何输出。

- 13.
  - a. `0`
  - b. `4`
  - c. `8`
  - d. `162`

- 15.
  - a. `10`
  - b. `21`
  - c. `-23`
  - d. `2`
  - e. `-56`

- 17.

  $$
  \operatorname{multiply}(m,n)=
  \begin{cases}
  0 & \text{if } n=0\\
  m & \text{if } n=1\\
  m+\operatorname{multiply}(m,n-1) & \text{otherwise}
  \end{cases}
  $$

  基准情形是 $n=0$ 或 $n=1$ 时。一般情形由 otherwise 选项指定。

- 19. 一种选择控制结构。

## 第 16 章

- 1. a. 正确；b. 错误；c. 错误；d. 错误；e. 错误；f. 正确；g. 正确；h. 错误；i. 错误；j. 正确；k. 正确；l. 错误；m. 错误；n. 正确

- 3. `nullptr`

- 5. 删除之前，第三个节点的链接字段存储第四个节点的地址。删除之后，第三个节点的链接字段将存储下一个节点，即原来的第五个节点的地址。如果不存在第五个节点，删除之后，链接字段将存储值 `nullptr`。因此，删除第四个节点后，第三个节点的链接字段会发生改变。所以需要一个指向第三个节点的指针。

- 7. a. 正确；b. 正确；c. 错误；d. 正确；e. 正确；f. 错误

9.

```cpp
a.  p->link->info = 24;
b.  q = current->link;
c.  first = first->link;
d.  trail = p->link;
e.  p = nullptr;
f.  temp->link->info = 54;
g.  while (first->info != 5)
        first = first->link;
```

11.

```cpp
a.  while (first != nullptr)
        first = first->link;

b.  q = new nodeType;
    q->info = 17;
    q->link = current->link;
    current->link = q;

c.  q = temp->link;
    q->link = nullptr;
    delete last;
    last = q;

d.  q = p->link;
    p->link = current;
    delete q;

e.  q = current->link;
    q->link = temp->link;
    temp->link = q;
    current->link = temp;
```

- 13. `65  5  78`

- 15. `39  26  78`

- 17. `nodeType head, p, q;`

```cpp
head = new nodeType;
head->info = 72;
head->link = nullptr;
p = new nodeType;
p->info = 43;
p->link = head;
head = p;
p = head->link;
q = new nodeType;
q->info = 8;
q->link = nullptr;
p->link = q;
q = new nodeType;
q->info = 12;
q->link = p;
head->link = q;

p = head;
while (p != nullptr)
{
    cout << p->info << " ";
    p = p->link;
}
cout << endl;
```

这段代码的输出为：**43 12 72 8**

- 19.
  - a. begin 函数返回指向链表第一个节点的迭代器。
  - b. end 函数返回指向链表最后一个节点之后位置的迭代器。

- 21. **要删除的项目不在链表中。**

  `90 15 65 36 30 27`

- 23. 此问题的答案可在本书配套网站上找到。

- 25. 此问题的答案可在本书配套网站上找到。

## 第 17 章

- 1. a. 正确；b. 错误；c. 错误；d. 正确；e. 错误；f. 正确；g. 错误；h. 错误；i. 正确；j. 正确；k. 正确；l. 错误；m. 错误；n. 错误

- 3.
  - a. 8
  - b. 7
  - c. `dec = stack.top();`
  - d. `stack.pop();`

- 5. 13

  `32 32 13 16 28`

  `temp = 16`

- 7. `secretNum = 226`

- 9.
  - a. 16
  - b. -4
  - c. 39
  - d. 12
  - e. 15

- 11.
  - a. `x * y + z - t`
  - b. `x * (y + z) - w / u`
  - c. `(x - y) * (z / u) - (t + s)`
  - d. `x * (y - (z + w))`

- 13. `1 16 27 16 5`

15. 如果栈非空，语句 `stack.top();` 返回栈顶元素，语句 `stack.pop();` 移除栈顶元素。

```cpp
template <class elemType>
elemType second(stackType<elemType> stack)
{
    elemType temp1, temp2;

    if (stack.isEmptyStack())
    {
        cout << "Stack is empty." << endl;
        exit(0); //terminate the program
    }

    temp1 = stack.top();
    stack.pop();

    if (stack.isEmptyStack())
    {
        cout << "Stack has only one element." << endl;
        exit(0); //terminate the program
    }

    temp2 = stack.top();
    stack.push(temp1);

    return temp2;
}
```

