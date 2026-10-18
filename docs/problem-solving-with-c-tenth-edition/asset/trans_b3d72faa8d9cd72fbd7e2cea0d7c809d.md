

所有在异常规范中列出的异常类型都被正常处理。当我们说异常被正常处理时，我们的意思是它被当作我们在本小节之前描述的那样处理。特别是，你可以将函数调用放在 try 块后跟一个 catch 块来捕获该类型的异常，并且如果函数抛出异常（并且在函数内部没有捕获它），那么跟在 try 块之后的 catch 块将捕获该异常。如果完全没有异常规范（没有 throw 列表，甚至没有空的），那么它就相当于所有可能的异常类型都被列在异常规范中；也就是说，抛出的任何异常都被正常处理。

如果在函数中抛出异常但未列在异常规范中（并且在函数内部未捕获）会发生什么？在这种情况下，程序结束。特别是要注意，如果在函数中抛出异常但未列在异常规范中（并且在函数内部未捕获），那么它将不会被任何 catch 块捕获，而是你的程序将结束。记住，如果完全没有规范列表，甚至没有空的，那么它就相当于所有异常都被列在规范列表中，因此按照本段所述抛出异常不会结束程序。

请记住，异常规范是针对“逃出”函数的异常。如果它们没有逃出函数，就不属于异常规范。如果它们逃出函数，就属于异常规范，无论它们起源于何处。如果在函数定义内部的 try 块中抛出异常，并且在函数定义内部的 catch 块中捕获，那么它的类型不必列在异常规范中。如果函数定义包含对另一个函数的调用，而该另一个函数可能抛出未被捕获的异常，那么该异常的类型应放在异常规范中。

要说一个函数不应该抛出在函数内部未被捕获的任何异常，你可以使用空的异常规范，如下所示：

```
void someFunction( ) throw ( );
```

总结如下：

```
void someFunction( ) throw (DivideByZero, OtherException);
//Exceptions of type DivideByZero or OtherException are
//treated normally. All other exceptions end the program
//if not caught in the function body.
```

```
void someFunction( ) throw ( );
//Empty exception list; all exceptions end the
//program if thrown but not caught in the function body.
```

```
void someFunction( );
//All exceptions of all types treated normally.
```

请记住，派生类的对象¹也是其基类的对象。因此，如果 D 是类 B 的派生类并且 B 在异常规范中，那么抛出类 D 的对象将被正常处理，因为它是类 B 的对象并且 B 在异常规范中。然而，不会自动进行类型转换。如果 double 在异常规范中，这并不能说明抛出 int 值。你需要在异常规范中同时包含 int 和 double。

最后警告：并非所有编译器都按应有的方式处理异常规范。一些编译器本质上将异常规范视为注释，因此对于这些编译器，异常规范对你的代码没有影响。这也是将你的函数可能抛出的所有异常都放在异常规范中的另一个原因。这样所有编译器都会以相同的方式处理你的异常。当然，你也可以通过完全不使用异常规范来获得相同的编译器一致性，但那样你的程序就不会得到很好的文档化，并且你也不会获得使用异常规范的编译器提供的额外错误检查。有异常规范处理的编译器，你的程序将在抛出你未预料到的异常时立即终止。 （请注意，这是一种运行时的行为，但你得到的运行时行为取决于你的编译器。）

警告！

## PITFALL Exception Specification in Derived Classes

当你在派生类中重新定义或覆盖函数定义时，它应具有与基类中相同的异常规范，或者它应具有异常规范，其异常是基类异常规范的子集。换句话说，当你重新定义或覆盖函数定义时，你不能向异常规范添加任何异常（但如果你愿意可以删除一些异常）。这是有道理的，因为派生类的对象可以在基类的对象可以使用的任何地方使用，因此重新定义或覆盖的函数必须适合为基类的对象编写的任何代码。

## SELF-TEST EXERCISES

8. 以下程序产生的输出是什么？

```
#include <iostream>
using namespace std;
void sampleFunction(double test) throw (int);
```

