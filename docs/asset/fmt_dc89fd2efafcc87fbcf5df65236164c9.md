
`this`指针很少被使用，但确实存在需要`this`指针的情况（参见第16章）。

### 9.4.1 连续赋值与`this`

C++的语法允许连续赋值，且赋值运算符从右到左关联。运算符在置于`int`中时的行为是符合预期的，所有其他实现都可能导致惊讶和困惑。因此，流上下文中的插入（`<<`）和提取（`>>`）运算符可能选择不当：这些操作与移位运算符没有任何共同点。

## 9.5. 拷贝构造函数：初始化与赋值

这里遇到的拷贝构造函数是新的。尽管它没有在类实例中声明，但它也不会导致编译错误。这引出了以下规则：

拷贝构造函数（几乎）总是可用的，即使它没有在类的接口中声明。

“（几乎）”的原因见第9.7.1节。

编译器生成的拷贝构造函数也称为平凡拷贝构造函数（trivial copy constructor）。它的用法很容易被抑制（使用`= delete`惯用法）。平凡拷贝构造函数将现有对象的原始数据进行字节级复制到新创建的对象中；拷贝构造函数则根据现有对象中的对应成员来初始化对象的数据成员；当使用继承时，它会调用类的拷贝构造函数来初始化新对象的基类。

因此，在示例使用了平凡拷贝构造函数。由于它对对象的原始数据类型进行逐字节复制，而这正是第3语句发生的情况，当`s3`消失时，它的析构函数删除了它的字符串数组。不幸的是，`d_string`是一个原始类型，因此在对象离开作用域时它会删除它的指针。

解决办法很简单：与其使用平凡拷贝构造函数，不如必须在类中显式声明它，并且其定义必须防止野指针，这与在重载赋值运算符中实现的方式类似。对象的动态分配内存被复制，以便其包含已分配的数据。但请注意，如果一个类还扩展了额外的（原始）内存，即如果它支持额外的容量，那么拷贝构造的对象中将不会提供未使用的容量。

拷贝构造可以用于丢弃多余的容量。拷贝构造函数并不一定要丢弃多余容量。例如，在构造`std::string`对象时，目标对象定义的容量与源对象相同。拷贝构造函数比重载赋值运算符更简单，因为它不需要删除之前分配的内存。由于对象即将被创建，因此还没有分配任何内存。

`Strings`的拷贝构造函数可以如下实现：

```cpp
Strings::Strings(const Strings &other)
d_string(new string[other.d_size]), d_size(other.d_size)
{
    for (size_t idx = 0; idx != other.d_size; ++idx)
        d_string[idx] = other.d_string[idx];
}
```

当使用同类的另一个对象初始化对象时，总是会调用拷贝构造函数。除了我们为止遇到的普通拷贝构造外，在其他情况下也会使用拷贝构造函数：

- 当函数定义一个类的值参数而不是指针或引用时，会使用它。函数的参数使用拷贝构造函数来初始化函数的参数。

示例：

```cpp
void process(Strings store)
{
  store.at(3) = "modified";
}
```

```cpp
int main(int argc, char **argv) {
  Strings outer(argv, argc);
  process(outer);
}
```

- 当函数定义类类型作为返回值时，会使用它。示例：

```cpp
Strings copy(Strings const &store) {
  return store;
}
```

`store`用于初始化`copy`的返回值。返回的`Strings`对象是一个临时匿名对象，可以被调用`copy`的代码立即使用，但之后对其生命周期不做任何假设。

## 9.6 修订赋值运算符

重载的赋值运算符具有与拷贝构造函数和析构函数遇到的类似的特征：

- （私有）数据的复制发生在 (1) 拷贝构造函数中和 (2) 重载赋值函数中。
- 已分配的内存会在 (1) 重载赋值函数中和 (2) 析构函数中删除。

拷贝构造函数和析构函数显然是需要的。如果重载的赋值运算符还需要返回分配的内存并为数据成员赋新值，难道不能用析构函数和拷贝构造函数吗？

正如我们在析构函数讨论（第9.2节）中所所示，析构函数可以显式调用，但拷贝构造函数并不如此。但让我们简单总结一下赋值运算符应该的作用：

- 它应该删除当前对象控制的动态分配内存；
- 它应该重新赋值对象的数据成员。

解决办法很简单：与其使用平凡拷贝构造函数，不如在类中显式声明它，并且其定义必须防止野指针，这与在重载赋值运算符中实现的方式类似。对象的动态分配内存被复制，以便其包含已分配的数据。但请注意，如果一个类还扩展了额外的（原始）内存，即如果它支持额外的容量，那么拷贝构造的对象中将不会提供未使用的容量。

拷贝构造可以用于丢弃多余的容量。拷贝构造函数并不一定要丢弃多余容量。例如，在构造`std::string`对象时，目标对象定义的容量与源对象相同。拷贝构造函数比重载赋值运算符更简单，因为它不需要删除之前分配的内存。由于对象即将被创建，因此还没有分配任何内存。

