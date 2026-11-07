
## 强化学习：导论

理查德·S·萨顿、安德鲁·G·巴托

第二版，编写中

MIT 出版社，马萨诸塞州剑桥，2017

这是该书的预印本版本，可在网上获取。该书是 1998 年经典版的第二版。主要变化是新增了一章关于深度强化学习，以及新增了一章关于强化学习与心理学和神经科学的关系。其他几章也进行了大幅修订。

![](img/bfd978e7e9b192bab46ec2a89e481263_617_0.png)

### 目录

-   前言
-   1. 强化学习问题
-   2. 多臂老虎机
-   3. 有限马尔可夫决策过程
-   4. 动态规划
-   5. 蒙特卡洛方法
-   6. 时序差分学习
-   7. n 步自举
-   8. 基于表格方法的规划与学习
-   9. 带近似的同策略预测
-   10. 带近似的同策略控制
-   11. 带近似的异策略方法
-   12. 资格迹
-   13. 策略梯度方法
-   14. 心理学
-   15. 神经科学
-   16. 应用与案例研究
-   17. 前沿
-   A. 记号
-   B. 注释参考书目

```cpp
// constructor template
template< typename T >
Stack< T >::Stack( int s )
   : size( s > 0 ? s : 10 ), // validate size
     top( -1 ), // Stack initially empty
     stackPtr( new T[ size ] ) // allocate memory for elements
{
   // empty body
} // end Stack constructor template

// push element onto Stack;
// if successful, return true; otherwise, return false
template< typename T >
bool Stack< T >::push( const T &pushValue )
{
   if ( !isFull() )
   {
      stackPtr[ ++top ] = pushValue; // place item on Stack
      return true; // push successful
   } // end if

   return false; // push unsuccessful
} // end function template push

// pop element off Stack;
// if successful, return true; otherwise, return false
template< typename T >
bool Stack< T >::pop( T &popValue )
{
   if ( !isEmpty() )
   {
      popValue = stackPtr[ top-- ]; // remove item from Stack
      return true; // pop successful
   } // end if

   return false; // pop unsuccessful
} // end function template pop

#endif
```

图 14.2 | Stack 类模板。（第 2 部分，共 2 部分。）

*类模板的成员函数定义是函数模板。* 出现在类模板定义之外的成员函数定义都以如下头部开始

```cpp
template< typename T >
```

（第 40、51 和 65 行）。因此，每个定义都类似于常规函数定义，只不过 Stack 类元素类型始终以类型参数 T 泛型列出。作用域解析运算符与类模板名 Stack<T>（第 41、52 和 66 行）一起使用，以将每个成员函数定义绑定到类模板的类型。在此情况下，泛型类名是 Stack<T>。当 doubleStack 被实例化为类型 Stack<double> 时，Stack 构造函数函数模板特化使用 new 创建一个 double 类型元素的数组来表示栈（第 44 行）。语句

```cpp
stackPtr( new T[ size ] );
```

在 Stack 类模板定义中，由编译器在类模板特化 Stack<double> 中生成如下

```cpp
stackPtr( new double[ size ] );
```

### 测试类模板 Stack<T> 的驱动程序

现在，让我们考虑用于测试 Stack 类模板的驱动程序（图 14.3）。该驱动程序首先实例化大小为 5 的对象 doubleStack（第 9 行）。此对象声明为 Stack<double> 类（读作“double 的 Stack”）。编译器将类型 double 与类模板中的类型参数 T 关联，以生成 double 类型的 Stack 类的源代码。尽管模板带来了软件可复用性的好处，但请记住，即使模板只编写一次，程序中也会（在编译时）实例化多个类模板特化。

```cpp
// Fig. 14.3: fig14_03.cpp
// Stack class template test program.
#include <iostream>
#include "Stack.h" // Stack class template definition
using namespace std;

int main()
{
   Stack< double > doubleStack( 5 ); // size 5
   double doubleValue = 1.1;

   cout << "Pushing elements onto doubleStack\n";

   // push 5 doubles onto doubleStack
   while ( doubleStack.push( doubleValue ) )
   {
      cout << doubleValue << ' ';
      doubleValue += 1.1;
   } // end while

   cout << "\nStack is full. Cannot push " << doubleValue
      << "\nPopping elements from doubleStack\n";

   // pop elements from doubleStack
   while ( doubleStack.pop( doubleValue ) )
      cout << doubleValue << ' ';

   cout << "\nStack is empty. Cannot pop\n";

   Stack< int > intStack; // default size 10
   int intValue = 1;
   cout << "\nPushing elements onto intStack\n";
```

**图 14.3** | Stack 类模板测试程序。（第 1 部分，共 2 部分。）