¹ 如果你尚未学习派生类，可以安全地忽略关于它们的说明。

```
int main()
{
    try
    {
        cout << "Trying.\n";
        sampleFunction(98.6);
        cout << "Trying after call.\n";
    }
    catch(int)
    {
        cout << "Catching.\n";
    }
    cout << "End of program.\n";
    return 0;
}
void sampleFunction(double test) throw (int)
{
    cout << "Starting sampleFunction.\n";
    if (test < 100)
        throw 42;
}
```

9. 如果对自我测试练习 8 中的程序进行以下更改，产生的输出是什么？将 try 块中的
sampleFunction(98.6);
更改为
sampleFunction(212);

## 16.2 PROGRAMMING TECHNIQUES FOR EXCEPTION HANDLING

> Only use this in exceptional circumstances.
> 
> WARREN PEACE, The Lieutenant's Tools

到目前为止，我们向你展示了大量解释 C++ 中异常处理如何工作的代码，但我们还没有展示甚至一个对异常处理进行良好且现实使用的程序示例。然而，现在你已经了解了异常处理的机制，本节可以继续解释异常处理技术。

### When to Throw an Exception

我们给出了一些非常简单的代码来说明异常处理的基本概念。然而，我们的例子是不切实际的简单。更复杂但更好的指导原则是将抛出异常和捕获异常分离到不同的函数中。在大多数情况下，你应该在函数定义中包含任何 *throw* 语句，将异常列在该函数的异常规范中，并在 *不同的函数* 中放置 *catch* 子句。因此，*try-throw-catch* 三元组的首选用法如下所示：

```
```cpp
void functionA() throw (MyException)
{
    .
    .
    .
    throw MyException(<Maybe an argument>);
    .
    .
    .
}
```
```

然后，在 *某个其他函数* 中（甚至可能是某个其他文件中的某个其他函数），你有

```
```cpp
void functionB()
{
    .
    .
    try
    {
        .
        .
        .
        functionA();
        .
        .
        .
    }
    catch(MyException e)
    {
        <Handle exception>
    }
    .
    .
    .
}
```
```

而且，即使这种 *throw* 语句的使用也应保留在不可避免的情况下。如果你可以用其他方式轻松处理问题，就不要抛出异常。保留 *throw* 语句用于异常情况的处理方式取决于函数如何以及在何处使用。如果异常情况的处理方式取决于函数如何以及在何处被调用，那么最好的

### When to Throw an Exception

在很大程度上，*throw* 语句应在使用函数内部并列在函数的异常规范中。而且，它们应保留在异常情况的处理方式取决于函数如何以及在何处使用时。如果异常情况的处理方式取决于函数如何以及在何处被调用，那么最好的做法是让调用该函数的程序员处理异常。在所有其他情况下，避免抛出异常几乎总是更可取的。

做法是让调用该函数的程序员处理异常。在所有其他情况下，避免抛出异常几乎总是更可取的。

## PITFALL Uncaught Exceptions

你的代码抛出的每个异常都应在你的代码中的某个地方被捕获。如果抛出异常但在任何地方都没有被捕获，你的程序将结束。

## PITFALL Nested *try-catch* Blocks

你可以在更大的 *try* 块内部或更大的 *catch* 块内部放置 *try* 块和随后的 *catch* 块。在极少数情况下，这可能是有用的，但如果你想这样做，你应该怀疑存在更优雅的方式来组织你的程序。几乎总是更好将内部的 *try-catch* 块放在函数定义内部，并在外部的 *try* 或 *catch* 块中放置对该函数的调用（或者也许完全消除一个或多个 *try* 块）。

如果你将 *try* 块和随后的 *catch* 块放在更大的 *try* 块内部，并且在内部 *try* 块中抛出异常但未在内部 *try-catch* 块中捕获，那么异常将被抛出到外部 *try* 块进行处理，并且可能在那里被捕获。

## PITFALL Overuse of Exceptions

异常允许你编写控制流如此复杂以至于几乎不可能理解程序的代码。而且，这并不难做到。抛出异常允许你将控制流从

