
# 图 32.1 块变量声明

![](img/a694739dec801cd745c57da9e19c2cd4_321_0.png)

在声明原始类型变量时，你给出它的类型和名称（例如 `i`）。但是对于块变量，名称位于声明的中间，紧跟在脱符号（`^`）之后。块变量的类型取决于块是如何构造的。在这种情况下，`devowelizer` 的类型是“一个接受一个对象、一个整数和一个 `BOOL` 指针且不返回任何内容的块”。

# 为我们的新变量赋值

让我们给我们的新变量赋值。对于块变量，其值始终是大括号内部的一组指令。在 `main.m` 中，添加以下赋值语句：

```objc
int main(int argc, const char * argv[]) {
    @autoreleasepool {
        NSMutableArray *newStrings = [NSMutableArray array];

        // 创建我们要从字符串中删除的字符列表
        NSArray *vowels = [NSArray arrayWithObjects:
                          @"a", @"e", @"i", @"o", @"u", nil
        ];

        // 声明块变量
        void (*devowelizer)(id, NSInteger, BOOL *);

        // 赋值给变量
        devowelizer = ^(id string, NSInteger i, BOOL *stop) {
            NSMutableString *newString = [NSMutableString stringWithString:string];

            // 遍历元音数组，将每个字符的出现处替换为空字符串。
            for (NSString *s in vowels) {
                NSRange fullRange = NSMakeRange(0, [newString length]);
                [newString replaceOccurrencesOfString:s
                                           options:NSCaseInsensitiveSearch
                                           range:fullRange
                                             withString:@""];
            }

            [newStrings addObject:newString];
        };
        // 块赋值结束
    }
    return 0;
}
```

再次编译你的程序以检查输入。关于未使用变量的警告应该会消失。

现在你组合了一个块——一组指令——并将该块赋值给了块变量 `devowelizer`。注意，块赋值以分号结尾，就像任何变量赋值一样。

和任何变量一样，你可以同时完成 `devowelizer` 的声明和赋值：

```objc
void (*devowelizer)(id, NSInteger, BOOL *) = ^(id string, NSInteger i, BOOL *stop) {
    NSMutableString *newString = [NSMutableString stringWithString:string];

    // 遍历元音数组，将每个字符的出现处替换为空字符串。
    for (NSString *s in vowels) {
        NSRange fullRange = NSMakeRange(0, [newString length]);
        [newString replaceOccurrencesOfString:s
                                   options:NSCaseInsensitiveSearch
                                   range:fullRange
                                 withString:@""];
    }

    [newStrings addObject:newString];
};
```

和之前一样，我们声明了一个接受三个参数且不返回内容的块变量，命名为 `devowelizer`。我们组合了一个实际的块并将其存储在 `devowelizer` 中。

## 传递块

由于 `devowelizer` 是一个变量，你可以将其作为参数传递。`NSArray` 有一个方法称为 `enumerateObjectsUsingBlock:`。该方法期望块作为其唯一参数。它会为数组中的每个对象执行一次块。

在 `main.m` 中，添加以下代码来调用 `enumerateObjectsUsingBlock:` 并传入 `devowelizer`，打印去元音后的字符串。

```objc
int main(int argc, const char * argv[]) {
    @autoreleasepool {
        // 创建要去元音的字符串数组和存放新字符串的容器
        NSArray *oldStrings = [NSArray arrayWithObjects:
                               @"Sauerkraut", @"Raygun", @"Big Nerd Ranch", @"Mississippi", nil];
        NSLog(@"old strings: %@", oldStrings);

        NSMutableArray *newStrings = [NSMutableArray array];

        // 创建我们要从字符串中删除的字符列表
        NSArray *vowels = [NSArray arrayWithObjects:
                           @"a", @"e", @"i", @"o", @"u", nil];

        // 声明块变量
        void (*devowelizer)(id, NSInteger, BOOL *);

        // 赋值给变量
        devowelizer = ^(id string, NSInteger i, BOOL *stop) {
            NSMutableString *newString = [NSMutableString stringWithString:string];

            // 遍历元音数组，将每个字符的出现处替换为空字符串。
            for (NSString *s in vowels) {
                NSRange fullRange = NSMakeRange(0, [newString length]);
                [newString replaceOccurrencesOfString:s
                                           options:NSCaseInsensitiveSearch
                                           range:fullRange
                                         withString:@""];
            }

            [newStrings addObject:newString];
        };
        // 块赋值结束

        // 使用我们的块遍历数组
        [oldStrings enumerateObjectsUsingBlock:devowelizer];

        NSLog(@"new strings: %@", newStrings);
    }
    return 0;
}
```

