

# 引用计数

```
int main (int argc, char *argv[]) {
    NSAutoreleasePool *pool = [NSAutoreleasePool alloc init];
    NSMutableString *myStr = [NSMutableString stringWithWithString:@"A string"];
    ClassA *myA = [[ClassA alloc init];

    NSLog(@"myStr retain count: %lx", [myStr retainCount]);

    myA setStr:myStr;
    NSLog(@"myStr retain count: %lx", [myStr retainCount]);

    [myA release];
    [pool drain];
    return 0;
}
```

# 程序 17.3 输出

myStr retain count: 1
myStr retain count: 1

该程序分配了一个由 `myA` 调用的 `ClassA` 对象，然后调用 setter 方法将其设置为 `myStr` 指向的 `NSString` 对象。正如你预期的，在调用 `setStr` 方法之前和之后，`myStr` 的引用计数均为 1，因为这个简单的方法将其参数的值存储在实例变量 `str` 中。再次强调，如果程序在调用 `setStr` 方法后释放了 `myStr`，那么存储在实例变量中的值将失效，因为引用计数将减为 0，它所引用的对象所占内存空间将被释放。

这种情况在程序 17.3 的自动释放池释放时会发生。尽管我们没有手动将其添加，但当我们使用 `stringWith:` 方法创建字符串对象 `myStr` 时，我们已经将其添加到了自动释放池中。当池被清空（drain）时，`myStr` 被释放。在清空后任何访问它的尝试都是无效的。

程序 17.4 对 `setStr:` 方法进行了修改，以保留 `str` 的值。这可以防止其他人之后释放对象 `str`。

# 程序 17.4

// 留存对象

```
#import <Foundation/Foundation.h>

@interface ClassA : NSObject
@property NSString *str;
-(void)setStr:(NSString *)s;
-(NSString *)str;

@end
```

```
@implementation ClassA
-(void)setStr: (NSString *) s
{
  str = s;
  [str retain];
}
```

```
-(NSString *) str
{
  return str;
}
@end
```

```
int main (int argc, char *argv[]) {
  NSAutoreleasePool *pool = [[NSAutoreleasePool alloc] init];
  NSMutableString *myStr = [NSMutable stringWithWith:@"A string"];
  ClassA *myA = [ClassA alloc];
  NSLog(@"myStr retain count: %lx", [myStr retainCount]);
  [myA setStr:myStr];
  NSLog(@"myStr retain count: %lx", [myStr retainCount]);
  [myStr release];
  NSLog(@"myStr retain count: %lx", [myStr retainCount]);
  [myA release];
  [pool drain];
  return 0;
}
```

# 程序 17.4 输出

myStr retain count: 1
myStr retain count: 2
myStr retain count: 1

你可以看到，在调用 `setStr` 方法后，`myStr` 的引用计数增加到了 2；这个特定问题已经解决了。随后在程序中释放 `myStr` 使其实例仍然有效，因为它的引用计数为 1。

因为你在程序中使用 `alloc` 分配了 `myA`，所以你有责任自己释放它。与其担心自己释放，如果你愿意，可以在对象分配后立即向它发送 `autorelease` 消息，将其添加到自动释放池中。记住，将对象添加到自动释放池并不会释放或使其失效；它只是将其标记为稍后释放。在对象被释放之前，你可以继续使用它，而对象的释放是在池被清空时发生的；那时，对象的引用计数将变为 0。你仍然面临一些你可能察觉到的潜在问题。你的 `setStr:` 方法执行了留存作为参数的字符串的工作，那么那个对象什么时候被释放呢？另外，你正在覆盖的实例变量 `str` 的旧值怎么办？难道不应该释放它的值以释放内存吗？程序 17.5 为这个问题提供了解决方案。

# 程序 17.5

 引用计数引言

