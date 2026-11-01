
使用 release 关键字时需要牢记的一个重要方面是，你不能释放不属于你拥有的对象。例如，考虑上一节中使用的示例：

```
NSString *str = [[NSString alloc] initWithString:@"Hello"];
NSString *str2 = str;
[str release];
[str2 release];  //---this is not OK as you do not own str2---
```

尝试释放 str2 将导致运行时错误，因为你不能释放不属于你拥有的对象。然而，如果你使用 retain 关键字来获得对象的拥有权，你就需要使用 release 关键字：

```
NSString *str = [[NSString alloc] initWithString:@"Hello"];
NSString *str2 = str;
[str2 retain];
[str release];
[str2 release];  //---this is now OK as you now own str2---
```

回想一下，在关于属性的章节中，你定义了 setName: 方法，在其中设置 name 字段的值：

```
-(void) setName:(NSString *) value {
    [value retain];
    [name release];
    name = value;
}
```

注意你首先必须保留 value 对象，然后释放 name 对象，最后再将 value 对象赋给 name。为什么需要这样做而不是下面的做法？

```
-(void) setName:(NSString *) value {
    name = value;
}
```

好吧，如果你使用的是垃圾回收，那么前面的语句是有效的。然而，由于 iPhone OS 不支持垃圾回收，前面的语句会导致 name 对象引用的原始对象丢失，从而造成内存泄漏。为了防止该泄漏，你首先保留 value 对象以表明你希望获得其拥有权；然后释放 name 引用的原始对象。最后，将 value 赋给 name：

```
[value retain];
[name release];
name = value;
```

## 使用类比理解引用计数

当你思考使用引用计数进行内存管理时，使用现实生活中的类比来帮助理解总是很有帮助的。

想象图书馆里一个可以预订用于学习目的的房间。最初房间是空的，因此灯是关着的。当你预订房间时，图书管理员会增加一个计数器以表示使用房间的人数。这类似于使用 `alloc` 关键字创建对象。

当你离开房间时，图书管理员会减少计数器，如果计数器现在为 0，这意味着房间不再被使用，因此灯可以被关掉。这类似于使用 `release` 关键字释放对象。

有时你可能预订了房间并且是房间里唯一的（因此计数器为 1），直到你的朋友来访。他可能只是来拜访你，因此没有向图书管理员登记。因此计数器不会增加。因为他只是来拜访你并且没有预订房间，所以他无权决定是否关灯。这类似于在不使用 `alloc` 关键字的情况下将对象赋给另一个变量。在这种情况下，如果你离开房间（释放），灯将被关掉，你的朋友就必须离开。

考虑另一种情况：你正在使用房间，另一个人也预订了房间并与你共享。在这种情况下，计数器现在为 2。如果你离开房间，计数器会降到 1，但灯仍然亮着，因为房间里还有另一个人。这种情况类似于你创建对象并将其赋给使用 `retain` 关键字的另一个变量。在这种情况下，只有当两个对象都释放它时，对象才会被释放。

## 便利方法和自动释放

到目前为止，你了解到使用 `alloc` 或 `new` 关键字创建的所有对象都由你拥有。

考虑以下情况：

```
NSString *str = [NSString stringWithFormat:@"%d", 4];
```

在这条语句中，你拥有 str 对象吗？答案是否定的，你不拥有。因为对象是使用便利方法之一创建的——用于直接分配和初始化对象的静态方法。在前面的情况下，你创建了一个对象但不拥有它。因为你不拥有它，所以你不能手动释放它。事实上，使用此方法创建的对象被称为 autorelease 对象。所有 autorelease 对象都是临时对象，并被添加到 autorelease 池中。当当前方法退出时，其中的所有对象都会被释放。Autorelease 对象对于你只想使用一些临时变量而不想为分配和释放而烦恼的情况很有用。

## AI驱动的文档提取

本文档展示了从图像中提取结构化内容的能力。系统识别各种元素，如标题、段落、列表、表格和图表。

### 1. 引言

- 光学字符识别 (OCR)
- 布局分析
- 语义理解

### 2. 方法

