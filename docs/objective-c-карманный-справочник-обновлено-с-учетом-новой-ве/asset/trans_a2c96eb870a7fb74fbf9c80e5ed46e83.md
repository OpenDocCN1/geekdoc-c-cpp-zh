

## 遍历集合

嵌套循环。在外部循环中，它将调用快速枚举方法，从集合中获取接几个对象。在内层循环中，它将遍历这个 C 语言数组。

**注意：** 如果你使用自动引用计数（ARC），那么快速枚举协议的契约更加严格。集合要求确保对象在枚举期间是有效的（或者信号集合已发生变动）。由于这一点，你不允许在不带显式修饰符的情况下给枚举变量赋值，因为如果你这样做了，ARC 不知道该如何处理你的赋值。通常情况下，最好在循环内部声明一个新变量来存放新的临时值。

你可以在没有编译器支持的情况下使用快速枚举。GNUStep 中的 `GSFastEnumeration.h` 头文件提供了 `FOR_IN` 和 `END_FOR_IN` 宏，这些宏会被展开并生成与编译器用于 **..in** 循环时所代码相同的代码。由于这些宏非常复杂，因此最好不要尝试自己去调用快速枚举方法。

带有 OS X 10.6，Apple 引入了另一种遍历集合的新方法：使用块（blocks）。块是 C 语言的一种新扩展，但设计用于与 Objective-C 紧密协作。像 Objective-C 对象一样，块也有一个 `isa` 指针。它指向一个实现了 `NSObject` 协议的私有类，因此可以将块存储在集合中。它们还支持使用 Objective-C 类型编码进行内省，尽管这种支持尚未成为它们在 OS X 上公共接口的一部分。

大多数集合类现在都实现了使用块的枚举方法。使用这些方法可能很方便，尽管这限制了你代码的可移植性。你可以通过将 `NSEnumerationConcurrent` 作为第一个参数传递给如 `-enumerateObjectsWithOptions:usingBlock:` 等方法，使用块执行并发枚举。通常只有当块在每个元素上的执行需要花费很长时间时，这种方法才可能带来性能提升。

每个集合都有不同的通过块进行枚举的方法。数组的版本接受对象的索引作为参数，字典的版本则同时接受键和值，以此此类推。这些方法会比其他替代方案更慢，因为它们需要为每个对象调用一次块（这与调用函数的开销相同）；但它们可以更方便。

在某些情况下，你可以完全避免枚举。例如，`NSArray` 实现了一个 `-makeObjectsPerformSelector` 方法，以及另一个接受对象作为第二个参数的版本。如果你在枚举时所做的只是向每个对象发送消息，

你可以使用这些方法代替创建循环。

## 在集合中查找对象

```objc
NSArray *array = [NSArray arrayWithObjects:
@"a", @"group", @"of", @"string", @"objects", nil];
NSSet *set = [NSSet initWithArray: array];
NSInteger i = [array indexOfObjectIdenticalTo:@"group"];
if (NSNotFound == i)
    i = [array indexOfObject:@"group"];
NSString *original = [set member:@"string"];
```
源自：getObject.m

`NSArray` 和 `NSSet` 都实现了 `-containsObject:` 方法，如果集合包含一个与参数相等的对象，则该方法返回 `YES`。这使用了我们之前在讨论集合类时介绍过的等性概念：如果向其中一个对象发送 `-isEqual:` 消息（以另一个对象作为参数）返回了 `YES`，则这两个对象是相等的。

在数组中，你可能想确切知道对象在哪里，而不仅仅是它是否存在。有两个方法可以告诉你：`-indexOfObject:` 和 `-indexOfObjectIdenticalTo:`。后者使用指针比较来确定等性。

这些方法在数组中都是缓慢的。它们都需要线性搜索，而且大多数方法需要向每个对象发送消息。通常情况下，你只应该在小型数组或不频繁调的代码路径中使用它们。如果你需要经常执行这种反向映射，最好使用字典或类似结构来存储这种反向关系。

对于集合，性能情况有所不同。因为集合根据对象的哈希值（hash）将对象存储在桶中，因此集合可以快速排除许多不同的对象。显然，由于集合是无序的，因此没有集合方法可以查找对象的索引。然而，有一个方法可以查找与某个对象相等的存储对象。

`NSSet` 上的 `-member:` 方法返回与参数相等的存储对象。这对于确保对象的唯一性非常有用。`unique:` 示例展示了一个从 C 字符串构建唯一常量字符串对象的方法。如果你两次向此方法传递相同的 C 字符串，你每次都会得到返回相同的 `NSString` 实例。

注意，此函数不是线程安全的。在检查字符串是否存在于集合中以及如果不在则添加新字符串之间，存在潜在的竞态条件。该方法的线程安全版本要求你在调用 `-member:` 后获取锁，再次发送此消息，最后在添加新对象后释放锁。

```objc
static NSMutableSet *unique_strings;
NSString *uniqueString(const char *str)
{
    NSString *new = [[NSString alloc]
    initWithUTF8String:str];

    NSString *old = [unique_strings member: new];

    if (nil != old)
    {
        [new release];
        return old;
    }
    [unique_strings addObject:new];
    return new;
}
```
源自：unique.m

如果你正在创建一个新的不可变类，你可能希望在构造函数实现类似这样的内容。这将牺牲一些速度换取内存使用，但意味着你可以通过指针比较来确定等性，这在某些情况下是一个巨大的收益。

## 类化集合

```objc
(NSUInteger)count{
    return [realArray count];
}
(id)objectAtIndex:(NSUInteger)anIndex{
    return [realArray objectAtIndex:anIndex];
}
```
源自：checkedArray.m

所有的集合都是类簇（class clusters）。这意味着为它们创建新的子类并非易。父类是抽象的，而具体的子类是私有的（所以你无法直接类化它们）。

每个集合都记录了你在子类中必须实现的方法。实现这一点简单方法是通过委托：只需将与要类化的集合类型相同的对象作为实例变量。`typedArray.m` 示例使用了这种方法。

`TypedArray` 类是 `NSMutableArray` 的子类。该类中的 `realArray` 变量是一个 `NSMutableArray`。它在类的指定初始化器中创建，就像任何其他创建 `NSMutableArray` 的代码一样，实际上获得的是该类某个具体子类的实例。另一个实例变量是 `Class` 类型，用于插入数组的对象的类型。

```objc
- (id)initWithType:(Class)aClass
{
    if (nil == (self = [super init]))
    {
        return nil;
    }
    type = aClass;
    realArray = [NSMutableArray new];
    return self;
}
-(void)dealloc
{
    [realArray release];
    [super dealloc];
}
```
源自：checkedArray.m

标准数组类是异质的，而这个版本要求你插入的每个对象都是传递给初始化器的类的实例（或子类）。如果你尝试插入其他对象，此版本将静默失败，但你可以轻松地修改它以抛出异常。

该类中的许多方法都是简单而易的。例如，`-removeObjectAtIndex:` 方法只是将相同的消息传递给封装的数组。其他方法，如 `-insertObject:AtIndex:`，则会进行类型检查然后调用真实的数组。

此示例实现了 `NSMutableArray` 中的全部七个原始方法。这

