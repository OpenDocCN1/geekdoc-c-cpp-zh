
## 加载设置值

在应用程序的用户界面准备就绪后，现在是时候了解如何以编程方式加载首选项设置的数值，然后在应用程序中显示它们的时候了。此显示很有用，因为它使用户有机会查看设置的数值，而无需进入设置应用程序。

### 试一试 加载设置值

- 1. 将以下以粗体显示的代码行插入到 `MainViewController.m` 文件中（请确保包含密码和喜欢的颜色标记的代码行全部在一行输入，与以下代码中的显示方式不同）：

```objective-c
#import "MainViewController.h"
#import "MainView.h"

@implementation MainViewController

- (IBAction) loadSettings: (id) sender{

    NSUserDefaults *defaults = [NSUserDefaults standardUserDefaults];

    NSString *strLoginname = [defaults objectForKey:@"login_name"];
    NSString *strPassword = [defaults objectForKey:@"password"];
    NSString *strColor = [defaults objectForKey:@"color"];

    NSString *str = [[[NSString alloc] initWithFormat:@"Login name is \"%@\", password is \"%@\", and favorite color is \"%@\"",
                      strLoginname, strPassword, strColor];

    UIAlertView *alert = [[UIAlertView alloc]
                          initWithTitle:@"Settings Values"
                          message:str
                          delegate:nil
                          cancelButtonTitle:@"Done"
                          otherButtonTitles:nil]
[alert show];

[strLoginname release];
[strPassword release];
[strColor release];
[str release];
[alert release];
}
```

- 2. 按 Command-R 在 iPhone 模拟器上测试应用程序。应用程序加载后，点击“加载设置值”按钮，您应该会在警报视图中看到设置值显示（见图 11-18）。

![](img/aab2d775c46f70cd606f2e58e2521324_309_0.png)

## 其工作原理

要加载首选项设置的数值，您使用一个名为 NSUserDefaults 的类：

```
NSUserDefaults *defaults = [NSUserDefaults standardUserDefaults];
```

前述语句返回 NSUserDefaults 类的唯一一个实例。可以将 NSUserDefaults 视为一个通用数据库，您可以使用它来存储应用程序的首选项设置。

要检索首选项设置的数值，您使用 objectForKey: 方法并指定要检索的首选项设置的名称：

```
NSString *strLoginname = [defaults objectForKey:@"login_name"];
NSString *strPassword = [defaults objectForKey:@"password"];
NSString *strColor = [defaults objectForKey:@"color"];
```

## 重置首选项设置值

有时您可能想要重置应用程序的首选项设置的数值。如果您在 Root.plist 文件中犯了错误并希望重置所有设置，则尤其如此。最简单的方法是从手机或模拟器中删除应用程序。为此，只需点按并按住应用程序的图标，当图标开始抖动时，点按 X 按钮以删除应用程序。与应用程序关联的首选项设置也将被删除。

另一种清除首选项设置数值的方法是导航到包含您应用程序的文件夹（在 iPhone 模拟器上）。iPhone 模拟器上的应用程序存储在以下文件夹中：~/Library/Application Support/iPhone Simulator/User/Applications/（请注意，波浪号 (~) 代表您的主目录，而不是根硬盘）。在该文件夹内，您需要找到包含您应用程序的文件夹。在应用程序文件夹内有一个 Library/Preferences 文件夹。删除以 application_name.plist 结尾的文件（见图 11-19）并且您的首选项设置现在将被重置。

![](img/aab2d775c46f70cd606f2e58e2521324_310_0.png)

图 11-19

## 保存设置值

现在您已经了解如何加载首选项设置的数值，请使用以下试一试来了解如何将数值保存回首选项设置。这允许用户直接在应用程序内修改其首选项设置，而无需使用设置应用程序来执行此操作。

### 试一试 保存设置值

- 1. 在 FlipsideViewController.m 文件中，插入以下以粗体显示的代码：

```objective-c
#import "FlipsideViewController.h"

@implementation FlipsideViewController

@synthesize delegate;
@synthesize loginName;
@synthesize password;
@synthesize favoriteColor;

NSMutableArray *colors;
NSString *favoriteColorSelected;

- (void)viewDidLoad {
colors = [[NSMutableArray alloc] init];
[colors addObject:@"Red"];
[colors addObject:@"Green"];
[colors addObject:@"Blue"];

NSUserDefaults *defaults = [NSUserDefaults standardUserDefaults];
loginName.text = [defaults objectForKey:@"login_name"];
password.text = [defaults objectForKey:@"password"];

//---find the index of the array for the color saved---
favoriteColorSelected = [[NSString alloc] initWithString:
[defaults objectForKey:@"color"]];
int selIndex = [colors indexOfObject:favoriteColorSelected];

//---display the saved color in the Picker view---
[favoriteColor selectRow:selIndex inComponent:0 animated:YES];
[super viewDidLoad];
self.view.backgroundColor = [UIColor viewFlipsideBackgroundColor];
}

- (IBAction)done {
NSUserDefaults *defaults = [NSUserDefaults standardUserDefaults];
[defaults setObject:loginName.text forKey:@"login_name"];
```

## 摘要

在本章中，您已经了解如何利用 iPhone 的应用程序首选项功能将应用程序的首选项保存到设置应用程序中。这样做可以让您将保存和加载应用程序首选项设置的绝大多数繁琐任务委托给操作系统。您需要做的就是使用 NSUserDefaults 类以编程方式访问首选项设置。

## 练习

- 1. 您已了解到可以使用 NSUserDefaults 类访问应用程序的首选项设置值。检索和保存值的操作方法是什么？
- 2. 可以通过哪两种方式删除应用程序的首选项设置？
- 3. 在属性列表编辑器中，“添加子项”按钮和“添加同级”按钮有什么区别？

## 本章学到的内容

| 主题 | 关键概念 |
|---|---|
| 向您的应用程序添加应用程序首选项 | Add a Settings Bundle file to your project and modify the Root.plist file. |
| 加载首选项设置的数值 | NSUserDefaults *defaults = [NSUserDefaults standardUserDefaults];<br>NSString *strLoginname = [defaults objectForKey:@"login_name"]; |
| 重置首选项设置值 | Either remove the entire application from the Home screen, or remove it via the iPhone Simulator folder on your Mac. |
| 保存首选项设置的数值 | NSUserDefaults *defaults = [NSUserDefaults standardUserDefaults];<br>[defaults setObject:loginName.text forKey:@"login_name"]; |

## 12

## 使用 SQLite3 进行数据库存储

### 本章将学习的内容

- 如何在 Xcode 项目中使用 SQLite3 数据库
- 如何创建和打开 SQLite3 数据库
- 如何使用各种 SQLite3 函数执行 SQL 字符串
- 如何使用绑定变量将值插入到 SQL 字符串中

在上一章中，您了解了使用文件进行数据持久化。对于简单的应用程序，您可以将要持久化的数据写入简单的文本文件。对于更结构化的数据，您可以使用属性列表。对于大型且复杂的数据，使用数据库存储更为高效。iPhone 随附 SQLite3 数据库库，您可以使用它来存储数据。将数据存储在数据库中后，您的应用程序可以填充表格视图或以结构化方式存储大量数据。

本章向您展示如何在应用程序中使用嵌入式 SQLite3 数据库。

## 使用 SQLITE3

要在应用程序中使用 SQLite3 数据库，首先需要在 Xcode 项目中添加 libsqlite3.dylib 库。使用以下试一试来了解如何操作。您需要下载本章中此项以及其余试一试功能所指示的代码文件。
