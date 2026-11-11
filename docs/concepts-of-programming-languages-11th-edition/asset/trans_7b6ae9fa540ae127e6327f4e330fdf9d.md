
Stack 的类定义可以同时包含这两个构造函数，因此用户既可以使用默认大小的栈，也可以指定其他大小。

通过将类设为模板类，可以使栈的元素类型泛型化。这样，元素类型就可以作为模板参数。栈类型的模板类定义如下：

```cpp
#include <iostream.h>
template <typename Type>  // Type is the template parameter
class Stack {
  private:
    Type *stackPtr;
    int maxLen;
    int topSub;
  public:
    // A constructor for 100 element stacks
    Stack() {
        stackPtr = new Type [100];
        maxLen = 99;
        topSub = -1;
    }
    // A constructor for a given number of elements
    Stack(int size) {
        stackPtr = new Type [size];
        maxLen = size - 1;
        topSub = -1;
    }
    ~Stack() {delete stackPtr;};  // A destructor
    void push(Type number) {
        if (topSub == maxLen)
            cout << "Error in push-stack is full\n";
        else stackPtr[++topSub] = number;
    }
    void pop() {
        if (empty())
            cout << "Error in pop-stack is empty\n";
        else topSub --;
    }
    Type top() {
        if (empty())
            cerr << "Error in top-stack is empty\n";
        else
            return (stackPtr[topSub]);
    }
    int empty() {return (topSub == -1);}
};
```

C++ 模板类在编译时被实例化，成为有类型的类。例如，模板 Stack 类的实例，以及有类型类的实例，都可以通过以下声明创建：

```cpp
Stack<int> myIntStack;
```

然而，如果已经为 int 类型创建了模板 Stack 类的实例，则无需再创建有类型的类。

### 11.5.2 Java 5.0

Java 5.0 支持一种参数化抽象数据类型形式，其中泛型参数必须是类。回想一下，第 9 章曾简要讨论过这些内容。

最常见的泛型类型是集合类型，例如 LinkedList 和 ArrayList，它们在对泛型的支持加入之前就已经存在于 Java 类库中。最初的集合类型存储 Object 类的实例，因此可以存储任何对象（但不能存储基本类型）。因此，集合类型一直能够存储多种类型（只要它们是类）。这样做有三个问题：第一，每次从集合中取出对象时，都必须将其强制转换为适当的类型。第二，向集合添加元素时没有错误检查。这意味着，一旦集合创建完成，任何类的对象都可以添加到该集合中，即使该集合原本只打算存储 Integer 对象。第三，集合类型不能存储基本类型。因此，要将 int 值存储到 ArrayList 中，必须先将该值放入一个 Integer 类实例中。例如，考虑以下代码：

```java
// Create an ArrayList object
ArrayList myArray = new ArrayList();
// Create an element
myArray.add(0, new Integer(47));
// Get first object
Integer myInt = (Integer)myArray.get(0);
```

在 Java 5.0 中，集合类（其中最常用的是 ArrayList）成为泛型类。此类类通过在类构造函数上调用 new 并向其传递尖括号中的泛型参数来实例化。例如，可以用以下语句实例化 ArrayList 类以存储 Integer 对象：

```java
ArrayList<Integer> myArray = new ArrayList<Integer>();
```

这个新类克服了 Java 5.0 之前集合的两个问题。只能将 Integer 对象放入 myArray 集合。此外，从集合中取出对象时无需进行强制转换。Java 5.0 还包括用于链表、队列和集合的泛型集合。用户还可以在 Java 5.0 中定义泛型类。例如，我们可以有如下定义：

```java
public class MyClass<T> {
}
```

这个类可以通过以下方式实例化：

```java
MyClass<String> myString;
```

这些用户定义的泛型类有一些缺点。首先，它们不能存储基本类型。其次，元素不能被索引。必须使用 add 方法将元素添加到用户定义的泛型集合中。接下来，我们使用 ArrayList 实现泛型栈示例。注意，ArrayList 的最后一个元素通过 size 方法找到，该方法返回结构中的元素数量。元素通过 remove 方法从结构中删除。以下是该泛型类：

```java
import java.util.*;
public class Stack2<T> {

    private ArrayList<T> stackRef;
    private int maxLen;
    public Stack2() { // A constructor
        stackRef = new ArrayList<T>();
        maxLen = 99;
    }
    public void push(T newValue) {
        if (stackRef.size() == maxLen)
            System.out.println("Error in push-stack is full");
        else
            stackRef.add(newValue);
    }
    public void pop() {
        if (empty())
            System.out.println("Error in pop-stack is empty");
        else
            stackRef.remove(stackRef.size() - 1);
    }
    public T top() {
        if (empty()) {
            System.out.println("Error in top-stack is empty");
            return null;
        } else
            return (stackRef.get(stackRef.size() - 1));
    }
    public boolean empty() {return (stackRef.isEmpty());}
}
```

这个类可以通过以下方式为 String 类型实例化：

```java
Stack2<String> myStack = new Stack2<String>();
```

回想第 9 章，Java 5.0 支持通配符类。例如，Collection<?> 是所有集合类的通配符类。这允许编写一个可以接受任何集合类型作为参数的方法。因为集合本身可以是泛型的，所以 Collection<?> 类在某种意义上是一个泛型类的泛型。

使用通配符类型的对象时必须小心。例如，由于该类型的特定对象的组成部分具有类型，因此不能将其他类型的对象添加到该集合中。例如，考虑

```java
Collection<?> c = new ArrayList<String>();
```

除非其类型为 String，否则使用 add 方法向此集合中放入内容是非法。

在 Java 5.0 中，可以很容易地定义一个仅适用于受限类型集的泛型类。例如，类可以声明一个泛型类型的变量，并通过该变量调用 compareTo 之类的方法。如果为该类实例化的类型不包含 compareTo 方法，则该类不能使用。为了防止为不支持 compareTo 的类型实例化泛型类，可以使用以下泛型参数来定义它：

```java
<T extends Comparable>
```

Comparable 是声明 compareTo 的接口。如果在类定义中使用此泛型类型，则不能为该类实例化任何未实现 Comparable 的类型。这里保留字 **extends** 的选择似乎有些奇怪，但它的使用与子类型的概念有关。显然，Java 的设计者不想向语言中添加另一个更具内涵的保留字。

### 11.5.3 C# 2005

与 Java 的情况一样，C# 的第一个版本为存储任何类的对象定义了集合类。这些类是 ArrayList、Stack 和 Queue。这些类与 Java 5.0 之前的集合类存在相同的问题。

泛型类在 C# 2005 版本中被加入。五个预定义泛型集合是 Array、List、Stack、Queue 和 Dictionary（Dictionary 类实现哈希）。与 Java 5.0 完全一样，这些类消除了集合中允许混合类型以及从集合中取出对象时需要强制转换的问题。

与 Java 5.0 一样，用户可以在 C# 2005 中定义泛型类。用户定义的 C# 泛型类的一项能力是，可以将其中的任何一个定义为允许其元素被索引（通过下标访问）。虽然索引通常是整数，但另一种选择是使用字符串作为索引。

Java 5.0 提供而 C# 2005 不提供的一项能力是通配符类。

## 11.6 封装结构

本章前五节讨论了抽象数据类型，它们是最小封装。本节描述较大程序所需的多类型封装。
