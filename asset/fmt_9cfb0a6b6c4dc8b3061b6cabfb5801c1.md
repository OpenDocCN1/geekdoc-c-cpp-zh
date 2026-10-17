
此外，在 iPhone 上，保存当前状态通常是必要的。如果某人正在使用你的应用程序然后接了电话，你希望在他们打完电话后将他们回到之前所在的地方。随着 iOS 4 和 5 以及多任务处理的实现，这现在不那么必要了，但如果你的应用程序在下次启动时能记住他们正在做什么，你的用户仍然会非常感谢。

一旦你实例化了对象，只需调用 `setObjectForKey` 一个对象。如果我们想保存 `sherlock.holmes` 的用户名，我们只需调用以下行代码：

```
[prefs setObject:@"sherlock.holmes forKey:@"username"]
```

你可以根据在偏好文件中存储的信息类型，使用 `setInteger`、`setDouble`、`setBool`、`setFloat` 和 `setObject`。假设你有书籍的数量，在偏好文件中存储它可以使用：

```
[prefs setInteger:10 forKey:@"booksList"]
```

在偏好文件中写入数据时，通常不需要 `synchronize`。为了写入，我们需要调用 `synchronize` 方法：

```
[synchronize]
```

只需三行代码，我们就可以使用 `UserDefaults`。这里是使用该对象的示例：

```
NSDefaults *prefs = [NSUserDefaults standardUserDefaults];
[prefs setObject:@"sherlock.holmes forKey:@"username"];
[prefs setInteger:10 forKey:@"booksList"]
```

# 读取偏好

读取偏好与写入偏好类似，同样简单。就像写入一样，第一步是获取 `UserDefaults` 对象：

```
NSDefaults *prefs = [NSUserDefaults standardUserDefaults];
```

现在我们有了该对象，就可以访问偏好值。对于读取，我们使用 `stringForKey`。这里是使用示例：

```
NSString *username = [prefs stringForKey:@"username"];
NSInteger booksList = [prefs integerForKey:@"booksList"];
```

在执行这些行代码时，请注意 `username` 是 `NSString`，而 `booksList` 是 `NSInteger`。在读取示例中，我们不需要 `synchronize`。

在商业世界，数据库可能会变得非常大。对于数据库管理员来说，处理 500GB 大的数据库并不意外，在某些情况下数据库可能会比这大得多。SQLite 能够毫无问题地处理较小的数据库，但如果你的数据库变得过大，就会开始遇到性能问题。

SQLite 缺乏企业级数据库解决方案的一些备份和数据恢复功能。

在本章中，我们将专注于使用 SQLite 作为我们的数据库引擎。如果你正在开发的应用程序中存在任何上述功能，你可能需要研究企业级数据库解决方案，这超出了本书的范围。

> 注意：SQLite 的名称来源于结构化查询语言或 SQL。SQL 是用于从数据库中输入、搜索和检索数据的语言。

Apple 努力解决了数据库开发中的许多挑战。作为开发者，你不需要熟悉 SQL，因为 Apple 已经为你处理了直接的数据库交互。Apple 有名为 Core Data 的框架，它让与数据库的交互变得简单得多。Core Data 是 Apple 从一个名为 Enterprise Object Framework 的 NeXT 产品改编的，它将为你处理所有的数据库交互。使用 Core Data 比通过 SQL 直接与 SQLite 数据库交互要容易得多，而后者超出了本书的范围。

# 开始使用 Core Data

让我们从创建一个新的 Core Data 项目开始。

1. 打开 Xcode 并选择 `File > New Project`。创建一个 Mac OS X Core Data 项目，从左侧菜单中选择 Application。它位于 Mac OS X 标题下方。见图 11–1。

![](img/322e107ddf8f5cd963a6efafdcd86f38_248_0.png)

图 11–1。创建一个新项目。

2. 完成后点击 Next 按钮。下一个屏幕将允许你决定保存项目的位置以及你想使用的名称。在本章中，我们将使用名称 BookStoreCoreData。