`Strings`的拷贝构造函数可以如下实现：

```cpp
Strings::Strings(const Strings &other)
d_string(new string[other.d_size]), d_size(other.d_size)
{
    for (size_t idx = 0; idx != other.d_size; ++idx)
        d_string[idx] = other.d_string[idx];
}
```

### 9.6.1 修改赋值运算符

之前：

之后：
图9.4：交换带有自引用数据的对象

`size_t d_data;`

图9.4的上半部分显示了两个对象；它们的上部数据成员指向它们的下部部数据成员。如果交换了这些对象，就会遇到图中下半部分所示的情况。如果地址`a`和`c`处的值被交换，那么它们不再指向自己的下部数据成员，而是突然指向了其他对象的数据成员。同样，这是一个坏消息。

这些操作失败的常见原因很容易识别：当数据成员或引用了涉及交换的数据时，必须避免简单的交换操作。如果图9.4中的`a`和`c`数据成员指向两个对象之外的信息（例如，如果它们会动态分配内存），那么简单的交换将会成功。

然而，在交换`SelfRef`对象时遇到的困难，并不意味着`SelfRef`对象不能交换；它只意味着我们在设计成员时必须小心。这里是`SelfRef::swap`的实现：

```cpp
void SelfRef::swap(SelfRef &other)
{
    swap(d_data, other.d_data);
}
```

这种实现保持了自引用数据成员不变，仅交换剩余的数据。对于图9.3所示的链表，也可以设计一个类似的`swap`成员。

#### 9.6.1.1 快速交换

正如我们所见，通过`placement new`可以在大小为`sizeof(Class)`字节的内存块中构造对象。因此，相同类的两个对象占用`sizeof(Class)`字节。

# 第9章：类与内存分配

如果我们的类对象是可以交换的，并且我们类的数据成员没有引用实际上实际上参与交换操作的数据，那么就可以实现一种基于“我们知道对象可能有多大”这一事实的极快速交换方法。

在这种快速交换方法中，我们只需交换`sizeof(Class)`字节的内容。此过程可以适用于可以使用成员间交换操作进行交换的类，并且（在实践中，这可能超出了C++ ANSI/ISO标准中描述的操作范围）也可以用于具有引用数据成员的类。它简单地定义了一个`sizeof(Class)`字节的缓冲区并执行循环`memcpy`操作。以下是针对假设类`Class`的实现。它实现了非常快速的交换：

```cpp
#include <cstring>
void Class::swap(Class &other)
{
    char buffer[sizeof(Class)];
    memcpy(buffer, &other, sizeof(Class));
    memcpy(static_cast<void *>(other), this, sizeof(Class));
    memcpy(static_cast<void *>(this), buffer, sizeof(Class));
}
```

`memcpy`目的地的`static_cast`用于防止编译器报错：由于`Class`是一个类类型，编译器（正确地）警告不要粗暴地拷贝字节。但如果你是`Class`的开发者并且知道自己在做什么，使用`memcpy`是没问题的。

这是一个定义了引用数据成员并提供了类似上述`swap`方法的类示例。运行程序后，包含两行 "hello to 1"，两个包含两行 "hello to 2"（为了简洁起见，所有的`Reference`都是内联定义的）：

```cpp
#include <iostream>
#include <cstring>
class Reference
{
    std::ostream &d_out;
public:
    Reference(std::ostream &out)
    :
        d_out(out) {}
    void swap(Reference &other)
    {
        char buffer[sizeof(Reference)];
        memcpy(buffer, this, sizeof(Reference));
        memcpy(static_cast<void *>(this), &other, sizeof(Reference));
        memcpy(static_cast<void *>(other), buffer, sizeof(Reference));
    }
    std::ostream &out()
    {
        return d_out;
    }
};
```

## 9.7. 移动数据

```cpp
int main() {
    std::ostream one("one");
    std::ostream two("two");
    Reference ref1(one);
    Reference ref2(two);
    ref1.out() << "hello to 1\n";
    ref2.out() << "hello to 2\n";
    ref1.swap(ref2);
    ref2.out() << "hello to 1\n";
    ref1.out() << "hello to 2\n";
}
```

快速交换应该只用于自定义类，且必须证明在交换时快速交换不会损坏其内部的对象。

## 9.7 移动数据

传统上，C++提供了两种方法将临时对象数据成员所指向的信息赋值给*ivalue*对象。必须使用拷贝构造函数或引用计数。除了这两种方法外，C++现在还支持移动语义，允许将临时对象指向的数据*转移*到目标位置。

移动信息是基于匿名（临时）数据的概念。临时值由如`operator-*`和`operator+(Type const &lhs, Type const &rhs)`等函数返回……

