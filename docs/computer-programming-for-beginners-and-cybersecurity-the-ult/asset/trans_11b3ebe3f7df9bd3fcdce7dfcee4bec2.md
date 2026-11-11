
使用虚拟内存较多的程序，运行速度远慢于使用虚拟内存较少的程序。

## 手动内存管理

使用 delete 和 new 时频繁出现的内存管理问题，其逻辑错误的根源通常极难发现并修复。程序员必须严格遵守以下原则：

-   每次调用 new 时，只要分配的内存不再需要，就应始终有一个与之对应的 delete 调用。这听起来可能很简单，但何时应使用 delete 并不总是很清楚；不过下面的函数展示了一个内存泄漏：

```cpp
void calc(int n) {
// ...
// Do some stuff
// ...
int *x = new int[n];
// ...
// Do some stuff with x
// ...
// Exit function without deleting x's memory
}
```

如果程序调用 calc 函数的次数足够多，程序最终会耗尽内存。在 calc 函数中，x 是局部变量。因此，x 位于栈上。所以，当某次对 calc 的调用完成时，该函数的清理代码会自动释放变量 x 所占用的空间。因为所有函数都会自动管理其局部变量和参数变量的内存。问题在于，x 通过 new 赋值，指向从堆而非栈分配的内存。函数执行并不会自动释放 x 所指向的内存。

-   delete 运算符绝不应被用来释放并非由先前 new 调用分配的内存。下面的代码片段展示了这样一个例子：

```cpp
int list[10], *x = list; // x points to list
// ...
// Do some stuff
// ...
delete [ ] x; // Logic error, attempt to deallocate x's memory
```

指针 x 所引用的空间并非由 new 运算符分配，因此不应使用 delete 运算符尝试释放该内存。当你试图删除并非由 new 分配的内存时，会导致未定义行为，这表示存在逻辑错误。

-   delete 运算符不得用于多次释放同一块内存。当两个指针指向同一块内存时，这种情况很常见。这样的指针称为别名。下面的代码片段展示了这种情况：

```cpp
int *x = new int[10], *y = x; // y aliases x
// ...
// Do some stuff with x and/or y
// ...
delete [ ] x; // Free up x's memory
// ...
// Do some other stuff
// ...
delete [] y; // Logic error, y's memory already freed!
```

由于指针 x 和指针 y 指向同一块内存，因此 x 和 y 互为别名。如果你释放了其中一个所引用的内存，那么另一个所引用的内存也会被释放，因为它们是同一块内存。

-   使用 delete 释放内存后，绝不应再访问该内存。当你试图访问已删除的内存时，会导致未定义行为，这表示存在逻辑错误。

```cpp
int *list = new int[10];
// ... // Use list, then
// ...
delete [] list; // Deallocate list's memory
// ...
// Sometime later
// ...
int x = list[2]; // Logic error, but sometimes works!
```

上面的代码片段说明了这种情况可能如何发生。为了提高效率，delete 运算符只是让堆空间变为可用，而不会修改该内存中的内容。

## 资源管理

程序员在用完链表对象后立即调用 clear，这一点至关重要。请看下面的定义：

```cpp
void x() {

IntList1 my_list; // Constructor called here

// Add some numbers to the list

my_list.insert(12);

my_list.insert(7);

my_list.insert(-14);

// Print the list

my_list.print();

} // Oops! Forgot to call my_list.clear!
```

在上面的代码中，变量 my_list 是函数 x 的局部变量。当函数 x 执行完毕时，变量 my_list 将离开作用域。此时，为名为 my_list 的局部 IntList1 变量在栈上分配的空间会被回收。尽管链表中堆分配的元素空间仍然存在，但程序能访问该内存的唯一途径是通过 my_list.head，而 my_list 已不复存在。这是内存泄漏的典型例子。请注意，到目前为止，我们设计的类中，除了 IntList1 之外，没有任何类有这个问题。不过，C++ 为类设计者提供了一种解决办法，可以指定在对象生命周期结束时必须执行的操作。构造函数在对象存在之初执行代码。析构函数是一种特殊方法，在对象停止存在之前立即执行。析构函数也可以与其类同名，并带有波浪号 ~ 前缀。此外，析构函数不接受参数。代码 9.2 展示了如何向类中添加析构函数，并加入前面建议的对 length 和 clear 方法的优化。

### 代码 9.2

```cpp
class IntList2 {

// The nested private Node class from before

struct Node {

int data; // A data element of the list

Node *next; // The node that follows this one in the list
Node(int d); // Constructor
};
Node *head; // Points to the first item in the list
Node *tail; // Points to the last item in the list
int len; // The number of elements in the list
public:
// The constructor makes an initially empty list
IntList2();
// The destructor that reclaims the list's memory
~IntList2();
// Inserts n onto the back of the list.
void insert(int n);
// Prints the contents of the linked list of integers.
void print() const;
// Returns the length of the linked list.
int length() const;
// Removes all the elements in the linked list.
void clear();
};
```

## 结论

在带你了解了 C++ 中十个必知主题之后，现在轮到你发展自己的技能了。对于语言——无论是英语、法语还是编程语言——有一点是共同的：熟能生巧。我们在本书中教给你的知识，可以比作学习英语字母表和一些基础单词。因此，我们建议你多加练习。把心思放在理解我们为什么使用某些语句，以及我们想要获得的结果上。

上网下载所有你觉得易于使用的必要应用程序；如果需要付费，就购买它。当你一切准备就绪后，选择一个项目来学习。你可以构建自己的小项目，也可以选择一个现成的项目并尝试复现它。如果你在任何地方卡住了，你随时可以回头查看程序员是如何制作该项目并推进的。但始终要努力挑战自己的极限，在查看答案之前深入思考。

拿起其他真正优秀的书籍也会对你大有帮助，让你对 C++ 的某个部分获得不同见解，从而拓宽你对它的理解。尽管我们可以向你保证，本书的质量足以让你走上在 C++ 中取得成功的正确道路，但我们仍建议你阅读其他关于这门编程语言的书。

此外，你可以考虑选择一门 C++ 之外的语言，与 C++ 并行学习。学习一门新语言是更深入理解 C++ 的高效方式。新语言有助于更好地理解一般意义上的编程语言。它还会拓宽你解决问题的思路，从而凸显 C++ 这门主要语言的特殊之处。即使你可能不会在 C++ 中使用这门新语言的代码，它也会让你接触到一些经过验证的思想，并可将这些思想转用到 C++ 中。我们建议你与 C++ 一起学习的一门编程语言是 Haskell。你也可以学习 Java，因为它比 C++ 更接近我们的日常英语，对你来说更容易理解。你也可以看看我们关于 Java 的书。

此外，始终努力保持与时俱进。跟上现代 C++ 特性，如 C++11、C++14、C++17 以及标准库中的许多其他新特性。其中一些最新特性，如 lambda，很容易掌握。你所需要的只是良好的资源和时间，很快你就会发现自己成为这些特性的高手。那么，为什么不泡一杯茶，找一个能让你更容易集中注意力的舒适放松之处，然后开始呢？正如那句名言所说：“千里之行，始于足下。”所以，今天就迈出这一步，让我们成为引导你走上正确道路的向导。
