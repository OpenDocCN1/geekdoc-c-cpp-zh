

这听起来很酷，只是表面上如此，但更酷的是，在声明一个分类时，你不需要访问你要扩展的类的原始源代码。此外，分类并不是一个子类。也就是说，你添加的方法实际上是被添加到你直接操作的类的实现中。只要你在该类上声明了一个分类，你应用程序中该类的任何使用者都可以通过该类的实例访问这些方法。

尽管这样做被认为是不好的做法，但你可以使用分类来覆盖现有的方法。这样做时，即使是第三方库，在引用该类时也会调用你修改过的方法，而不是原始方法。

如果你是从 Ruby 或 Smalltalk 等其他动态语言转到 Objective-C，你可能熟悉 mixin 的概念。Mixin 和分类有很多共同点，你甚至可以说分类是 Objective-C 版的 mixin。

## 声明分类

分类的声明方式与声明类接口类似。也就是说，你通过先输入 @interface，然后是你要修改的类名来声明一个分类。在类名之后，而不是像声明类时那样写超类，你把要声明的分类名称放在括号内。清单 8.1 显示了在 NSMutableString 类上声明的一个示例分类。

Listing 8.1

在 NSMutableString 上添加将 GUID 插入字符串能力的示例分类

```
#import <Foundation/Foundation.h>

@interface NSMutableString (GUID)

- (void)appendGuid;

@end
```

在这段特定的代码中，我为 NSMutableString 类添加了一个分类，用于生成全局唯一标识符（GUID）。目前，这个分类只是将 GUID 追加到已有字符串的末尾。

## 实现分类方法

与协议不同，仅仅声明分类的接口是不够的，因为你实际上是将方法实现添加到你要修改的类中。这意味着除了声明分类的接口之外，你还必须为相关方法添加实现。清单 8.2 显示了我刚刚在上一节为 NSMutableString 类声明的方法的实现。请注意，@implementation 行，就像声明类时一样，告诉你要为哪个类创建实现，在本例中是 NSMutableString，同样后面跟着括号中的分类名。

```
```objective-c
#import "NSMutableString+GUID.h"

@implementation NSMutableString (GUID)

-(void)appendGuid
{
    CFUUIDRef uuid = CFUUIDCreate(kCFAllocatorDefault);
    NSString *str =
        (NSString *)CFUUIDCreateString(kCFAllocatorDefault, uuid);
    [self appendString:str];
    CFRelease(uuid);
}

@end
```
```

就像在类实现中定义方法一样，你在实现块内定义分类中的方法。这些方法可以访问类中的所有成员变量，可以使用 self 调用类上的其他方法，甚至可以使用 super 关键字调用超类的方法。

唯一的限制是，你不能作为分类的一部分声明新的成员变量。确实有一种方法可以向现有类添加变量，我将在本章后面向你展示，但分类无法做到这一点。

一旦我包含了头文件，我就可以像它们实际声明在原始类上一样简单地使用这些方法。

## 使用分类拆分功能

分类提供的另一个便利是能够从变得过大类中提取功能组件。在这些情况下，你可能有一个包含大量代码的类。大型类代码在需要修改时很快就会变得难以管理。通过将类的功能离散部分提取到分类中，可以更轻松地搜索大量源代码以找到需要更改的方法。这样，当你对给定类进行影响其功能一部分的更改时，你可以将与该功能相关的所有方法放在一个分类文件中，从而更轻松地进行更改。

显然，你应该尽量保持类尽可能简单。你不应该使用分类作为向给定类添加过多额外功能的借口。然而，类确实有横向增长的倾向，很高兴知道在重构时你可以使用此工具。

## 扩展类方法

分类不仅限于对象方法。你也可以使用它们来添加类方法。例如，如果你想为 GUID 分类向 NSMutableString 添加一个工厂方法，你可以简单地按清单 8.4 所示添加工厂方法。

# Listing 8.4
向 NSMutableString 添加工厂方法

```
#import <Foundation/Foundation.h>

@interface NSMutableString (GUID)
- (void)appendGUID;
+ (id)stringWithGUID;
@end

@implementation NSMutableString (GUID)
- (void)appendGUID
{
}

```

# Listing 8.5 (continued)

```
- (void)appendGuid
{
    CFUUIDRef uuid = CFUUIDCreate(kCFAllocatorDefault);
    NSString *str =
        (NSString *)CFUUIDCreateString(kCFAllocatorDefault, uuid);
    [self appendString:str];
    CFRelease(uuid);
}

+ (id)stringWithGuid;
{
    NSMutableString *ret = [self string];
    [ret appendGuid];
    return ret;
}

@end
```

## 探索分类的限制

分类确实有一些相关的限制。分类不能向扩展的类添加任何成员变量。它们绝对可以在分类方法的作用域内声明并使用局部变量，并且它们当然可以使用全局变量，或作为参数传递给它们的任何变量，但它们不能向类添加任何成员变量。

分类可以通过使用 super 关键字调用超类方法。然而，没有机制允许分类调用分类本身覆盖的方法的原始实现。换句话说，如果你使用分类覆盖现有对象方法，就没有办法调用原始的现有对象方法。

回想一下，当我谈到创建协议时描述的多重继承的危险时，问题是如果两个超类定义了相同方法的实现，编译器在给定情况下难以确定调用哪个实现。这个问题不影响协议，因为协议只是接口的声明而不是实现。另一方面，分类就没有那么幸运了。

就像多重继承的情况一样，如果两个分类在同一个类上定义了相同的方法，运行时实际调用哪个方法是不确定的。因此，你应该

NSObject 是一个“特殊类”，因为它为运行时提供了其他类所没有的某些功能。其结果是，NSObject 类，指的是类对象本身而不是类定义，能够调用对象方法。它是 Objective-C 中唯一能够做到这一点的类。为了做到这一点，NSObject 对 self 对象做了一些不寻常的 voodoo。因此，self 在 NSObject 上定义的分类的上下文中使用时，它们指的是类或对象。

由于这些风险，通常来说，你应该只以接口的形式声明 NSObject 上的分类，并且不提供实现。分类实现可能应限于子类。虽然存在为 NSObject 分类提供实现的可能性，但总体而言，预计 NSObject 上的分类将仅用于声明非正式协议的目的。

## 使用匿名分类扩展类

虽然 Objective-C 没有将私有方法声明内置到类声明语法中的机制，但有一种方法可以定义私有 API，仅向类的特权用户公开，而不向其他用户公开，你可以使用分类来实现。

你用来做这件事的工具称为匿名分类。基本上，匿名分类是在给定类上声明但没有名称的分类。也就是说，当你声明分类时，而不是在分类名后括号内放置分类名称，括号在那里，但留空。在使用匿名分类时，你只声明接口，而不作为分类本身的一部分实现。通常，你将此分类声明放在另一个头文件中，可以由有权访问私有 API 的类使用者导入。实现是在原始类的实现内部完成的。你只是创建了一个在外部访问该实现的机制。

这给了你一种方法，可以将方法声明为匿名分类中的私有 API 的一部分，但不是你公共类声明中的公共 API 的一部分。当导入匿名分类接口时，编译器将期望匿名分类接口中声明的方法由扩展类实现。因此，这也为你提供了一种方法，可以拥有一个声明的、编译时检查的 API，该 API 是私有的，对类的使用者不可见，除非他们知道要包含私有 API 分类头。

清单 8.6 显示了匿名分类声明的示例。