3. 在底部附近你会看到三个复选框。第一个复选框标记为 Use Core Data。确保已勾选了此项，然后点击 Next。

![](img/322e107ddf8f5cd963a6efafdcd86f38_249_0.png)

图 11–2。使用 Core Data。

一旦完成这些操作，你的新项目就会打开。它看起来与标准应用程序相似，不同之处在于你现在有一个 `BookstoreCoreData.xcdatamodel`。这个文件被称为数据模型，将包含你将存储在 Core Data 中的数据信息。

## 模型

如果你点击文件夹旁边的三角形，你会看到一个名为 `BookStoreCoreData.xcdatamodel` 的文件。该文件将包含你想存储在数据库中的数据信息。点击模型文件，它就会打开。你将看到一个与图 11–3 显示的窗口。

![](img/322e107ddf8f5cd963a6efafdcd86f38_250_0.png)

图 11–3。空白模型。

窗口分为四个部分。在左侧你有你的实体 `entities`。在更常见的术语中，这些是你想要存储在数据库中的对象或项目。

右右上窗口包含属性 `attributes`。属性是关于实体的信息片段。例如，书可以是一个实体，而书名将是该实体的一个属性。

# 第 11 章：存储信息

> 注意：在数据库术语中，实体是你的表，实体的属性被称为列。从这些实体创建的对象被称为行。

右中间窗口将向你显示实体的所有关系。关系将一个实体连接到另一个实体。例如，我们将创建一个 Book 和一个 Author 实体。然后我们将它们关联起来，使得每本书都有一个作者。右下部分处理抓取属性 `fetched properties`。抓取属性超出了本书的范围，但它们允许你为数据创建过滤器。

让我们创建一个实体。

1. 点击窗口左下角的加号，或从菜单中选择 `Editor > Add Entity`。见图 11–4

![](img/322e107ddf8f5cd963a6efafdcd86f38_251_0.png)

图 11–4。添加新实体。

2. 在左侧，你现在有了命名实体的选项。我们将为此实体使用名称 Book。

# 第 11 章：存储信息

> 注意：通常认为将实体的名称首字母大写是一项良好的做法。

3. 现在让我们添加一些属性。属性被视为书的细节，因此我们将存储标题、作者、价格和书出版的年份。显然，在你自己的应用程序中，你可能想要存储更多信息，如出版者、页数和类型，但我们想从简单的开始。点击窗口右下角的加号，或选择添加属性选项，确保你已选择了左侧的实体。

![](img/322e107ddf8f5cd963a6efafdcd86f38_252_0.png)

图 11-5。添加新属性。

4. 你的属性只有两个选项：名称和数据类型。让我们把此属性称为 title。与实体不同，属性名称应该全小写。

5. 现在，我们需要选择一个数据类型。选择正确的数据类型非常重要。它将影响数据如何从数据库中存储和检索。列表中有 12 个项目，看起来可能非常令人生畏。我们将讨论最常用的选项，随着你熟悉 Core Data，你可以尝试其他选项。最常用的选项是 String、Integer 32、Float 和 Date。对于书名，选择 String。

**String：** 这是用于存储文本的属性类型。这应该用于存储任何非数字或日期的信息。在这个示例中，书名和作者将是字符串。

**Integer 32：** 属性实际上有三种不同的整数值。每种类型仅在于可能的最小值和最大值。在存储整数时，Integer 32 应该涵盖你的大部分需求。整数是不带小数的数字。如果你在整数属性中保存小数，小数部分将被截断。在这个示例中，出版年份将是一个整数。

**Float：** float 是一种可以存储小数数字的属性类型。float 与 double 属性相似，但它们在最小最大值上不同。float 能够处理任何值。在这个示例中，我们将使用 float 来存储书的价格。

**Date：** 日期属性顾如其名。它允许你存储日期和时间，然后根据这些值进行搜索和查找。我们将在本示例中使用这种类型。

