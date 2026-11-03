

```cpp
using namespace std;

int main()
{
  Stack< double > doubleStack; // create a Stack of double
  const size_t doubleStackSize = 5; // stack size
  double doubleValue = 1.1; // first value to push

  cout << "Pushing elements onto doubleStack\n";

  // push 5 doubles onto doubleStack
  for ( size_t i = 0; i < doubleStackSize; ++i )
  {
      doubleStack.push( doubleValue );
      cout << doubleValue << ' ';
      doubleValue += 1.1;
  } // end while

  cout << "\n\nPopping elements from doubleStack\n";

  // pop elements from doubleStack
  while ( !doubleStack.isEmpty() ) // loop while Stack is not empty
  {
      cout << doubleStack.top() << ' '; // display top element
      doubleStack.pop(); // remove top element
  } // end while

  cout << "\nStack is empty, cannot pop.\n";

  Stack< int > intStack; // create a Stack of int
  const size_t intStackSize = 10; // stack size
  int intValue = 1; // first value to push

  cout << "\nPushing elements onto intStack\n";

  // push 10 integers onto intStack
  for ( size_t i = 0; i < intStackSize; ++i )
  {
      intStack.push( intValue );
      cout << intValue++ << ' ';
  } // end while

  cout << "\n\nPopping elements from intStack\n";

  // pop elements from intStack
  while ( !intStack.isEmpty() ) // loop while Stack is not empty
  {
      cout << intStack.top() << ' '; // display top element
      intStack.pop(); // remove top element
  } // end while

  cout << "\nStack is empty, cannot pop. " << endl;
} // end main
```

```text
Pushing elements onto doubleStack
1.1 2.2 3.3 4.4 5.5

Popping elements from doubleStack
5.5 4.4 3.3 2.2 1.1
Stack is empty, cannot pop

Pushing elements onto intStack
1 2 3 4 5 6 7 8 9 10

Popping elements from intStack
10 9 8 7 6 5 4 3 2 1
Stack is empty, cannot pop
```

**图 23.2** | Stack 类模板测试程序。（第 3 部分，共 3 部分。）

第 34 行用声明

```cpp
Stack<int> intStack;
```

实例化了 int 栈 intStack（读作“intStack 是一个 int 类型的 Stack”）。第 41–45 行反复调用 push（第 43 行）将值放入 intStack，然后第 50–54 行反复调用 top 和 pop 将值从 intStack 中移除，直到它为空。再次注意输出中值按后进先出的顺序弹出。

## 23.3 操作类模板特化对象的函数模板

注意图 23.2 中函数 main 的代码中，第 9–32 行的 doubleStack 操作和第 34–56 行的 intStack 操作*几乎完全相同*。这再次提供了使用函数模板的机会。图 23.3 定义了函数模板 testStack（第 10–39 行）来执行与图 23.2 中 main 相同的任务——将一系列值压入 `Stack<T>` 并从 `Stack<T>` 中弹出值。

```cpp
1  // Fig. 23.3: fig23_03.cpp
2  // Passing a Stack template object
3  // to a function template.
4  #include <iostream>
5  #include <string>
6  #include "Stack.h" // Stack class definition
7  using namespace std;
8
9  // function template to manipulate Stack<T>
10 template< typename T >
11 void testStack(
12     Stack< T > &theStack, // reference to Stack< T >
13     const T &value, // initial value to push
14     const T &increment, // increment for subsequent values
15     size_t size, // number of items to push
16     const string &stackName ) // name of the Stack< T > object
17 {
```

**图 23.3** | 将 Stack 模板对象传递给函数模板。（第 1 部分，共 2 部分。）

```cpp
18        cout << "\nPushing elements onto " << stackName << '\n';
19    T pushValue = value;
20
21    // push element onto Stack
22    for ( size_t i = 0; i < size; ++i )
23    {
24        theStack.push( pushValue ); // push element onto Stack
25        cout << pushValue << ' ';
26        pushValue += increment;
27    } // end while
28
29    cout << "\n\nPopping elements from " << stackName << '\n';
30
31    // pop elements from Stack
32    while ( !theStack.isEmpty() ) // loop while Stack is not empty
33    {
34        cout << theStack.top() << ' ';
35        theStack.pop(); // remove top element
36    } // end while
37
38    cout << "\nStack is empty. Cannot pop." << endl;
39  } // end function template testStack
40
41  int main()
42  {
43    Stack< double > doubleStack;
44    const size_t doubleStackSize = 5;
45    testStack( doubleStack, 1.1, 1.1, doubleStackSize, "doubleStack" );
46
47    Stack< int > intStack;
48    const size_t intStackSize = 10;
49    testStack( intStack, 1, 1, intStackSize, "intStack" );
50  } // end main
```

