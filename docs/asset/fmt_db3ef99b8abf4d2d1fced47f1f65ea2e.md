

### 使用时区

处理日期和时间时，另一个相当常见的项目是时区问题。Foundation 提供了 `NSTimeZone`，使你可以指定给定日历对象中的时区。就像指定不同的日历类型一样，给定 `NSCalendar` 的时区会影响某个特定时刻的计算时间，与另一个区域的相同时间相比会有所不同。换句话说，在另一个时区中的“一周前的这个时刻”，在小时数上实际上会与你当前时区的相同时间不同。

`NSTimeZone` 还通过类方法 `+knownTimeZoneNames` 提供了它所知道的所有时区的列表。你可以使用这个类方法向用户展示时区列表。

你可以通过将时区名称作为参数传递给工厂方法 `+timeZoneWithName:`，或者通过使用工厂方法 `+timeZoneWithAbbreviation:` 指定该时区的缩写，来创建 `NSTimeZone` 对象。这些展示在清单 15.8 中。

#### 清单 15.8 创建 NSTimeZone 对象

```
NSTimeZone *est = [NSTimeZone timeZoneWithAbbreviation:@"PST"];

NSTimeZone *azZone = [NSTimeZone timeZoneWithName:@"America/Arizona/Phoenix"];
```

在构造了这些对象之后，你可以将它们与你的 `NSCalendar` 对象结合使用。如果你没有在日历上显式设置时区，它将使用系统的默认时区。但如果你希望时间采用特定时区，你可以在 `NSCalendar` 上设置时区，然后从该日历获得的任何日期都将相应地进行调整。

### 使用 NSDateFormatter

大多数情况下，在处理日期时，你最终会将日期以字符串的形式呈现给用户。就像处理日期本身一样，在进行日期到字符串的转换时，需要考虑许多边缘条件。除了简单的标准本地化问题（例如确保月份和日期的名称在用户的区域中正确），还要考虑日期可以使用的不同表示格式。例如，一周中的某一天可以用其全名 `Tuesday` 表示，可以用缩写 `Tue` 表示，或者仅用字母 `T` 表示。月份则更加复杂。它们可以用全名 `September`、缩写 `Sept.` 或数字 `9` 表示。在美国，日期通常表示为 `MM/DD/YYYY`，而在欧洲，则表示为 `DD/MM/YYYY`。正如你所看到的，可能的变体是无穷无尽的。

处理日期格式的所有复杂性时，Foundation 为你提供了 `NSDateFormatter` 类。此类允许你指定所需的行为类型，然后将给定的 `NSDate` 对象转换为与你请求的行为相匹配的该日期的字符串表示形式。例如，要使用短的、仅数字的样式显示日期，例如 `09/20/10`，你将使用 `NSDateFormatterShortStyle`，如清单 15.9 所示。

### Listing 15.9

#### Formatting the date for short numerical format

```
NSDate *date = [NSDate date];
NSDateFormatter *f = [[NSDateFormatter alloc] init];
[f setDateStyle:NSDateFormatterShortStyle];
NSString *dateStr = [f stringFromDate:date]; // yields MM/DD/YY
```

这两种方式都可行，因为你也可以使用 `NSDateFormatter` 将表示给定日期的自然语言字符串转换为实际的 `NSDate` 对象。此示例在清单 15.10 中显示。

### Listing 15.10

#### Converting a natural language string into an NSDate object

```
NSDateFormatter *f = [[NSDateFormatter alloc] init];
[f setDateStyle:NSDateFormatterShortStyle];
NSDate *date = [f dateFromString:@"02/25/10"];
```

为你需要处理的几乎任何日期格式构造一个 `NSDateFormatter` 是不可能的，但通常你会使用系统提供的标准格式化程序集之一。

## Summary