6. 让我们为书创建剩余的属性。现在，添加 price。它应该是 float。添加书出版的年份。对于双单词的属性，标准做法是将第一个单词小写，第二个单词的首字母大写。例如，出版年份的理想名称可能是 yearPublished。选择 integer 32 作为属性类型。当你添加了所有属性后，你的屏幕看起来应该像图 11–6。

注意：属性名称不能包含空格。

# 第 11 章：存储信息

![](img/322e107ddf8f5cd963a6efafdcd86f38_254_0.png)

注意：如果你在处理数据库，你会注意到我们没有添加主键。主键是一个字段，通常是数字，用于唯一标识数据库中的每条记录。在 Core Data 数据库中，没有必要创建主键。框架将为你处理这一切。

现在我们已经完成了 Book 实体，让我们添加 Author 实体。

1. 添加一个新实体并命名为 Author。

2. 为此实体添加 lastName 和 firstName，它们都被视为字符串。

一旦完成这些操作，你的关系窗口中应该有两个实体。现在我们需要添加关系。

1. 点击“书籍” `Book` 实体，然后点击并按住屏幕右下角的加号。选择“添加关系” `Add Relationship`，如图 11–7 所示。

![](img/322e107ddf8f5cd963a6efafdcd86f38_255_0.png)

图 11–7。添加新关系。

2. 现在你将获得机会为你的关系命名。你通常会将关系命名为与其派生自实体相同的名称。在名称框中输入“author”，或从下拉菜单中选择 Author。

3. 现在，我们已经创建了关系的一半。要创建另一半，点击“作者” `Author` 实体。现在，点击屏幕底部的加号并选择“添加关系” `Add Relationship`。我们将使用我们正在连接的实体名称作为此关系的名称，因此将其命名为 books。我们会在实体名称后添加一个“s”，因为一个作者可以有很多本书。在“目标” `Destination` 下，选择 Book；在“反向” `Inverse` 下，选择你上一步步骤中创建的关系。你的模型现在看起来应该像这样

## 第 11 章：存储信息

> 注意：有时在 Xcode 中，在处理模型时，需要按下 tab 键来更新实体、属性和关系的名称。这个小特性可以一直追溯到早期的 WebObjects 工具。

![](img/322e107ddf8f5cd963a6efafdcd86f38_256_0.png)

图 11–8。最终的关系。

现在我们需要告诉代码关于我们的新实体。要做到这一点，选择 Book 实体和 Author 实体，然后选择 `编辑` `Editor` ➤ `创建 NSManagedObject 子类` `Create NSManagedObject Subclass`。你的屏幕看起来应该如图 11–9 所示。

## 第 11 章：存储信息

![](img/322e107ddf8f5cd963a6efafdcd86f38_257_0.png)

**图 11–9。** 将托管对象添加到你的项目中。

选择存储位置并将其添加到你的项目中。你不必更改此页面上的任何默认设置。然后点击“创建” `Create`。你会发现项目已添加四个文件。`Book.h` 和 `Author.h` 包含了关于书籍的头文件信息，`Book.m` 和 `Author.m` 包含了实际实现。这些文件非常简单，因为 Core Data 会为它们完成工作。你还会注意到，如果你回到模型并点击 Book，它将拥有一个新的类。它将不再是一个 `NSManagedObject`，而将是一个 Book 类。

让我们看看 `Author.h` 的部分内容：

```
#import <Foundation/Foundation.h>
#import <CoreData/CoreData.h>
```

```
@class Book;

@interface Author : NSManagedObject {
@private
}
@property (nonatomic, retain) NSString * lastName;
@property (nonatomic, retain) NSString * firstName;
@property (nonatomic, retain) Book * book;
}

end
```

```
@end
```

你会发现该文件开头包含了 Core Data 框架。这允许 Core Data 管理你的信息。在下下方，你将看到你创建的三个属性。

## 托管对象上下文 Managed Object Context

我们创建了一个名为 Book 的托管对象。Xcode 的巧妙之处在于，它会生成必要的代码来管理这些新的数据对象。在 Core Data 中，每个托管对象都应该存在于托管对象上下文中。上下文负责跟踪对象的更改、执行撤销操作以及将数据写入数据库。在这个示例中，我们不需要编写代码来创建或管理对象上下文，但当你探索在项目中使用 Core Data 时，你需要意识到它的存在。目前，生成类所提供的基础功能可以正常工作。

