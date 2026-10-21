

```cpp
void ExGen()
{
    cout << "Inside the function \n";
    cout << "Inside try block\n";
    cout << "Assuming error and throwing exception now\n";
    MyException Error1(20, "Error testing");
    throw Error1;
    cout << "This statement will not be executed";
}

void main()
{
    try
    {
        cout << "Inside main\n";
        ExGen(); // This would generate exception
        cout << "This will not be executed";
    }
    catch (MyException Except)
    {
        cout << "Inside main catch \n";
        Except.ShowEx();
    }
}
```

## How the Program Works

该程序与程序 8.1 几乎没有区别。之前，异常的生成和抛出发生在 main 中，而现在它们是 ExGen() 函数的一部分。匹配的 catch 在 main 中而不是函数本身。当 ExGen() 使用 throw Error1; 抛出异常时，它不会在 ExGen() 中被捕获。它向上层传递到 main 去寻找匹配的 catch。幸运的是，它找到了一个匹配的 catch 并执行它。main 的剩余语句将不会被执行。在执行完 catch 块后，main 立即退出。

## Catching an Exception by a Caller Function

该程序可以稍作修改，如程序 8.3 所示，以了解在其他地方寻找匹配如何改变场景。

## PROGRAM 8.3 Catching up in the hierarchy

```cpp
//CatchInHierarchy.cpp
#include <iostream>
#include <string>
using namespace std;

class MyException
{
private:
    int ExNumber;
    string ExMessage;
public:
    MyException(int ErrNo, string Description)
{
    ExNumber = ErrNo;
    ExMessage = Description;
}

void ShowEx()
{
    cout << "Error number is" << ExNumber << "\n";
    cout << ExMessage << "\n";
};
/* Function generating exception as well as catching */
void ExGen()
{
    cout << "Inside the function \n";
    cout << "Inside try block\n";
    cout << "Assuming error and throwing exception now\n";
    MyException Error1(20, "Error testing");
    throw Error1;
    cout << "This statement will not be executed";
}
// Exception is caught in this block
void TestGen()
{
    try
    {
        cout << "Inside TestGen\n";
        ExGen();  // This would generate exception
        cout << "This will not be printed";
    }
    /* When an exception is thrown, the remaining statements of that function will not be executed, as the control gets permanently transferred to the catch block */
    catch (MyException Except)
    {
        cout << "Inside main catch \n";
        Except.ShowEx();
    }
}
int main()
{
    TestGen();
    cout << "This statement would be printed\n";
    return 0;
}
```

## Output

Inside main
Inside the function
Inside try block
Assuming error and throwing exception now
Inside main catch
Error number is 20
Error testing
This statement would be printed

## Note

按设计，当抛出异常时，控制权会永久转移到 catch 块。这种行为一旦我们了解现实世界问题是如何解决的，就会显得非常合乎逻辑。假设一个库设计者开发了一个图形库，被另一个用户使用。假设用户向图形库发送一个尺寸，而尺寸不正确，那么就没有必要执行剩余语句并继续绘制该对象。

## How the Program Works

## Exceptions thrown

需要注意的是，现在 TestGen() 函数调用了 ExGen() 函数。从 ExGen() 抛出的异常在 TestGen() 中被捕获，因此它正常返回到 main。因此，在 TestGen() 的函数调用结束后，main 的剩余单个语句会执行。还需要注意的是，TestGen() 中的剩余语句不会被执行。

## Separation of reporting from handling

尽管程序 8.2 和 8.3 看起来与程序 8.1 相似，但有一个小的变化。异常的抛出和捕获不再在同一个函数中进行，而是分开进行。虽然这似乎是一个简单的改变，但考虑到错误报告和处理部分的分离，这是一个很大的改变。在程序 8.2 和 8.3 中，抛出发生在 ExGen() 中，而捕获分别发生在 main 和 TestGen() 中。

