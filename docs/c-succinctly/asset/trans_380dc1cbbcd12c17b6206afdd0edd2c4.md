
```cpp
public:
        inline InvalidArgumentException(
                const char* className,
                const char* functionSignature,
                const char* parameterName,
                T parameterValue
        );

        inline virtual ~InvalidArgumentException(void) throw();

        inline virtual const char* what(void) const throw() override;

private:
        std::string m_whatMessage;
};

template<class T>
InvalidArgumentException<T>::InvalidArgumentException(
        const char* className,
        const char* functionSignature,
        const char* parameterName,
        T parameterValue) : InvalidArgumentExceptionBase(),
        m_whatMessage()
{
        std::stringstream msg;
        msg << className << "::" << functionSignature <<
                " - parameter '" << parameterName << "' had invalid value '" <<
                parameterValue << "'.";
        m_whatMessage = std::string(msg.str());
}

template<class T>
InvalidArgumentException<T>::~InvalidArgumentException(void) throw()
{ }

template<class T>
const char* InvalidArgumentException<T>::what(void) const throw()
{
        return m_whatMessage.c_str();
}
```

# 示例：ExceptionsSample\ExceptionsSample.cpp

```cpp
#include <iostream>
#include <ostream>
#include <exception>
#include <stdexcept>
#include <typeinfo>
#include <algorithm>
#include <cstdlib>
#include "InvalidArgumentException.h"
#include "../pch.h"

using namespace CppForCsExceptions;
using namespace std;

class ThrowClass
{
public:
    ThrowClass(void)
        : m_shouldThrow(false)
    {
        wcout << L"Constructing ThrowClass." << endl;
    }

    explicit ThrowClass(bool shouldThrow)
        : m_shouldThrow(shouldThrow)
    {
        wcout << L"Constructing ThrowClass. shouldThrow = "
              << (shouldThrow ? L"true." : L"false.") << endl;

        if (shouldThrow)
        {
            throw InvalidArgumentException<const char*>(
                "ThrowClass",
                "ThrowClass(bool shouldThrow)",
                "shouldThrow",
                "true"
            );
        }
    }

    ~ThrowClass(void)
    {
        wcout << L"Destroying ThrowClass." << endl;
    }

    const wchar_t* GetShouldThrow(void) const
    {
        return (m_shouldThrow ? L"True" : L"False");
    }

private:
    bool          m_shouldThrow;
};

class RegularClass
{
public:
    RegularClass(void)
    {
        wcout << L"Constructing RegularClass." << endl;
    }

    ~RegularClass(void)
    {
        wcout << L"Destroying RegularClass." << endl;
    }
};

class ContainStuffClass
{
public:
    ContainStuffClass(void) :
        m_regularClass(new RegularClass()),
        m_throwClass(new ThrowClass())
    {
        wcout << L"Constructing ContainStuffClass." << endl;
    }

    ContainStuffClass(const ContainStuffClass& other) :
        m_regularClass(new RegularClass(*other.m_regularClass)),
        m_throwClass(other.m_throwClass)
    {
        wcout << L"Copy constructing ContainStuffClass." << endl;
    }

    ~ContainStuffClass(void)
    {
        wcout << L"Destroying ContainStuffClass." << endl;
    }

    const wchar_t* GetString(void) const
    {
        return L"I'm a ContainStuffClass";
    }

private:
    unique_ptr<RegularClass>        m_regularClass;
    shared_ptr<ThrowClass>          m_throwClass;
};

void TerminateHandler(void)
{
    wcout << L"Terminating due to unhandled exception." << endl;

    // If you call abort (from <cstdlib>), the program will exit
    // abnormally. It will also exit abnormally if you do not call
    // anything to cause it to exit from this method.
    abort();

    /// If you were instead to call exit(0) (also from <cstdlib>),
    /// then your program would exit though nothing had
    /// gone wrong. This is bad because something did go wrong.
    /// I present this so you know that it is possible for
    /// a program to throw an uncaught exception and still
    /// exit in a way that isn't interpreted as a crash, since
    /// you may need to find out why a program keeps abruptly
    /// exiting yet isn't crashing. This would be one such cause
    /// for that.
    ///exit(0);
}

int wmain(int /*argc*/, wchar_t* /*argv*/[])
{
    // Set a custom handler for std::terminate. Note that this handler
    // won't run unless you run it from a command prompt. The debugger
    // will intercept the unhandled exception and will present you with
    // debugging options when you run it from Visual Studio.
    set_terminate(&TerminateHandler);

    try
    {
        ContainStuffClass csc;
        wcout << csc.GetString() << endl;

        ThrowClass tC(false);
        wcout << L"tC should throw? " << tC.GetShouldThrow() << endl;

        tC = ThrowClass(true);
        wcout << L"tC should throw? " << tC.GetShouldThrow() << endl;
    }
    // One downside to using templates for exceptions is that you need a
    // catch handler for each specialization, unless you have a base
    // class they all inherit from, that is. To avoid catching
    // other std::invalid_argument exceptions, we created an abstract
    // class called InvalidArgumentExceptionBase, which serves solely to
    // act as the base class for all specializations of
    // InvalidArgumentException<T>. Now we can catch them all, if desired,
    // without needing a catch handler for each. If you wanted to, however,
    // you could still have a handler for a particular specialization.
    catch (InvalidArgumentExceptionBase& e)
    {
        wcout << L"Caught '" << typeid(e).name() << L"'." << endl <<
            L"Message: " << e.what() << endl;
    }
    // Catch anything derived from std::exception that doesn't already
    // have a specialized handler. Since you don't know what this is, you
    // should catch it, log it, and re-throw it.
    catch (std::exception& e)
    {
        wcout << L"Caught '" << typeid(e).name() << L"'." << endl <<
            L"Message: " << e.what() << endl;
        // Just a plain throw statement like this is a re-throw.
        throw;
    }
    // This next catch catches everything, regardless of type. Like
    // catching System.Exception, you should only catch this to
    // re-throw it.
    catch (...)
    {
        wcout << L"Caught unknown exception type." << endl;
        throw;
    }

    // This will cause our custom terminate handler to run.
    wcout << L"tC should throw? " <<
        ThrowClass(true).GetShouldThrow() << endl;

    return 0;
}
```

