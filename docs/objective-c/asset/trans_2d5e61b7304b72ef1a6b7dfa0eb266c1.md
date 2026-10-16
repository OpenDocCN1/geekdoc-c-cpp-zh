

单词 `typedef` 来自 *type definition*，本质上允许你定义自己的类型。将它与结构体结合使用，可以定义一个自定义类型来表示你的结构体。然后你可以在任何原本会使用结构体定义的地方使用这种自定义类型。清单 2.13 显示了 `Point` 结构体示例的 `typedef` 版本。

## Listing 2.13
### Working with point structures and typedefs

```
#import <Foundation/Foundation.h>

// declaring the point structure.
typedef struct
{
    float x;
    float y;
} Point;

int main(int argc, const char *argv[])
{
    // declaring the point variable...
    Point p;
    // assigning values to the struct's members...
    p.x = 20.0;
    p.y = 50.0;

    // ... then to use the point...
    moveCursorToPoint(p);

    return 0;
}
```

正如你所见，只需在 `struct` 关键字前加上 `typedef` 关键字，并将 `struct` 名称移到结构体的末尾，它就能实现一件很神奇的事情；它允许你通过简单地写 Point p 来声明你的 p 变量。本质上，Point 成为了一种一等类型，你可以在任何使用其他类型的地方使用它。

使用 `typedef` 关键字的语法是 `typedef variable-definition new-type-name`。其中 `variable-definition` 是当你使用新类型时要插入的实际类型，而 `new-type-name` 是你在程序中将使用的新类型名称。

由于 typedef 允许你使用更清晰地描述变量中将存储的数据类型的类型名称，因此 typedef 是一种很好的补充，它使你的代码比不使用它们时更具自文档性。我将在第 5 章讨论使用 blocks 时再次提到使用 typedef。

## Using enum

定义自定义数据类型的另一种方法是使用 enum 关键字。Enum 是 enumerated type 的缩写，它允许你创建一个数据类型，该数据类型具有可存储在其中的有限可能值列表。Enums 在 Cocoa 和 Cocoa Touch 中经常用于参数和返回值，其中可能值的列表属于特定的有限集合。

要定义一个 enum，你使用 enum 关键字，后跟你要声明的 enum 的标签，然后后跟 {}，其中包含 enum 的可能值列表，以逗号分隔。清单 2.14 显示了一个 enum 定义。

## Listing 2.14
### Creating an enum

```
enum MyEnum
{
    Value1,
    Value2,
    Value2
};
```

要在代码中使用 enum，你必须声明一个变量的类型为 enum，后跟你在定义 enum 时指定的标签。然后，要为其赋值，你只需使用来自 enum 定义的允许值之一。清单 2.15 显示了如何操作。

## Listing 2.15
### Using an enum

```
enum MyEnum foo;
foo = Value1;

// or for a function
enum MyEnum myFunction();

// as a parameter to a function
void myFunction(enum MyEnum foo);
```

enum 本身的实际值由编译器确定，但它们默认为整数，从第一个值的 0 开始，第二个值为 1，以此类推。你可以通过在 enum 定义中提供该值来强制 enum 为其中一个值分配特定值，如清单 2.16 所示。

## Listing 2.16
### Assigning values to the enum options

```
enum MyEnum
{
    Value1 = 20,
    Value2 = 13,
    Value3 = 155
};
```

当处理期望特定值的遗留代码时，这会很有用。

每次使用 enum 时都输入 enum 会很不方便。因此 enums 可以像结构体一样被 typedef。清单 2.17 显示了如何操作。

## Listing 2.17
### Using typedef with an enum

```
enum MyEnumType
{
    Value1,
    Value2,
    Value3
};
typedef enum MyEnumType MyEnum;

// Now this allows you to type...
MyEnum foo;
foo = Value1;
```

Cocoa 和 Cocoa Touch 大量使用 enums。enum 的好处在于它们允许你在编译时检查以验证传递给你的函数的参数是否为有限集合中的一个值之一。如果不小心传递了错误的值，编译器会生成错误。

## Understanding pointers

我要讨论的第三种变量类型是指针。指针可能是一个难以理解的概念，但幸运的是，在 Objective-C 中，指针的更复杂方面很少使用。然而，理解它们很重要。

回想一下，典型的变量将数据存储在 RAM 中。计算机通过使用 RAM 中的地址来查找变量。比喻地说，如果你能想象一个变量是一个人们（数据）居住的房子，那么房子的街道地址就是该变量的地址。

指针是一个包含另一个变量地址的变量。声明指针类似于声明你要指向的类型的变量，只是声明中还包括指针运算符。指针运算符是星号 (*)。你可以通过使用取地址运算符 (&) 来获取变量的地址。

清单 2.18 显示了声明指向整数的指针的示例。

## Listing 2.18
### Declaring pointers

```
#import <Foundation/Foundation.h>

int main(int argc, char *argv[])
{
    int x = 5;
    int *y = &x;

    NSLog(@"X:%ld - Y:%ld", x, y);
    return 0;
}
```

在这段代码中，你声明了一个变量 x，它是一个 int。在此变量中，你存储了值 5。然后我们声明另一个变量 y，它的类型是指向 int 的指针，并且在其中存储了 x 的地址。

指针可以像普通变量一样使用，但当你直接访问它们时，例如我们在本程序第 8 行所做的那样，你得到的值是一个内存地址。在这种情况下，当你运行此程序时，你应该会看到输出，如图 2.2 所示。

你的 y 值可能与我的不同，因为你的计算机可能将你的 x 值存储在与我不同的地址。这很正常。星号运算符 (*) 也是指针解引用运算符。解引用指针的过程允许你访问指针指向的变量的值。所以换句话说，在你的程序示例中，你想打印白色指针指向的值，换句话说 x 的值，那么你可以重写你的程序使其看起来像清单 2.19。

## Figure 2.2
Output of the pointer program

![](img/aaee977487e7a3eefe7b1dd596e0f6fb_64_0.png)

## Listing 2.19
### Dereferencing pointers

```
#import <Foundation/Foundation.h>

int main(int argc, char *argv[])
{
    int x = 5;
    int *y = &x;

    NSLog(@"X:%ld - Y:%ld", x, *y);
    return 0;
}
```

请注意，我们现在正在解引用 y，这意味着当你运行此应用程序时，你应该会看到类似于图 2.3 的内容。

## Figure 2.3
Output of the dereferencing example code

![](img/aaee977487e7a3eefe7b1dd596e0f6fb_65_0.png)

指针有趣的地方在于它们可以像普通变量一样被操作。这意味着你可以递增它们，可以递减它们，可以加到它们上，也可以从它们中减去。你可以做所有这些事情，但你真正做的是改变指针指向的 RAM 位置。因此，你可以在新位置解引用指针并访问与原来指向位置不同的值。

指针的大部分讨论都是相对高级的主题。在日常的 Objective-C 中，你通常不需要解引用很多指针。 （对此规则有几个例外，我将在本书中介绍时指出。）要更深入地了解低级指针，我建议你找一本关于 C 编程语言的好书。

Objective-C 对指针的典型使用主要限于对象的声明。Objective-C 中的对象实际上是指针。幸运的是，在很大程度上，即使它们是指针，你也很少需要以这种方式思考它们。你最需要记住的重要一点是，每当你声明一个对象时，它都需要声明为指针。例如，查看清单 2.20。