```cpp
// push 10 integers onto intStack
while ( intStack.push( intValue ) )
{
   cout << intValue++ << ' ';
} // end while

cout << "\nStack is full. Cannot push " << intValue
     << "\nPopping elements from intStack\n";

// pop elements from intStack
while ( intStack.pop( intValue ) )
   cout << intValue-- << ' ';

cout << "\nStack is empty. Cannot pop" << endl;
} // end main
```

```text
Pushing elements onto doubleStack
1.1 2.2 3.3 4.4 5.5
Stack is full. Cannot push 6.6

Popping elements from doubleStack
5.5 4.4 3.3 2.2 1.1
Stack is empty. Cannot pop

Pushing elements onto intStack
1 2 3 4 5 6 7 8 9 10
Stack is full. Cannot push 11

Popping elements from intStack
10 9 8 7 6 5 4 3 2 1
Stack is empty. Cannot pop
```

**图 14.3** | Stack 类模板测试程序。（第 2 部分，共 2 部分）

第 15–19 行调用 push，将 double 值 1.1、2.2、3.3、4.4 和 5.5 压入 `doubleStack`。当驱动程序尝试将第六个值压入 doubleStack 时（此时该栈已满，因为它最多容纳五个元素），while 循环终止。当函数 push 无法将值压入栈时，它返回 false。

第 25–26 行在 while 循环中调用 pop，以从栈中移除这五个值（请注意，在图 14.3 的输出中，这些值确实按后进先出顺序弹出）。当驱动程序尝试弹出第六个值时，doubleStack 为空，因此 pop 循环终止。第 30 行通过以下声明实例化整数栈 intStack

```cpp
Stack< int > intStack;
```

（读作“intStack 是 int 的 Stack”）。由于未指定大小，大小默认为默认构造函数中指定的 10（图 14.2，第 10 行）。第 35–38 行循环并调用 push 将值压入 intStack，直到它满；然后第 44–45 行循环并调用 pop 从 intStack 中移除值，直到它为空。再次请注意，在输出中，这些值按后进先出顺序弹出。

-   **Stack 类（图 14.2）** 提供了函数 isFull，您可以在尝试 push 操作之前用它来确定栈是否已满。这避免了向满栈压入元素可能导致的错误。我们也可以让函数 push 抛出异常。您可以捕获该异常，然后决定如何针对应用程序适当地处理它。当尝试从空栈中弹出元素时，同样的技术也可用于函数 pop。

### 创建函数模板以测试类模板 Stack<T>

请注意，图 14.3 中函数 main 的代码对于第 9–28 行中的 doubleStack 操作和第 30–47 行中的 intStack 操作几乎完全相同。这提供了另一个使用函数模板的机会。图 14.4 定义了函数模板 testStack（第 10–34 行），以执行与图 14.3 中 main 相同的任务——将一系列值压入 Stack<T>，并从 Stack<T> 中弹出这些值。函数模板 testStack 使用模板参数 T（在第 10 行指定）表示存储在 Stack<T> 中的数据类型。该函数模板接受四个参数（第 12–15 行）——一个对 Stack<T> 类型对象的引用、一个类型为 T 的值（该值将作为第一个压入 Stack<T> 的值）、一个用于递增压入 Stack<T> 的值的类型为 T 的值，以及一个表示 Stack<T> 对象名称以用于输出的字符串。函数 main（第 36–43 行）实例化一个名为 doubleStack 的 Stack<double> 类型对象（第 38 行）和一个名为 intStack 的 Stack<int> 类型对象（第 39 行），并在第 41 和 42 行使用这些对象。编译器根据用于实例化该函数第一个参数的类型（即用于实例化 doubleStack 或 intStack 的类型）推断 testStack 的 T 类型。图 14.4 的输出与图 14.3 的输出完全一致。

```cpp
// Fig. 14.4: fig14_04.cpp
// Stack class template test program. Function main uses a
// function template to manipulate objects of type Stack<T>.
#include <iostream>
#include <string>
#include "Stack.h"  // Stack class template definition
using namespace std;

// function template to manipulate Stack<T>
template< typename T >
void testStack(
   Stack< T > &theStack, // reference to Stack<T>
   T value,              // initial value to push
   T increment,          // increment for subsequent values
   const string stackName ) // name of the Stack<T> object
{
   cout << "\nPushing elements onto " << stackName << '\n';

   // push element onto Stack
   while ( theStack.push( value ) )
   {
      cout << value << ' ';
      value += increment;
   } // end while
}
```

**图 14.4** | 将 Stack 模板对象传递给函数模板。（第 1 部分，共 2 部分。）

