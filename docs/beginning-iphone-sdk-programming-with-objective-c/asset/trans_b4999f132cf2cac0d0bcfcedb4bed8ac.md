
```objc
//---write something to the file---
[self writeToFile:@"a string of text" withFileName:fileName];

//---read it back---
NSString *fileContent = [self readFromFile:fileName];

//---display the content read in the Debugger Console window---
NSLog(fileContent);

[super viewDidLoad];
}
```

## 在临时文件夹中存储文件

除了将文件存储在 Documents 目录中，您还可以将临时文件存储在 tmp 文件夹中。存储在 tmp 文件夹中的文件不会被 iTunes 备份，因此您需要为想要确保保留的文件找到永久位置。要获取 tmp 文件夹的路径，可以调用 `NSTemporaryDirectory()` 函数，如下所示：

```objc
-(NSString *) tempPath{
    return NSTemporaryDirectory();
}
```

在真实设备上，tmp 文件夹返回的路径为：`/private/var/mobile/Applications/<application_id>/tmp/`。

然而，在 iPhone Simulator 上，返回的路径实际上是 `/var/folders/<application_id>/tmp-/data.txt`，而不是 `~/Library/Application Support/iPhone Simulator/User/Applications/<application_id>/tmp/`。

以下语句返回要存储在 tmp 文件夹中的文件的路径：

```objc
NSString *fileName = [[self tempPath]
    stringByAppendingPathComponent:@"data.txt"];
```

## 使用属性列表

在 iPhone 编程中，您可以使用属性列表通过键/值对存储结构化数据。属性列表以 XML 文件形式存储，并且在文件系统和网络之间具有高度可移植性。例如，您可能希望在应用程序中存储 AppStore 应用程序标题的列表。由于 AppStore 中的应用程序按类别组织，因此使用如图 13-3 所示结构的属性列表来存储此信息是自然的。

| 类别 | 文件 |
|---|---|
| Games | “Animal Park”, “Biology Quiz”, “Calculus Test” |
| Entertainment | “Eye Balls”, “iBlower”, “iBell”, “iCards Birthday” |
| Utilities | “Battery Monitor”, “SystemInfo” |

图 13-3

在 Xcode 中，您可以在应用程序的 Resources 文件夹中创建并添加属性列表，并使用内置的 Property List Editor 用项目填充它。当应用程序部署时，属性列表会与应用程序一起部署。编程上，您可以使用 NSDictionary 类检索存储在属性列表中的值。更重要的是，如果您需要对属性列表进行更改，可以将更改写入文件，以便随后可以直接引用该文件而不是属性列表。

在下面的 Try It Out 中，您将创建一个属性列表并用一些值填充它。然后您将在运行时从属性列表中读取值，进行一些更改，然后将修改后的值保存到另一个属性列表文件中。

> NOTE 如果您想存储用户可以在应用程序外部修改的应用程序特定设置，应考虑使用 NSUserDefaults 类将设置存储在 Settings 应用程序中。应用程序设置在第 11 章中讨论。

## 试一试 创建和修改属性列表

- 1. 使用之前创建的同一项目，在 Xcode 中右键单击项目名称并选择“添加新文件”。
- 2. 在“新建文件”对话框左侧选择“其他”项，并在对话框右侧选择“属性列表”模板（见图 13-4）。

![](img/aab2d775c46f70cd606f2e58e2521324_337_0.png)

图 13-4

- 3. 将属性列表命名为 Apps.plist。
- 4. 按图 13-5 所示填充 Apps.plist。

![](img/aab2d775c46f70cd606f2e58e2521324_338_0.png)

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
}
```

```objective-c
//---if the property list file can be found---
if ([[NSFileManager defaultManager] fileExistsAtPath:plistFileName])
{
    //---load the content of the property list file into a NSDictionary
    // object---
    NSDictionary *dict = [[NSDictionary alloc]
        initWithContentsOfFile:plistFileName];

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
    }
    [dict release];
}
else {
    //---load the property list from the Resources folder---
    NSString *pListPath = [[NSBundle mainBundle] pathForResource:@"Apps"
        ofType:@"plist"];

    NSDictionary *dict = [[NSDictionary alloc]
        initWithContentsOfFile:pListPath];

    //---make a mutable copy of the dictionary object---
    NSMutableDictionary *copyOfDict = [dict mutableCopy];

    //---get all the different categories---
    NSArray *categoriesArray = [[copyOfDict allKeys]
        sortedArrayUsingSelector:@selector(compare:)];

    //---for each category---
    for (NSString *category in categoriesArray)
    {
        //---get all the app titles in that category---
        NSArray *titles = [dict valueForKey:category];

        //---make a mutable copy of the array---
        NSMutableArray *mutableTitles = [titles mutableCopy];

        //---add a new title to the category---
        [mutableTitles addObject:@"New App title"];

        //---set the array back to the dictionary object---
        [copyOfDict setObject:mutableTitles forKey:category];

        [mutableTitles release];
    }

    //---write the dictionary to file---
    fileName = [[self documentsPath]
                stringByAppendingPathComponent:@"Apps.plist"];

    [copyOfDict writeToFile:fileName atomically:YES];

    [dict release];
    [copyOfDict release];

    [super viewDidLoad];
}
```

- 5. 按 Command-R 在 iPhone Simulator 上测试应用程序。
- 6. 第一次运行应用程序时，您会看到应用程序在应用程序的 Documents 目录中创建了一个新的 `.plist` 文件。如果您双击 `.plist` 文件以使用 Property List Editor 查看它，您会看到对于每个应用程序类别，您都有一个名为 New App title 的新项目（见图 13-6）。

![](img/aab2d775c46f70cd606f2e58e2521324_340_0.png)

**图 13-6**

- 7. 如果您现在第二次运行应用程序，应用程序会将 Documents 目录中 `.plist` 文件的内容打印到调试器控制台窗口（见图 13-7）。

![](img/aab2d775c46f70cd606f2e58e2521324_341_0.png)

## 工作原理

此示例的第一部分展示了如何向应用程序添加属性列表文件。在属性列表文件中，您添加了三个代表 AppStore 中应用程序类别的键：Entertainment、Games 和 Utilities。每个类别都包含一个应用程序标题列表。

当视图加载时，您首先尝试在应用程序的 Documents 目录中定位名为 `Apps.plist` 的文件：

```objective-c
//---get the path to the property list file---
NSString *plistFileName = [self.documentsPath
                            stringByAppendingPathComponent:@"Apps.plist"];
```

如果找到该文件，则将内容加载到 NSDictionary 对象中：

```objective-c
//---if the property list file can be found---
if ([[NSFileManager defaultManager] fileExistsAtPath:plistFileName])
{
    //---load the content of the property list file into a NSDictionary
    //   object---
    NSDictionary *dict = [[NSDictionary alloc]
                          initWithContentsOfFile:plistFileName];
    //...
}
```

接下来，您遍历字典对象中的所有键，并在调试器控制台窗口中打印每个应用程序的标题：

```objective-c
//---for each category---
for (NSString *category in dict)
{
}
```
