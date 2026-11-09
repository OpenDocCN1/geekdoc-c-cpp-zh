
tile 的最小宽度。程序应比之前运行得稍快一些，但更重要的是，观察起来挺有趣。

### 26.7 在主队列上同步

我们加快了应用程序的速度——它现在看起来和用起来都更好了——但我们也引入了一个问题。由于这是一个并发应用程序，每次运行应用程序时，你都可能在控制台中看到这条消息。当最小尺寸足够小时，我几乎每次都会看到这个警告：

```
*** -[NSCFArray initWithObjects:count:]:
    attempt to insert nil object at objects[5733]
```

问题在于，我们正在向 `tiles` 属性（一个属于 `Grid` 对象的数组）中添加对象和从中移除对象。我们是在主队列（一个全局串行队列）中向数组添加对象，但并没有从该队列中移除对象，因此程序可能会在 tile 已从数组中移除之后，还去检查它是否需要绘制。我们可以通过将“从 `tiles` 数组中移除对象”的调用派发到主队列来修复这个问题。

```objc
- (void) split {
    CGFloat size = (self.frame.size.width)/2;
    CGFloat x = self.frame.origin.x;
    CGFloat y = self.frame.origin.y;
    dispatch_async(
        dispatch_get_global_queue(DISPATCH_QUEUE_PRIORITY_DEFAULT, 0), ^{
        [self tileWithX:x Y:y size:size];
        [self tileWithX:x Y:y+size size:size];
        [self tileWithX:x+size Y:y size:size];
        [self tileWithX:x+size Y:y+size size:size];
    });
    dispatch_async(dispatch_get_main_queue(), ^{
        [self.grid.tiles removeObject:self];
    });
}
```

主队列是串行队列，因此只从主队列访问该数组，就能确保不会发生资源争用。主队列也是处理事件的地方，因此你可以在那里执行任何其他需要完成的 UI 任务。

你可能还会注意到动画有些不同。我更喜欢之前的方式：先对整个视图进行初始着色，然后随着进一步计算进行细化。现在动画从左下角开始，并大致向右上推进。

### 26.8 私有调度队列

使用主队列来同步对 tiles 数组的访问是合理的，因为我们正用它来进行主线程上的绘制。我们还在数千个 tile 对象之间同步这些调用。

然而，有时你想在很短的时间跨度内或在一小段代码中组织一小组任务。你可以使用自己创建并释放的串行队列来实现。串行队列不是全局的；你必须自己创建它们，使用类似下面这样的调用：

第一个参数是队列的标签，用于调试。请使用反向 DNS 命名方案，并给队列取一个唯一名称，这样你就能弄清问题出在哪里。第二个参数目前未使用，文档让你直接传 NULL。

```objc
dispatch_queue_t myQ = dispatch_queue_create("com.pragprog.myQ", NULL);
```

这是一个串行队列，因此我们添加到队列的每个任务都会在下一个任务开始之前执行。这里我们会向队列添加两个任务。实际上，每个任务都是一次向队列的调度。在第一个任务中，我们生成四个子 tile；在第二个任务中，我们从 tiles 数组中移除父 tile。

下载 Dispatch/Newton6/tile.m

```objc
- (void) split {
    CGFloat size = (self.frame.size.width)/2;
    CGFloat x = self.frame.origin.x;
    CGFloat y = self.frame.origin.y;
    dispatch_queue_t myQ =
                    dispatch_queue_create("com.pragprog.myQ", NULL);
    dispatch_async(myQ, ^{
        dispatch_async(
            dispatch_get_global_queue(
                DISPATCH_QUEUE_PRIORITY_DEFAULT, 0), ^{
            [self tileWithX:x Y:y size:size];
            [self tileWithX:x Y:y+size size:size];
            [self tileWithX:x+size Y:y size:size];
            [self tileWithX:x+size Y:y+size size:size];
        });
    });
    dispatch_async(myQ, ^{
        dispatch_async(dispatch_get_main_queue(), ^{
            [self.grid.tiles removeObject:self];
        });
    });
    dispatch_release(myQ);
}
```

这些私有调度队列采用引用计数，目前不会由自动垃圾回收清理。你可以在上面最后一行高亮代码中看到，我们必须像这样显式释放队列：

