

使用 `release` 关键字时，一个重要方面是：你不能释放一个并不属于你的对象。例如，考虑前面章节中使用过的示例：

```objectivec
NSString *str = [[NSString alloc] initWithString:@"Hello"];
NSString *str2 = str;
[str release];
[str2 release]; //---this is not OK as you do not own str2---
```

尝试释放 `str2` 会导致运行时错误，因为你不能释放不属于你的对象。但是，如果你使用 `retain` 关键字获取对象的所有权，那么你就确实需要使用 `release` 关键字：

```objectivec
NSString *str = [[NSString alloc] initWithString:@"Hello"];
NSString *str2 = str;
[str2 retain];
[str release];
[str2 release]; //---this is now OK as you now own str2---
```

回想一下前面在属性一节中，你定义了 `setName:` 方法，用来设置 `name` 字段的值：

```objectivec
-(void) setName:(NSString *) value {
    [value retain];
    [name release];
    name = value;
}
```

注意，你首先必须保留 `value` 对象，接着释放 `name` 对象，最后才把 `value` 对象赋值给 `name`。为什么需要这样做，而不是像下面这样呢？

```objectivec
-(void) setName:(NSString *) value {
    name = value;
}
```

好吧，如果你使用垃圾回收机制，前面的语句是有效的。然而，由于 iPhone OS 不支持垃圾回收，前面的语句会导致 `name` 对象原先引用的对象丢失，从而造成内存泄漏。为了防止这种泄漏，你首先要保留 `value` 对象，表示你希望获得它的所有权；然后释放 `name` 所引用的原始对象。最后，把 `value` 赋值给 `name`：

```objectivec
[value retain];
[name release];
name = value;
```

## 用类比理解引用计数

当你考虑使用引用计数的内存管理时，用一个现实生活中的类比来帮助理解总是好的。

想象图书馆里有一个可以预留给学习使用的房间。最初，房间是空的，因此灯是关着的。当你预定这个房间时，图书管理员会增加一个计数器，用来表示正在使用房间的人数。这类似于使用 `alloc` 关键字创建对象。

当你离开房间时，图书管理员会减少计数器，如果计数器变为 0，这意味着房间不再被使用，因此可以关灯。这类似于使用 `release` 关键字释放对象。

有些时候，你预定了房间，并且是房间里唯一的人（因此计数器为 1），直到你的一个朋友过来。他可能只是来看你，因此不会在图书管理员那里登记。所以，计数器不会增加。因为他只是来看你，并没有预定房间，所以他没有权利决定是否应该关灯。这类似于在没有使用 `alloc` 关键字的情况下将对象赋值给另一个变量。在这种情况下，如果你离开房间（释放），灯会被关掉，而你的朋友也不得不离开。

再考虑另一种情况：你正在使用房间，另一个人也预定了这个房间，并与你共用。在这种情况下，计数器现在是 2。如果你离开房间，计数器降到 1，但灯仍然亮着，因为房间里还有另一个人。这种情况类似于你创建一个对象，并将其赋值给另一个使用 `retain` 关键字的变量。在这种情况下，只有当两个对象都释放它时，该对象才会被释放。

## 便捷方法和自动释放（Autorelease）

到目前为止，你已经了解到，使用 `alloc` 或 `new` 关键字创建的所有对象都归你所有。

考虑以下情况：

```objectivec
NSString *str = [NSString stringWithFormat:@"%d", 4];
```

在这个语句中，你拥有 `str` 对象吗？答案是否定的，你不拥有。这是因为该对象是使用便捷方法之一创建的——这些静态方法用于直接分配和初始化对象。在前面的情况中，你创建了一个对象，但你不拥有它。因为你不拥有它，所以你不能手动释放它。事实上，使用这种方法创建的对象被称为自动释放对象（autorelease objects）。所有自动释放对象都是临时对象，并被添加到自动释放池（autorelease pool）中。当当前方法退出时，其中包含的所有对象都会被释放。自动释放对象适用于那些你只是想使用一些临时变量，不想让自己负担分配和释放操作的情况。

使用 `alloc`（或 `new`）关键字创建的对象与使用便捷方法创建的对象之间的关键区别在于所有权，如下例所示：

