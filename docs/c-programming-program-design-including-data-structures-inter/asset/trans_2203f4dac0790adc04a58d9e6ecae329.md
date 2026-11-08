
- 19. 假设有一个类（例如 `temp`）重载了前置和后置自增运算符 `++`，并且 `tempObj` 是类 `temp` 的对象。那么，语句 `++tempObj;` 被编译为 `tempObj.operator++();`，语句 `tempObj++;` 被编译为 `tempObj.operator++(0);`。哑元参数用于区分前置和后置自增运算符函数。前置和后置自减运算符也有类似约定。
- 21. 无。
- 23. 一个。
- 25. 本题答案可在本书配套网站获取。
- 27. 第4行有错误。模板实例化只能针对内置类型或用户定义类型。尖括号之间的单词“type”必须替换为内置类型或用户定义类型。
- 29. a. 12；b. Sunny Day。

```cpp
template <class Type>
void swap(Type &x, Type &y)
{
    Type temp;
    temp = x;
    x = y;
    y = temp;
}
```

## 第14章

- 1. a. 假；b. 真；c. 真；d. 假
- 3. 程序将终止并显示一条错误消息。
- 5. 如果在 `try` 块中抛出异常，则该 `try` 块中剩余的语句将被忽略。程序按 `try` 块之后 `catch` 块出现的顺序搜索这些 `catch` 块，并寻找合适的异常处理程序。如果所抛出异常的类型与某个 `catch` 块中的参数类型匹配，则执行该 `catch` 块的代码，并忽略此 `catch` 块之后的其余 `catch` 块。
- 7. 该 `catch` 块没有关联的 `try` 块，也就是说，该 `catch` 块不跟在任何 `try` 块之后。此外，该 `try` 块没有关联的 `catch` 块，也就是说，没有 `catch` 块跟在 `try` 块之后。`catch` 块之前的 `cout` 语句使 `catch` 块与 `try` 块脱离关联。正确的代码是：

```cpp
double radius;

try
{
    cout << "Enter the radius: ";
    cin >> radius;
    cout << endl;

    if (radius < 0.0)
        throw radius;

    cout << "Area: " << 3.1416 * radius * radius << endl;
}
catch (double x)
{
    cout << "Negative radius: " << x << endl;
}
```

- 9.
  a. 离开 try 块。
  b. 当前余额：975  
     余额必须大于 1000.00
  c. 当前余额：-2000  
     余额必须大于 1000.00
- 11.
  a. 进入 try 块。  
     异常：违反下限。  
     catch 块之后
  b. 进入 try 块。  
     异常：0  
     catch 块之后
  c. 进入 try 块。  
     退出 try 块。  
     catch 块之后
  d. 进入 try 块。  
     异常：0  
     catch 块之后