```text
Pushing elements onto doubleStack
1.1 2.2 3.3 4.4 5.5

Popping elements from doubleStack
5.5 4.4 3.3 2.2 1.1
Stack is empty, cannot pop

Pushing elements onto intStack
1 2 3 4 5 6 7 8 9 10

Popping elements from intStack
10 9 8 7 6 5 4 3 2 1
Stack is empty, cannot pop
```

**图 23.3** | 将 Stack 模板对象传递给函数模板。（第 2 部分，共 2 部分。）

函数模板 testStack 使用 T（在第 10 行指定）来表示 Stack<T> 中存储的数据类型。该函数模板接受五个参数（第 12–16 行）：
- 要操作的 Stack<T>
- 一个类型为 T 的值，它将是压入 Stack<T> 的第一个值
- 一个类型为 T 的值，用于递增压入 Stack<T> 的值
- 要压入 Stack<T> 的元素个数
- 一个表示 Stack<T> 对象名称的字符串，用于输出

函数 main（第 41–50 行）实例化了一个类型为 Stack<double> 的对象，名为 doubleStack（第 43 行），以及一个类型为 Stack<int> 的对象，名为 intStack（第 47 行），并在第 45 行和第 49 行使用这些对象。编译器从用于实例化函数第一个参数的类型（即用于实例化 doubleStack 或 intStack 的类型）推断 testStack 的 T 类型。

## 23.4 非类型参数

第 23.2 节的类模板 Stack 在其模板声明中只使用了一个类型参数（图 23.1，第 7 行）。也可以使用非类型模板参数，它们可以有默认实参，并且被视为常量。例如，C++ 标准中的 array 类模板以如下模板声明开头：

```
template < class T, size_t N >
```

（回想一下，关键字 class 和 typename 在模板声明中可以互换。）因此，如下声明：

```
array< double, 100 > salesFigures;
```

会创建一个包含 100 个 double 的数组的类模板特化，然后使用它来实例化对象 salesFigures。array 类模板封装了一个内置数组。当你创建一个 array 类模板特化时，数组的内置数组成员具有声明中指定的类型和大小——在前面的示例中，它将是一个包含 100 个 double 值的内置数组。

## 23.5 模板类型参数的默认实参

此外，类型参数可以指定默认类型实参。例如，C++ 标准中的 stack 容器适配器类模板以如下声明开头：

```
template < class T, class Container = deque< T > >
```

它指定了 stack 默认使用 deque 来存储类型为 T 的栈元素。声明

```
stack< int > values;
```

会创建一个 int 栈的类模板特化（在幕后）并使用它来实例化名为 values 的对象。栈的元素存储在一个 deque<int> 中。

默认类型参数必须是模板类型参数列表中最右边（尾随）的参数。当你使用两个或更多默认实参实例化一个模板时，如果省略的实参不是最右边的，那么它右边的所有类型参数也必须被省略。从 C++11 开始，你可以在函数模板中为模板类型参数使用默认类型实参。

## 自测练习答案

23.1 a) 错误。关键字 typename 和 class 在此上下文中也允许基本类型的类型参数。 b) 正确。 c) 错误。函数模板之间的模板参数名不必唯一。 d) 正确。

23.2 a) 函数模板特化，类模板特化。 b) 模板，尖括号（< 和 >）。 c) 重载。 d) 参数化。 e) 作用域解析。

## 练习

23.3 （模板中的运算符重载）为谓词函数 isEqualTo 编写一个简单的函数模板，用相等运算符（==）比较其两个相同类型的参数，如果相等则返回 true，否则返回 false。在程序中仅使用各种基本类型调用 isEqualTo。现在编写一个单独的程序版本，使用用户定义的类类型调用 isEqualTo，但不重载相等运算符。当你尝试运行此程序时会发生什么？现在重载相等运算符（使用运算符函数）operator==。再次尝试运行此程序时会发生什么？

23.4 （Array 类模板）将图 18.10–18.11 中的 Array 类重新实现为类模板。

23.5 区分“函数模板”和“函数模板特化”这两个术语。

23.6 解释哪个更像模板（stencil）——类模板还是类模板特化？

23.7 函数模板和重载之间有什么关系？

23.8 编译器执行匹配过程以确定在调用函数时调用哪个函数模板特化。在什么情况下尝试匹配会导致编译错误？

23.9 为什么将类模板称为参数化类型是合适的？

23.10 解释为什么 C++ 程序会使用语句 `Array< Employee > workerList( 100 );`

23.11 回顾你对练习 23.10 的回答。解释为什么 C++ 程序可能会使用语句 `Array< Employee > workerList;`

23.12 解释在 C++ 程序中使用以下记号的含义：`template< typename T > Array< T >::Array( int s )`

23.13 为什么你会对诸如数组或栈之类的容器使用带非类型参数的类模板？

