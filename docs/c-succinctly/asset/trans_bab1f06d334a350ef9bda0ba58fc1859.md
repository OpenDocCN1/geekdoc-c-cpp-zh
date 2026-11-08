
# 如何使用 RAII？

RAII 的用途从其名称即可看出：获取动态资源应当完成对象的初始化。如果遵循这种每对象一资源的模式，那么就不可能最终出现资源泄漏。要么你成功获取资源，此时封装该资源的对象将完成构造并会被销毁；要么获取尝试失败，此时你并未获取资源，因此没有资源需要释放。

封装资源的对象的析构函数必须释放该资源。除其他原因外，这也是析构函数绝不应抛出异常（除非它们自行捕获并处理）的重要原因之一。

如果析构函数抛出了未捕获的异常，那么引用本贾尼·斯特劳斯特鲁普的话来说，“各种糟糕的事情都可能发生，因为标准库和语言本身的基本规则将遭到违反。不要这样做。”

正如他所说，*不要这样做*。要确保你知道析构函数中调用的所有内容可能抛出哪些异常（如果有的话），以便确保正确处理它们。

现在你可能会想，如果遵循这种模式，最终会编写大量类。你偶尔会在这里或那里额外写一个类，但由于智能指针的存在，你不太可能写太多类。智能指针也是对象。大多数类型的动态资源都可以放入至少一种现有智能指针类中。当你将资源获取放入合适的智能指针中时，如果获取成功，那么该智能指针对象将完整构造。如果发生异常，则会调用该智能指针对象的析构函数，资源将被释放。

有几种重要的智能指针类型。我们来看看它们。

## `std::unique_ptr`

唯一指针 `std::unique_ptr` 旨在持有指向动态分配对象的指针。仅当希望该对象只存在一个指针时，才应使用此类型。它是一个模板类，接受一个必需模板实参和一个可选模板实参。必需实参是它将持有的指针类型。例如，`auto result = std::unique_ptr<int>(new int());` 将创建一个包含 `int*` 的唯一指针。可选实参是删除器的类型。我们将在后续示例中了解如何编写删除器。通常可以避免指定删除器，因为如果未指定删除器，就会为你提供 `default_deleter`，它几乎涵盖你能想象到的所有情况。

以 `std::unique_ptr` 作为成员变量的类不能有默认复制构造函数。`std::unique_ptr` 的复制语义被禁用。如果希望在有唯一指针的类中提供复制构造函数，就必须自己编写。还应编写复制运算符的重载。通常在这种情况下，你需要的是 `std::shared_ptr`。

然而，你可能拥有类似数据数组的东西。你还可能希望该类的任何副本都创建当时存在的数据副本。在这种情况下，带有自定义复制构造函数的唯一指针可能是正确选择。

`std::unique_ptr` 定义在 `<memory>` 头文件中。

`std::unique_ptr` 有四个值得关注的成员函数。

`get` 成员函数返回存储的指针。如果需要调用某个函数并向其传递所含指针，可使用 `get` 获取该指针的副本。

release 成员函数也返回存储的指针，但 release 在此过程中通过将存储的指针替换为空指针来使 unique_ptr 失效。如果你有一个函数，希望创建动态对象然后返回它，同时仍保持异常安全，那么可以使用 std::unique_ptr 存储动态创建的对象，然后返回调用 release 的结果。这样既提供了异常安全，又允许你返回动态对象，而不会在末尾返回 release 得到的指针值、控制流退出函数时，让 std::unique_ptr 的析构函数销毁它。

swap 成员函数允许两个唯一指针交换它们存储的指针，因此如果 A 持有指向 X 的指针，B 持有指向 Y 的指针，调用 A::swap(B); 的结果是 A 现在持有指向 Y 的指针，B 持有指向 X 的指针。各自的删除器也会被交换，因此如果你为任一或两个唯一指针设置了自定义删除器，请放心，每个唯一指针都会保留其关联的删除器。