- 13. 一条 throw 语句。
- 15. （假设类 tornadoException 的定义在头文件 tornadoException.h 中。）

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
    catch (tornadoException &E)
    {
        cout << E.what() << endl;
    }

    return 0;
}
```

- 17. 函数在其头部使用 throw 子句指定它抛出的异常。

## 第15章

- 1. a. 真；b. 真；c. 假；d. 假；e. 假
- 3. 解由自身的较小版本来定义的情形。
- 5. 如果一个函数调用另一个函数，并最终导致对原函数的调用，则称该函数是间接递归的。
- 7.
  a. 第2行和第3行中的语句。
  b. 第4行和第5行中的语句。
  c. 任何非正整数。
  d. 这是一次有效调用。`mystery(0)` 的值为 0。
  e. 这是一次无效调用。它将导致无限递归。
  f. 这是一次有效调用。`mystery(-3)` 的值为 6。
- 9. a. 8 5 2；b. 7；c. 6 3；d. −85
- 11.
  a. 它不产生任何输出。
  b. 5 6 7 8 9
  c. 它不产生任何输出。
  d. 它不产生任何输出。
- 13. a. 2；b. 3；c. 5；d. 21
- 15.

$$\operatorname{multiply}(m,n)=
\begin{cases}
0 & \text{if } n=0\\
m & \text{if } n=1\\
m+\operatorname{multiply}(m,n-1) & \text{otherwise}
\end{cases}$$

基准情形是 n = 0 或 n = 1。一般情形由 otherwise 选项指定。

## 第16章

- 1. a. 假；b. 假；c. 假；d. 假
- 3. NULL
- 5. 删除前，第三个节点的链接字段存储第四个节点的地址。删除后，第三个节点的链接字段将存储下一个节点的地址，即原来的第四个节点。如果没有第五个节点，那么删除后，链接字段将存储值 NULL。因此，删除第四个节点后，第三个节点的链接字段发生了变化。所以需要一个指向第三个节点的指针。
- 7. a. 假；b. 真；c. 真；d. 真；e. 真
- 9.
  a. `current->link->info = 52;`
  b. `current = temp->link;`
  c. `trail = current->link;`
  d. `temp->link->link->info = 36;`
  e. `while (current->info != 10)`  
     `current = current->link;`
- 11.
  a. `while (current != NULL)`  
     `current = current->link;`
  b. `temp = new nodeType;`  
     `temp->info = 68;`  
     `temp->link = last;`  
     `trail->link = temp;`
  c. `delete last;`  
     `trail->link = NULL;`  
     `last = trail;`
  d. `trail = temp->link;`  
     `temp->link = trail->link;`  
     `delete trail;`
- 13. 第5行语句执行后，trail 为 NULL，因此 trail->info 不存在。这段代码将导致运行时错误。
- 15. 33 62 28
- 17.

```cpp
nodeType head, p, q;

head = new nodeType;
head->info = 72;
head->link = NULL;
p = new nodeType;
p->info = 43;
p->link = head;
head = p;
p = head->link;
q = new nodeType;
q->info = 8;
q->link = NULL;
p->link = q;
q = new nodeType;
q->info = 12;
q->link = p;
head->link = q;

p = head;
while (p != NULL)
{
    cout << p->info << " ";
    p = p->link;
}
cout << endl;
```

这段代码的输出为：
12 4 3 72 8

- 19. 要删除的项不在列表中。  
  93 66 38 55 18 35
- 20. 本题答案可在本书配套网站获取。
- 21. 本题答案可在本书配套网站获取。

## 第17章

- 1. 栈上的两个基本操作是 push（向栈中添加元素）和 pop（从栈中移除元素）。
- 3. 4
- 5. 13 5 12  
  num1 = 15  
  num2 = 21
- 7. a. 40  
  b. 11  
  c. 2  
  d. 70
- 9. a. (x + y) * z - w  
  b. x * y / z + w  
  c. x * (y + z) - w
- 11. 1 16 27 16 5
- 13. 如果栈非空，语句 `stack.top();` 返回栈顶元素，语句 `stack.pop();` 移除栈顶元素。
- 15.

```cpp
template <class elemType>
elemType second(stackType<elemType> stack)
{
    elemType temp1, temp2;

    if (stack.isEmptyStack())
    {
        cout << "Stack is empty." << endl;
        exit(0); // terminate the program
    }

    temp1 = stack.top();
    stack.pop();

    if (stack.isEmptyStack())
    {
        cout << "Stack has only one element." << endl;
        exit(0); // terminate the program
    }
    temp2 = stack.top();
    stack.push(temp1);

    return temp2;
}
```

- 17. 48 72 0 15  
  栈：36  
  队列：0 88 10 52 67
- 19. a. queueFront = 50；queueRear = 0。  
  b. queueFront = 51；queueRear = 99。
- 21. a. queueFront = 25；queueRear = 76。  
  b. queueFront = 26；queueRear = 75。
- 23. 51
- 25.

```cpp
template <class Type>
void reverseStack(stackType<Type> &s)
{
    linkedQueueType<Type> q;
    Type elem;

    while (!s.isEmptyStack())
    {
        elem = s.top();
        s.pop();
        q.addQueue(elem);
    }

    while (!q.isEmptyQueue())
    {
        elem = q.front();
        q.deleteQueue();
        s.push(elem);
    }
}
```

