

**图14.13**  
探索自动 UI，并发现它的一些绑定

![](img/2b293e29fc15b0797f113b85dd429b6e_385_0.png)

如图14.15所示，打开日期格式化器的属性，删除现有格式，然后从“Format”窗口下的集合中拖拽年份格式化器来替换它。

这解决了格式问题。Year 列现在应该能正确显示单个年份。以相同方式修改用于在年份输入文本框中显示年份的日期格式化器。它位于滚动视图上方，在“Static Text (Year)”标签下方的文本框内。

要解决第二个问题，你需要用代码访问模型数据。虽然 Core Data 支持用于数据展示的通用过滤，但在这里没有简单的实现方式。虽然可以添加一个自定义数据转换器，检查 Artist 字符串并相应地过滤结果。但你可以通过直接搜索数据，并将结果列表打包到一个数组中，在单独的表格中显示，从而获得相同的结果。为此，你需要了解 Core Data 的类和编程模型。

**图14.14**  
探索数组控制器如何绑定到一个称为*托管对象上下文*的公共数据存储

![](img/2b293e29fc15b0797f113b85dd429b6e_386_0.png)

**图14.15**  
修改日期格式以消除时间、星期和日期字符串

![](img/2b293e29fc15b0797f113b85dd429b6e_386_1.png)

## 了解 Core Data 的对象和编程模型

Core Data 使用三个对象定义其工作环境，如表14.1所示。如果你在项目中使用 Core Data 模板和 Xcode 编辑器，持久化存储协调器和托管对象模型会“开箱即用”。然而，你仍然需要访问托管对象上下文来读写数据。

**表14.1 Core Data 环境对象**

| 对象 | 用途 |
|---|---|
| `NSPersistentStoreCoordinator` | 对数据进行归档和反归档，并保持已保存数据和实时数据同步。在 Core Data 模板中你可以忽略此对象。样板代码会为你初始化它，并且它会自动工作。 |
| `NSManagedObjectModel` | 数据模型中使用的实体、属性、关系及其他特性的集合。托管对象模型定义了数据的组织方式，但不存储数据——它是模型的模板。不要动态更改模型。最好将模型管理交给 Xcode 中的模型编辑器。 |
| `NSManagedObjectContext` | 完整的数据库，包含数据。模板会自动创建一个上下文。应用程序可以使用多个上下文——但通常一个就足够了。 |

用于读写数据的 Core Data 类如表14.2所示。

**表14.2 用于编辑和搜索的 Core Data 对象**

| 对象 | 用途 |
|---|---|
| `NSManagedObject` | 实体对象的包装器，可将它们接入 Core Data 内置的归档和编辑功能中。有时你需要直接访问托管对象，其他时候则访问其关联的实体描述对象。支持键值编码（Key-Value Coding，KVC）。 |
| `NSEntityDescription` | 定义命名实体的名称、属性列表和关系。托管对象保存数据，其实体描述则说明数据是如何组织的。 |
| `NSFetchRequest` | 搜索的包装器。搜索请求会被发送到上下文，上下文返回符合搜索条件的对象数组。 |
| `NSPredicate` | 定义搜索请求细节的谓词对象。它保存搜索字符串或模式、匹配条件、大小写敏感等底层细节。 |
| `NSSortDescriptor` | 指定搜索结果排序方式的对象。可选地，可以在搜索请求之前将其传递给谓词对象。 |

### 创建获取请求

要读取数据，请创建获取请求并将其传递给托管上下文。获取请求可能很复杂，代码接口也不直观，但概括地说，搜索无非就是创建请求、设置参数、传递给上下文，然后读取结果。

示例代码如下：

```objective-c
NSEntityDescription *albumEntity =
    [NSEntityDescription entityForName:@"Album"
    inManagedObjectContext:managedObjectContext];
NSFetchRequest *theRequest = [[NSFetchRequest alloc] init];
[theRequest setEntity:albumEntity];
returnArray = [managedObjectContext
    executeFetchRequest:theRequest error:&error];
```

在模型的上下文中，这段代码执行了最简单的搜索。`returnArray` 返回上下文中所有 Album 实体的列表，也就是所有专辑的列表。然后你可以处理这个数组，进一步从中提取值。

### 使用谓词

要缩小搜索范围，可以向搜索请求添加谓词：

```objective-c
NSPredicate *thePredicate =
    [NSPredicate predicateWithFormat:@"Name == 'An Album Name'"];

[theRequest setPredicate:thePredicate];
//Run the search...
```