```
#import <Foundation/Foundation.h>

@interface ClassA : NSObject
NSString *str;

-(void)setStr:(NSString *) s;
-(NSString *)str;
-(void)dealloc;
@end

@implementation ClassA
-(void)setStr:(NSString *) s
{
    // 释放旧对象，因为我们不再需要它了
    [str autorelease];

    // 留存参数以防他人释放它
    str = [str retain];
}

-(NSString *) str
{
    return str;
}

-(void)dealloc {
    NSLog("@ClassA dealloc");
    [str release];
    [super dealloc];
}
@end

int main (int argc, char *argv[]) {
    NSAutoreleasePool *pool = [NSAutoreleasePool init];
    NSMutableString *myStr = [NSMutableString stringWithString:@"A string"];
    ClassA *myA = [[ClassA alloc] init];

    NSLog(@"myStr retain count: %lx", [myStr retainCount]);
    [myA autorelease];

    [myA setStr:myStr];
    NSLog(@"myStr retain count: %lx", [myStr retainCount]);

    [pool drain];
    return 0;
}
```

# 程序 17.5 输出

myStr retain count: 1
myStr retain count: 2
ClassA dealloc

`setStr:` 方法执行了留存其作为参数的字符串的工作，那么那个对象什么时候被释放呢？另外，你正在覆盖的实例变量 `str` 的旧值怎么办？难道不应该释放它的值以释放内存吗？程序 17.5 为这个问题提供了解决方案。

`setStr:` 方法执行了留存其作为参数的字符串的工作，那么那个对象什么时候被释放呢？另外，你正在覆盖的实例变量 `str` 的旧值怎么办？难道不应该释放它的值以释放内存吗？程序 17.5 为这个问题提供了解决方案。

`setStr:` 方法执行了留存其作为参数的字符串的工作，那么那个对象什么时候被释放呢？另外，你正在覆盖的实例变量 `str` 的旧值怎么办？难道不应该释放它的值以释放内存吗？程序 17.5 为这个问题提供了解决方案。

`setStr:` 方法执行了留存其作为参数的字符串的工作，那么那个对象什么时候被释放呢？另外，你正在覆盖的实例变量 `str` 的旧值怎么办？难道不应该释放它的值以释放内存吗？程序 17.5 为这个问题提供了解决方案。

`setStr:` 方法执行了留存其作为参数的字符串的工作，那么那个对象什么时候被释放呢？另外，你正在覆盖的实例变量 `str` 的旧值怎么办？难道不应该释放它的值以释放内存吗？程序 17.5 为这个问题提供了解决方案。

`setStr:` 方法执行了留存其作为参数的字符串的工作，那么那个对象什么时候被释放呢？另外，你正在覆盖的实例变量 `str` 的旧值怎么办？难道不应该释放它的值以释放内存吗？程序 17.5 为这个问题提供了解决方案。

`setStr:` 方法执行了留存其作为参数的字符串的工作，那么那个对象什么时候被释放呢？另外，你正在覆盖的实例变量 `str` 的旧值怎么办？难道不应该释放它的值以释放内存吗？程序 17.5 为这个问题提供了解决方案。

当自动释放池清空时，`myStr` 被释放了。在清空后任何访问它的尝试都是无效的。

```
str = [str retain];
```解决该特定问题的解决方案是在 setter 内部对字符串创建一个新副本，并使其与参数完全独立。这就是为什么你在第 15 章的 `setName:` 和 `setEmail:` 方法中选择对 name 和 email 成员创建副本。

# 自动释放示例

让我们来看本章的最后一个程序，以确保你真正理解引用计数、保留以及释放/自动释放对象是如何工作的。检查程序 17.6，它定义了一个名为 `Foo` 的哑类，包含继承的实例方法。

程序 17.6

```
@import <Foundation/Foundation.h>

@interface Foo: NSObject
    int x;
@end

@implementation Foo
@end

int main (int argc, char *argv[]) {
    AutoreleasePool *pool = [[AutoreleasePool alloc] init];
    Foo *myFoo = ([Foo alloc] init];
    NSLog(@"myFoo retain count = %lx", (unsigned long) [myFoo retainCount]);

    [pool drain];
    NSLog(@"after pool drain = %lx", (unsigned long) [myFoo retainCount]);

    pool = [[AutoreleasePool alloc] init];
    [myFoo autorelease];
    NSLog(@"after autorelease = %lx", (unsigned long) [myFoo retainCount]);

    [myFoo retain];
    NSLog(@"after retain = %lx", (unsigned long) [myFoo retainCount]);

    [pool drain];
    NSLog(@"after second pool drain = %lx", (unsigned long) [myFoo retainCount]);
    return 0;
}
```

