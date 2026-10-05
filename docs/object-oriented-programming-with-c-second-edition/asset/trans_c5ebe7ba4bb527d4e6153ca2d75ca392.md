

```cpp
* ClassDeletePtr01 = new ClassDeletePtr;
ClassDeletePtr01->setx(10);
cout<<ClassDeletePtr01->getx()<<endl;
* ClassDeletePtr02 = new ClassDeletePtr;
ClassDeletePtr02->setx(20);
cout<<ClassDeletePtr02->getx()<<endl;
* ClassDeletePtr03 = new ClassDeletePtr;
ClassDeletePtr03->setx(30);
cout<<ClassDeletePtr03->getx()<<endl;
* ClassDeletePtr04 = new ClassDeletePtr;
ClassDeletePtr04->setx(40);
cout<<ClassDeletePtr04->getx()<<endl;
* ClassDeletePtr05 = new ClassDeletePtr;
ClassDeletePtr05->setx(50);
cout<<ClassDeletePtr05->getx()<<endl;
* ClassDeletePtr06 = new ClassDeletePtr;
ClassDeletePtr06->setx(60);

/*End of NewDeleteForMemorySave.cpp*/
Output
10
20
30
40
50
60
```

当此程序运行时，首先会为 `ClassNew` 的静态数据成员分配内存。静态数据成员 `NO_OF_OBJECTS` 存储了池中将同时共存的块（对象）数量。该数据成员应该是静态的，因为它包含了一组对象的信息，因此它不属于任何一个特定的对象。该数据成员的值应该被谨慎选择。内存过大将浪费内存，并可能适得其反。池的大部分可能在很长时间内保持闲，甚至在整个程序生命周期内都不被使用。非常小的内存将导致频繁分配更多的池，从而减慢程序速度。如果认为在任何给定时刻都会存在大量对象，则该变量的值应该保持较大，否则该值应该较小。在本例中，我们将 `NO_OF_OBJECTS` 初始化为 '5'。

接下来，会初始化另一个静态数据头指针（head）。该指针指向池中的下一个可用块。该数据成员也应该是静态的，因为它将为一组对象提供服务，因此不会是任何特定对象的一部分。每次调用 `new` 运算符都会返回此指针当前的值，并增加其值，使其指向池中的下一个可用块。由于某些很快就会明确的原因，此指针已初始化为 NULL。

现在主函数开始。为 `ClassNewPtr01`（由于是指针，所以是四个字节）分配内存。目前，它是一个垃圾值。接下来是 `ClassNew` 的 `new` 运算符函数。创建两个指针：`temp`（用于保存 `head` 的当前值，以便 `head` 移动到下一个块）和 `p`（用于遍历池）。`temp` 指针初始化为 `head` 的当前值。现在评估 `head` 指针的值。在第一次调用 `new` 运算符期间，其值将为 NULL。很快就会发现，在某种特定情况下其值也将 NULL。`if` 结构中的测试表达式执行成功。因此，执行 `if` 块。通过调用 `new` 运算符分配了足够存放 `NO_OF_OBJECTS` 个对象的内存。随后，该池的地址（即该池中第一个对象的地址）被存储在 `temp` 指针中。此后，循环将新创建池中每个对象（最后一个对象除外）的 `next` 指针设置为下一个对象的地址。循环结束后，`if` 块的最后语句将最后一个对象的 `next` 指针置为 NULL。至此，`if` 块结束。函数的最后语句使 `head` 指针指向池中的第二个对象。`new` 运算符函数返回 `temp` 的值，即池第一个对象的地址。因此，`ClassNewPtr01` 现在指向池的第一个对象。`ClassNewPtr01` 现在通过调用该 `ClassNew` 的函数来操作池中的第一个对象。

现在让我们看列表 8.48 中主函数的第四条语句。`ClassNew` 类的 `new` 运算符函数将被再次调用。同样，`temp` 指针将初始化为 `head` 的当前值，该值不是 NULL（`head` 指向池中的第二个对象）。如果执行 `if` 块，则执行最后两条语句。`head` 指针增加以指向下一个对象（在本例中为第三个），以及当前正在运行的对象地址（在本例中为第二个对象）。

这一过程将一直持续直到第五次调用 `ClassNew` 的 `new` 函数（`ClassNew * ClassNewPtr05 = new ClassNew`）。尽管这是 `if` 块的测试表达式将执行，但 `head` 指针的值将为 NULL，同时返回池头和最后一个对象的地址。现在，当第六次调用 `new` 运算符时，`if` 块的测试表达式成功。分配一个新的池并重复该过程。

为了使 `new` 运算符函数成功，需要使用循环释放内存。这需要在池的每个对象中存在 `next` 指针。由于这个 `next` 指针导致的内存浪费（这会违背重载 `new` 运算符的初衷），可以通过使用联合体（union）来轻易防止。

现在让我们看看如何删除 `ClassNew` 类的 `delete` 运算符。`delete` 运算符将被重载，使其不再释放内存。相反，应用 `delete` 运算符所指向的块将被放回空列表。当下次调用 `new` 运算符时，将返回该块的地址。在查看实际代码之前，让我们先看看它的效果。

考虑仅调用一次 `new` 运算符的情况。该孤立调用之后是是对 `delete` 运算符的调用（列表 8.49）。

### 列表 8.49 调用重载的 delete 运算符

```cpp
/**ClassName NewDeleteForMemorySaveMain.cpp*/
#include<iostream>
#include"NewDeleteForMemorySave.h"
void main() {
    ClassNew* ClassNewPtr01 = new ClassNew;
    ClassNewPtr01->setx(10);
    cout<<ClassNewDeletePtr01->get()<<endl;
    delete ClassNewDeletePtr01;
}
```

