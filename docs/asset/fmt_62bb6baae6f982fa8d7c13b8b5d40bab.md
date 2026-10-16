
When using parameters with a macro the parameters are specified inside parentheses just as if you were defining parameters for procedures. There are, however, a few subtle differences.

First, you do not need to provide a data type for the parameters. This code will not be compiled. Instead, the macro will be expanded where it is used in the parameters will be inserted directly into the expanded macro code. Therefore, variable types are not necessary here.

Secondly, the opening parenthesis of the parameter list must come directly after the name of the macro. Notice when we have been defining other macros, that the value that we are defining for the macro is separated from the macro name by a space. Therefore, if you were to put a space between the macro name and the opening parenthesis of the parameter list, the preprocessor would assume that the parameter list is the beginning of the macro value instead of part of the macro name.

Another subtle difference between procedures and macros with arguments is in the handling of the values inside the body of the macro value. Notice in the example above that there are a lot of extra parentheses being used in the body of the macro. Again, this has to do with the fact that the macro will be expanded in the code and that the values will be expanded inside the macro in the code. To illustrate this point, consider the expansion of the code `NSLog (@"Max Value: %ld", MAX ( x & 20, 10 ) );`. Without the additional parentheses, this might expand to `NSLog (@"Max Value: %ld", (x & 20 > 10 ? x & 20 : 10 ) );`. In this case, order of operations dictates that the greater than comparison has higher precedence than the bitwise-AND operation and therefore would be performed on the 20 and the 10 rather than on `x & 20` and the 10. By including the extra parentheses inside the body of the macro, you ensure that the order of operations is performed in exactly the way that you expect them to be. In other words, this code would actually expand to `NSLog (@"Max Value: %ld", ( (x & 20) > (10) ? (x & 20) : (10) ) );`.

### Using stringification

One of the macro tricks that I like to use in my own code is in logging values of particular variables as my application is running. Doing this can be useful because I can see what the state of my application is without necessarily stopping it in the debugger and looking at particular values one at a time.

To do this, I have to create a macro that takes a variable as a parameter. Because I might use this macro in multiple locations on different variables I also need to get the variable name and print it alongside the value of that variable. To do this, I use a special macro capability called stringification.

Stringification takes whatever code is passed to it and converts it to a C string by enclosing it in quotes. So, for example, if given `'x + 10'` as a parameter, it will turn it into `"'x + 10'"`. This makes it ideal for solving this kind of problem.

### Listing 9.10：打印变量值的宏

```
#define LOGVAR(var) NSLog(@"%s: %@", #var, var);
```

关键在于用`#`符号为变量名本身加上前缀。这会调用字符串化。

如果像 Listing 9.11 所示在应用程序中使用此宏，你会看到它首先打印变量的名称，然后打印该变量的值。

### Listing 9.11：使用宏打印变量的值

```
#import <Foundation/Foundation.h>

#define LOGVAR(var) NSLog(@"%s: %@", #var, var);

int main (int argc, const char * argv[])
{
    NSAutoreleasePool * pool = [[NSAutoreleasePool alloc] init];

    NSString *someVar = @"This is the value.";

    LOGVAR(someVar);

    [pool drain];
    return 0;
}
```

`LOGVAR(someVar)`行会被展开成类似 Listing 9.12 的内容。

### Listing 9.12：展开后的代码

```
#import <Foundation/Foundation.h>

int main (int argc, const char * argv[])
{
    NSAutoreleasePool * pool = [[NSAutoreleasePool alloc] init];

    NSString *someVar = @"This is the value.";

    NSLog(@"%s: %@", "someVar", someVar);

    [pool drain];
    return 0;
}
```

## NOTE

此代码出于示例目的而刻意保持简单。在你实际想要创建此类宏的情况下，你可能需要做一些事情来确定传入变量的数据类型，以便在打印时使用正确的格式字符串。

### Handling conditional switching

你可以通过使用条件预处理器指令`#if`、`#ifdef`、`#ifndef`以及它们的同伴`#else`、`#elif`和`#endif`来有条件地编译代码的特定部分。你可以根据某个内容是否已定义、未定义，或某个表达式是否求值为 true，来选择性地包含或不包含代码的整个块。

