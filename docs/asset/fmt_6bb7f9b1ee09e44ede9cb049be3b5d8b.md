
有了你创建的 UI，其余卡片的创建将是轻而易举。

## 添加事件处理

你还没有完成 UI，所以现在开始讨论事件处理器可能显得为过早，但由于只有两个处理器对于你可能添加的每个卡片位置都是相同的，你完全可以添加它们。你需要对每个形状元素以及代表卡片背面的 `TextBlock` 元素的 `Tapped` 事件做出响应。你不会对 `cardGrid` 单元格中的 `Grid` 事件进行响应，因此它们本质上是静态的。

让我们从一个正方形开始。在 `Rectangle` 的 XAML 中，右键点击 `Tapped` 属性的值，并在键菜单中选择“事件处理器”（Event Handler）。`MainPage.xaml` 文件的内容将显示，你会看到已经添加了 `Shape_Tapped(object)` 处理器的实现。返回 XAML，并对 `TextBlock` 元素中 `Tapped` 处理器的属性值重复此过程。你已经添加了卡片所需的所有处理器，并将为它们添加代码。简单，不是吗？

如果在游戏进行时，能够高亮鼠标光标下的卡片将会很好。实现这一点的一种方法是为 `cardGrid` 单元格中的外部 `Grid` 元素实现 `PointerEntered` 和 `PointerExited` 事件的处理器，并将卡片的背景颜色更改为天蓝色（azure）。你可以在鼠标光标进入和离开网格时实现这些处理。你可以通过属性面板（Properties pane）来操作，仅为了体验一下。

点击带有天蓝色颜色的 `Grid` 元素并显示其属性面板。点击属性面板顶部的按钮显示元素的事件处理器。在 `PointerEntered` 事件的值中输入 `Card_Entered` 并按回车键。这将创建处理器实现并返回。返回 XAML 并对 `PointerExited` 事件重复此过程。`PointerExited` 事件的值可以为 `Card_Exited`。两个处理器都将处理任何卡片。

你现在可以在 UI 中定义其他卡片位置。

## 创建所有卡片

你需要在 UI 中创建 23 张卡片。当你完成此过程后，你会感激折叠父元素 XAML 的努力。重复 23 次将非常麻烦，但幸运的是有一个快捷方法。`cardGrid (1,0)` 的内容与 grid (0,0) 的完全相同，除了定义背景颜色的 `Grid` 元素中的 `Grid.Row` 附加属性值设为 "1"。你可以通过复制 XAML 元素（包括其子元素）并将 `Grid.Row` 的值设置为 "1" 来创建 `cardGrid` 的内容。新的 `Grid` 将：

```xml
<Grid Row="1" Grid.Column="0" Background="Azure" Margin="5"
PointerEntered="Card_Entered" PointerExited="Card_Exited">
  <Grid Margin="10" Width="50" Height="50">
  <!-- 之前是 Rectangle, Ellipse, Polygon 和 TextBlock 元素-->
  </Grid>
</Grid>
```

子元素将保持完全相同。所有形状的 `Tapped` 事件将调用 `Shape_Tapped()` 处理器，而源自任何代表卡片背面的 `TextBlock` 元素的 `Tapped` 事件将由 `Callback_Tapped()` 函数处理。`Card_Entered()` 和 `Card_Exited()` 处理器函数将处理来自两个 `Grid` 元素的事件。

当然，你可以同样地更改 `cardGrid` 单元格 (2,0) 和 (3,0) 的 XAML；只需将每个的 `Grid.Row` 属性值更改为 "2" 和 "3"。完成后，你将发现设计面板中的网格的第一列已填充了卡片。

`cardGrid` 两列的 XAML 与单列的 XAML 相同，但 `Grid` 元素中的 `Grid.Column` 附加属性值为 "1"。因此，你可以通过将新集合中的四个 `Grid` 元素复制设置为 "1" 来创建两列的 XAML。我相信你将找到完成的方法。

`cardGrid` 中的特定形状对象可以是三种形状类型中的任意，因此你将将其存储为形状基类类型的句柄，即 `Windows::UI::Shapes` 命名空间中的 `Shape` 类型。在 `Windows::UI::Xaml::Grid` 中，作为卡片背面的元素句柄可以是一个 `Windows::UI::Xaml::Controls::TextBlock` 对象的句柄。如果你将这些作为类的公有属性，将很容易访问。以下是完整的 `Card` 类定义：

