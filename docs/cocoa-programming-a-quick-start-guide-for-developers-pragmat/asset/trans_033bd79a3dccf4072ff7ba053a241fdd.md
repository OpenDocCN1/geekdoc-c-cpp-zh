
通过这个简单的改动，我们在第二个文本字段中显示错误。

![](img/9355405953264484a02198b0e3d25b7e_303_0.png)

尽管这种处理不需要的输入的机制很好，但更好的做法是设计一个不允许用户输入未定义键的界面。你可以使用预填充的下拉列表，也可以使用带固定字段的界面——每个想要显示的属性对应一个字段。

## 19.4 练习：使用 KVC 设置变量

有设置方法 `setValue:forKey:`，它与获取方法 `valueForKey:` 配对使用。向 `BookshelfController` 添加一个名为 `setValue:` 的动作。

在这个方法中，你把顶部文本字段中出现的属性名设置为底部文本字段中输入的值。换句话说，用户正在输入一个键值对，其中键（*author* 或 *title*）是顶部文本字段的内容，而你要赋给该键的值则在底部文本字段中输入。

## 19.5 解决方案：使用 KVC 设置变量

诚然，这是一个简单的示例，但它说明了如何使用 KVC 获取和设置属性。你需要向 `BookshelfController` 头文件添加一个输出口和一个动作：

```
Download KVC/Bookshelf13/BookshelfController.h

#import <Cocoa/Cocoa.h>
@class PragBook;

@interface BookshelfController : NSViewController {
    NSTextField *keyField;
    NSTextField *valueField;
    PragBook *book;
}
@property IBOutlet NSTextField *valueField, *keyField;
@property PragBook *book;

-(IBAction) getValue:(id) sender;
-(IBAction) setValue:(id) sender;
@end
```

在 nib 文件中连接新的输出口和动作。将底部文本字段设置为可选择和可编辑，并在按下 Enter 时发送其值。

在实现文件中合成 `keyField` 属性，并像这样实现 `setValue:` 动作：

```
Download KVC/Bookshelf3/BookshelfController.m
- (IBAction) setValue:(id) sender {
    [self.book setValue:[sender stringValue]
                forKey:[self.keyField stringValue]];
}
```

现在，你可以像在字典中使用键和值一样，获取和设置任何已定义属性的值。让我们更进一步。

## 19.6 KVC 与字典

所以，我们已经看到，键值编码让我们可以像对待字典中的条目一样对待属性及其值。让我们更进一步——事实证明，只要键与属性名匹配，使用字典填充对象的属性或从类创建字典都非常简单。

让我们改造正在使用的 Bookshelf 示例，以实例化 PragBook 并用从字典中取出的值填充它。这一次，我们不再在 book 中初始化属性，而是创建一个名为 bookInfo 的字典，其键为 title 和 author。现在，我们像这样从 bookInfo 字典一次性设置 book 的属性值：

```
Download KVC/Bookshelf4/BookshelfController.m
- (PragBook *) book {
    if (!book) {
        self.book = [[PragBook alloc] init];
        NSDictionary *bookInfo =
            [NSDictionary dictionaryWithObjectsAndKeys:
                @"Manage Your Project Portfolio", @"title",
                @"Johanna Rothman", @"author", nil];
        [self.book setValuesForKeysWithDictionary: bookInfo];
    }
    return book;
}
```

就是这样。

反过来做只是稍微复杂一点。我们需要传入一个数组，其中填充新字典的键。这些键与我们要在这个字典中捕获的对象属性相同。在我们的例子中，我们会捕获这两个属性。将下面这一行添加到 `setValue:` 中，以便在用户更改 title 或 author 的值时创建字典并记录它：

```
Download KVC/Bookshelf15/BookshelfController.m

-(IBAction) setValue:(id) sender {
    [self.book setValue:[sender stringValue]
        forKey:[self.keyField stringValue]];
    NSLog(@"%@", [self.book dictionaryWithValuesForKeys:
        [NSArray arrayWithObjects:@"author", @"title", nil]]);
}
```

这里，我已将 author 变量的值从 Johanna Rothman 改为 JR：

```
Bookshelf[6388:a0f] {
    author = JR;
    title = "Manage Your Project Portfolio";
}
```

