
支持 GNUstep，因此如果你想编写可移植的代码，就应该避免使用垃圾回收。

如果你在垃圾回收模式下编译代码，所有的 -retain、-release 和 -autorelease 消息都会被忽略。编译器会在每个赋值到堆内存的赋值操作中，自动插入对运行时函数的调用。

代码必须在垃圾回收支持下进行编译才能使用垃圾回收器。这会在任何对堆内存的赋值处插入一组函数调用，在 Mac 运行时，这些函数被声明在 `objc-auto.h` 中。

这些函数确保垃圾回收器能够感知到这些写入操作。之所以需要这些函数，是因为回收器是并发的。它会在后台线程中运行，并在无法找到对对象的引用时删除它们。必须通知回收器指针的更新，否则它可能会意外地删除你刚刚创建了引用的对象。

在针对垃圾回收进行编译时，你有两个选项。如果你使用 `-fobjc-gc-only` 标志编译，你的代码将仅支持垃圾回收。如果你使用 `-fobjc-gc-flag` 标志编译，代码将同时支持引用计数和自动垃圾回收。这在编译框架时非常有用。你仍然必须记得在正确的位置添加 -retain 和 -release 调用，但你框架的用户可以在开启或不开启回收的情况下使用它。

# 与 C 85 互操作

```
OBJ_EXPORT BOOL objc_atomicCompareAndSwapGlobal(id predicate, id replacement, volatile id *objectLocation)
OSX_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_NA) OBJC_ARC_UNAVAILABLE;
OBJECT_EXPORT BOOL objc_atomicCompareAndSwapBarrier(id predicate, id replacement, volatile id *objectLocation)
OSX_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_NA) OBJC_ARC_UNAVAILABLE;
// atomic update of an instance variable
OBJECT_EXPORT BOOL objc_atomicCompareAndSwapInstanceVariable(id predicate, id replacement, volatile id *objectLocation)
OSX_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_NA) OBJC_ARC_UNAVAILABLE;
OBJECT_EXPORT BOOL objc_atomicCompareAndSwapInstanceVariableBarrier(id predicate, id replacement, volatile id *objectLocation)
```

源自：objc-auto.h

# 与 C 互操作

在垃圾回收模式下，并不是所有内存都会扫描。任何通过 `malloc()` 分配的内容对垃圾回收器都是不可见的。如果你将一个对象指针作为 `void*` 参数传递给 C 函数，然后将其存储在 `malloc()` 分配的内存中，它将对回收器不可见，尽管仍有指向它的引用，它也可能被释放。

在 ARC 模式下，编译器将自动为你处理栈上或实例变量中的指针，但它不会跟踪结构体或显式声明为 `unsafe_unretained` 的任何内容的指针。

通常情况下，你会在对象存储到堆上之前向它发送 -retain 消息，这在垃圾回收模式下是无效，且在 ARC 模式下是被禁止的。相反，你必须使用 `CFRetain()` 函数。这会增加对象的引用计数，无论回收器是否在运行。回收器只有在对象的引用计数为零且在追踪的内存中找不到对它的任何引用时，才会释放对象。

当你完成一个不在回收器范围内的引用后，你需要调用 `CFRelease()`。

ARC 为此类操作提供了更丰富的内存模型。不再允许从对象到非对象指针类型的显式类型转换。它们必须被*桥接转换*（bridged casts）取代。考虑非 ARC 模式下的这段代码：

```
void *aPointer = (void*)someObject;
```

在 ARC 模式下，这将从一个被跟踪的指针创建一个未被跟踪的指针，这并不是你在不经思考的情况下想要做的。
你有三个基本选项。第一种常用于栈上变量，或指向保证在其他地方被引用的变量：

```
void *aPointer = (__bridge void*)someObject;
```

这执行转换但不转移所有权。如果 `someObject` 的所有其他引用都丢失，那么 `aPointer` 将变成一个悬空指针。如果 `void*` 指针将进入某处的堆并应该保留对对象的所有权引用，那么你应该使用保留的桥接转换：

```
void *aPointer = (__bridge_retained void*)nsomeObject;
```

这将一个所有权引用从 ARC 的控制中移出。这大致等于在存储 `someObject` 之前向它发送了 -retain 消息。如果你在没有赋值的情况下写下 `(__bridge_retained void*)someObject`，那么这会告诉编译器保留该对象。这样做被认为是非常糟糕的风格。在转换回对象指针时，你应该使用相反的操作：

```
id anotherObjectPointer = (__bridge_transfer id)aPointer;
aPointer = NULL;
```

这会将一个所有权引用转移到 ARC 的控制中。ARC 现在负责释放该对象，所以记住将 C 指针置零非常重要。如果你不获取指针的所有权，则应该使用简单的 `__bridge` 转换。

# 第 3 章：内存管理

# 理解对象的析毁

```
@interface Example : NSObject
{
    void *cPointer;
    id objectPointer;
}
@end
@implementation Example
-(void)finalize
{
    if (NULL != cPointer) { free(cPointer);
    [super finalize];
}
-(void)dealloc
{
    if (NULL != cPointer) { free(cPointer);
#if !has_feature(objc_arc)
    [objectPointer release];
#endif
    [super dealloc];
}
@end
```

源自：dealloc.m

# 理解对象的析毁

根据模式的不同，有三种方法在对象析毁期间被调用。其中一个总是运行，但不能由你编写。cxx_destruct 方法由 Objective-C 运行时调用，并处理任何 C++ 对象的析毁。

另外两个是 -finalize 和 -dealloc。在垃圾回收模式下，你不需要对 Objective-C 对象执行任何操作，但你仍然需要清理任何不受回收器管理的资源。这包括关闭句柄、释放通过 `malloc()` 分配的内存等。如果你的类需要这种手动清理，你应该声明 -finalize 方法。

**注意：**垃圾回收器通常在一个特殊的线程中调用 -finalize 方法。这意味着 -finalize 方法必须是线程安全的。如果它们引用全局资源，则必须确保这样做不会引入竞态条件。

如果你没有使用垃圾回收，则应该在 adealloc 方法中清理。方法的内容取决于是否使用 ARC。传统上，dealloc 方法充满了向类声明的每个实例变量发送 -release 消息。使用 ARC 后，这不再需要。ARC 会在 cxx_destruct 中释放对象的引用，因此你只需要在 adealloc 中清理非对象的实例变量。

在 GC 和手动引用计数模式下，你都应该向父类传递消息，根据情况调用 [super dealloc] 或 [super finalize]。在 ARC 模式下，不允许显式调用 -dealloc。相反，ARC 会在任何非根类的 dealloc 方法末尾插入一个 [super dealloc] 调用。

注意本节开头的示例过于复杂。在实际代码中，你可能不需要同时支持 ARC 和手动引用计数模式。它们可以在同一个程序中协作。支持非 ARC 模式的唯一原因是你想支持旧编译器。

# 使用弱引用

```
__weak id weak;
int main(void) {
    id obj = [Object new];
    weak = obj;
    obj = nil;
    objc_collect(OBJC_FULL_COLLECTION);
    fprintf(stderr, "Weak reference: %p\n", weak);
    return 0;
}
```

源自：weak.m