## Inability of designer to provide appropriate messages

ExGen() 可以在抛出异常的各种情况下使用。可以在程序中为每种情况在 catch 语句中编写适当的错误消息。这里，ExGen() 是一个非常简单的函数，几乎什么都不做，但在实际情况下，它可能会执行许多操作以在特定错误发生时恢复到稳定状态。

例如，假设存在一个全局可用的大数组，并且 ExGen() 被设计为在用户请求时在数组中分配一些内存。数组的那部分可能用于在调用程序中存储信息。理解 ExGen() 是一个通用函数，供多个对象使用，并且在不同位置由不同对象用于存储不同类型的对象。有人可能会使用 ExGen() 来存储 Employee 对象，另一个人可能会使用它来存储学生的成绩，等等。虽然 ExGen() 数组的尺寸很大，但它不是无限的，因此在某个时间点可能会耗尽内存。在那时，而不是在数组中提供空间，ExGen() 会抛出 NotEnoughMemory 异常。

假设 ExGen() 用于在 main 中为员工对象分配内存，其中捕获 NotEnoughMemory 异常，可以显示消息“创建的员工对象太多，无法再创建”，这很容易理解。假设错误消息在 ExGen() 本身中提供，那么它将类似于“数组中没有剩余空间”。ExGen() 对员工对象没有任何概念，因此它无法像 main() 函数那样精确。

## Note

ExGen() 对员工数组一无所知有两个原因。库设计者不知道该数组将如何使用，也不知道哪个用户会存储什么信息在数组中。其次，即使用户知道库的用途，也没有方法可以为特定用途打印选择性消息。考虑使用航空航天设计程序和建筑师使用此库的情况。当要打印超出尺寸的消息时，库设计者会更倾向于打印什么？在给出的示例中，用户肯定更希望看到“员工对象太多”而不是“数组中没有剩余空间”。

## Solution

在这种情况下，传递异常更好。ExGen() 函数不是打印消息，而是将异常传递给调用者，调用者决定如何处理该异常，因为它肯定处于更有利的位置来打印更用户友好的消息。可以说，库设计者将该消息传递给用户，用户打印适当的<|message|>消息。如果稍后将相同的 ExGen() 用于获取课程中注册学生的内存，则可以在异常发生时显示适当的消息。因此，这种方法也更灵活。

异常处理比错误处理更结构化。如果为 ExGen() 函数提供错误代码，描述可能无法直接从函数中获得；它可能需要从其他地方获得。此外，已知错误代码不是标准化的。没有了解错误代码值和每个错误代码含义的人将无法使用 ExGen() 函数。

在这两种情况下，异常处理都是更有序且可接受的形式。然而，它可能会使效率和性能水平下降几个档次。参考第 8.15 节，了解当包含异常处理时程序的性能如何受到影响。

## 8.6.1 Handling Exceptions

当 catch 与抛出内容匹配时，它可以匹配以下任何一种：

- 1. 一个精确的类型
- 2. 一个派生自 catch 语句所用类型的类型，因此如果提供 catch (base) 且执行 throw derived，则会被捕获。
- 3. 一个 void 指针，它与任何指针匹配。因此，catch (void *) 与 throw 语句抛出的任何指针匹配。

可以把一个 try 块写在另一个 try 块内部。如果在 try 块内部未捕获抛出的异常，则会传递给外部 try 块。假设我们有以下代码

```
try
{
    try
    {
        MyException Something;
        throw Something;
    }
    catch (AnotherException AE)
    {
        Body of the catch block
    }
}

catch (MyException ME)
{
    // This is where Something is handled
}
```

这里，Something 并未在同一个 try 块中处理；而是在外部 try 块中处理。如果它未在外部 try 块中处理，则会像其他异常一样处理。它会被传递给调用函数，然后传递给调用函数的调用函数，依此类推，直到被捕获或到达 main 之外，此时会调用 terminate()。