## 设置界面

以下步骤将帮助你设置界面：

1. 在项目中的 Resources 资源文件夹中，你应该有一个 `MainMenu.xib`。双击此文件，接口生成器 Interface Builder 应该会在新窗口中打开。在该窗口的左侧，你应该能看到当前对象的列表。如果没有看到这个窗口，点击窗口左下角的小箭头。点击“窗口” `Window` 对象。你的窗口将显示在屏幕的右侧。见图 11–10。

![](img/322e107ddf8f5cd963a6efafdcd86f38_259_0.png)

图 11–10。创建界面。

2. 应该有一个空白窗口。为了给我们的窗口添加一些功能，我们需要从对象库 Object Library 中添加一些对象。要查看对象库，选择 `View` 视图 > `Utilities` 工具 > `Object Library` 对象库。此对象库将向你展示添加到窗口的所有对象。我们将从添加一个数组控制器 Array Controller 开始。在对象库中，向下滚动直到找到 Array Controller。将其拖到窗口左侧的对象面板 Objects pane 中。见图 11–11。

![](img/322e107ddf8f5cd963a6efafdcd86f38_260_0.png)

图 11–11。新的数组控制器。

3. 双击 Array Controller 并输入名称 BookArray。现在选择 Array Controller 并查看对象的绑定 bindings。

> 注意：要查看任何对象的绑定，请选择 `View` 视图 > `Utilities` 工具 > `Show Bindings Inspector` 显示绑定检查器，或者如果你已经打开了工具窗口，请点击圆形符号。

4. 在 Parameters 参数下，如果托管对象上下文部分未展开，点击其旁边的箭头。现在勾选 Bind 绑定旁边的复选框，并从下拉菜单中选择 Book Store Data App Delegate。

5. 在 Model Key Path 模型键路径中输入 managedObjectContext。这将我们的 Array Controller 绑定到应用程序的默认 managedObjectContext。这将允许我们添加并保存书籍。见图 11–12。

![](img/322e107ddf8f5cd963a6efafdcd86f38_261_0.png)

图 11–12。绑定。

6. 在 Object Controller 对象控制器下，将模式从 Class 类改为 Entity Name 实体名称。在 Entity Name 处输入 Book。

![](img/322e107ddf8f5cd963a6efafdcd86f38_262_0.png)

图 11–13。分配实体名称。

7. 我们需要设置界面。在对象库中找到 Table View 表格对象并拖到窗口中。你可以移动它并调整大小以适应视觉需求。

8. 我们找到两个推按钮并将它们拖到窗口中。将其中一个按钮的文本更改为 Add，另一个改为 Delete。

> 注意：要更改按钮或其他许多图形对象的文本，只需双击对象并输入替换文本。

## 第 11 章：存储信息

![](img/322e107ddf8f5cd963a6efafdcd86f38_263_0.png)

图 11–14。窗口

我们现在有一个外观良好的窗口，但没有任何控件可以发挥作用。为了让这些对象具有意义，我们需要对它们进行绑定。

> 注意：Cocoa Bindings 是一种保持视图与控制器同步的方法。它们有助于减少你所需的代码量。

要将对象连接到控制器，你只需要 control 点击一个项目并将其拖到要连接的项上。

1. 首先，control 点击你的 Array Controller 并将其拖到 table view。会弹出一个小窗口，并选中一个输出 outlet。选择 content 内容。你正在告诉 table view 它将显示数组控制器的内容。见图 11–15。

![](img/322e107ddf8f5cd963a6efafdcd86f38_264_0.png)

图 11–15。设置绑定。

2. 现在 control-drag 从 Add 按钮到数组控制器并选择 Add。control-drag 从 Delete 按钮拖到数组控制器并选择 remove 删除。

> 注意：当对象成功连接时，它会闪烁两次以提醒程序员。
