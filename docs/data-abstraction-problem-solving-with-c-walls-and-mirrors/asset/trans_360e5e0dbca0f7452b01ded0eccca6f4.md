

## 4.4 测试多个 ADT 实现

在第 3 章中，我们编写了一个短程序（见列表 3-2），测试了我们基于数组的实现的核心方法。由于我们在测试该实现时使用了 ADT bag，因此我们可以使用相同的代码（仅需少量修改）来测试我们的链表实现。你只需要将每个 `ArrayBag` 更改为 `LinkedBag` 并重新编译程序。

但如果我们想更改回基于数组的实现并测试它呢？你需要将每个 `LinkedBag` 改回 `ArrayBag`。让我们考虑一种方法，通过让用户决定需要测试哪种包实现来验证该测试程序。利用多态的特性，我们可以在不复制重复代码的情况下实现这一点。

在第 1 章中，我们已经在抽象类 `BagInterface` 中声明了 ADT。由于 `ArrayBag` 和 `LinkedBag` 都共享类中定义的公共方法，我们使每一个类都成为 `BagInterface` 的子类。在我们的测试程序中，我们把 `bagPtr` 声明为指向 `BagInterface` 中方法所在对象的指针，我们可以使用 `ArrayBag` 或 `LinkedBag` 的实例作为对象引用。我们声明了 `bagPtr`：

```
BagInterface<string>* bagPtr;
```

然后我们询问用户想要测试哪种实现，如果我们将 'A' 或 'L' 赋值给变量 `userChoice`，可以通过以下代码实例化请求的包类型的实例并运行测试：

```
if (userChoice == 'A') {
    bagPtr = new ArrayBag<string>();
    cout << "Testing the Array-Based Bag:" << endl;
} else {
    bagPtr = new LinkedBag<string>();
    cout << "Testing the Link-Based Bag:" << endl;
} // end if
```

```
cout << "The initial bag is empty." << endl;
bagTester(bagPtr);
delete bagPtr;
bagPtr = nullptr;
```

为了适应 `bagPtr` 的数据类型，我们需要如下所示更改测试程序中函数的参数列表：

```
void displayBag(BagInterface<string>* bagPtr);
```

以及

```
void bagTester(BagInterface<string>* bagPtr);
```

最后，我们必须更改用于调用 `bagPtr` 实例方法的符号，因为它是一个指针。例如，

```
bag.isEmpty()
```

必须更改为

```
bagPtr->isEmpty()
```

列表 4-4 是用于 ADT bag 实现类的类的核心方法的修改后测试程序的完整列表。

## 列表 4-4 一个测试派自抽象类 BagInterface 的类的核心方法的程序

```
#include "BagInterface.h"
#include "ArrayBag.h"
#include "LinkedBag.h"
#include <iostream>
#include <string>
#include <cctype>

using namespace std;

void displayBag(BagInterface<string>* bagPtr)
{
    cout << "The bag contains " << bagPtr->getCurrentSize();
    cout << " items:" << endl;
    vector<string> bagItems;
    bagPtr->toVector(bagItems);
    int numberOfEntries = bagItems.size();
    for (int i = 0; i < numberOfEntries; i++)
    {
        cout << bagItems[i] << " ";
    }
    cout << endl << endl;
 // end displayBag

void bagTester(BagInterface<string>* bagPtr)
{
    cout << "isEmpty returns : " << bagPtr->isEmpty();
    cout << " should be 1 (true)" << endl;
    string items[] = { "one", "two", "three", "four", "five", "one" };
    cout << "Add 6 items to the bag: " << endl;
    for (int i = 0; i < 6; i++)
    {
        bagPtr->add(items[i]);
    }
    displayBag(bagPtr);
    cout << "isEmpty returns : " << bagPtr->isEmpty();
    cout << " should be 0 (false)" << endl;
    cout << "getCurrentSize returns : " << bagPtr->getCurrentSize();
    cout << " should be 6" << endl;
    cout << "To add another entry: add(\"extra\") returns "
    cout << bagPtr->add("extra") << endl;
}
 // end bagTester

int main()
{
    BagInterface<string>* bagPtr = nullptr;
    char userChoice;
    cout << "Enter 'A' to test the array-based implementation\n";
    cout << " ' or 'L' to test the link-based implementation: ";
    cin >> userChoice;

    if (toupper(userChoice) == 'A')
    {
        bagPtr = new ArrayBag<string>();
        cout << "Testing the Array-Based Bag:" << endl;
    } else
    {
        bagPtr = new LinkedBag<string>();
        cout << "Testing the Link-Based Bag:" << endl;
    } // end if

    cout << "The initial bag is empty." << endl;
    bagTester(bagPtr);
    delete bagPtr;
    bagPtr = nullptr;
    cout << "All done!" << endl;

    return 0;
} // end main
```

示例输出 1
Enter 'A' to test the array-based implementation
or 'L' to test the link-based implementation: A
Testing the Array-Based Bag:
The initial bag is empty.
isEmpty() returns 1; should be 1 (true)
Add 6 items to the bag:
The bag contains 6 items:
one two three four five one
isEmpty() returns 0; should be 0 (false)
getCurrentSize() returns 6; should be 6
Try to add another entry: add("extra") returns 0
All done!

示例输出 2
Enter 'A' to test the array-based implementation
or 'L' to test the link-based implementation: L
Testing the Link-Based Bag:
The initial bag is empty.
isEmpty() returns 1; should be 1 (true)
Add 6 items to the bag:
The bag contains 6 items:
one five four three two one
isEmpty() returns 0; should be 0 (false)
getCurrentSize() returns 6; should be 6
Try to add another entry: add("extra") returns 1
All done!

**问题 15** 修改列表 4-4 中的程序使其能够测试基于数组的实现和基于链表的实现。

## 4.5 比较数组实现链链实现

通常，基于数组的实现具有固定大小。当你选择数组时，必须权衡其优缺点。数组的一个优点是它提供随机访问。然而，如果数组满了，你可能需要分配一个新的更大的数组并复制所有元素。这是一个昂贵的操作。

基于链表的实现没有固定大小。你始终可以向链表中添加另一个项目。然而，缺点是链表不提供随机访问。要找到第 $n$ 个元素，你必须从头遍历链表。这是一个缓慢的操作。

基于链表的实现的另一个优点是它可以动态增长大小。缺点是每个元素都需要额外的内存来存储指向下一个元素的指针。这意味着对于相同数量的元素，链表使用的内存比数组多。