## 9.7. 移动数据

```cpp
error: cannot bind 'Class' lvalue to 'Class&&'
error: initializing argument 1 of 'Class::Class(Class&&)'
```

```cpp
class Class {
public:
    Class() = default;
    Class(Class &&tmp);
};
```

```cpp
int main() {
    Class one;
    Class two{ one };
}
```

解决办法很简单，只需声明一个（可能是默认的）拷贝构造函数，错误就消失了：

```cpp
class Class {
public:
    Class() = default;
    Class(Class const &other) = default;
    Class(Class &&tmp);
};
```

```cpp
int main() {
    Class one;
    Class two{ one };
}
```

### 9.7.2 移动构造函数（组合）

不使用指向由其对象控制的内存的指针成员（且没有基类，此情况请参见第13章）的类也可以从期望右值引用中获益。当一个或多个组合的数据成员本身支持移动操作时，这些类就能从移动操作中获益。

如果组合数据成员的类型不支持移动或拷贝，则无法实现移动操作。目前，`stream`就属于这一类。

感知移动的类的示例是`std::string`。一个`Person`类可以通过定义`std::string d_name`和`std::string d_address`来使用组合。那么它的移动构造函数将具有如下原型：

```cpp
Person(Person &&tmp);
```

然而，该构造函数的以下实现是错误的：

```cpp
Person::Person(Person &&tmp);
```

# 第9章：类与内存分配

```cpp
d_name(tmp.d_name),
d_address(tmp.d_address)
{}
```

调用`string`的拷贝构造函数而不是`string`的移动构造函数是不准确的。如果你在想知道为什么会发生这种情况，请记住移动操作只对匿名对象执行。对于编译器来说，任何带有名称的东西都不是匿名的。因此，隐含地，拥有值引用并不意味着我们正在引用一个匿名对象。但我们知道移动构造函数只为匿名参数调用。为了使用相应的移动操作，我们必须告诉编译器我们也在讨论匿名数据成员。对于这种情况，可以使用（例如`static_cast<Person &&>(tmp)`），但因此C++03标准的移动构造如下：

```cpp
Person::Person(Person &&tmp)
d_name(std::move(tmp.d_name)),
d_address(std::move(tmp.d_address))
{}
```

`std::move`函数被许多头文件（间接地）调用。如果没有头文件已经声明`std::move`，则使用`std::utility::`。

当使用组合时，不仅是类类型数据成员，还有其他类型的数据（指针、基本数据类型），那么这些其他数据类型可以像往常一样初始化。基本数据类型可以拷贝；引用可以像往常一样初始化，指针可以像上一节讨论的那样使用移动操作。

编译器永远不会为不同的名称调用移动操作。让我们通过下一个例子来考虑它的影响，假设类`Class`提供了一个移动构造函数和一个拷贝构造函数：

```cpp
Class factory();
void fun(Class const &other);
void fun(Class &&tmp);
void callee(Class &&tmp)
{
    fun(tmp);
}
int main()
{
    callee(factory());
}
```

- 在1处调用了一个函数。乍看这可能令人惊讶，但`fun`的参数不是一个匿名对象，而是一个命名的临时对象。

意识到`fun(tmp)`可能会被调用两次，编译器的选择是可以理解的。如果`tmp`的数据在第一次调用时被获取，第二次调用将收到没有任何数据的`tmp`。

但在最后一次调用时，我们可能知道`tmp`不再被使用，因此我们可能希望确保调用`fun(Class &&)`。为此，再次使用了`std::move`：

```cpp
fun(std::move(tmp));
```

### 9.7.3 移动赋值

除了重载的赋值运算符外，支持移动操作的类还可以实现移动赋值运算符。在这种情况下，如果类支持交换（swap），实现将出奇地简单。不需要拷贝构造，移动赋值运算符可以简单地实现：

```cpp
Class &operator=(Class &&tmp)
{
  swap(tmp);
  return *this;
}
```

如果不支持交换，则可以逐个对每个数据成员执行赋值，如上一节在类中所示使用`std::move`。这里是一个显示如何对`Person`类这样做的示例：

```cpp
Person &operator=(Person &&tmp)
{
  d_name = std::move(tmp.d_name);
  d_address = std::move(tmp.d_address);
  return *this;
}
```

如之前（9.7.1）所述，声明移动赋值运算符会抑制拷贝构造函数的默认可用性。它通过在类的接口中声明拷贝构造函数变为可用（当然也可以通过提供显式实现或使用`= default`）。

### 9.7.4 修订赋值运算符（第二部分）

现在我们已经熟悉了重载的赋值运算符和移动赋值，让我们再次回到它们对`Class`类的实现，通过其成员支持交换。这里是重载赋值运算符的通用实现：

```cpp
Class &operator=(Class const other)
{
  Class tmp(other);
  swap(tmp);
```
