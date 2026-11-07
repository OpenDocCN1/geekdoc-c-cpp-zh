

读取一个用简单而又功能强大的高级语言编写的语句文件，该语言类似于早期版本的 BASIC。你的编译器会将这些语句翻译成一个 Simpletron 机器语言（SML）指令文件——SML 是你在第 8 章特别专题：构建你自己的计算机中学过的语言。然后，你的 Simpletron 模拟器程序将执行编译器生成的 SML 程序！该特别专题讨论了这种高级语言，以及将每种高级语言语句转换为机器码所需的算法。我们提供了编译器理论练习，并在特别专题中建议对编译器和 Simpletron 模拟器进行增强。

## 19.2 自引用类

自引用类包含一个指向同类类对象的成员。例如，下面的定义：

```cpp
class Node
{
public:
   explicit Node( int ); // constructor
   void setData( int ); // set data member
   int getData() const; // get data member
   void setNextPtr( Node * ); // set pointer to next Node
   Node *getNextPtr() const; // get pointer to next Node
private:
   int data; // data stored in this Node
   Node *nextPtr; // pointer to another object of same type
}; // end class Node
```

定义了一个类型 Node。类型 Node 有两个私有数据成员——整型成员 data 和指针成员 nextPtr。成员 nextPtr 指向一个 Node 类型的对象——即与这里声明的对象同类型的对象，因此称为自引用类。成员 nextPtr 被称为链接（link）——也就是说，nextPtr 可以将一个 Node 类型的对象“绑”到另一个同类型的对象上。类型 Node 还有五个成员函数——一个接收整数以初始化成员 data 的构造函数，一个设置成员 data 值的 setData 函数，一个返回成员 data 值的 getData 函数，一个设置成员 nextPtr 值的 setNextPtr 函数，以及一个返回成员 nextPtr 值的 getNextPtr 函数。

自引用类对象可以链接在一起，形成链表、队列、栈和树等有用的数据结构。图 19.1 展示了两个自引用类对象链接在一起形成一个链表。注意，第二个自引用类对象的链接成员中放置了一条斜线——表示空指针（nullptr）——用于指示该链接不指向另一个对象。这条斜线仅用于示意；它并不对应 C++ 中的反斜杠字符。空指针通常表示数据结构的末尾。

> **常见编程错误 19.1**
>
> *没有将链接数据结构中最后一个节点的链接设置为 nullptr，是一个（可能致命的）逻辑错误。*

![](img/b42ba5cd262b1358d16610173f975e4d_814_0.png)

![](img/b42ba5cd262b1358d16610173f975e4d_815_0.png)

**图 19.1** | 两个自引用类对象链接在一起。

接下来的几节将讨论链表、栈、队列和树。本章介绍的数据结构是使用*动态内存分配*（第 10.9 节）、*自引用类*、*类模板*（第 18 章）和*函数模板*（第 6.19 节）创建和维护的。

## 19.3 链表

链表是自引用类对象的*线性*集合，这些对象称为**节点**，通过**指针链接**连接在一起——因此得名“链表”。链表通过指向其第一个节点的指针来访问。每个后续节点都通过前一个节点中存储的*链接指针成员*来访问。按照惯例，列表中最后一个节点的链接指针被设置为 `nullptr`，以表示链表的末尾。数据是*动态*存储在链表中的——每个节点在需要时创建和销毁。节点可以包含任何类型的数据，包括其他类的对象。如果节点包含指向通过继承关联的基类对象和派生类对象的基类指针，那么我们可以拥有这样的节点链表，并使用虚函数调用对它们进行*多态*处理。栈和队列也是**线性数据结构**，而且我们将会看到，它们可以看作是链表的受限版本。树则是**非线性数据结构**。

与数组对象和内建数组相比，链表有若干优势。当一次需要表示的数据元素数量*不可预测*时，链表是合适的。链表是动态的，因此链表的长度可以根据需要增加或减少。然而，数组对象或内建数组的大小无法改变，因为数组大小在编译时就固定了。数组对象或内建数组可能会满。链表只有在系统内存不足、无法满足额外的动态存储分配请求时才会满。

> **性能提示 19.1**
>
> 数组对象或内建数组可以声明为包含比预期元素数量更多的元素，但这会浪费内存。在这些情况下，链表可以提供更好的内存利用率。链表允许程序在运行时自适应。类模板 `vector`（第 7.10 节）实现了一种基于数组、可动态调整大小的数据结构。

链表可以通过将每个新元素插入到列表中的适当位置来保持*有序*。现有链表元素无需移动。只需更新指针，使其指向正确的节点即可。

> **性能提示 19.2**
>
> 在有序数组对象或内建数组中插入和删除可能很耗时——插入或删除元素之后的所有元素都必须相应地移动。链表允许在列表中的任何位置进行高效的插入操作。

```cpp
case 4: // remove from end
    if ( !listObject.removeFromBack( value ) )
        cout << value << " removed from list\n";

    listObject.print();
    break;
} // end switch
} while ( choice < 5 ); // end do...while

cout << "End list test\n\n";
} // end function testList

int main()
{
    // test List of int values
    List< int > integerList;
    testList( integerList, "integer" );

    // test List of double values
    List< double > doubleList;
    testList( doubleList, "double" );
} // end main
```

```text
Testing a List of integer values
Enter one of the following:
  1 to insert at beginning of list
  2 to insert at end of list
  3 to delete from beginning of list
  4 to delete from end of list
  5 to end list processing
? 1
Enter integer: 1
The list is: 1

? 1
Enter integer: 2
The list is: 2 1

? 2
Enter integer: 3
The list is: 2 1 3

? 2
Enter integer: 4
The list is: 2 1 3 4

? 3
2 removed from list
The list is: 1 3 4

? 3
1 removed from list
The list is: 3 4

? 4
4 removed from list
The list is: 3
```

**图 19.3** | 操作链表：（第 2 部分，共 3 部分。）

```cpp
// delete node from back of list
bool removeFromBack( NODETYPE &value )
{
   if ( isEmpty() ) // List is empty
      return false; // delete unsuccessful
   else
   {
      ListNode< NODETYPE > *tempPtr = lastPtr; // hold item to delete

      if ( firstPtr == lastPtr ) // List has one element
         firstPtr = lastPtr = nullptr; // no nodes remain after removal
      else
      {
         ListNode< NODETYPE > *currentPtr = firstPtr;

         // locate second-to-last element
         while ( currentPtr->nextPtr != lastPtr )
            currentPtr = currentPtr->nextPtr; // move to next node

         lastPtr = currentPtr; // remove last node
         currentPtr->nextPtr = nullptr; // this is now the last node
      } // end else

      value = tempPtr->data; // return value from old last node
      delete tempPtr; // reclaim former ListNode
      return true; // delete successful
   } // end else
} // end function removeFromBack

// is List empty?
bool isEmpty() const
{
   return firstPtr == nullptr;
} // end function isEmpty

// display contents of List
void print() const
{
   if ( isEmpty() ) // List is empty
   {
      std::cout << "The list is empty\n\n";
      return;
   } // end if

   ListNode< NODETYPE > *currentPtr = firstPtr;

   std::cout << "The list is: ";

   while ( currentPtr != nullptr ) // get element data
   {
      std::cout << currentPtr->data << ' ';
      currentPtr = currentPtr->nextPtr;
   } // end while
}
```

**图 19.5** | List 类模板定义。（第 3 部分，共 4 部分。）