处理日期是一个复杂且充满细节的主题，这些细节可能会让粗心的开发者陷入困境。多年来，Apple 和其他公司在 `NSDate` 和 `NSCalendar` 类上投入了大量思考和精力，以使日期对开发者来说不再是问题。你应该避免手动操作日期，而应使用这些类。这样可以节省时间。

## IV

### Exploring

### Advanced Topics

## In This Part

- Chapter 16

- Multiprocessing with Threads

- Chapter 17

- Objective-C Design Patterns

- Chapter 18

- Reading and Writing Data with NSCoder

- Chapter 19

- Using Objective-C on Other Platforms

## Multiprocessing with Threads

线程。也许没有其他计算主题能像线程一样让经验丰富的程序员感到恐惧和忐忑。它应该如此。线程会导致难以追踪、难以重现、令人抓狂的错误。与此同时，它们却承诺能比任何其他现代软件技术更能释放我们的多计算潜力。这种双重特性使其成为一个复杂的主体，值得用一整章来专门讨论如何正确处理它们。

每个程序至少有一个线程，通常称为主线程。主线程在你的 `main` 函数中开始执行，然后负责执行你的其余应用程序，除非你显式创建另一个线程。

概念上，你可以将线程视为通过你的应用程序的一条执行线，指令按顺序执行。当你创建另一个线程时，你实际上拥有了两条独立的执行线程，并行地通过你的应用程序运行。如果你的应用程序运行在单核、单 CPU 机器上，你的线程可能看起来是同时运行的，然而，它们实际上是在 CPU 上获得不同的时间片。另一方面，如果你的应用程序运行在多核或多 CPU 机器上，那么你的应用程序中的两个线程完全有可能真正同时执行。

当两个线程以这种方式同时执行时，可能出现两个线程同时尝试访问同一块内存的情况。当这种情况发生时，其确切行为是未定义的，因此，这可能导致你的程序出现错误。这种情况称为不安全的线程条件。这些情况仅在代码编写时未考虑线程安全的情况下才会发生。

为了防止此类情况，你必须防止一个线程在另一个线程同时访问时访问同一内存或数据。这称为使你的代码线程安全。只要你使用线程，就必须确保你编写的所有代码都是线程安全的，这一点至关重要。

## In This Chapter

- Understanding the causes of thread errors

- Learning how to prevent thread errors with locks

- Using @synchronize

- Creating threads with NSThread

- Using NSOperation and NSOperationQueue

safe. 调试线程中的问题极其困难，因为错误通常只在非常特定、非常狭窄的竞争条件下出现。这意味着错误可能在特定用户的计算机上出现，因为其计算机的速度和配置，而在你的计算机上却从未出现。此外，由于调试器本身可以让你的应用程序在特定点停止，并且因为它将你的应用程序的执行缩小到特定线程，线程错误通常在调试器中根本不会出现。正因为这些问题，线程错误有时被称为“海森虫”。它们得此绰号是因为你知道它们会发生，但当你试图观察它们时，它们就会消失。

许多开发者看到 Objective-C 中可用的各种线程相关工具，他们的第一反应是认为线程 somehow 会解决他们所有的设计问题。很诱人地将线程在后台启动以执行各种任务，让主线程自由处理用户界面交互；但这样做是个坏主意。即使在网络代码等情况下，其他语言可能会鼓励你使用线程来防止阻塞 I/O，99% 的时间里，对于 Objective-C 来说，使用线程将是错误的工具。线程是一种技术，应该保留用于狭窄的需求，例如 CPU 密集型计算的情况。即使在这些情况下，编写良好、线程安全的代码也可能因共享资源（如 GUI 交互）而被阻塞。这些问题可能导致多线程代码在某些情况下实际上比单线程替代方案更慢。

Objective-C 提供了多种用于创建和操作线程以及编写线程安全代码的工具。在本章中，我回顾了一些编写线程安全代码所需的关键技术，然后向你介绍一些使在 Objective-C 中创建和使用线程变得简单的类。

### CAUTION

