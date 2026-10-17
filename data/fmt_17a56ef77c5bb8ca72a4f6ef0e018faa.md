
```objectivec
Bar *bar = (Bar *)inData;

// do stuff with bar...

CFRelease(bar);
}

-(void)startLongOperation
{
    Bar *bar = [[Bar alloc] init];
    CFRetain(bar);
    foo = [[Foo alloc] init];
    [foo startLongOperationWithDelegate:self callbackMethod:
        @selector(callbackMethodForObject:withUserInfo:)
        userInfo:bar];
}

@end
```

本质上，在将你的用户数据指针传递给将调用你回调的对象之前，你手动调用 `CFRetain`，并将你的用户数据指针作为其参数传递。此时，针对该对象建立了一个强引用。

随后，当你的回调被调用并传递用户数据指针时，你应该调用 `CFRelease`，再次将指针作为其参数传递。这移除了对该指针的强引用，并且使得下一次垃圾收集器执行时，假设你没有为此对象建立另一个强引用，它将被回收。

### 使用垃圾收集器的面向对象接口

除了适用于在低级代码中使用的垃圾收集器的函数式接口外，Apple 还提供了一个更高级别的抽象 `NSGarbageCollector` 类，用于处理垃圾收集器。

`NSGarbageCollector` 类是一个单例，允许你通过 Objective-C 接口与垃圾收集器交互。你可以通过调用 `defaultCollector` 方法来访问当前线程的垃圾收集器。获得垃圾收集器的单例实例后，你可以使用它来禁用或启用特定指针的收集，甚至是整个线程的收集。此外，你还可以使用 `collectExhaustively` 或 `collectIfNeeded` 方法来强制进行收集。

表 4.1 中列出了 `NSGarbageCollector` 类上可用的方法

| Table 4.1 Commonly Used NSGarbageCollector Methods |

|---|---| 

| Method | Purpose |

| `+defaultCollector` | Returns the `NSGarbageCollector` singleton for the current thread. |

| `-disable/-enable` | Disables or enables garbage collection temporarily. |

| `-isEnabled` | Returns YES if garbage collection is currently enabled, otherwise NO. |

| `-collectExhaustively` | Triggers an exhaustive collection of garbage objects. |

| `-collectIfNeeded` | Triggers a collection, but only if memory consumption has grown beyond thresholds since the last collection. |

| `-disableCollectionForPointer:` | Causes the given pointer to become a root object, and thus ineligible for collection. |

| `-enableCollectionForPointer:` | Removes the given pointer from the list of root objects, making it eligible for collection. |

### 理解为你的项目使用何种内存管理模型

也许关于垃圾收集最重要需要理解的是何时适合使用以及何时不适合使用。在某些情况下，垃圾收集并不是你应用程序的良好选择。如我之前提到的，它仅在 MacOS X 版本 10.5 及更高版本上可用。如果你的代码需要在任何其他平台上运行，包括 iPhone 或 iPad，垃圾收集甚至都不是你的选择。除此之外，如果你有一个不使用垃圾收集的应用程序，并且有一个使用引用计数内存管理的庞大现有代码库，那么将其转换为垃圾收集可能没有意义。所需的努力可能过于高昂。

最后，由于垃圾收集器在应用程序中任何给定时间活跃对象的数量方面效率略低，已释放的对象在收集器找到它们之前并不会真正被释放。此外，垃圾收集器本身必须利用 CPU 周期来完成其工作。如果其中任何一个对你来说都是考虑因素，那么在你的应用程序中使用垃圾收集可能不是合适的选择。

然而，在你的应用程序中使用垃圾收集也可以带来显著的优势。例如，一般来说，使用垃圾收集的应用程序更容易实现线程安全。这是因为访问器可以变成简单的赋值操作，不再需要线程锁来保证线程安全。

使用垃圾收集的应用程序通常也更容易编码。对委托的弱引用等维护不再必要的需要，导致代码更简单，更易于维护。

最后，也是最明显的是，能够几乎忽略引用计数内存管理所需的典型样板代码是一大胜利。人们常说，最好的代码，也是最无 bug 的代码，是你根本不需要编写的代码。毫无疑问，垃圾收集通过减少你需要编写的代码量来帮助减少代码中出现 bug 的机会。

记住，你应该使用能够在你要求的性能参数范围内实现目标的最高抽象级别。也就是说，如果你可以使用垃圾收集，并且它能为你的问题域提供足够的性能，那么你就应该使用它。如果垃圾收集导致你特定问题域的性能不佳，那么就不要使用它。Objective-C 为开发者提供的最大优势之一是能够轻松地在框架栈中上下移动，并使用最容易解决所需问题的抽象级别。

## Summary

本章可能是本书中最重要的章节之一。对内存管理技术以及引用计数和垃圾收集的正确使用有深入理解，是所有 Objective-C 程序员必备的重要技能。在本章中，我首先向你介绍了 Objective-C 的传统内存管理模型，即引用计数。我向你展示了如何在对象中分配内存，并在不再使用时释放该内存。我还向你展示了如何在 MacOS X 上使用新技术，即垃圾收集。垃圾收集可以使你的代码比传统的引用计数内存管理更简单、更不易出错。你必须自行决定哪种内存管理技术适合你的项目。然而，我希望我已为你提供了足够的工具，以便你能够有效地做出该决定。