```cpp
#pragma once

namespace MemoryTest
{
    public class Card sealed
    {
        public:
        Card() {}
        // 拷贝构造函数
        Card(Card* card)
        {
            type = card->type;
            color = card->color;
            shape = card->shape;
            back = card->back;
        }
        public:
            property Platform::String* type; // 形状类型
            property Windows::UI::Xaml::Media::SolidBrush* color; // 形状颜色
            property Windows::UI::Xaml::Shapes* shape; // 形状句柄
            property Windows::UI::Xaml::Controls::TextBlock* back; // 卡片背面
    }
}
```

该类必须指定为 `sealed`，因为如果不定义为 `sealed`，它会被删除，代码将无法编译。你不需要在默认构造函数和拷贝构造函数之外定义任何成员。你需要拷贝构造函数来创建相同的卡片对。

# 向 MainPage 类中添加数据成员

你可以将所有想要添加到 `MainPage` 类的成员设为私有。第一个要添加到 `MainPage` 的数据成员将存储卡片的数量：

```cpp
size_t cardCount; // 卡片数量
```

你将在 `MainPage` 构造函数对其进行初始化。你可以向 `MainPage` 类定义中添加任何字符串来用于处理 `cardGrid` 中形状句柄的句柄句柄：

```cpp
Platform::Array<Windows::UI::Xaml::Controls::Grid^> grids;
Platform::Array<Windows::UI::Xaml::Shapes::Ellipse^> circles;
Platform::Array<Windows::UI::Xaml::Shapes::Rectangle^> squares;
Platform::Array<Windows::UI::Xaml::Shapes::Polygon^> triangles;
Platform::Array<Windows::UI::Xaml::Controls::TextBlock^> cardBacks;
```

这些数组将各包含 `cardCount` 个元素。

你还需要一个 `Card` 对象的数组：

```cpp
Platform::Array<Card>^ cardPack; // 卡牌包
```

这需要在 `MainPage.xaml` 中添加 `#include Card.h`。你将在 `MainPage` 构造函数中创建包含 `cardCount` 个元素的数组，存储指向 `Card` 对象的句柄。你将洗牌此数组中的句柄以进行新的游戏排布，因为这个数组是游戏的牌组。

你可以添加指向 `String` 对象的句柄成员，它们将用于存储 `cardGrid` 中子元素的名称：

```cpp
// 卡片元素的类型名称
Platform::String^ typeCircle;
Platform::String^ typeSquare;
Platform::String^ typeTriangle;
```

你将在 `MainPage` 构造函数中初始化这些。你将能够获取由 `Shape` 类型句柄引用的对象的类型名称，并与这些类型名称变量进行比较，以确定句柄所引用的 `Shape` 对象的类型。当你实现事件处理器时，还会添加其他数据成员，但目前这些足够了。

# 添加函数成员

你可以添加之前确定的三个函数：

```cpp
private:
// 游戏函数
void InitializeCardPack(); // 初始化 cardPack 以包含每种卡片的两张
void SetUpUIState(); // 初始化 cardGrid 的子元素
void InitializeGame(); // 设置一个带有洗过牌 cardPack 的游戏
```

如果你在 `MainPage.xaml.cpp` 中为这些函数提供大纲定义，应用程序应该是可编译的：

```cpp
// 初始化包，使其包含 12 对不同的牌
void MainPage::InitializeCardPack()
{
  // 在处添加代码
}
```

```cpp
// 设置网格单元的 UI 状态
void MainPage::SetUpUIState()
{
  // 在处添加代码
}
```

```cpp
// 洗牌并初始化
void MainPage::InitializeGame()
{
    // 在处添加代码
}
```

初始化牌包的初始化将在 `MainPage` 构造函数中完成。所有基础初始化将在 `MainPage` 构造函数中完成。通过 `InitializeComponent()` 调用设置 UI 组件。

```cpp
MainPage::MainPage()
{
    InitializeComponent();
    // cardGrid 中的单元格
    grid = new Array<Grid>(cardCount);
    // 形状类型名称
    circles = new Array<Ellipse>(cardCount);
    // 正方形类型
    squares = new Array<Rectangle>(cardCount);
    // 三角形类型
    tangles = new Array<Polygon>(cardCount);
    // 卡片背面
    cardBacks = new Array<TextBlock>(cardCount);

InitializePack();
SetUpUIState();
InitializeGame();
}
```

