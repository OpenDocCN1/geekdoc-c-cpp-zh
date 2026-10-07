

实例变量和方法名似乎会在某种程度上产生混淆。由于实例变量的访问方式与方法名完全不同，Objective-C 运行时环境对实例变量和方法名相同的情况不会产生问题。

现在，这是 setter（设置方法）：

```
- (void)setTitle:(NSString *)newTitle
{
  if ([newTitle length] > 0) {
    title = newTitle;
  }
}
```

这个例子比我们的 getter 方法稍微复杂一点，尽管并不一定如此。在我们的 setter 示例中，有一个检查来判断 `newTitle` 的长度是否大于零（`NSString` 类的 `length` 方法返回字符串中的字符数）。显然，我们的 setter 代码不希望当前的标题为空。

使用 getter/setter 方法时，它们的使用方式如下代码段所示：

```
1 Book *myBook = [Book alloc init];
3 [myBook setTitle:@"My Great Book"]; // 调用 setter
5 NSString *title = [myBook title]; // 调用 getter 并将其放入 'title' 对象中。
```

setter 方法的用处是对象在接受值之前可以对参数执行一些验证逻辑。如果对象允许直接访问实例变量，那么任何类型的验证都必须无处不在，或者根本没有任何验证，导致对象的标题可能被设置为某些无效值（例如空标题）。

现在，没有必要为每个实例变量创建一个 getter 和/或 setter。一个很好的例子可能是一个代表今天日期的对象。它不需要被设置，只需要被检索，因此会有一个 getter 方法。

对象和变量的需求将决定 getter 和 setter 方法的构建方式。如果一个 getter 获取值而一个 setter 设置值，那么在对象中编写所有所有的 getter 和 setter 将需要大量代码，特别是当有许多实例变量时。坦率地说，Objective-C 2.0 引入了一种通过让程序员付出极少精力来减轻这种负担的方法。Objective-C 2.0 中的这些特性被称为属性（properties）。

> 注意：Objective-C 2.0 于 2006 年随 Xcode 3.4 引入，并包含在 Xcode 4 及更高版本中。

## 属性简介

当我们为 Book 对象创建实例变量时，我们手动创建了可以用于访问这些变量的方法。现在你已经知道如何手动这样做了，让我们来看看如何利用所谓的“属性”。属性是一种简便的方法，让编译器函数来获取和/或设置实例变量的值。正如你之前学到的，实例变量通常可以从对象本身的外部访问，因此拥有获取和设置这些变量的方法变得至关重要。

以下是我们之前创建的 Book 对象的接口（头文件）。让我们来看看，让 Objective-C 编译器为我们创建它的 getter 和 setter 需要什么。

列表 8-13. 为 Book 对象添加属性。
```objc
// Book.h
// Mybookstore
// Created于 M.R. Fisher 于 8/28/11. 保留所有。
// 版权所有 (c) 2011 www.committed-code.com.
//
#import <Foundation/Foundation.h>
@interface Book : NSObject {
}
// @property(nonatomic,strong) NSString *title;
// @property(nonatomic,strong) NSString *author;
// @property(nonatomic,strong) NSString *description;
//
@end
```

第 14–16 行显示了实例变量的属性声明。并不是所有的实例变量都需要属性，我们想要暴露给世界的那些除外。但在示例中，我们为所有的实例变量都创建了属性。注意，原本位于 `{ }` 括号之间的实际实例变量声明现在消失了。在 Xcode 4 中使用属性时，不再需要声明实例变量和属性。编译器现在足够智能可以为你完成这一切。

属性以 `@property` 指令开始。这告诉 Objective-C 编译器为我们构建自动的 getter 和/或 setter。是 getter 还是 setter 包含在声明中。让我们讨论一下这段代码：

```objc
@property (nonatomic,strong) NSString* title;
```

### 1. 这是属性指令。

2. 括号以及其中逗号分隔的关键字有时是可选的。在我们的特殊情况下，我们指定了 `nonatomic` 和 `strong`。`nonatomic` 关键字告诉编译器不要为线程安全生成特殊代码——我们没有使用线程，所以使用 `nonatomic` 是没问题的。第二个关键字 `strong` 用于指示这是一个强类型变量——这将在第 13 章讨论内存管理时进行进一步讨论。这里还可以包含许多其他选项；其中之一是 `readonly`，它告诉编译器只创建 getter 而不创建 setter，从而防止实例变量从对象外部被修改。

3. 最后，`NSString* title` 是实例变量声明。它必须包含类型和实例变量名。

这定义了属性的一半。你会说：“只有一半？还需要什么？”嗯，属性的另一半是在实现（.m）文件中定义的。列表 8-14. 为 Book 对象定义 getter 和 setter。

```objc
//
// Book.m
// MyBookstore
//
// Created于 M.R. Fisher 于 8/28/11.
//
#import "Book.h"

@implementation Book
@synthesize title, author, description;
@end
```

这是 Book 对象的实现文件。这里的意义是需要 `@synthesize` 来完成属性。这是属性。

## 使用属性

一旦在接口和实现文件中指定了属性，使用属性就会变得直观简单。首先，语法发生了变化。让我们看看传统的 setter：

```
[myBook setTitle:@"My Great Book"]; // 传统的 setter
```

这是一个使用消息设置标题的示例——使用属性时，情况发生了变化：

```objc
myBook.title = @"My Great Book"; // setter 示例
```

有些点非常重要。首先，对象的访问不在括号 `[ ]` 中。其次，使用属性名，而不是 `setTitle` 方法。内部仍然有一个 `setTitle` 方法。为什么这很重要？因为如果我们创建了自己的显式 setter，将调用我们的方法而不是编译器生成的方法。

对于 getter，看起来非常熟悉：

```
NSString *title = myBook.title; // getter 示例
```

获取信息的属性也叫 `title`。这里的意义在于访问属性的方式决定了调用 getter 还是 setter。如果我们尝试设置变量，就会调用 setter。如果我们尝试获取变量的值，就会调用 getter。

一个很大的区别是访问属性的语法现在在对象和方法之间使用点号 `.`。这是必要的，因为括号消失了，点号区分了使用属性和向对象发送消息。