## Exploring Deeper Features

## In This Part

- Chapter 5

  - Working with Blocks

- Chapter 6

  - Using Key Value Coding and Key Value Observing

- Chapter 7

  - Working with Protocols

- Chapter 8

  - Extending Existing Class Capabilities

- Chapter 9

  - Writing Macros

- Chapter 10

  - Handling Errors

## Working with Blocks

Objective-C 的最新也是最强大的补充之一是包含了一种称为 blocks 的功能。使用它，你可以指定任意代码片段，这些代码可以像对象一样传递给方法和函数。在本章中，我将向你展示如何使用它们。

### Understanding Blocks

如果你是从 Ruby 或 lisp 等其他语言转到 Objective-C，你可能已经熟悉 blocks 的概念，也称为闭包。Listing 5.1 显示了 Ruby 中一个 block 的示例。

#### Listing 5.1

## An example block in Ruby

```
items.each { |item| puts item }
```

本质上，block 使你能够在代码中内联定义一个函数对象。这些函数对象可以通过使用传统变量来引用，包括传递给其他函数。这意味着，你可以定义可重用的代码块，这些代码块可以像对象一样被传递，从而使该代码能够在其他对象内部动态执行。这听起来可能令人困惑，但我认为随着我们逐步完成即将到来的示例，这个概念会变得更清晰。

在上述 block 的情况下，此代码实际上是在遍历 items 数组中的每个项目，然后执行大括号内的代码，并将当前项目传递到 block 中。

## In This Chapter

- Using blocks to encapsulate algorithms

- Using the block directive

- Creating map and filter functions using blocks

- Running blocks in parallel using threads and Grand Central Dispatch

### 声明代码块

在本节中，我将向你介绍在 Objective-C 中代码块是什么样子。代码清单 5.2 展示了一个简单代码块的示例。

#### 代码清单 5.2

##### Objective-C 中的一个简单代码块

```
int main (int argc, const char * argv[])
{
    NSAutoreleasePool * pool = [[NSAutoreleasePool alloc] init];
    
    void (^myBlock)(NSString *x);
    
    myBlock = ^(NSString *x)
    {
        NSLog(@"%@", x);
    };
    
    [pool drain];
    return 0;
}
```

从本质上讲，代码块是一个变量，就像任何其他变量一样。代码块的不同之处在于，存储在代码块内部的数据是一个函数体。使用代码块时，你可以像调用任何标准函数一样调用它，向它传递参数并从它那里获得返回值。

就这段代码而言，持有代码块的变量名为 `myBlock`。首先，你使用 `void (^myBlock) (NSString *)` 这一行来声明变量。普通变量在声明时相对简单。普通变量不需要传入参数，也不需要返回值。相反，代码块存储在变量中，并且必须声明其参数和返回类型。因此，它的声明比传统变量更复杂。

代码块的声明由它的返回类型（此处为 `void`）组成。代码块的返回类型放在你通常期望看到所声明变量类型定义的位置。然而，在代码块声明中，你声明的是代码块执行后将要返回的值类型。

在返回类型定义之后，有一个特殊运算符，用于告诉编译器你定义的是代码块而不是另一种类型的变量。这个运算符就是 `^` 字符。

你可能会觉得把这想象成声明指针变量更容易理解。就像声明指针变量时一样，`^` 字符用于表示所讨论的变量是一个指针。然而，在代码块的情况下，使用的也是 `^` 字符。

在 `^` 字符之后，是存储代码块的变量名（`myBlock`）。该变量名被括在圆括号中，以便与后面的参数分隔开。

变量名遵循语言中其他变量名的命名约定；它只能包含字母数字字符，并且不能以数字开头。

在代码块变量名的右括号之后，列出使用代码块时需要传入的参数，参数用逗号分隔，并括在另一组圆括号中（此处为 `(NSString *x)`）。列出这些参数时，你不需要提供参数本身的变量名。是否提供由你自己决定，但并非必需。一个好理解方式是，此时你实际上并没有声明函数体。因此，提供参数的变量名没有意义，因为此时它们不会被使用。相反，你只需告诉编译器期望的参数类型。你只需提供用逗号分隔的参数类型。许多代码块文档在声明中省略了参数名。我选择不省略，因为我认为那样会让代码变得混乱，特别是对新手开发者而言。

和往常一样，用分号结束语句。此时，你已经声明了一个变量，它可以存储一个代码块，该代码块返回你指定的值类型，并接受你指定的参数。在我们上面的示例中，这个变量的名称是 `myBlock`。

正如我们所知，仅仅声明变量还不够。你还需要存储代码块才能使用它。用代码块初始化新变量很简单，只需使用赋值运算符，然后再次使用一种特殊语法来表示你正在创建将要存储到变量中的实际代码块。

