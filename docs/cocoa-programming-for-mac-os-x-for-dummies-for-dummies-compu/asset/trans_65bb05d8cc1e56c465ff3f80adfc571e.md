

# 处理你自己的类

由于类构成了 Cocoa 项目的基础，你会经常使用它们。通常，你创建一个类来存储和操作应用程序的数据。Cocoa 将这种类型的类称为模型（Model）。负责显示数据的类是视图（View）。第三种类——控制器（Controller）——在模型和视图之间进行协调。

以下是如何在棋盘（board）术语中创建和使用你自己的类：

- 1. 创建一个类。
- 2. 构建一个接口。
- 3. 添加一个控制器类并将其连接到接口。
- 4. 定义该类的方法。
- 5. 定义该类的一个动作（action）。

若要尝试在 Objective-C 中使用类，请遵循以下步骤：

- 1. 创建一个 Cocoa 项目。
  启动 Xcode 并选择“文件：新建项目”（File:New Project）。在弹出的对话框中，从选项列表中选择“Cocoa 应用程序”（Cocoa Application），命名该项目，然后创建它。

- 2. 创建一个类。
  你可以在 Xcode 或 Interface Builder 中创建类。对于此类，请使用 Xcode：
  - a. 选择“文件：新建文件”（File:New File）。
  - b. 在弹出的窗口中，选择 Objective-C 类并点击“下一步”（Next）。
  - c. 在出现的下一个窗格中，为新类的实现文件命名。将其命名为 Driver.m，如图 6-1 所示。

这是你将用来创建出租车司机对象的类。当你创建 Driver 类时，头文件和实现文件——分别是 Driver.h 和 Driver.m——将出现在你的项目中。

- 3. 创建一个新的控制器类：
  - a. 在 Xcode 中双击 mainMenu.xib 以显示 Interface Builder。
  - b. 在“库”（Library）窗口中，搜索 object 并将一个 NSObject 项拖到项目窗口中。
  - c. 按下 Cmd+D，并在“身份检查器”（Identity Inspector）中将新类命名为 MyViewController，如图 6-2 所示。

此类将与你的界面进行通信。

- 4. 创建一个接口：
  - a. 在 Interface Builder 中，打开 NIB 文件中的默认窗口。
  - b. 从“库”窗口中，将一个推送按钮（NSButton）、一个复选框和四个标签（Label）控件拖到窗口中，以显示你的窗口。

你使用两个标签控件来显示出租车司机的姓名以及本次行程的司机。另外两个标签控件只是界面的标签（票价和司机）：

![](img/ea40cad434a338535474e82c1a6ace20_140_0.png)

**图 6-1：** 创建一个类来表示出租车司机。

![](img/ea40cad434a338535474e82c1a6ace20_140_1.png)

**图 6-2：** 在“身份检查器”窗口中将该类命名为 MyController。

图 6-3 显示了界面，此时空的标签控件已被选中。

![](img/ea40cad434a338535474e82c1a6ace20_141_0.png)

- 5. 为 MyController 类添加出口（outlets）。

对于该项目，你需要在 MyController 类中定义三个出口：

- a. 在 XIB 项目窗口中，选中 MyController 类（图 6-2）。
- b. 按下 Cmd+6 以打开“检查器”（Inspector）窗口，并为该类添加三个出口（distanceCheckbox、driverDisplay 和 fareDisplay）。

driverDisplay 和 fareDisplay 出口让你能够访问界面中的两个标签控件，从而显示票价和司机的姓名。第三个出口（distanceCheckbox）允许你查看“距离 > 10 英里”复选框是否被选中。

图 6-4 显示了新的出口。

- 6. 为 MyController 类添加一个动作。

为 MyController 添加一个动作并将其命名为 calculateFare:（注意所需的尾随冒号），如图 6-5 所示。这是“计算票价”按钮触发的动作。当用户点击此按钮时，应用程序将显示出租车司机的姓名，并基于一个参数：距离，来计算票价。如果行程超过十英里，程序返回一种票价。如果行程少于十英里，程序返回另一种票价。

![](img/ea40cad434a338535474e82c1a6ace20_142_0.png)