```objc
dispatch_release(myQ);
```

同样，如果你需要传递这些队列中的某一个，任何需要拥有该队列的对象都必须显式保留它，并在之后释放它。当你使用 `dispatch_queue_create()` 创建串行队列时，返回队列的引用计数为 1。这就是为什么我们在用完它之后需要手动释放它。

点击 Build & Run，这样可以正常工作。不过，这里的开销很大。你正在创建和销毁大量调度队列对象。你可以通过使用 Dispatch instrument 对项目的这个版本运行 Instruments 来看到这一点。你会看到大量队列被创建出来，并且只使用了很短时间。

一般来说，当你创建或使用队列时，你希望确保它做了足够多的工作，以证明使用它是合理的。不幸的是，有时你无法避免这种开销。接下来我们会考虑一种不需要使用主队列或这些私有调度队列的情况。

### 26.9 同步任务

一切运行得又快又好，以至于你会忍不住到处使用调度队列。例如，让我们把 tile 颜色的计算推入一个并发队列：

```objc
-(void) cycle {
    dispatch_async(
        dispatch_get_global_queue(
            DISPATCH_QUEUE_PRIORITY_DEFAULT, 0), ^{
            [self calculateColor];
        });
    dispatch_async(dispatch_get_main_queue(), ^{
        [self.grid.tiles addObject:self];
        [self.grid setNeedsDisplayInRect:self.frame];
    });
    if (self.frame.size.width > 1 ) {
        [self split];
    }
}
```

如果我们去掉上一节添加的串行队列，就更容易看出这种方法的问题：

```objc
- (void) split {
    CGFloat size = (self.frame.size.width)/2;
    CGFloat x = self.frame.origin.x;
    CGFloat y = self.frame.origin.y;
    dispatch_async(
        dispatch_get_global_queue(DISPATCH_QUEUE_PRIORITY_DEFAULT, 0), ^{
            [self tileWithX:x Y:y size:size];
            [self tileWithX:x Y:y+size size:size];
            [self tileWithX:x+size Y:y size:size];
            [self tileWithX:x+size Y:y+size size:size];
    });
}
```

点击 Build & Run。我在黑色背景上看到一块块颜色斑块。将矩形绘制到屏幕的代码在颜色计算完成之前就被调用了。如果你愿意，可以通过把牛顿法中的迭代次数从 2,000 改为 200 再改为 20，来看到不同数量的黑色。

![](img/9355405953264484a02198b0e3d25b7e_422_0.png)

我们遇到了竞态条件。无法保证 calculateColor 会在主队列中绘制 self 之前执行。这说明了我们在上一节通过使用串行调度队列所避免的问题。在这段代码中，我们使用 dispatch_async() 将 tile 颜色的计算发送到全局并发线程。当我们向主队列发送异步请求以绘制 tile 时，并不会等待颜色计算完成。

让我们对代码做一处微小改动。把 cycle 中对函数 dispatch_async() 的第一次调用改为 dispatch_sync()。

```objc
-(void) cycle {
    dispatch_sync(
        dispatch_get_global_queue(DISPATCH_QUEUE_PRIORITY_DEFAULT, 0), ^{
            [self calculateColor];
        });
    dispatch_async(dispatch_get_main_queue(), ^{
        [self.grid.tiles addObject:self];
        [self.grid setNeedsDisplayInRect:self.frame];
    });
    if (self.frame.size.width > 1) {
        [self split];
    }
}
```

现在，tile 颜色的计算会在我们将绘制 tile 的请求推送到主线程之前完成。这个版本与使用串行队列的版本运行方式相同，但没有创建那些队列的开销。

在这个对调度队列的简要介绍中，我们了解了三种基本队列类型，以及如何使用 dispatch_async() 和 dispatch_sync() 函数向它们发送任务。如果这个示例程序是终点而非手段，那么我们还有很多调优工作要做。我们可以精简绘制例程，避免重绘没有变化的单元格。我们还可以在不损失准确性的前提下加速算法。

使用队列可以获得很高的速度和响应性，但也是有代价的。你需要确保不会意外引入非预期行为，并且必须确保队列所需的复杂性确实带来了可感知的改进。