代码块的定义同样使用 `^` 字符来告诉编译器接下来是一个代码块定义。在定义中可以省略返回类型，因为编译器可以通过查看代码块所存储到的变量来确定返回类型。但是，你必须再次在圆括号内提供代码块的参数规范。在这种情况下，你还必须提供所传参数的变量名。这很合理，因为你是在声明参数在代码块体内使用的变量名。

在参数列表的右括号之后，你提供代码块的实际主体。这段代码主体的形式与声明普通函数几乎相同。你将代码块代码用花括号括起来，执行你选择的任何操作，按需使用你的参数，并在完成后返回任何合适的值。就像定义标准函数一样，代码块内的代码可以跨越多行，但正常的空白规则仍然适用。

#### 代码清单 5.3

##### 不同类型的代码块定义

```
void (^myBlock)(NSString *x) = ^(NSString *x)
{
    NSLog(@"%@", x);
};

void (^anotherBlock)(NSString *x) = ^(NSString *x) { NSLog(@"%@", x); };

void (^aVoidBlock)() = ^{ NSLog(@"blah"); };

doIt(^(NSString *x){ NSLog(@"%@", x); });
```

## 注意

在定义不带参数的代码块时，不提供参数的外层圆括号在语法上是允许的，因为没有参数。但是，你仍然必须为定义提供圆括号。

如这里所示，你可以将代码块变量的声明和初始化放在同一个表达式中完成。这同样与使用普通变量类似。你可以先声明变量，然后单独初始化，也可以一次性完成。

在上述代码清单的最后一行，你可以看到，也可以直接以内联方式定义代码块，来替换任何需要该代码块的参数，就像你可以将硬编码值而不是变量作为参数传递给函数一样。这是完全合法的。

### 使用代码块

你声明代码块的主要目的是让它们可以在其他地方使用。因此，理解代码块如何传递给其他函数和方法，以及当你收到一个代码块对象后如何使用它，非常重要。

要声明一个函数或方法将代码块作为参数，你可以像在代码中声明代码块变量那样声明该参数。例如，代码清单 5.4 展示了一个以代码块作为参数的函数。所涉及的代码块接收一个 `NSString` 参数，并返回一个 `NSComparisonResult`。

#### 代码清单 5.4

##### 声明一个以代码块为参数的函数

```
void useCodeBlock(NSComparisonResult (^theBlock)(NSString *value));
```

在使用代码块的函数体内，你调用代码块时，可以把它当作普通函数名来使用。换句话说，你只需像使用函数一样使用该变量，在圆括号内传入代码块所需的参数，并按需使用赋值运算符存储返回结果。

#### 代码清单 5.5

##### 一个使用代码块的函数

```
void useCodeBlock(NSComparisonResult (^theBlock)(NSString *value))
{
    if(NSOrderedSame == theBlock(@"foo"))
        doSomethingIfSame();
    else
        doSomethingElse();
}
```

当把代码块参数作为参数传递给对象或类方法（而不是函数的参数）时，语法略有不同。代码清单 5.6 展示了如何做到这一点的示例。

#### 代码清单 5.6

##### 将代码块传递给对象方法

```
-(NSMutableArray *)filterArray:(NSArray *)inArray
                    withBlock:(BOOL (^)(NSUInteger))block
{
    NSMutableArray *result = [NSMutableArray array];
```

## 清单 5.6（续）

```
for (NSNumber *number in inArray)
{
    if (block([number integerValue]))
        [result addObject:number];
}
return result;
}
```

注意，在定义 block 之后，你传入的是 block 参数的名字（也就是在方法体内持有 block 的变量的名字）。因此，本来通常用来提供 block 变量名的地方，只需传入 `(^)`。

Objective-C 的这一新特性强大得惊人。你可以创建比以前更加灵活、更可复用的代码。

不过，在使用这一强大的语言特性之前，你应该先了解一些细节。

### 理解重要的 block 作用域

如果 block 只能使用传给它的参数，并且只能返回它自己定义的值，那么这本身就是一项强大的特性。然而，block 在表面之下还有更多工具，使其更加强大。

当你在另一段代码内部定义一个 block 时，你定义的 block（也就是 block 内部的指令）不仅能访问其他所有代码都能访问的常规全局变量，还会自动获得 block 所在作用域内所有栈变量的只读副本。这意味着，你的 block 在定义时，可以（只读地）访问程序在运行时的整个状态。

为了让你理解我说的意思，请看清单 5.7。

### 清单 5.7

#### 一个访问其定义所在栈中变量的 block

```
int main (int argc, const char * argv[])
{
    NSAutoreleasePool * pool = [[NSAutoreleasePool alloc] init];

NSString *formatStr = @"%s";

void (^myBlock)(char *x) = ^(char *x) { NSLog(formatStr, x); };

doIt(myBlock);

[pool drain];
return 0;
}
```

如你所见，这个 block 访问了一个并非传给它的变量（`formatStr`），该变量来自创建这个 block 的环境。

同样，这些变量在 block 内部是只读的。不过，你可以在声明变量时使用特殊的语言指令 `__block`，显式地让变量在引用它的任何 block 内部变为可读写。
