
已经存在。

复制对象涉及复制其数据成员的值，这种拷贝被称为浅拷贝。如果浅拷贝就足够，你可以省略构造函数，在这种情况下编译器会生成一个执行浅拷贝的构造函数。在第 3 章的 `ArrayBag` 中就是这种情况，尽管我们没有提到它。基于数组的实现使用编译器生成的拷贝构造来同时拷贝数组项和项的数量。

### 调用拷贝构造的情况

编译器生成的拷贝构造执行浅拷贝。基于链接的 ADT 实现

图 4-8 (a) 链接链及其浅拷贝；(b) 链接链及其深拷贝

![](img/d0cb862f18db56996ad7c74351e_173_0.png)

对于我们新的基于链接的实现，编译器生成的拷贝构造将只会拷贝 `itemCount` 和 `headPtr`。例如，图 4-8a 链接链及其拷贝的结果。原始 `headPtr` 和它的拷贝指向同一个链接链。换句话说，链没有被拷贝。如果你需要创建链接链的拷贝，必须编写自己的拷贝构造。也就是说，需要深拷贝，如图 4-8b 所示。因此，拷贝构造如下：

```cpp
template <class ItemType>
LinkedBag<ItemType>::LinkedBag(const LinkedBag<ItemType>& a_bag)
{
    itemCount = a_bag.itemCount;
    Node<ItemType>* origChainPtr = a_bag.headPtr;
    if (origChainPtr == nullptr)
        headPtr = nullptr; // 原始包为空，所以我们拷贝
    else {
        // 拷贝第一个节点
        headPtr = new Node<ItemType>();
        headPtr->setItem(origChainPtr->getItem());
        // 拷贝剩余节点
        Node<ItemType>* newChainPtr = headPtr;
        origChainPtr = origChainPtr->getNext();
        while (origChainPtr != nullptr) // 移动指针
        {
            // 从原始链获取下一个项
            ItemType nextItem = origChainPtr->getItem();
            // 创建包含下一个项的新节点
            Node<ItemType>* newNodePtr = new Node<ItemType>(nextItem);
            // 将节点链接到链的末尾
            newChainPtr->setNext(newNodePtr);
            // 移动指针到最后一个节点
            newChainPtr = newNodePtr;
        }
        newChainPtr->setNext(nullptr); // 链的末尾
    } // end if
} // end copy constructor
```

你可以看到，构造函数是一个开销很大的操作。它需要遍历原始链接链并复制每个节点。

## 4.3 在基于链接的实现中使用递归

递归处理链接链是可能的，有时也是理想的。本节将检查如何将之前的迭代方法写为递归方法。此类递归方法需要头指针作为参数。因此，它们不应该是公有的，因为头指针是类的私有数据成员，客户端无权访问它。否则，客户端可以直接访问链接节点，违反了 ADT 的安全性。

### 4.3.1 LinkBag 中方法的递归定义

作为该主题的介绍，我们将回顾 `LinkBag` 类中两个使用递归的方法。这些方法简单地遍历链接链，而不对其进行任何修改。

`toVector` 方法有一个直观的递归实现。该操作要求我们遍历链接链。由于 `toVector` 是一个公共方法，我们通常定义一个私有的辅助方法来执行递归：

```cpp
// 辅助方法声明
void toVector(vector<ItemType>& v, Node<ItemType>* curPtr);
```

其递归实现如下：

```cpp
template <class ItemType>
void LinkedBag::toVector(vector<ItemType>& v, Node<ItemType>* curPtr)
{
    if (curPtr != nullptr) {
        v.push_back(curPtr->getItem());
        toVector(v, curPtr->getNext());
    }
}
```

然后，公共方法调用它：

```cpp
vector<ItemType> LinkedBag::toVector() const {
    vector<ItemType> v;
    toVector(v, headPtr);
    return v;
}
```

同样，`remove` 方法也可以通过递归来实现：

```cpp
// 辅助方法声明
void remove(const ItemType& item, Node<ItemType>*& cur);
```

其递归实现如下：

```cpp
template <class ItemType>
void LinkedBag::remove(const ItemType& item, Node<ItemType>*& cur)
{
    if (cur != nullptr) {
        if (cur->getItem() == item) {
            Node<ItemType>* nodeToDelete = cur;
            cur = cur->getNext();
            delete nodeToDelete;
            itemCount--;
        } else {
            remove(item, cur->getNext());
        }
    }
}
```

最后，公共方法调用它：

```cpp
void LinkedBag::remove(const ItemType& item) {
    remove(item, headPtr);
}
```

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