编译并运行你的程序。你会在控制台上看到两个数组。第二个数组应该与第一个匹配——只是没有了讨厌的元音。

```text
2011-09-03 10:27:02.617 VowelMovement[787:707] old strings: (
    Sauerkraut,
    Raygun,
    "Big Nerd Ranch",
    Mississippi
)
2011-09-03 10:27:02.618 VowelMovement[787:707] new strings: (
    Srkrt,
    Rygn,
    "Bg Nrd Rnch",
    Msssspp
)
```

值得注意的是，`enumerateObjectsUsingBlock:` 不接受任意块作为参数。该方法要求“一个接受一个对象、一个整数和一个 `BOOL` 指针且不返回任何内容的块”。这就是我们这样构造赋值给 `devowelizer` 的块的原因。

第一个参数是当前对象的指针。注意该指针的类型是 `id`，无论数组包含什么种对象它都有效。第二个参数是当前对象的索引 `NSInteger`。第三个参数是指向 `BOOL` 的指针，默认为 `NO`。如果我们希望数组在当前迭代后停止，可以将其更改为 `YES`。

在块赋值的开头添加一个检查：

```objc
devowelizer = ^(id string, NSInteger i, BOOL *stop) {
    // 我找到了 y 吗？
    NSRange yRange = [string rangeOfString:@"y" options:NSCaseInsensitiveSearch];
    if (yRange.location != NSNotFound) {
        *stop = YES; // 防止进一步迭代
        return; // 停止本次迭代
    }

    NSMutableString *newString = [NSMutableString stringWithString:string];

    // 遍历元音数组，将每个元音出现替换为空字符串。
    for (NSString *s in vowels) {
        NSRange fullRange = NSMakeRange(0, [newString length]);
        [newString replaceOccurrencesOfString:s
                                   options:NSCaseInsensitiveSearch
                                   range:fullRange
                                 withString:@""];
    }

    [newStrings addObject:newString];
    // 块赋值结束
};
```

这将检查用于当前迭代的字符串是否包含大写或小写字符 'y'。如果是，则指针被设置为 `YES`（这将阻止块执行任何迭代），然后停止当前迭代。编译并运行程序。再次，数组被记录到调试器输出中，但这次在第二次迭代期间，当块遇到一个包含 'y' 的单词时，枚举被取消了。你得到的只有一些位。既然你已经练习了一些块，让我们回到块是如何解决回调问题的。当你使用回调函数时，例如在第 24 章中，你有这样一行代码：标识一个方法（通常使用 `@selector()`），然后在文件的其他地方实现该方法。你可以使用 `NSNotificationCenter` 方法 `addObserverForName:object:queue:usingBlock:` 并传递一个块。通过这种方法，你可以直接在那里处理回调，因此你不需要将回调代码放在该处的其他地方。任何阅读你代码的人都将在同一段代码中看到发送给 `NSNotificationCenter` 的消息，以便在章节末尾准确获得这一变化。

## typedef

块的语法可能会让人困惑，但你可以使用在第 1 章中学到的 `typedef` 关键字让它变得更友好。记住，`typedef` 应该位于文件顶部或头文件中，位于任何方法实现之外。在 `main.m` 中，添加以下内容：

```objc
#import <Foundation/Foundation.h>

typedef void (^EnumerationBlock)(id, NSInteger, BOOL *);

int main(int argc, const char *argv[]) {
    // ...
}
```

注意，这看起来与块的声明完全相同。然而，在这里我们定义的是一个类型而不是变量。这允许我们简化相似块的声明。与其像这样声明它，你可以用以下声明替换掉那行：

```objc
EnumerationBlock devowelizer;
```

这使得你的块变量声明看起来更加熟悉。请注意，块类型本身只定义了块的参数和返回值；它对该类型块内部的指令没有影响。

## 返回值

最后，当块返回一个值时，你可以像调用函数一样调用它的块变量。

```objc
double (^divBlock)(double, double) = ^double(double k, double j) {
    return k / j;
};
```

在这段代码中，你将 `divBlock` 声明为一个返回 `double` 并期望两个 `double` 作为参数的块变量。然后你给它赋值了一个值，该值包含了返回两个参数除法结果的指令。你可以这样使用这个块：

```objc
double quotient = divBlock(42.0, 12.5);
```
