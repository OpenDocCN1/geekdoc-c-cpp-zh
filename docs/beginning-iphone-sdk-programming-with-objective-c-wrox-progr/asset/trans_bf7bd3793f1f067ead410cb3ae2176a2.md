
在 Xcode 中，你可以在应用程序的 Resources 文件夹中创建并添加一个属性列表，并使用内置的属性列表编辑器填充项目。部署应用程序时，属性列表会随应用程序一起部署。程序上，你可以使用 NSDictionary 类检索存储在属性列表中的值。更重要的是，如果你需要对属性列表进行更改，可以将更改写入文件，这样随后就可以直接引用该文件而不是属性列表。

在下面的 Try It Out 中，你将创建一个属性列表并填充一些值。然后在运行时从属性列表中读取值，进行一些更改，然后将修改后的值保存到另一个属性列表文件。

> **注意** 如果你想存储用户可以在应用程序外部修改的应用程序特定设置，应考虑使用 NSUserDefaults 类将设置存储在设置应用程序中。应用程序设置在第 11 章中讨论。

## 试用 创建和修改属性列表

1. 使用之前创建的同一项目，在 Xcode 中右键单击项目名称并选择 添加 ▸ 新建文件。
2. 在新建文件对话框左侧选择 其他 项目，并在对话框右侧选择 属性列表 模板（见图 13-4）。

![](img/16991b58db5894715c4a443315e06a22_337_0.png)

3. 将属性列表命名为 Apps.plist。
4. 按图 13-5 所示填充 Apps.plist。

![](img/16991b58db5894715c4a443315e06a22_338_0.png)

图 13-5

在 viewDidLoad 方法中，添加以下以粗体显示的语句：

```objc
- (void)viewDidLoad {
    //---filename---
    NSString *fileName = [[self documentsPath]
        stringByAppendingPathComponent:@"data.txt"];
    //---write something to the file---
    [self writeToFile:@"a string of text" withFileName:fileName];
    //---read it back---
    NSString *fileContent = [self readFromFile:fileName];
    //---display the content read in the Debugger Console window---
    NSLog(fileContent);
    //---get the path to the property list file---
    NSString *plistFileName = [[self documentsPath]
        stringByAppendingPathComponent:@"Apps.plist"];

    [mutableTitles release];
    }
    //---write the dictionary to file---
    fileName = [[self documentsPath]
        stringByAppendingPathComponent:@"Apps.plist"];

    [copyOfDict writeToFile:fileName atomically:YES];

    [dict release];
    [copyOfDict release];
    }
    [super viewDidLoad];
}
```

5. 按 Command-R 在 iPhone 模拟器上测试应用程序。
6. 第一次运行应用程序时，你会看到应用程序在你的应用程序的 Documents 目录中创建了一个新的 .plist 文件。如果双击 .plist 文件以使用属性列表编辑器查看它，你会看到对于每个应用程序类别，你都有一个名为 New App title 的新项目（见图 13-6）。

![](img/16991b58db5894715c4a443315e06a22_340_0.png)

图 13-6

7. 如果现在第二次运行应用程序，应用程序会将 Documents 目录中 .plist 文件的内容打印到调试器控制台窗口（见图 13-7）。

![](img/16991b58db5894715c4a443315e06a22_341_0.png)

图 13-7

## 工作原理

此示例的第一部分展示了如何向应用程序添加属性列表文件。在属性列表文件中，你添加了三个表示 AppStore 中应用程序类别的键：Entertainment、Games 和 Utilities。每个类别都包含一个应用程序标题列表。

当视图加载时，你首先尝试在应用程序的 Documents 目录中定位名为 Apps.plist 的文件：

```objc
//---get the path to the property list file---
NSString *plistFileName = [[self documentsPath]
    stringByAppendingPathComponent:@"Apps.plist"];
```

如果找到该文件，然后将内容加载到 NSDictionary 对象中：

```objc
//---if the property list file can be found---
if ([[NSFileManager defaultManager] fileExistsAtPath:plistFileName])
{
    //---load the content of the property list file into a NSDictionary
    // object---
    NSDictionary *dict = [[NSDictionary alloc]
        initWithContentsOfFile:plistFileName];
    //...
}
```

接下来，你遍历字典对象中的所有键，并在调试器控制台窗口中打印每个应用程序的标题：