谓词语法很复杂，但明显类似于它所基于的正则表达式匹配。`predicateWithFormat:` 允许使用通常的 `withFormat:` 选项进行替换。使用它来动态搜索字符串和其他值。

```objective-c
NSPredicate *thePredicate =
    [NSPredicate predicateWithFormat:@"Name == %@", aString];
```

表14.3展示了一些其他示例。有关谓词编程的更多信息，请参阅 Cocoa 文档中的《谓词编程指南》。

**表14.3 谓词搜索字符串示例**

| 谓词 | 用途 |
|---|---|
| `like 'string'` | 搜索相似的字符串。字面字符串必须包含单引号。 |
| `contains[c] 'ey'` | 查找所有包含“ey”的记录，忽略大小写和变音符号；即带重音符号的非英文字符。 |
| `beginsWith 'A'` | 查找所有以“A”开头的记录。 |
| `ANY salary < 20000` | 返回找到的第一个薪资小于 20,000 的记录。数字无需加引号。 |
| `ALL salary > 1000000` | 返回所有超过一百万货币单位的薪资。（单位取决于数据和上下文。） |

### 使用排序描述符

排序描述符可以根据指定的键将结果按升序或降序排序。描述符通过数组传递，因此可以指定多个描述符——虽然这并不总是有用的。

```objective-c
NSSortDescriptor *sortDescriptor = [[NSSortDescriptor alloc]
    initWithKey:@"Artist" ascending:YES];
[theRequest setSortDescriptors:
    [NSArray arrayWithObject: sortDescriptor]];
```

获取请求必须指定一个实体，并且可以指定谓词和排序描述符。

> **提示**
>
> 新手面临的最大挑战之一是没有简单的查询机制。没有类似“帮我找到具有以下属性的对象”这样的简单方法。相反，查询是通过查询对象处理的，每次查询都必须组装和打包这些对象。你可以编写查询包装器来简化代码接口，从而使 Core Data 更易于使用。

### 创建针对对多关系的获取请求

通常，你可以使用简单的谓词搜索来返回结果数组，无需更多代码。

遗憾的是，Core Data 不支持目标为对多关系的搜索——也就是说，一个项目可以链接到许多其他项目。

例如，如果你想按艺术家过滤专辑，很自然会认为可以这样做：

```objective-c
NSEntityDescription *albumEntity =
    [NSEntityDescription entityForName:@"Album"
    inManagedObjectContext:managedObjectContext];
NSFetchRequest *theRequest = [[NSFetchRequest alloc] init];
[theRequest setEntity:albumEntity];
NSPredicate *thePredicate =
    [NSPredicate predicateWithFormat:@"Artist == %@", aString];

[theRequest setPredicate:thePredicate];
```

但这行不通。Artist 键是一个关系，正则表达式搜索代码无法跟踪对多关系链接。

一种变通方法是创建一个单独的数组来存放专辑的键和值，并在该数组中搜索 Artist 键。你可以不指定谓词，而是请求所有专辑的列表，然后搜索返回的数组。

与直觉相反的是，这解决了问题，而且只增加了很少的额外复杂性。完整的解决方案代码如下。搜索被封装在一个 `refreshList:` 方法中，应用程序需要刷新过滤后的专辑列表时可以调用该方法。

```objective-c
- (void) refreshList: (id) sender {
    NSEntityDescription *albumEntity =
        [NSEntityDescription entityForName:@"Album"
        inManagedObjectContext:managedObjectContext];
    NSFetchRequest *theRequest = [[NSFetchRequest alloc] init];
    [theRequest setEntity:albumEntity];
    searchReturnArray = [NSMutableArray arrayWithCapacity:50];
    tempArray =
        [managedObjectContext executeFetchRequest:theRequest
        error:nil];
    [tempArray enumerateObjectsUsingBlock:^(id obj,
        NSUInteger idx, BOOL *stop) {
        NSString *albumName = [obj valueForKey:@"Name"];
        NSString *artistName =
            [[obj valueForKey:@"Artist"] valueForKey:@"Name"];
        if ([artistName isEqual:selectedName.stringValue])
            [self.searchReturnArray insertObject:
                [NSDictionary dictionaryWithObject: albumName
                forKey:@"FileName"] atIndex: 0];
    }];
    self.searchReturnArray = searchReturnArray;
    NSLog(@" %@", searchReturnArray);
}
```

