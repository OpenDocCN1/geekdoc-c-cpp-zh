
# 洗牌

你可以使用定义在 STL `<algorithm>` 头文件中的 `random_shuffle()` 函数，对存储在 `Platform::Array` 对象中的元素进行洗牌操作。该函数有两个版本。简单版本接受两个参数，即迭代器，用于指定要洗牌序列中的第一个和最后一个项目。若要获取卡牌的开始和结束迭代器，你需要使用 `begin()` 和 `end()` 函数来传递数组引用。这些不是 STL 函数，而是来自 `Windows::Foundations::Collections` 命名空间的 `begin()` 和 `end()` 的特殊版本。

`random_shuffle()` 函数使用来自 `stdlib.h` 的 `rand()` 随机数生成器并带有默认的洗牌值，结果是完全重复的，因此你会获得相同的洗牌牌组序列。不过，你可以使用当前时间为数字生成器设置种子以进行洗牌，例如：

```cpp
rand(static_cast<unsigned int>(time(nullptr)));
```

`time()` 函数返回当前时间，即自 1970 年 1 月 1 日午夜以来的秒数。参数是一个指向存储时间的变量的指针。时间值的类型为 `time_t`，是一种整数类型。你可以在调用 `random_shuffle()` 之前，在 `MainPage()` 构造函数的种子设置之后添加以下语句。

生成洗牌牌组的 `ShuffleCards()` 函数实现只需要语句：

```cpp
void MainPage::ShuffleCards() {
    std::random_shuffle(begin(cardPack), end(cardPack));
}
```

这使用 `begin()` 和 `end()` 迭代器为传递给 `random_shuffle()` 函数的 `cardArray` 创建迭代器。这使用了数组中的 `Card` 对象引用。

你需要在 `MainPage.xaml.cpp` 中添加以下指令：

```cpp
#include <algorithm>
#include <ctime>
```

`<algorithm>` 头文件用于 `random_shuffle()` 函数，`<ctime>` 头文件提供了 `time()` 函数。

# 高亮 UI 卡片

当鼠标光标悬停在卡片上时高亮卡片是通过 `Card_Entered()` 和 `Card_Exited()` 处理函数实现的。你可以通过简单更改其颜色来高亮卡片，这意味着在 `Card_Entered()` 处理中更改 `Grid` 对象的 `Background` 属性的值：

```cpp
void MemoryTest::MainPage::Card_Entered(Platform::Object^ sender,
    Windows::UI::Xaml::Input::PointerRoutedEventArgs^ e) {
    safe_cast<Grid>(sender)->Background = steelBrush;
}
```

你知道 `sender` 是 `Grid` 类型对象的句柄，因此你可以将 `Background` 属性的值设置为由 `steelBrush` 引用的 `SolidColorBrush` 对象提供的颜色。你可以将此以及原始颜色的 `SolidColorBrush` 句柄作为类私有成员，以避免每次调用处理函数都创建一个对象。

在 `MainPage` 类中添加以下私有成员：

```cpp
Windows::UI::Xaml::Media::SolidColorBrush^ steelBrush; // 卡片高亮颜色
Windows::UI::Xaml::Media::SolidColorBrush^ azureBrush; // 卡片正常颜色
```

你可以在 `MainPage` 构造函数中初始化它们：

```cpp
MainPage::MainPage() : cardUp(nullptr), cardUp(nullptr), pairCount(0) {
    InitializeComponent();
    // 卡片颜色的刷子
    steelBrush = new SolidColorBrush(Windows::UI::Colors::SteelBlue);
    azureBrush = new SolidColorBrush(Windows::UI::Colors::Azure);
    // 其他代码同前...
}
```

`Card_Exited()` 处理函数会将卡片还原为原始颜色：

```cpp
void MemoryTest::MainPage::Card_Exited(Platform::Object^ sender,
    Windows::UI::Xaml::Input::PointerRoutedEventArgs^ e) {
    safe_cast<Grid>(sender)->Background = azureBrush;
}
```

如果你重新编译并运行应用程序，你应该能够看到卡片高亮效果。

# 处理卡片反面事件

点击卡片反面通过 `Card_Entered()` 和 `Card_Exited()` 处理函数实现。你可以通过简单更改其颜色来高亮卡片，这意味着在 `Card_Entered()` 处理中更改 `Grid` 对象的 `Background` 属性的值：

```cpp
void MemoryTest::MainPage::Card_Entered(Platform::Object^ sender,
    Windows::UI::Xaml::Input::PointerRoutedEventArgs^ e) {
    safe_cast<Grid>(sender)->Background = steelBrush;
}
```

你知道 `sender` 是 `Grid` 类型对象的句柄，因此你可以将 `Background` 属性的值设置为由 `steelBrush` 引用的 `SolidColorBrush` 对象提供的颜色。你可以将此以及原始颜色的 `SolidColorBrush` 句柄作为类私有成员，以避免每次调用处理函数都创建一个对象。

在 `MainPage` 类中添加以下私有成员：

```cpp
Windows::UI::Xaml::Media::SolidColorBrush^ steelBrush; // 卡片高亮颜色
Windows::UI::Xaml::Media::SolidColorBrush^ azureBrush; // 卡片正常颜色
```

你可以在 `MainPage` 构造函数中初始化它们：

```cpp
MainPage::MainPage() : cardUp(nullptr), cardUp(nullptr), pairCount(0) {
    InitializeComponent();
    // 卡片颜色的刷子
    steelBrush = new SolidColorBrush(Windows::UI::Colors::SteelBlue);
    azureBrush = new SolidColorBrush(Windows::UI::Colors::Azure);
    // 其他代码同前...
}
```

`Card_Exited()` 处理函数会将卡片还原为原始颜色：

```cpp
void MemoryTest::MainPage::Card_Exited(Platform::Object^ sender,
    Windows::UI::Xaml::Input::PointerRoutedEventArgs^ e) {
    safe_cast<Grid>(sender)->Background = azureBrush;
}
```

如果你重新编译并运行应用程序，你应该能够看到卡片高亮效果。

# 处理卡片反面事件

（注：原文提供的文本在此处中断或为重复内容，以上已翻译所有可见部分。）

# 这是 `Shape_Tapped()` 的代码：

```cpp
```