这些指令中的第一个是`#if`指令。`#if`指令用于根据表达式的结果允许或阻止代码的特定部分进行编译。表达式可以是任何有效表达式，使用其他宏、常量、宏展开周围代码中的变量等等。关键是它必须求值为 true，紧随`#if`指令之后的块才会被编译。你用`#end`语句终止`#if`语句。如果你想在表达式求值为 false 的情况下提供额外的代码块进行编译，你可以在`#if`块内、在`#end`指令之前放置一个`#else`指令。或者，你也可以放置一个`#elif`指令。

`#elif`指令也接受一个表达式，并且只有当该表达式求值为 true 时，才会编译它与下一个指令之间的代码，就像`#if`指令一样。基本上，整个`#if`、`#else`、`#elif`、`#endif`结构与`if`、`else`结构非常相似，只是它影响的不是程序执行期间的程序流程，而是影响应用程序的哪些部分被编译。`#ifdef`和`#ifndef`指令的工作方式与`#if`类似，只是它们不使用表达式，而是简单地测试某个值是否已被定义。对于`#ifdef`来说，如果该值已被定义，则编译代码；对于`#ifndef`来说，如果该值未被定义，则编译代码。

### Using built-in macros

GCC，即 Xcode 用于编译代码的底层编译器，已经为你提供了多种内置宏供使用。你在本章的示例中已经见过其中一些宏的使用。宏如`__FILE__`、`__LINE__`等等。要了解更多信息，请访问位于 http://gcc.gnu.org/onlinedocs/cpp/ 的 GCC 文档。

## Summary

在本章中，我向你介绍了 Objective-C 预处理器，这是一个强大的工具，可让你编写在编译时修改代码的代码。使用它，你可以做各种事情，从使用常量防止语法错误，到打印出你的变量，甚至有条件地编译代码的某些部分而不编译其他部分。这是一个你可能不会经常使用的工具，但在需要时却非常方便。

### Handling Errors

你希望运行时错误不会发生，但你知道它们会发生。你会采取防御性编程，确保使用的变量具有你期望的值。

你编写单元测试以确保可能发生的任何条件都已被预见，并且该问题的解决方案已内置到你的应用程序中。你知道你无法预见所有问题。然而，你知道无论你多么努力地让应用程序抵御现实世界的危险，一旦你的应用程序在具有现实世界问题的现实环境中启动，例如内存有限、磁盘空间有限，以及用户在最糟糕的时候中断你的应用程序，你就会遇到问题。你会遇到错误。

值得庆幸的是，Objective-C 内置了多种错误处理功能，你可以利用它们编写健壮、弹性且稳定的代码。你可以编写在错误发生时弯曲而不是断裂的应用程序。

在本章中，我将向你介绍 Objective-C 和 Foundation 框架中内置的三种主要机制，它们将帮助你编写在面对这些危险时勇敢的代码，并在遇到不可预见问题时“做正确的事情”。在开始之前，先看看在典型的应用程序中你可能会遇到什么类型的错误。

#### Classifying Errors

在典型的运行程序中可能发生的错误可分为三大类。

第一类错误只是由成功或失败条件组成的。无法获得关于发生了什么的额外信息，操作只是成功或不成功。通常，这是最轻微的错误，不会严重中断程序流程。例如，如果你试图通过互斥锁访问共享资源，你的程序可能会尝试

![](img/aaee977487e7a3eefe7b1dd596e0f6fb_258_0.png)

访问该资源，但失败，因为另一个程序或你的程序的另一部分已经在访问该资源。在这种情况下，你想知道访问资源失败了，并且你只想重试再次访问资源。这是一类轻微的错误条件。你确切知道调用失败时该做什么，以及可能导致失败的原因。

返回码非常适合这种错误。理想情况下，返回码可以简单到布尔值。返回码可以在调用成功时返回`YES`，调用失败时返回`NO`。在缺乏我即将向你介绍的更复杂的错误处理机制的一些语言中，错误代码是你返回无效条件的唯一选择。在这些语言中，错误代码通常被赋予多重含义。这些语言通常要求错误代码被设置为特定值以表示特定错误条件。通常，Objective-C 不这样做，因为其他机制已到位，使你能够提供比普通错误代码更丰富、更具描述性的错误消息。