同样，这个示例在如此简单的形式下看起来有点傻，但你可以很容易想到这种机制会有用的场景。例如，想象一下，每当值发生变化时，你都希望将图书信息保存到磁盘。你已经知道如何读写磁盘上的字典，而现在你也知道如何在符合 KVC 的类和字典之间进行转换。这使你能够存储和检索任何符合 KVC 的类。

## 19.7 用于遍历类层次结构的键路径

目前我们的书架只有一本书。现在让我们给这本书添加一章。Chapter 对象将拥有用于存储标题和页数的变量。我的目标是向你展示如何通过使用键路径代替键，用 KVC 遍历层次结构。

创建一个名为 Chapter 的新 Objective-C 类。以下是其头文件：

```
Download KVC/Bookshelf16/Chapter.h

#import <Cocoa/Cocoa.h>

@interface Chapter : NSObject {
    NSString *chapterTitle;
    NSNumber *pageCount;
}
@property(copy) NSString *chapterTitle;
@property(copy) NSNumber *pageCount;
@end
```

同样，我们只需在实现文件中合成这些属性：

下载 KVC/Bookshelf6/Chapter.m

```objc
#import "Chapter.h"

@implementation Chapter
@synthesize chapterTitle, pageCount;

@end
```

现在向上一层，并向 PragBook 添加一个 Chapter 实例：

下载 KVC/Bookshelf6/PragBook.h

```objc
#import <Cocoa/Cocoa.h>
@class Chapter;

@interface PragBook : NSObject {
    NSString *title;
    NSString *author;
    Chapter *chapter;
}
@property (copy) NSString *title, *author;
@property Chapter *chapter;
@end
```

合成 chapter 的访问器。在 PragBook 的 init 方法中创建并初始化 chapter：

下载 KVC/Bookshelf6/PragBook.m

```objc
#import "PragBook.h"
#import "Chapter.h"

@implementation PragBook
@synthesize title, author, chapter;

-(id)init {
    if (self=[super init]) {
        self.chapter = [[Chapter alloc] init];
    }
    return self;
}

-(id) valueForUndefinedKey:(NSString *)key {
    return [NSString stringWithFormat:@"No property with key %@.", key];
}
@end
```

现在我们的 BookshelfController 对象有一个 PragBook 实例，而该实例又有一个 Chapter 实例，后者拥有名为 chapterTitle 和 pageCount 的属性。让我们在 BookshelfController.m 的 book 方法中使用 KVC 设置 chapter 的标题和页数。我在高亮行中两次使用了 setValue:forKeyPath:。

```objectivec
Download KVC/Bookshelf6/BookshelfController.m

-(PragBook *) book {
    if (!book) {
        self.book = [[PragBook alloc] init];
        NSDictionary *bookInfo =
            [NSDictionary dictionaryWithObjectsAndKeys:
                @"Manage Your Project Portfolio", @"title",
                @"Johanna Rothman", @"author", nil];
        [self.book setValuesForKeysWithDictionary: bookInfo];
        [self.book setValue:@"Preface"
                 forKeyPath:@"chapter.chapterTitle"];
        [self setValue:[NSNumber numberWithInt:4]
                 forKeyPath:@"book.chapter.pageCount"];
    }
    return book;
}
```

我用了两条不同的路径只是为了说明。当我从 book 开始时，我使用键路径 chapter.chapterTitle。当我从 self（换句话说，在 BookshelfController 层级）开始时，键路径是 book.chapter.pageCount。

注意，我们使用了方法 setValue:forKeyPath:，而以前使用的是方法 setValue:forKey:。你实际上可以把键看作一个非常短的键路径，并在我们的 setValue: 动作中使用 setValue:forKeyPath:。

```objectivec
Download KVC/Bookshelf6/BookshelfController.m

-(IBAction) setValue:(id) sender {
    [self.book setValue:[sender stringValue]
             forKeyPath:[self.keyField stringValue]];
}
```

同样，在以前使用 valueForKey: 的地方，现在使用获取方法 valueForKeyPath:。这将让我们可以输入键或键路径，而以前只能输入键。

```objectivec
Download KVC/Bookshelf6/BookshelfController.m

-(IBAction) getValue:(id) sender {
    [self.valueField setStringValue:
        [self.book valueForKeyPath:[sender stringValue]]];
}
```

所以现在，除了在顶部文本字段中输入 author 和 title 键之外，我们还可以安全地使用键路径 "chapter.chapterTitle" 和 "chapter.pageCount" 来获取和设置这些值。