在初始化 `cardGrid` 的单元格数量后，初始化这些类型名称。你将能够获取由 `Shape` 类型句柄引用的对象的类型名称，并与这些类型名称变量进行比较，以确定句柄所引用的 `Shape` 对象的类型。通过 `String` 属性获取 `Shape` 对象的类型名称。`Card` 对象的继承自 `type` 属性。

为了在不指定命名空间的情况下使用形状类型，需要在 `MainPage.xaml.cpp` 中添加以下 `using` 指令：

```cpp
using namespace Windows::UI::Shapes;
```

# 初始化牌包

你将创建 `cardCount` 个对象并将句柄存储在 `cardPack` 数组中。卡片对象必须由 12 对相同对象组成。12 张不同的卡片由三种形状和四种颜色组成。你可以通过遍历颜色和形状类型来实现。如下所示：

```cpp
void MainPage::InitializeCardPack()
{
    // 创建形状和颜色数组
    Array<String*> shapeTypes = {typeCircle, typeSquare, typeTriangle};
    Array<SolidBrush*> colors = {
        ref new SolidBrush(Windows::UI::Colors::Red),
        ref new SolidBrush(Windows::UI::Colors::Green),
        ref new SolidBrush(Windows::UI::Colors::Blue),
        ref new SolidBrush(Windows::UI::Colors::Yellow)
    };
    // 初始化牌包
    cardPack = new Array<Card*>(cardCount);
    size_t index = 0; // cardPack 数组索引
    Card* card;
    for(auto color : colors) {
        for(auto shapeType : shapeTypes) {
            card = ref new Card(); // 创建卡片...
            card->type = shapeType; // 使用当前类型...
            card->color = color;
            card->shape = nullptr; // 我们稍后查找形状...
            card->back = nullptr; // 稍后查找背面。
            cardPack[index++] = card; // 将卡片存入包中...
            cardPack[index++] = ref new Card(card); // 以及拷贝。
        }
    }
}
```

# 设置 cardGrid 的子元素

`SetUpUIState()` 函数设置 `cardGrid` 中单元格的元素，使得卡片背面可见。此设置将 `cardGrid` 中每个单元的形状清除为不可见。元素是否可见取决于其 `Visibility` 属性的值。这

# 创建 Windows 8 应用 | 885

可以是两个值之一，Visible（可见）或 Collapsed（折叠），这些值由 `Windows::UI::Xaml` 命名空间中的 `Visibility` 枚举类定义。

该函数还会将 Grid 元素的句柄存储在 `grids` 数组中，并将作为 Grid 子元素的形状句柄存储在相应类型 `shape` 数组的某个元素中。你希望存储形状、卡牌背面和网格句柄的数组中的元素与它们在 `cardGrid` 中出现的顺序一致。以下是代码：

```cpp
void MainPage::SetupUI()
{
// 处理 cardGrid 中网格的集合
auto elements = cardGrid->Children;
UIElement element;           // 集合元素的句柄
Grid* grid;
UIElementCollection^ shapes; // 子网格中形状的集合
UIElement^ shape;            // 子网格中形状的句柄
int row(0);                   // 网格行
int column(0);               // 网格列位置
index index(0);                // 形状数组索引
unsigned int rowLength(cardGrid->ColumnDefinitions->Size);// 网格行的长度
```

```cpp
// 遍历 cardGrid 的子元素并顺序
// 将网格句柄存储在 grids 数组中
for(size_t i = 0; i < elements->Size; ++i)
```

```cpp
auto element = elements->GetAt(i);           // 获取下一个元素...
String^ elementType = element->GetType()->FullName; // ... 获取其类型
if(grid->GetType()->FullName == elementType)         // 确保它是 Grid
grid = safe_cast<Grid*>(element)->GetRow(row);      // 获取网格行
column = cardGrid->GetColumn(grid);               // 以及列位置。
index = row*rowLength + column;                   // 行/列索引
grid[index] = grid;                                // 保存网格
```

```cpp
// 每个单元格中的 Grid 包含另一个子元素。
// 我们知道情况总是如此的，所以获取子网格：
grid = safe_cast<Grid*>(grid->Children)->GetAt(0);
```

```cpp
shapes = grid->Children;               // 获取子形状
// 遍历当前 Grid 的元素并顺序
// 将形状元素句柄存储在数组中
for(size_t j = 0; j < shapes->Size; ++j)
```

```cpp
element = shapes->GetAt(j);           // 获取子形状句柄
elementType = element->GetType()->FullName;     // 以及其类型
```