第二类错误与第一类正好相反。如果不处理，这种类型的错误会导致数据丢失或应用程序失败。这些错误显然比第一类严重得多，包括无法打开应用程序继续运行所绝对必需的资源、数据存储中的一致性错误等等。想象一下，如果你不采取措施，这些错误很重要，以至于你宁愿让应用程序崩溃也不愿继续运行，以免造成更大的损害。这些错误，毫不夸张地说，是异常条件，因此最适合处理它们的错误处理机制被称为异常。幸运的是，在 Objective-C 中，这类错误很少见。尽管如此，我将在本章后面向你展示如何处理它们，以及如何从中恢复。

最后，第三类错误在严重程度上介于前两类之间。这种类型的错误足够严重，你确实需要将更多上下文信息传回调用你函数的上层，但又不至于严重到无法恢复。

这是 Objective-C 程序中发生的最常见的运行时错误类型。它如此常见，以至于 Apple 为处理这类错误提供了一种标准化的错误机制。它使用返回码来指示成功，并在失败时使用专门的`NSError`对象提供上下文信息。使用`NSError`可能很棘手，但到本章结束时，你将能够像专业人士一样处理此类错误。

### Understanding how to interrupt program flow

知道何时中断程序流程很重要。

我之前提到的三种错误类别在中断程序流程的处理方式上各自需要不同的设计模式。当设计一个可能返回错误的 API 时，要考虑 API 的使用者以及处理可能发生的错误会对调用你 API 的代码设计产生怎样的影响。理想情况下，你希望设计 API 时，使用者开发者可以用尽可能少的额外基础设施来使用它，同时又能够捕获并处理可能发生的任何错误情况。

如果你的错误很轻微、显而易见，并且需要很少的外部（开发者侧）支持或干预，那么你可能考虑使用返回码来表示某个调用失败。另一方面，如果发生的错误情况极其严重，以至于你必须完全停止应用程序以避免对系统造成更大损害，那么使用异常可能是正确的做法。你必须假设如果你的 API 的使用者没有处理该异常，应用程序将会崩溃，因为这正是异常所做的。从这个角度来看待异常，即把未处理的异常视为崩溃，确实能让这种错误情况更清晰，并可能帮助你思考异常在何时才真正合理（提示：非常罕见）。

最后，对于大多数其他错误情况——那些介于极其轻微和极其严重之间的错误——`NSError`机制可能是正确的选择。它很容易将调用失败的事实向上层传递给调用者，同时又把判断错误严重性的责任放在了正确的位置，即由同一个调用者来决定。

### 使用不同的错误处理机制

那么，让我们深入探讨如何使用这三种不同的错误处理技术。在以下各节中，我将介绍如何在 Objective-C 中使用三种不同的错误处理功能，它们在你的代码中如何工作，以及你需要做什么来处理他人代码中发生的错误。

#### 使用返回码

你已经看到方法 and 过程都具有在退出时返回值的能力。你通过使用`return`关键字来实现这一点。你在方法签名中声明返回值的类型，这决定了你的方法返回哪种类型的返回值。

使用此返回值来指示失败或成功是编程语言中最古老的错误处理机制之一。在 Objective-C 派生的 C 编程语言中，看到过程返回`int`返回码来指示不同种类的错误是很常见的。通常这些返回码会被映射到错误消息，以便你通过查看返回值来确定实际发生的错误。尽管有这种查找错误码的能力，错误码本身通常仍然只是一个数字。这往往很不方便，因为不同的函数使用不同的值来指示不同类型的错误，而查找它们意味着根据你使用的过程查阅不同的代码到错误消息的表格。

因此，其他错误处理机制被开发出来，使用返回码的方式逐渐被淘汰。尽管如此，使用返回码处理简单错误仍然是值得理解和利用的技术。然而，在这样做时最好避免返回码最大的问题，即代码到错误消息的查找，而是坚持使用简单的布尔值，在成功时返回`YES`，在失败时返回`NO`。这通常是你会在 Objective-C 中看到的用于错误处理的返回码使用方式。

当然也有例外，例如在方法可能在成功调用时返回某个值的情况下，有时调用会返回`nil`而不是预期值。幸运的是，在 Objective-C 中，`nil`和`NO`在用作`if`语句的控制变量时，结果相同，它们都被评估为`false`。因此，你可以在处理它们时将这些返回值视为相似。

清单 10.1 显示了一个用作磁盘文件包装器的类的示例。在这个特定示例中，期望磁盘上的数据文件存在且可读。但如果不是呢？如果文件不存在，就无法打开。在这种特定情况下，对象方法`-openFileAtPath:`将返回`nil`。

**清单 10.1**

**文件包装器类的类定义**