```objectivec
NSString *str1 = [[NSString alloc] initWithFormat:@"%d", 4];
[str1 release]; //---this is ok because you own str1---
NSString *str2 = [NSString stringWithFormat:@"%d", 4];
[str2 release]; //---this is not ok because you don't own str2---
//---str2 will be removed automatically when the autorelease pool is activated---
```

如果你想在使用便捷方法时获得对象的所有权，可以使用 `retain` 关键字：

```objectivec
NSString *str2 = [[NSString stringWithFormat:@"%d", 4] retain];
```

要释放该对象，你可以使用 `autorelease` 或 `release` 关键字。你之前了解到，`release` 关键字会立即将引用计数减 1，当引用计数达到 0 时，对象会立即从内存中释放。相比之下，`autorelease` 关键字承诺将引用计数减 1，但不是在立即执行，而是在稍后的某个时候。这就像在说：“嗯，我现在仍然需要这个对象，但以后我可以放手。”下面的代码可以说明这一点：

```objectivec
NSString *str = [[NSString stringWithFormat:@"%d", 4] retain];
[str autorelease]; // you don't own it anymore; still available
NSLog(str);       // still accessible for now
```

> 注意：在自动释放一个对象后，不要再将其释放。

注意，语句

```objectivec
NSString *str2 = [NSString stringWithFormat:@"%d", 4];
```

与下列语句具有相同的效果

```objectivec
NSString *str2 = @"4";
```

虽然自动释放对象通过自动释放不再需要的对象，似乎让你的生活变得简单，但你在使用它们时必须小心。考虑下面的示例：

```objectivec
for (int i=0; i<=99999; i++){
    NSString *str = [NSString stringWithFormat:@"%d", i];
    //...
    //...
}
```

你在每次循环迭代中都创建了一个 NSString 对象。由于这些对象直到函数退出时才被释放，你很可能在自动释放池介入释放这些对象之前就用完了内存。

解决这个问题的一种方法是使用自动释放池，这将在下一节中讨论。

## 引用计数：类比的延续

继续我们关于图书馆房间的类比：想象你正要在图书管理员那里登记离开，这时你意识到你把书落在了房间里。你告诉图书管理员，你用完了房间，现在要登记离开，但因为你的书还在房间里，你告诉图书管理员先不要关灯，这样你可以回去取书。稍后，图书管理员可以自行决定何时关灯。这就是自动释放对象的行为。

## 自动释放池

所有自动释放对象都是临时对象，并被添加到自动释放池中。当当前方法退出时，其中包含的所有对象都会被释放。然而，有时你希望控制自动释放池何时被清空，而不是等待系统调用它。为此，你可以创建 `NSAutoreleasePool` 类的一个实例，如下所示：

```objectivec
for (int i=0; i<=99999; i++){
    NSAutoreleasePool *pool = [[NSAutoreleasePool alloc] init];
    NSString *str1 = [NSString stringWithFormat:@"%d", i];
    NSString *str2 = [NSString stringWithFormat:@"%d", i];
    NSString *str3 = [NSString stringWithFormat:@"%d", i];
    // ...
    [pool release];
}
```

在这个示例中，对于循环的每次迭代，都会创建一个 `NSAutoreleasePool` 对象，并且在循环内创建的所有自动释放对象——`str1`、`str2` 和 `str3`——都会放入其中。在每次迭代结束时，`NSAutoreleasePool` 对象被释放，因此其中包含的所有对象都会被自动释放。这确保了你在任意时刻内存中最多只有三个自动释放对象。

## dealloc

你已经了解到，通过使用 `alloc` 或 `new` 关键字，你拥有你创建的对象。你也看到了如何使用 `release` 或 `autorelease` 关键字来释放你拥有的对象。那么，什么时候是释放它们的最佳时机呢？

根据经验法则，你应该在不再需要对象时尽快释放它们。所以如果你在方法中创建了一个对象，你应该在退出方法之前释放它。对于属性，回想一下你可以使用 `@property` 编译指令以及 `retain` 关键字：

```objectivec
@property (retain, nonatomic) NSString *name;
```