请注意，Cocoa UI 框架（UIKit 和 AppKit）实际上并不是线程安全的。任何时候对应用程序中任何 GUI 元素的任何交互都必须始终在主线程上完成。如果必须从后台线程更新 GUI 元素，你可以使用 `NSObject` 方法 `-performSelectorOnMainThread:withObject:...` 将方法分派到主线程上调用。

### CAUTION

一些程序员遇到的常见错误是在使用 `NSNotificationCenter` 发送通知时。通知是在它们被发布所在的线程上发送的。这意味着如果你从后台线程发布通知，然后更新 GUI 组件，你就有线程安全问题的危险。因此，在线程应用程序中处理通知时要小心。

### Synchronizing Code

编写线程安全代码的关键在于记住，没有任何线程在读取或写入可能同时被另一个线程写入的特定内存块时是安全的。如果正在被读取或写入的内存同时也在线程下方发生变化，应用程序的行为是未定义的。任何事情都可能发生。因此，关键在于确保当你写入特定内存块或变量时，没有其他线程能够在你完成之前从中读取。

防止另一个线程在你写入时访问你正在写入的内存的最常见方法是使用互斥锁，或 mutex。

### Using Locks

互斥锁，或 mutex，是一种对象，可防止对公共资源（通常是内存）的同时访问。它被称为互斥锁，因为它锁定了对资源的访问，并允许一次只有一个线程独占访问。

Objective-C 基础框架提供了两种主要的互斥锁类型。第一种，也是最简单的，是 `NSLock` 类。`NSLock` 类表示一个简单的互斥锁，你可以实例化它，然后在写入特定变量或内存位置之前锁定它。其他想要写入或读取同一变量的线程，应该在启动数据访问之前尝试锁定同一个 `NSLock` 对象。尝试锁定 `NSLock` 会阻塞线程，直到锁被解锁并可以再次锁定。通过这种方式，尝试锁定 `NSLock` 将防止在第一个线程完成访问之前访问数据。

要创建 `NSLock` 的实例，你只需使用标准的 alloc/init 模式实例化一个。清单 16.1 显示了如何执行此操作的示例。通常，你将 `NSLock` 的实例作为访问数据的任何类的成员变量持有。锁必须作为变量维护并可用，以便两个线程都可以访问它以便相应地获取锁。

### Listing 16.1

#### Creating an instance of an NSLock

```
-(id)init
{
    if((self = [super init]))
    {
        lock = [[NSLock alloc] init];
    }
    return self;
}
```

通常，你会在类的初始化器中像我在这里展示的那样创建 `NSLock` 的实例。然后，在你想要保护的数据的访问器中，你只需在尝试访问数据之前获取 `NSLock` 实例的锁。清单 16.2 显示了使用此技术编写的一些访问器的示例。

### Listing 16.2

```
-(void)setSomeVar:(id)inValue
{
    [inValue retain];
    [lock lock];
    id originalValue = someVar;
    someVar = inValue;
    [lock unlock];
    [originalValue release];
}

-(id)someVar
{
    id ret = nil;
    [lock lock];
    ret = [someVar retain];
    [lock unlock];
    return [ret autorelease];
}
```

请记住，尝试锁定一个已经被锁定的 `NSLock` 实例会导致你的线程阻塞，直到能够获取锁为止。如果这会带来问题，`NSLock` 为你提供了两种便捷方法来帮助处理。第一个是 `-tryLock` 方法。此方法尝试获取锁，但如果无法获取，则会立即返回结果 `NO`。如果能够获取锁，则返回结果 `YES`。在你可能想要尝试获取锁后再执行某些操作，但如果无法获取锁，则可以在等待再次尝试的同时执行其他操作的情况下，这会很方便。

`NSLock` 提供的第二个便捷方法是 `-lockBeforeDate:` 方法。与 `-tryLock` 方法一样，它也会根据是否能够锁定 `NSLock` 实例返回布尔值，是或否。然而，在这种情况下，此方法会在指定日期之前的时间段内阻塞。当此方法过期时，如果仍未获得锁，则会返回 `NO`。

