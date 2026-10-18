

正如我们在本小节开头所指出的，类 `StringVar` 是使用动态数组实现的。实现显示在 Display 11.12 中。当声明一个类型为 `StringVar` 的对象时，会调用构造函数来初始化该对象。构造函数使用 *new* 运算符为成员变量 `value` 创建一个新的字符动态数组。字符串值以普通字符串值的形式存储在数组 `value` 中，并使用 `\0` 来标记字符串的结束。请注意，该数组的大小并不是在声明对象之前就确定的，而是在对象被声明时，构造函数被调用，并且构造函数的参数决定了动态数组的大小。如 Display 11.11 所示，该参数可以是类型为 `int` 的变量。查看函数 `conversation` 定义中对象 `yourName` 的声明。构造函数的参数是传值参数 `maxNameSize`。请回忆，传值参数是一个局部变量，因此 `maxNameSize` 是一个变量。任何 `int` 变量都可以用这种方式作为构造函数的参数。

成员函数 `length`、`input_line` 以及重载的输出运算符 `<<` 的实现都很直接。在接下来的几个小节中，我们将讨论函数 `~StringVar` 和标记为 *Copy constructor* 的构造函数。

## Destructors

动态变量有一个问题。它们不会自行消失，除非你的程序对 `delete` 进行了合适的调用。即使动态变量是使用局部指针变量创建的，并且局部指针变量在函数调用结束时消失，动态变量仍会保留，除非有对 `delete` 的调用。如果你不使用对 `delete` 的调用来消除动态变量，它们将继续占用内存空间，这可能会导致你的程序因耗尽 freestore 中的所有内存而中止。此外，如果动态变量嵌入在类的实现中，使用该类的程序员并不知道动态变量的存在，也不能期望他执行对 `delete` 的调用。事实上，由于数据成员通常是私有成员，程序员通常 *无法* 访问所需的指针变量，因此 *无法* 使用这些指针变量调用 `delete`。为了解决这个问题，C++ 有一种特殊的成员函数，称为 *destructor*。

**destructor** 是在类的对象超出作用域时自动调用的成员函数。这意味着如果你的程序包含一个局部变量，该局部变量是一个具有析构函数的对象，那么当函数调用结束时，析构函数会自动被调用。如果析构函数定义正确，析构函数会调用 `delete` 来消除对象创建的所有动态变量。这可能只需要一次对 `delete` 的调用，也可能需要多次对 `delete` 的调用。你可能还希望析构函数执行其他一些清理工作，但将内存返回 freestore 是析构函数的主要任务。

![](img/88b1f375f11336dbd9dac8b1675d0698_707_0.png)

成员函数 ~StringVar 是 Display 11.11 中显示的类 StringVar 的析构函数。与构造函数一样，析构函数始终与它所属的类具有相同的名称，但析构函数在其名称开头带有波浪号符号 ~，以便你可以区分它是析构函数而不是构造函数。与构造函数一样，析构函数没有返回值的类型，甚至不是 void 类型。析构函数没有参数。因此，一个类只能有一个析构函数；你不能重载类的析构函数。否则，析构函数就像任何其他成员函数一样定义。

请注意 Display 11.12 中给出的析构函数 ~StringVar 的定义。~StringVar 调用 delete 来消除成员指针变量 value 所指向的动态数组。再次查看 Display 11.11 中显示的示例程序中的函数 conversation。局部变量 yourName 和 ourName 都创建了动态数组。如果这个类没有析构函数，那么在对 conversation 的调用结束后，这些动态数组仍会占用内存，即使它们对程序已无用。这在这里不是问题，因为示例程序在完成对 conversation 的调用后不久就结束了；但如果你编写了一个程序，反复调用 conversation 之类的函数，并且如果类 StringVar 没有合适的析构函数，那么函数调用可能会消耗 freestore 中的所有内存，你的程序随后会异常结束。

## DISPLAY 11.12 Implementation of StringVar (part 1 of 2)

```
//This is the implementation of the class StringVar.
//The definition for the class StringVar is in Display 11.11.
#include <cstdlib>
#include <cstddef>
#include <cstring>

//Uses cstddef and cstdlib:
StringVar::StringVar(int size) : maxLength(size)
{
   value = new char[maxLength + 1];//+1 is for '\0'.
   value[0] = '\0';
}

//Uses cstddef and cstdlib:
StringVar::StringVar() : maxLength(100)
{
   value = new char[maxLength + 1];//+1 is for '\0'.
   value[0] = '\0';
}

//Uses cstring, cstddef, and cstdlib:
StringVar::StringVar(const char a[]) : maxLength(strlen(a))
{
   value = new char[maxLength + 1];//+1 is for '\0'.
   (continued)
```

## DISPLAY 11.12 Implementation of StringVar (part 2 of 2)

```
   strcpy(value, a);
}
//Uses cstring, cstddef, and cstdlib:
StringVar::StringVar(const StringVar& stringObject)
   : maxLength(stringObject.length())
{
   value = new char[maxLength + 1];//+1 is for '\0'.
   strcpy(value, stringObject.value);
}
StringVar::~StringVar()
{
   delete [] value;
}
//Uses cstring:
int StringVar::length() const
{
   return strlen(value);
}
//Uses iostream:
void StringVar::inputLine(istream& ins)
{
   ins.getline(value, maxLength + 1);
}
//Uses iostream:
ostream& operator <<(ostream& outs, const StringVar& theString)
{
   outs << theString.value;
   return outs;
}
```

## Destructor

析构函数是类的成员函数，当类的对象超出作用域时会自动调用它。在其他事情中，这意味着如果类的对象是函数的局部变量，那么在函数调用结束前的最后一个操作中，析构函数会自动被调用。析构函数用于消除对象已创建的任何动态变量，以便这些动态变量占用的内存被返回到 freestore。析构函数也可以执行其他清理任务。析构函数的名字必须由波浪号符号 ~ 后跟类的名字组成。

## PITFALL Pointers as Call-by-Value Parameters

当传值参数的类型是指针类型时，其行为可能很微妙且麻烦。考虑 Display 11.13 中显示的函数调用。函数 sneaky 中的参数 temp 是一个传值参数，因此它是一个局部变量。当函数被调用时，temp 的值被设置为参数 p 的值，并且函数体被执行。由于 temp 是一个局部变量，对 temp 的任何更改都不应超出函数 sneaky 的范围。特别是，指针变量 p 的值不应被更改。然而，示例对话看起来像是指针变量 p 的值发生了变化。在调用函数 sneaky 之前，*p 的值是 77，而在调用 sneaky 之后，*p 的值是 99。发生了什么？

## DISPLAY 11.13 A Call-by-Value Pointer Parameter (part 1 of 2)

```
//Program to demonstrate the way call-by-value parameters
//behave with pointer arguments.
#include <iostream>
using namespace std;

typedef int* IntPointer;

void sneaky(IntPointer temp);

int main()
{
    IntPointer p;

    p = new int;
    *p = 77;
    cout << "Before call to function *p == "
        << *p << endl;

    sneaky(p);

    cout << "After call to function *p == "
        << *p << endl;

    return 0;
}

void sneaky(IntPointer temp)
{
    *temp = 99;
    cout << "Inside function call *temp == "
        << *temp << endl;
}
```

