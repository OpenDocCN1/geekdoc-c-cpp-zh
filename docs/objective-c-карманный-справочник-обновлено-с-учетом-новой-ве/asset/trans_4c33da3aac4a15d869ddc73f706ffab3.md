

## 检查类

```c
const char *name = [className UTF8String];
printf("%s\n\tivars:\n\n", name);
Class cls = NSStringFromString(className);
unsigned int ivarCount;
Ivar *ivars =
class_copyIvarList(cls, &ivarCount);
for (unsigned int i=0; i<ivarCount; i++) {
    printf("\t%s\n\n", ivar_getName(ivars[i]));
}
free(ivars);
unsigned int methodCount;
Method *methods =
class_copyMethodList(cls, &methodCount);
printf("%s\n\tMethods:\n\n", name);
for (unsigned int i=0; i<methodCount; i++) {
    printf("\t%s\n", sel_getName(method_getName(methods[i])));
}
```

来自：class.m
一旦你拥有了类的指针（通过枚举所有类、向对象发送 -class 消息或使用 `NSStringFromString()`），你就可以对其进行检查。类结构包含了大量关于 Objective-C 类的信息，所有这些信息对程序员都是可见的。

在旧版本的运行时，`Class` 是 `struct objc_class` 的类型定义，该结构定义在头文件中。在更现代的系统中，`Class` 是一个不透明类型，你应当通过一组公共函数与之交互。这使得随着时间的推移 ABI 变得更加容易。类结构的布局可以通过修改编译器和运行时更改，而无需修改任何其他代码。

`Tree.m` 示例打印了系统中所有类的实例变量和方法。你还有很多元数据可以访问。例如，实例变量存储了它们的类型以及从对象起始位置的偏移。

这些信息被用于 KVC 的实现。当你为一个键设置值且允许 KVC 直接访问实例变量时，它会首先找到一个具有匹配名称的实例变量。然后它会找到类型并确定是否需要对对象进行解箱（unbox）。最后，它会将 ivar 指针添加到对象，然后在该地址执行赋值。

它对访问器方法（accessor methods）执行类似的操作。方法存储了它们的名称、类型和方法指针。类型信息非常重要，因为它允许其他代码构建调用帧。通过检查访问器方法的类型，KVC 代码可以将方法指针强制转换为正确的类型然后调用它，从而设置或获取特定的属性。

在较新的运行时，为声明的属性也存储了元数据。你对类设置的几乎任何内容都可以通过调用运行时函数进行检查。你唯一无法做到的就是获取单个方法的源代码。

## 创建新类

```objc
#include <objc/runtime.h>

id fakeDealloc(id self, SEL _cmd, ... ) {
    NSLog(\@"%@ sent a -dealloc message", self);
}
void makeIndestructible(id obj) {
    Class new =
        objc_allocateClassPair(obj->isa, "Fake", 0);
    class_addMethod(new, @selector(dealloc),
        (IMP)fakeDealloc, "v@");
    objc_registerClassPair(new);
    obj->isa = new;
}
```

来自：newClass.m

在运行时创建新类是很罕见的，但它确实为非常动态的行为或优化提供了许多机会。我们已经看过了执行此操作 Foundation 框架的一部分。键值观察（KVO）机制就会创建新类来拦截访问器方法的调用。

在运行时创建类最重要的一点是，它展示了 Objective-C 的核心原理之一：编译器所做的一切都不是魔法。你可以在自己的 C 代码中生成编译器从 Objective-C 代码中生成的所有内容。当然，编译器在优化结果方面可能做得更好，而且 Objective-C 的版本会更简单。如果不是这样，那么 Objective-C 就没什么意义了。创建一个新类涉及三个步骤：第一，你分配类对（class pair），然后，你添加方法、实例变量和协议，最后，你向运行时注册该类对。

> **注意：** “类对”（class pair）这个术语可能看起来很困惑。你源代码中的每个 Objective-C 类在运行时都会编译为两个类。对象是*类*（class）的实例，而类是*元类*（metaclass）的实例。实例方法附加在类上，而类方法附加在元类上。当你向类发送消息时，会使用元类来查找对应的方法。

当你分配类对时，你必须提供父类、新类的名称以及在类结构末尾添加的额外空间大小。新类的名称必须是唯一的。如果你调用两次该函数，本节的示例代码将无法工作。解决此问题最简单的方法是在静态变量中保持计数器，每当创建一个新类时原子地递增，并将其附加到类名字符串上。

当将类创建与 isa 交换（isa-swizzling）结合时，类末尾的额外空间非常有用。更改现有类的 isa 指针可以让你添加方法，但不能添加实例变量。不过，你可以在类结构的末尾创建一些空间并在那里存储额外数据。以类作为参数调用 `object_getIndexedIvars()` 将为你提供这些数据的起始地址。

你可以使用此功能来实现其他对象模型。我曾使用过它，例如为 Objective-C 添加了基于原型的面向对象特性，允许闭包作为方法使用并添加到单个对象中。

## 添加新的实例变量

```objc
#include <objc/runtime.h>

@interface NSObject (Annotated)
-(NSString*)annotation;
-(void)setAnnotation:(NSString*)aString;
@end
static char key;

@implementation NSObject (Annotated)
-(NSString*)annotation
{
    return objc_getAssociatedObject(self, &key);
}
-(void)setAnnotation:(NSString*)aString
{
    objc_setAssociatedObject(self, &key, aString, OBJC_ASSOCIATION_RETAIN);
}
@end

int main(void) {
    [AutoreleasePool new];
    id obj = [NSDictionary new];
    [obj setAnnotation:@"A note"];
    NSLog("Annotation: %@", [obj annotation]);
    return 0;
}
```

从 OS X 10.6 开始，Objective-C 运行时提供了一种机制，允许你几乎可以——向现有类添加实例变量。有两个函数用于存储关联引用（associative references）。这些是在对象创建后与该对象关联的对象指针。

在对象创建后添加新的实例变量是不可能的，因为此时它的内存布局已经固定了，但这并不是最好的办法。本节开头的示例展示了一个 NSObject 的分类，它演示了这一功能。它允许你通过一对方法为任何对象关联一个字符串值。

关于设置和获取关联引用的函数有两个点需要注意。第一个是键（key）。这必须是一个唯一的指针值，不被任何其他代码用于识别不同的关联引用。实现此点最简单的方法是在文件中定义一个静态变量并使用其地址。

另一个需要注意的是关联策略（association policy）。这些策略与声明属性的可用策略镜像。在这种情况下，我们告诉运行时现在保留（retain）该对象并在对象销毁时释放它。

在某些情况下，关联引用非常有用，特别是在调试时。如果你使用 retain 策略，关联对象会在其所属的对象被销毁时释放，因此你可以使用块来记录关于销毁的消息（例如），而无需修改正在销毁的对象。你也可以用它来轻松区分两个对象，例如通过类似示例中的分类添加指示其创建位置的注释。但要注意，关联引用的开销很大。如果你在生产代码中大量使用它们，不要惊讶于你的代码变得非常慢。