| 步骤 | 描述 |
|------|-------------|
| 1 | 预处理 |
| 2 | 文本检测 |
| 3 | 内容提取 |

### 3. 结果

下图显示了不同文档类型的准确率结果。

![](img/16991b58db5894715c4a443315e06a22_502_0.png)

> “准确的提取是智能文档处理的基础。”

## 引用计数：类比继续

继续我们关于图书馆房间的类比，想象一下你正准备向图书管理员办理退房手续时，意识到你把书留在房间里了。你告诉图书管理员你已经用完房间，现在想办理退房，但因为你把书留在房间里，你告诉图书管理员暂时不要关灯，这样你就可以回去取书。稍后，图书管理员可以根据自己的选择关灯。这就是 autorelease 对象的行为。

## 自动释放池

所有 autorelease 对象都是临时对象，并被添加到 autorelease 池中。当当前方法退出时，其中的所有对象都会被释放。然而，有时你希望控制 autorelease 池何时被清空，而不是等待操作系统调用。为此，你可以创建 NSAutoreleasePool 类的一个实例，如下所示：

```
for (int i=0; i<=99999; i++){
    NSAutoreleasePool *pool = [[NSAutoreleasePool alloc] init];
    NSString *str1 = [NSString stringWithFormat:@"%d", i];
    NSString *str2 = [NSString stringWithFormat:@"%d", i];
    NSString *str3 = [NSString stringWithFormat:@"%d", i];
    //...
    [pool release];
}
```

在这个示例中，在每次循环迭代中都会创建一个 NSAutoreleasePool 对象，并且在循环内创建的所有 autorelease 对象——str1、str2 和 str3——都会进入其中。在每次迭代结束时，NSAutoreleasePool 对象被释放，以便其中包含的所有对象都会自动释放。这确保了在任何时候内存中最多只有三个 autorelease 对象。

## dealloc

你已经了解到，通过使用 alloc 或 new 关键字，你拥有创建的对象。你也看到了如何使用 release 或 autorelease 关键字释放你拥有的对象。那么什么时候是释放它们的好时机？

作为一般规则，你应该在完成对象使用后立即释放它们。因此，如果你在方法中创建了一个对象，你应该在退出方法之前释放它。对于属性，请回想一下你可以使用 @property 编译器指令与 retain 关键字一起使用：

```
@property (retain, nonatomic) NSString *name;
```

因为属性的值会被保留，所以在退出应用程序之前释放它很重要。执行此操作的好地方是类的 dealloc 方法（例如 View Controller）：

```
-(void) dealloc {
    [self.name release];    //---release the name property---
    [super dealloc];
}
```

类的 dealloc 方法在对象的引用计数达到 0 时触发。
考虑以下示例：

```
SomeClass *scl = [[SomeClass alloc] initWithName:@"Wei-Meng Lee" andRate:35];
//...do something here..
[scl release];  //---reference count goes to 0; dealloc will be called---
```

前面的示例显示，当 scl 的引用计数降到 0（当 release 语句被调用时），类中定义的 dealloc 方法将被调用。如果你在类中未定义此方法，则将调用基类中的实现。

## 内存管理技巧

内存管理是 iPhone 编程中的一个棘手问题。虽然有工具可以用来测试内存泄漏，但本节介绍了一些简单的操作，可以帮助你检测可能影响应用程序的内存问题。

首先，确保在你的 View Controller 中实现 didReceiveMemoryWarning 方法：

```
- (void)didReceiveMemoryWarning {
    //---insert code here to free unused objects---
    [super didReceiveMemoryWarning];
}
```

didReceiveMemoryWarning 方法会在你的 iPhone 内存不足时被调用。你应该在此方法中插入代码，以便释放不需要的资源/对象。

此外，你还应该在应用程序委托中处理 applicationDidReceiveMemoryWarning: 方法：

```
- (void)applicationDidReceiveMemoryWarning:(UIApplication *)application
{
    //---insert code here to free unused objects---
    [[ImageCache sharedImageCache] removeAllImagesInMemory];
}
```

在此方法中，你应该停止所有内存密集型活动，例如音频和视频播放。你还应该删除内存中缓存的所有图像。