reset 成员函数在大多数情况下会销毁存储指针所指向的对象（如果有）。如果当前存储的指针为空，则不会销毁任何内容。如果传入一个指向当前存储指针所指向对象的指针，则不会销毁任何内容。可以选择传入新指针、nullptr，或不带参数调用该函数。如果传入新指针，则存储该新对象。如果传入 nullptr，则唯一指针将存储空值。不带参数调用该函数与传入 nullptr 调用它相同。

## `std::shared_ptr`

共享指针 std::shared_ptr 旨在持有指向动态分配对象的指针，并为其维护引用计数。它并非魔法；如果创建两个共享指针，并分别向它们传入指向同一对象的指针，最终会得到两个共享指针——每个的引用计数都是 1，而不是 2。先被销毁的那个会释放底层资源，当你尝试使用另一个，或另一个被销毁并试图释放已经释放的底层资源时，就会产生灾难性结果。

要正确使用共享指针，先用对象指针创建一个实例，然后基于该对象已有的有效共享指针，为该对象创建所有其他共享指针。这可确保共用同一个引用计数，从而使资源具有正确的生命周期。我们来看一个简短示例，了解创建 shared_ptr 对象的正确与错误方式。

**示例：SharedPtrSample\\SharedPtrSample.cpp**

```cpp
#include <memory>
#include <iostream>
#include <ostream>
#include "../pchar.h"

using namespace std;

struct TwoInts
{
        TwoInts(void) : A(), B() { }
        TwoInts(int a, int b) : A(a), B(b) { }
        int A;
        int B;
};

wostream& operator<<(wostream& stream, TwoInts* v)
{
        stream << v->A << L" " << v->B;
        return stream;
}
```

```cpp
int _pmain(int /*argc*/, wchar* /*argv*/[])
{
    /// Bad: results in double free.
    //try
    //{
    //    TwoInts* p_i = new TwoInts(10, 20);
    //
    //    auto sp1 = shared_ptr<TwoInts>(p_i);
    //    auto sp2 = shared_ptr<TwoInts>(p_i);
    //    p_i = nullptr;
    //
    //    wcout << L"sp1 count is " << sp1.use_count() << L"," << endl <<
    //        L"sp2 count is " << sp2.use_count() << L"." << endl;
    //}
    //catch(exception& e)
    //{
    //    wcout << L"There was an exception." << endl;
    //    wcout << e.what() << endl << endl;
    //}
    //catch(...)
    //{
    //    wcout << L"There was an exception due to a double free " <<
    //        L"because we tried freeing p_i twice!" << endl;
    //}

    // This is one right way to create shared_ptrs.
    {
        auto sp1 = shared_ptr<TwoInts>(new TwoInts(10, 20));
        auto sp2 = shared_ptr<TwoInts>(sp1);

        wcout << L"sp1 count is " << sp1.use_count() << L"," << endl <<
            L"sp2 count is " << sp2.use_count() << L"," << endl;

        wcout << L"sp1 value is " << sp1 << L"," << endl <<
            L"sp2 value is " << sp2 << L"." << endl;
    }

    // This is another right way. The std::make_shared function takes the
    // type as its template argument, and then the arguments (values) to the
    // constructor you want as its parameters, and it automatically
    // constructs the object for you. This is usually more memory-
    // efficient, as the reference count can be stored with the
    // shared_ptr's pointed-to object at the time of the object's creation.
    {
        auto sp1 = make_shared<TwoInts>(10, 20);
        auto sp2 = shared_ptr<TwoInts>(sp1);

        wcout << L"sp1 count is " << sp1.use_count() << L"," << endl <<
            L"sp2 count is " << sp2.use_count() << L"," << endl;

        wcout << L"sp1 value is " << sp1 << L"," << endl <<
            L"sp2 value is " << sp2 << L"." << endl;
    }

    return 0;
}
```
