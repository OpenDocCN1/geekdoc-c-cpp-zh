

```
}
else
{
    NSDictionary *errorInfo =
        [NSDictionary dictionaryWithObject:@"Unknown error."
                         forKey:NSLocalizedDescriptionKey];

    *outError = [NSError errorWithDomain:@"FileWrapper"
                                    code:501
                                userInfo:errorInfo;
}
return NO;
}
return YES;
}
```

NSError 是一个在 Cocoa 和 Cocoa Touch 框架中广泛实现的正式化设计模式。

要使用它，你需要扩展你的方法签名以接受一个对 NSError 对象的间接引用。该对象由调用方提供。间接引用本质上是指向指针的指针。换句话说，它是指向另一个指针的指针；在这种情况下，它是指向调用方栈中分配的变量的指针。当你为该变量赋值时，你解引用间接引用，从而实际上为其指向的变量赋值。

![](img/aaee977487e7a3eefe7b1dd596e0f6fb_270_0.png)

> **注意**
> 
> 一些程序员会将间接引用称为“指针到指针”、“传引用”或“引用”。我更喜欢使用“间接引用”这一术语，以将其与你在使用 Objective-C++ 时可能会遇到的普通引用区分开来。“指针到指针”可能是最准确的描述，但我觉得对于新程序员来说，“指针到指针”这个说法令人困惑。

这个间接引用的概念听起来可能非常令人困惑。如果是这样的话，那么很好，你完全正常。幸运的是，只要你理解在创建和返回 NSError 对象时需要使用的语法，底层的细节大多并不重要。

在方法参数列表中声明 NSError 间接引用时，你将使用 “(NSError **)” 语法进行声明。双 * 号表示这是一个间接引用。

## 创建 NSError 对象

一旦进入你的方法，如果发生错误，在从方法返回 NO 之前，你必须先创建你的 NSError 对象并将其分配给被解引用的 NSError 间接引用。为此，你可以像平常一样创建 NSError 对象，但在将其分配给传入变量时，你通过使用解引用运算符 (*) 来解引用该变量。所以，换句话说，要创建并将新的 NSError 对象分配给传入的 NSError 间接引用，你可以像清单 10.8 那样操作。

### 清单 10.8

### 将 NSError 对象分配给传入的 NSError 间接引用

```
*outError = [NSError errorWithDomain:@"FileWrapper"
    code:404
    userInfo:errorInfo];
```

NSError 工厂方法接受三个参数。第一个是错误域。这是一个字符串值，用于指示错误起源的子系统。Cocoa 本身提供了几个错误域，例如 NSCocoaErrorDomain、NSPOSIXErrorDomain 等。这些在 NSError.h 头文件中声明。你可以，也应该为自己创建的 NSError 实例指定自己的错误域。如果你选择这样做，错误域字符串应以反向 DNS 记法指定，例如 com.yourcompanyname.productname.classname。

第二个参数是错误代码参数。错误代码完全特定于应用程序，并为你提供了一种在错误对象中指定传统错误代码的方式。你如何使用错误代码由你决定，但它必须是无符号整数。

## 理解 NSError userInfo 字典

在很大程度上，错误代码和错误域是今天大多未使用的遗留参数。NSError 对象真正的精华在于 userInfo 字典。在为此参数创建字典时，你可以使用多个键来表示不同的错误信息。键如表 10.1 所示。

并非所有这些键总是存在，而且此外，NSError 类的用户也可以为字典添加特殊的域特定键，以便对发生的错误进行编码。

能够对显示给用户的错误消息所需的所有信息进行编码，包括描述、错误原因、如何恢复的建议，甚至对话框的按钮，使得甚至可以使用 NSAlert 类方法 +alertWithError: 来显示适当的警告框，并使用 NSError 对象中的数据显示适当的按钮和文本字段。

### 表 10.1

| Key | Purpose |
|---|---|
| NSLocalizedDescriptionKey | 错误条件的本地化描述，例如 "文件无法打开，因为它不存在。" 也可通过 NSError 对象方法 -localizedDescription 访问。 |
| NSLocalizedFailureReasonKey | 错误的本地化原因，例如 "文件不存在。" 也可通过 NSError 对象方法 -localizedFailureReason 访问。 |
| NSLocalizedRecoverySuggestionErrorKey | 用户可能采取的解决问题的本地化描述。也可通过 NSError 方法 -localizedRecoverySuggestion 访问。 |
| NSLocalizedRecoveryOptionsErrorKey | 用于在向用户展示错误时在对话框中使用的按钮字符串数组。第一个字符串将用作最右边的按钮，然后依次向左排列。 |
| NSRecoveryAttemptErrorKey | 一个符合 NSErrorRecoveryAttempting 协议的对象，可用于尝试从错误中恢复。 (仅限 Mac OS X) |
| NSUnderlyingErrorKey | 另一个表示实际底层错误的 NSError 对象。 |

## 使用恢复尝试器

恢复尝试器是 NSError 中鲜为人知且很少使用的组件。仅在 Mac OS X 上可用，它提供了一个可用于自动尝试从发生的错误中恢复的对象。

提供对象必须符合 NSErrorRecoveryAttempting 协议，该协议定义了两种方法，-attemptRecoveryFromError:optionIndex:，该方法仅在应用程序使用模态、非文档中心的用户界面时调用，以及 -attemptRecoveryFromError:optionIndex:delegate:didRecoverSelector:contextInfo:，该方法由具有文档中心用户界面的应用程序调用。

恢复尝试器与 OS X 响应者链紧密配合。要使恢复尝试器被使用，你可以在响应者链中的任何对象上调用 -presentError: 或 -presentError:modalForWindow:delegate:didPresentSelector:contextInfo:。这两种方法分别对应于为模态应用程序和基于文档的应用程序展示错误。当你调用它们时，它们会向用户展示一个警告，显示 NSError 中的信息。当用户点击按钮时，将在恢复尝试器上调用适当的恢复尝试方法，并将所点击按钮的索引作为 optionIndex 参数传递。

-attemptRecoveryFromError:optionIndex: 方法返回一个 BOOL 值，如果错误能够被恢复。-presentError:modalForWindow:delegate:didPresentSelector:contextInfo: 方法预计会在委托对象上调用提供的选择器。该选择器应采用与清单 10.9 类似的形式。

### 清单 10.9

### 恢复尝试器回调函数

```
- (void)didPresentErrorWithRecovery:(BOOL)didRecover
    contextInfo:(void *)contextInfo;
```

再次，恢复尝试器很少使用，可能不是你在代码中通常会遇到的东西。尽管如此，它是 NSError 的一个有趣特性。

## 在方法中使用 NSError

回到文件包装器示例，为了利用这个新的 NSError 代码，你必须将主块更改为类似于清单 10.10 的样子。

### 清单 10.10

### 使用 NSError 的方法

```
int main (int argc, const char * argv[])
{
    NSAutoreleasePool * pool = [[NSAutoreleasePool alloc] init];

    FileWrapper *wrapper = [[FileWrapper alloc] init];

    NSError *error = nil;

    if([[wrapper openFileAtPath:@"..." withError:&error]])
    {
        // do stuff with the file here...
    }
    else
    {
        // tell the user the file couldn’t be opened.
        // here you have the error object filled in.
        showErrorToUser(error);
    }

    [pool drain];
    return 0;
}
```

