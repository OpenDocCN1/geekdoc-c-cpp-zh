

### 表2.1（续）

| 类型 | 描述 |
|------|-------------|
| long long | 一个64位整数。 |
| char | 一个单独的字符。从技术上讲，它是以int来表示的。 |
| BOOL | 一个布尔值，可以是YES或NO。 |
| NSInteger | 编译为32位架构时，与int相同；编译为64位架构时，范围为±4,294,967,296。 |
| NSUInteger | 编译为32位架构时，与unsigned int相同；编译为64位架构时，值介于0到2^64之间。 |

这些标量类型中的大部分也与C和C++共享，但其中有几个是Objective-C所独有的。

苹果在操作系统和库中对32位和64位架构的支持做得非常出色。然而，从编程的角度来看，这样做并非易事。例如，某些值（如数组索引）可能会受益于64位整数更高的上限。因此，在理想情况下，我们希望代码能够在32位和64位平台之间无缝切换。为此，苹果为我们提供了NSInteger和NSUInteger类型，它们会根据编译时的架构自动变为32位或64位。

使用标量类型非常简单。要声明一个标量变量，只需告诉编译器变量的类型和名称。你也可以为它赋予一个初始值。例如，清单2.6展示了如何声明一些典型的标量变量。

### 清单2.6：声明标量变量

```
int foo = 10;
double bar = 500.0;
float baz;
unsigned long n;
NSInteger x;
char a = 'a';
```

### 注意

请注意，变量`a`已被初始化为值`'a'`。在字符周围使用单引号告诉编译器将该字符的值视为char类型。这不应与字符串混淆，字符串将在后面讨论，它使用`@""`结构来指定。

## 使用特殊的变量修饰符

除了变量类型和变量名之外，还有许多关键字用于修饰你正在声明的变量类型。这些修饰关键字中最重要、也是你会在本书中看到的，是`static`和`const`关键字。

正如我之前提到的，在声明局部变量时，变量的内存通常会在程序每次进入局部变量作用域时被分配，并在离开局部作用域时被释放。这类存储被称为自动存储，或者按照默认的修饰关键字，称为`auto`。

`static`关键字会修改所声明变量的内存分配方式，使其在程序运行期间只被分配一次。之后在应用程序中访问同一个变量时，实际上访问的是最初分配的内存。这一点很重要，因为它让你能够指定一个局部变量，使其内容无限期保持。这使得它非常适合存储那些创建时需要大量资源、但变量内容不经常变化的局部变量。清单2.7展示了如何将`static`关键字与函数结合使用，以优化如变量初始化之类的昂贵操作。

### 清单2.7：使用static

```
void someFunction()
{
    // x will be created and initialized only once,
    // no matter how often you call this
    static Expensive *x = [[Expensive alloc] initWithData:...];
    // do things with x here...
    [x doSomeOperation];
}

int main(int argc, char *argv[])
{
    someFunction(); // x is created up in someFunction
    someFunction(); // x already exists and will not be created again.
    return 0;
}
```

全局变量由于作用域是全局的，默认情况下行为类似于静态变量。也就是说，它们只被分配一次，并在整个应用程序运行期间保持其内容。然而，当你将`static`关键字应用于全局变量时，它会修改全局变量的作用域，使其只能在其声明所在的文件内被访问。这与全局变量的正常行为形成对比。普通的全局变量在程序中的任何位置都处于作用域内。

`static`关键字被称为存储修饰符。在Objective-C中有几种这种类型的修饰符。有`register`修饰符，它可以向编译器提供提示，表明所存储的数据将被频繁访问，因此存储在CPU寄存器中可能更有益。这个关键字很少使用。另一个更常用的关键字是`extern`。这个修饰符表示变量或函数声明引用的是应用程序中另一个编译单元中定义或分配的实际变量或函数。在本章后面讨论函数时，你会看到`extern`关键字的使用。

`const`关键字同样修改所声明变量的内存行为，但在`const`的情况下，变量被设置为只读。这意味着一旦变量被初始化，其内容就不能被更改。这在声明不应被修改的变量（如常量）时非常有用。通过将这类变量声明为`const`，编译器将强制执行该行为。如果你之后不小心尝试修改这些变量之一，这将是一个错误，编译器会生成一个错误。清单2.8展示了如何使用`const`关键字来避免覆盖常量。

### 清单2.8：使用const关键字

```
int main(int argc, char *argv[])
{
    const NSString *foo = @"MY_CONSTANT";

    // do things here....

    foo = @"SOME_OTHER_VALUE"; // this will generate a compiler error.

    if([foo isEqualToString:@"MY_CONSTANT"])
    {
        // take action here...
    }
}
```

## 理解结构体

结构体，或简称为struct，是你自己定义的类型，可以在其中包含多个子变量。例如，如果你想声明一个将x和y坐标分组以表示一个点的变量，你可以使用结构体来声明该变量。你可以使用`struct`关键字来实现。

声明结构体分为两个阶段。首先，你必须告诉编译器关于结构体本身的信息，然后你可以使用该结构体来声明属于你所定义结构体类型的变量。继续我们声明点变量的示例，清单2.9展示了如何初步定义这个结构体。同样，这是过程的第一步——定义结构体。

### 清单2.9：声明结构体

```
struct Point
{
    float x;
    float y;
};
```

在这种情况下，我定义了一个Point结构体，包含两个成员变量x和y，它们都是float类型。现在，在定义了Point结构体之后，你就可以声明你的变量了，该变量最终将实际保存你所引用的具体点。清单2.10展示了如何做到这一点。

### 清单2.10：声明结构体实例

```
struct Point p;
```

结构体甚至可以由其他结构体的复合体组成。例如，清单2.11展示了一个通过组合两个点来定义线段的结构体。

### 清单2.11：复合结构体

```
struct Line
{
    struct Point start;
    struct Point end;
};
```

将这些内容整合起来，展示一段实际使用结构体来存储和显示一些点的代码。如清单2.12所示。

### 清单2.12：使用点结构体

```
#import <Foundation/Foundation.h>

// declaring the point structure.
struct Point
{
    float x;
    float y;
};

int main(int argc, const char *argv[])
{
    // declaring the point variable...
    struct Point p;
    // assigning values to the struct's members...
    p.x = 20.0;
    p.y = 50.0;

    // ... then to use the point...
    moveCursorToPoint(p);

    return 0;
}
```

Objective-C和Cocoa使用结构体来存储点、矩形等数据。使用结构体的好处在于，它们是一种非常轻量级的存储相关变量组的方式。在第3章中，你将看到如何使用对象来分组相关变量以及作用于这些变量的方法。然而，对象可能伴随相当大的开销。相比之下，结构体的开销不会超过其成员变量本身的开销。因此，在对象显得过于沉重的性能敏感区域，有时可以使用结构体。

## 使用typedef

自然，每次声明点时都要输入`struct Point`很快就会变得繁琐。幸运的是，Objective-C提供了另一种结构来帮助解决这个问题。这种结构被称为`typedef`。