虽然我在注释中提到了这一点，但我想再次指出，除非你从命令提示符运行此示例，否则你不会看到自定义终止函数运行。如果你在 Visual Studio 中运行它，调试器会拦截程序，并在给你机会检查状态以确定哪里出错之后，自行安排程序终止。另外，请注意该程序总是会崩溃。这是有意为之，因为它让你看到终止处理程序的实际运行。

# 第7章 指针、引用和常量正确性

## 指针概述

指针无非是一个保存内存地址的变量。如果使用得当，指针保存的是一个有效内存地址，该地址包含一个与指针类型兼容的对象。与 C++ 中的引用类似，在特定执行环境中，所有指针都具有相同的大小，无论指针指向的数据类型是什么。例如，当程序为 32 位操作系统编译并运行时，指针通常为 4 字节（32 位）。

指针可以指向任何内存地址。你可以（而且经常会有）指向栈上对象的指针。你也可以有指向静态对象、线程局部对象，以及当然还有动态（即堆分配）对象的指针。那些对指针只是略有了解的程序员在想到指针时，通常是在动态对象的上下文中。

由于可能发生泄漏，你绝不应在智能指针之外分配动态内存。C++ 标准库提供了两种你应该考虑的智能指针：`std::shared_ptr` 和 `std::unique_ptr`。

通过将动态存储期对象放入其中一种智能指针，你可以保证当 `std::unique_ptr` 或包含指向该内存的指针的最后一个 `std::shared_ptr` 超出作用域时，内存将使用正确的 delete 版本（delete 或 `delete[]`）被正确释放，从而不会泄漏。这就是上一章中 RAII 模式的实际应用。

当你用智能指针正确实现 RAII 时，只可能发生两种情况：分配成功，因此当智能指针超出作用域时内存将被正确释放；或者分配失败，在这种情况下没有分配内存，因此也没有泄漏。实际上，最后一种情况在现代 PC 和服务器上应该相当罕见，因为它们拥有大内存并提供虚拟内存。

如果你不使用智能指针，那你就是在自找内存泄漏。在用 `new` 或 `new[]` 分配内存与用 `delete` 或 `delete[]` 释放内存之间出现的任何异常，都很可能导致内存泄漏。如果你不小心，你可能会意外地使用一个已经被删除但未被设置为 `nullptr` 的指针。然后你会访问内存中的某个随机位置，并将其当作有效指针来使用。

在那种情况下，最好的结果就是程序崩溃。如果没有崩溃，那么你就在以奇怪、未知的方式破坏数据，并可能将这些损坏的数据保存到数据库或通过网络传输。你也可能为安全问题敞开大门。所以请使用智能指针，让语言为你处理内存管理问题。

## 常量指针

常量指针的形式为 `SomeClass* const someClass2 = &someClass1;`。换句话说，`*` 位于 const 之前。结果是指针本身不能指向其他任何东西，但指针所指向的数据保持可变。在大多数情况下，这不太可能非常有用。

## 指向常量的指针

指向常量的指针的形式为 `const SomeClass* someClass2 = &someClass1;`。在这种情况下，`*` 位于 const 之后。结果是指针可以指向其他东西，但你不能修改它所指向的数据。这是一种常见的方式，用于声明你只想检查而不修改其数据的参数。