`NSLock` 最大的问题是，如果你错误地尝试再次锁定一个已经被当前线程锁定的锁，这会导致所谓的“死锁”。因为尝试锁定锁会阻塞当前线程，你可能会陷入一种情况，即你在等待锁被解锁，但它永远不会被解锁，因为负责解锁它的线程正是正在等待它被解锁的线程。这听起来可能非常曲折复杂，但在复杂的应用中这种情况确实会发生。

为了解决这个问题，还有另一种锁叫做 `NSRecursiveLock`。此锁会跟踪锁定它的线程，如果该线程再次尝试锁定它，则会立即返回。你无需担心从现有线程访问你自己锁定的数据。因此，尝试锁定你已经持有的锁是没有意义的。在这些情况下使用 `NSRecursiveLock` 可以解决此问题。

## 使用 @synchronize 关键字

使用锁是一种简单高效的方式来确保你的代码是线程安全的。然而，在你编写了一定量的基于 `NSLock` 的代码后，你可能会发现某些模式开始出现。

第一个模式是你经常想要锁定对特定变量的访问，或某个特定对象的全部成员变量，因此你有与这些特定变量关联的锁实例。通常，你有一个使用给定类的成员作为其锁对象的锁。你可能在需要访问该类中的任何数据时锁定此锁。或者，你可能有与特定变量关联的特定锁，并且你希望确保在访问这些特定变量时锁定这些锁。换句话说，你试图保护数据之间的耦合。理想情况下，你希望有某种语言结构能够在你的代码中表达这种关系。

使用线程锁时出现的第二个模式是，很容易忘记解锁你的锁。当这种情况发生时，你会遇到死锁情况，这可能会毁掉你的整天。这在引入异常时尤其成问题，会导致调用栈的正常执行被中断的情况。由于这些问题，Objective-C 引入了一个内置的语言指令，称为 `@synchronized`。此指令提供了一个内置的低级互斥锁机制，其中还包括特定的作用域和变量参数。这意味着 `@synchronized` 指令使你能够为特定变量指定一个锁，并指定该锁存在于特定代码作用域内。Listing 16.3 显示了 `@synchronized` 指令的使用示例。

### Listing 16.3

#### 使用 @synchronized

```
- (void)setSomeVar: (id) inValue
{
    [inValue retain];
    @synchronized(someVar)
    {
        id originalValue = someVar;
        someVar = inValue;
        [originalValue release];
    }
}
```

正如你所见，`@synchronized` 指令接受一个参数，指定锁定的目标变量。此外，它接受一段用大括号括起来的代码块，指定锁将被锁定的作用域。本质上，你可以将此视为作用域锁。锁仅存在于大括号内代码的作用域中。

通常，`@synchronized` 指令会与 `self` 变量一起使用，以指定整个对象在 `@synchronized` 块的作用域内被锁定。Listing 16.4 是此示例。

### Listing 16.4

#### 使用 self 作为要同步的变量。

```
- (void)setSomeVar:(id)inValue
{
    [inValue retain];
    @synchronized(self)
    {
        id originalValue = someVar;
        someVar = inValue;
        [originalValue release];
    }
}
```

`@synchronized` 的一个优点是，因为它指定了锁的作用域，如果任何情况，包括异常，导致它退出该作用域，锁将被释放。

使用 `@synchronized` 而不是 `NSLock` 或 `NSRecursiveLock` 被认为是在确保线程安全方面更现代、更正确的方式。在可能的情况下，你应该在应用程序中使用此技术。

### NOTE

不可变的 Foundation 类，例如 `NSString`、`NSArray`、`NSDictionary` 和 `NSSet`，由于创建后无法修改，因此天然是线程安全的。然而，你存储它们的变量不是线程安全的，因此如果要修改它，应使用锁来保护。

### 理解原子性