```objc
//---for each category---
for (NSString *category in dict)
{
    NSLog(category);
    NSLog(@"==========");
    //---return all the titles in an array---
    NSArray *titles = [dict valueForKey:category];

    //---print out all the titles in that category---
    for (NSString *title in titles)
    {
        NSLog(title);
    }
    [dict release];
}
```

当应用程序首次运行时，Apps.plist 文件不可用，因此你从 Resources 文件夹加载它：

```objc
else
{
    //---load the property list from the Resources folder---
    NSString *pListPath = [[NSBundle mainBundle] pathForResource:@"Apps"
        ofType:@"plist"];

    NSDictionary *dict = [[NSDictionary alloc]
        initWithContentsOfFile:pListPath];

    //...
}
```

因为你要对字典对象进行更改，所以需要对字典对象进行可变复制并将其分配给 NSMutableDictionary 对象：

```objc
//---make a mutable copy of the dictionary object---
NSMutableDictionary *copyOfDict = [dict mutableCopy];
```

此步骤很重要，因为 NSDictionary 对象是不可变的，这意味着在从属性列表填充项目后，你无法向字典对象添加内容。使用 NSDictionary 类的 mutableCopy 方法允许你创建字典对象的可变实例，即 NSMutableDictionary。

然后你检索一个包含可变字典对象中所有键的数组：

```objc
//---get all the different categories---
NSArray *categoriesArray = [[copyOfDict allKeys]
    sortedArrayUsingSelector:@selector(compare:)];
```

你使用此数组遍历字典中的所有键，以便可以为每个类别添加一些额外的标题：

```objc
//---for each category---
for (NSString *category in categoriesArray)
{
}
```

## 练习

1. 描述应用程序文件夹内各个文件夹的用途。
2. `NSDictionary` 和 `NSMutableDictionary` 类有什么区别？
3. 在真实设备上命名 `Documents` 和 `tmp` 文件夹的路径。

## 本章你学到了什么

| 主题 | 关键概念 |
|---|---|
| 应用程序文件夹中的子目录 | Documents, Library, and tmp |
| 获取 Documents 目录的路径 | `NSArray *paths = NSSearchPathForDirectoriesInDomains(NSDocumentDirectory, NSUserDomainMask, YES);`<br>`NSString *documentsDir = [paths objectAtIndex:0];` |
| 获取 tmp 目录的路径 | `-(NSString *) tempPath {`<br>`return NSTemporaryDirectory();`<br>`}` |
| 检查文件是否存在 | `if ([[NSFileManager defaultManager] fileExistsAtPath:filePath]) {`<br>`}` |
| 真实设备上 Documents 目录的位置 | `/private/var/mobile/Applications/<application_id>/Documents/` |
| 真实设备上 tmp 目录的位置 | `/private/var/mobile/Applications/<application_id>/tmp/` |
| 从 Resources 文件夹加载属性列表 | `NSString *pListPath = [[NSBundle mainBundle] pathForResource:@"Apps" ofType:@"plist"];` |
| 创建 NSDictionary 对象的可变副本 | `NSDictionary *dict = [[NSDictionary alloc] initWithContentsOfFile:pListPath];`<br>`NSMutableDictionary *copyOfDict = [dict mutableCopy];` |

## 第四部分
### 高级 iPhone 编程技术

- **第 14 章：** 编程多点触控应用程序
- **第 15 章：** 简单动画
- **第 16 章：** 访问内置应用程序
- **第 17 章：** 访问硬件

## 14 编程多点触控应用程序

### 本章你将学到什么

- 如何在你的应用程序中检测触摸
- 如何区分单击和双击
- 如何实现捏合手势
- 如何实现拖动手势

iPhone 最重要的卖点之一是其屏幕，可以检测多个输入点。多点触控输入允许用户与你的应用程序之间进行非常自然的交互。由于多点触控，移动 Safari 网络浏览器很容易成为智能手机上最用户友好的网络浏览器之一。

在本章中，你将学习如何在应用程序中检测触摸，然后实现一些酷炫的功能，从而改善用户与应用程序之间的交互，例如拼图应用程序。通过在应用程序中检测触摸，用户可以重新排列屏幕上图像的位置，并使用捏合手势更改图像大小。

### 检测触摸

在学习如何在应用程序中检测触摸之前，你首先需要熟悉处理触摸检测的几个事件。然后你将能够知道用户是否在你的应用程序上单击或双击，并做出相应反应。