图 6-4：为 MyController 类添加三个出口。

![](img/ea40cad434a338535474e82c1a6ace20_142_1.png)

![](img/ea40cad434a338535474e82c1a6ace20_142_2.png)

![](img/ea40cad434a338535474e82c1a6ace20_142_3.png)

图 6-5：为 MyController 类添加 calculateFare: 动作。

- 7. 将界面连接到 MyController 实例。

在将这三个出口和一个动作连接到界面之前，你无法在代码中执行任何操作。

- a. 从 NIB 文件窗口中的 MyController 实例按住 Control 键并拖拽到紧邻 Fare 标签的标签上。
- b. 当松开鼠标时，会显示一个小的黑色连接列表叠加层，从中选择 fareDisplay。

在项目窗口中选中 MyController，按下 ⌘+5 以查看你建立的那些连接。

- c. 对其他标签控件和看起来像复选框的 NSButton 重复相同的过程，将它们分别连接到各自的出口（driverDisplay 和 distanceCheckbox）。

图 6-6 显示了完成的连接。

- 8. 创建 MyController 的文件。

在项目窗口中选中 MyController 类，并选择“文件：写入类文件”（File:Write Class Files）。MyController.h 和 MyController.m 文件将被添加到 Xcode 中的项目中。

![](img/ea40cad434a338535474e82c1a6ace20_143_0.png)

![](img/ea40cad434a338535474e82c1a6ace20_143_1.png)

图 6-6：MyController 的出口和动作。

9. 完成后，在 Interface Builder 中选择“文件：保存”（File:Save）以保存 NIB 文件。

10. 返回 Xcode 添加代码以使你的项目运行。

你会找到以下四个文件：Driver.h、Driver.m、MyController.h 和 MyController.m。参见图 6-7。如果 Driver 和 MyController 的头文件和实现文件不在 Classes 文件夹中，请将它们移动过去。创建它们时，它们会出现在项目中最后选定的文件夹中。这有助于保持条理清晰。

继续以下章节以完成你的项目。

![](img/ea40cad434a338535474e82c1a6ace20_144_0.png)

图 6-7：在 Xcode 中移动控制器的头文件和实现文件到 Classes 文件夹。

### 定义类

点击 Driver.h 文件以查看其内容。Driver 类充当模型。向此文件添加以下代码以定义类接口：

```objective-c
#import <Cocoa/Cocoa.h>

@interface Driver : NSObject {
    NSString *firstName;
}
- (int)go:(BOOL)distance;
- (NSString *)firstName;
- (void)setFirstName:(NSString *)name;
@end
```

代码首先包含适当的头文件：

```objective-c
#import <Cocoa/Cocoa.h>
```

Cocoa 框架为你的 Cocoa 应用程序提供基本功能。

然后，代码定义了一个 Driver 类，它从 NSObject 继承功能：

```objective-c
@interface Driver : NSObject {
    NSString *firstName;
}
@end
```

你在 Cocoa 中使用的大多数类都继承自 NSObject。事实上，本书中的所有类都继承自 NSObject 超类。NSObject 是 Cocoa 编程的主要基类。你可以将 NSObject 视为一种包含用于创建对象的方法和变量的通用类。当你创建基于窗口、按钮或其他元素的类时，请使用 NSObject。在这个例子中，你定义了一个类（Driver），它是一个 NSObject。Driver 类有一个存储出租车司机姓名的 firstName 实例变量。

其余的代码定义了 Driver 类的三个方法：

```objective-c
- (int)go:(BOOL)distance;
```

第一个方法 go 是当用户希望司机带他到某处时代码执行的内容。go 有一个参数：代表距离的布尔值。对于这个例子，想象出租车司机对短途行程（十英里以下）使用一种费率，对长途行程使用另一种费率。由于这种费率方案只包含两种价格，你可以使用布尔变量来确定收取哪种费率。布尔值可以是两个可能的值之一：YES 或 NO。

剩余的两个方法用于设置和获取出租车司机的姓名。稍后，当你从此类创建实例时，你将使用 setFirstName 来分配出租车司机的姓名：

```objective-c
- (void)setFirstName:(NSString *)name;
```

