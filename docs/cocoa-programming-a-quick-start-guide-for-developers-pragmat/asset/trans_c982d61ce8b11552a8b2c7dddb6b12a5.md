
现在，我们先把这个即时书架放到一边；我们将从数据模型重新开始，并手动添加控制器和视图。这将帮助你理解 Core Data 应用程序中涉及的各个层。

### 22.3 托管对象上下文

回到项目的一个全新副本，我们从你已经创建好数据模型之后继续：该模型包含一个名为 PragBook 的单一实体，其中有 title 和 author 两个必需的字符串属性。打开你的 nib 文件。

向 nib 的 Document 窗口添加一个数组控制器。使用 Identity inspector 将数组控制器的名称设置为 BookController。注意，我们更改的是名称，而不是类。要设置该数组控制器，我们只需做两处小改动。

首先，打开 BookController 的 Attributes inspector。这次将模式设置为 Entity，并在实体名称中输入 *PragBook*。

![](img/9355405953264484a02198b0e3d25b7e_353_0.png)

接下来，打开该数组控制器的 Bindings inspector。在底部的“Parameters”标题下，展开 Managed Object Context 的展开三角形。我会告诉你需要设置什么，然后解释你做了什么。

选中“Bind to”复选框，并从下拉列表中选择 CDBookshelf_AppDelegate。将 Controller Key 和 Value Transformer 条目留空。将 Model Key Path 设置为 managedObjectContext。

你应当得到类似下面的内容：

![](img/9355405953264484a02198b0e3d25b7e_354_0.png)

托管对象上下文是你的运行中应用程序与从磁盘保存和检索数据的机制之间的分界线。你的运行中应用程序将使用在运行时根据数据模型创建的对象（实际上是托管对象）与托管对象上下文交互。

将创建 NSManagedObject 或 NSManagedObject 的子类来表示数据模型中的每个实体。实际对象按需创建。

因此，你通过两个步骤将控制器连接到模型。你必须通过应用程序委托将控制器绑定到其托管对象上下文。你还必须使用 Attributes inspector 指明该控制器负责哪个实体。

你的模型和控制器已经设置好。现在，完全按照你在第345页第21.8节 *创建书架视图* 中所做的那样重新创建视图。这是使用 MVC 的优点之一。我们完全更改了模型，而无需对视图做任何更改。

![](img/9355405953264484a02198b0e3d25b7e_355_0.png)

你甚至不需要修改视图与控制器之间的连接和绑定。和之前一样，使用 Controller Key 设置 arrangedObjects，并将第一列的 Model Key Path 设置为 title、第二列设置为 author，从而将表格列绑定到控制器。你需要将按钮连接到控制器的 add: 和 remove: 方法。

### 22.4 持久化层

点击 Build & Run。向你的应用程序添加一些书籍，然后退出。重新启动。嘿，等一下。你的数据怎么了？为什么迎接你的是一个空表格？

还记得第17章 *将数据保存到磁盘*（第270页）中说过，你的应用程序数据存储在用户主目录的 ~/Library/Application Support 下。该目录的名称与你的应用程序相同，所以我查看 CDBookshelf 内部，找到了文件 storedata。用你喜欢的文本编辑器打开 storedata，你应该会看到数据已被存储，内容大致如下：

```
<object type="PRAGBOOK" id="z106">
    <attribute name="title" type="string">
                  The Passionate Programmer</attribute>
    <attribute name="author" type="string">Chad Fowler</attribute>
</object>
```

因此，数据无需你费任何力气就保存到了磁盘。你只需做一个简单更改，就能让应用程序重新启动时从磁盘读取数据。在 Book Controller 的 Attributes inspector 中，选中 Prepares Content 复选框。

![](img/9355405953264484a02198b0e3d25b7e_356_0.png)

点击 Build & Run，应用程序启动时，表格中会填充你之前输入的值。³ 所有这些都在后端由持久化存储协调器为你处理。你的托管对象上下文与运行中的应用程序交互，根据数据模型创建所需对象。它还与持久化存储协调器交互，以存储和检索数据。

如果你查看为你生成的模板代码，会发现你在应用程序委托中创建了一个 NSPersistentStoreCoordinator。以下是 persistentStoreCoordinator 方法中的一段代码：

```
NSURL *url = [NSURL fileURLWithPath: [applicationSupportDirectory
    stringByAppendingPathComponent: @"storedata"]];
persistentStoreCoordinator = [[NSPersistentStoreCoordinator alloc]
    initWithManagedObjectModel: mom];
if (![persistentStoreCoordinator
    addPersistentStoreWithType:NSXMLStoreType
    configuration:nil URL:url options:nil error:&error]){
```

在第一处高亮行中，我们将 storedata 追加到 Application Support 目录中 CDBookshelf 文件夹的路径后，补全了数据在磁盘上的存储路径。在第二处高亮行中，我们将持久化存储添加到持久化存储协调器，并将其类型设置为 NSXMLStoreType。因此，我们指定希望将数据存储为 XML，并命名了将包含数据的文件。

你经常会使用 XML 作为持久化格式进行开发工作，然后决定是否切换到 SQLite 或某种自定义格式。

> ³. 这是代码下载中的项目 CDBookshelf1。

我们的实体关系图现在如下所示：

![](img/9355405953264484a02198b0e3d25b7e_359_0.png)

我们有一个简单的数据模型，包含三个实体、少量属性，以及每对实体之间的关系。在我们的模型可以正式投入使用之前，还有一步要做。

### 22.6 选择关系的删除规则

在完成这个数据模型之前，我们需要考虑用户删除数据时会发生什么。例如，当用户删除一本书时，该书中的章节也应该消失。但当用户删除一个章节时，书不应该消失。当用户删除一本书时，作者应该发生什么？

当用户删除实体时，我们有几种选项：Deny（拒绝）、Nullify（置空）、Cascade（级联）和 No Action（不操作）。这些删除规则是定义关系的一部分。让我们看看当前模型中的一些示例。

首先，我们应如何设置 chapters 关系的删除规则？我们要确保，如果一本书中还有任何章节，用户就不能删除当前包含这些章节的书。

换句话说，我们选择 Deny 选项，这样当用户尝试删除该书时，如果仍有章节会因为失去所属的书而变成孤儿，他们的请求就会被拒绝。如果关系目标处至少有一个项，Deny 选项就不会让你删除该实体。

作者则不同。一个作者可能写了不止一本书，因此我们删除一本书时不想删除作者。在这种情况下，我们选择 Nullify 选项。使用 Nullify 时，即使一个或多个作者仍然存在，也不会阻止我们删除该书。我们会将每个作者中的 book 关系设置为 null。我们将该关系置空，因为那本书已不存在，所以作者不可能写过它。

对于 chapters 关系，我们还有另一个选项。当我们删除书时，也可以删除该书的所有章节。换句话说，我们希望删除操作向下级联。我们仍然坚持这一想法：如果书不存在，章节继续存在就没有意义——我们只是选择了不同的结果。

因此，将 chapters 的 Delete rule 设置为 Cascade。反向关系 book 的 Delete rule 应设置为 Nullify。当我们删除一个章节时，不删除它所属的书，但要确保该书不再引用这个已删除的章节。类似地，authors 和 books 的规则应设置为 Nullify。⁶

### 22.7 更新视图

到这一步，你应该已经能够轻松使用 Interface Builder，而不需要太多指导。打开你的 nib 文件，选择表格视图，并将列数减少到一。选中内容视图中的所有组件，然后选择 Layout > Embed Objects In > Box。将框的标题改为 Prag Books。选中该框，粘贴两次，并自定义内容使其如下所示：

![](img/9355405953264484a02198b0e3d25b7e_360_0.png)

章节框和作者框的内容需要取决于选中了哪本书。这是控制器层的任务。

> 6. 你可以将你的工作与代码下载中 CDBookshelf2 的数据模型进行比较。
