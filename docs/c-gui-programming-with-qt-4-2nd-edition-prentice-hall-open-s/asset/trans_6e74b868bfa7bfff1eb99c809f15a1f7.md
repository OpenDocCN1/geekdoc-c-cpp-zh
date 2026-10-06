
是的。在这些语言中，应用程序的语言方向可能是反向的，这是通过调用 `QApplication::setLayoutDirection(Qt::RightToLeft)` 来完成的。Qt 的翻译文件包含一个名为 'LTR' 的特殊标记，它告诉 Qt 语言是从左到右还是从右到左，因此我们通常不需要自己调用 `setLayoutDirection()`。

如果我们在应用程序中使用 Qt 的资源系统，对用户来说可能会证明更加方便。这不仅减少了作为产品一部分发布的文件数量，还避免了翻译文件不小心丢失或删除的风险。假设 `.qm` 文件位于源码树中的 `translations` 子目录下，那么我们将有一个包含如下内容的 `myapp.qrc` 文件：

```
<RCC>
<resource>
    <file>translations/myapp_de.qm</file>
    <file>translations/myapp_fr.qm</file>
    <file>translations/myapp_zh.qm</file>
    <file>translations/qt_de.qm</file>
    <file>translations/qt_fr.qm</file>
    <file>translations/qt_zh.qm</file>
</resource>
</RCC>
```

`.pro` 文件将包含以下项目：

```
RESOURCES += myapp.qrc
```

最后，在 `main()` 中，我们必须指定 `:/translations` 为翻译文件的路径。开头的冒号表示该路径指向资源，而不是文件系统中的文件。

现在我们已经涵盖了使应用程序能够使用其他语言翻译运行的所有内容。但语言和书写方向并不是国家和文化之间唯一的不同之处。国际化程序还必须考虑区域设置和日期格式、数字格式、字符串排序顺序。Qt 包含一个 `QLocale` 类，提供了本地化的数字和日期/时间格式。要查询其他特定于区域的信息，我们可以使用标准的 C++ `setlocale()` 和 `localeconv()` 函数。

某些 Qt 类和函数会根据区域设置调整其行为：

`QString::localeAwareCompare()` 以依赖区域的方式比较两个字符串。它对于排序用户可见的项目非常有用。

`QDate`、`QTime` 和 `QDateTime` 提供的 `toString()` 函数在以 `Qt::LocalDate` 作为参数调用时，会返回本地格式的字符串。

默认情况下，`QDateEdit` 和 `QDateTimeEdit` 控件以本地格式显示日期。

最后，翻译后的应用程序可能在某些情况下需要使用不同的图标而不是原始图标。例如，在处理从右向左的语言时，网络浏览器“后退”和“前进”按钮上的左右箭头应该调换。我们可以按照如下方式操作：

```
if (QApplication::rightToLeft()) {
    backAction->setIcon(forwardIcon);
    forwardAction->setIcon(backIcon);
} else {
    backAction->setIcon(backIcon);
    forwardAction->setIcon(forwardIcon);
}
```

包含字母字符的图标经常需要翻译。例如，与文字处理器斜体选项相关的工具栏按钮上的字母 'I' 在西班牙语中应被替换为 'C' (Cursivo)，在丹麦语、德语、挪威语和瑞典语中应替换为 'K' (Kursiv)。这里是一种简单的处理方法：

```
if (tr("Italic")[0] == 'c') {
    italicAction->setIcon(iconC);
} else if (tr("Italic")[0] == 'K') {
    italicAction->setIcon(iconK);
} else {
    italicAction->setIcon(iconI);
}
```

另一种方法是使用资源系统对多个区域设置的支持。在 `.qrc` 文件中，我们使用 `lang` 属性为资源指定区域设置。例如：

```
<resource>
    <file>italic.png</file>
</resource>
<resource lang="es">
    <file alias="italic.png">cursivo.png</file>
```

如果用户的区域设置是 `es` (Español)，`:italic.png` 就会引用 `cursivo.png` 图片。如果区域设置是 `sv` (Svenska)，则使用 `kursiv.png` 图片。对于其他区域设置，则使用 `italic.png`。

# 动态语言切换

对于大多数应用程序，在 `main()` 中检测用户的优语言并加载相应的 `.qm` 文件即可。但在某些情况下，用户可能需要动态切换语言的能力。不同人员连续使用的应用程序可能需要在不需要重启的情况下更改语言。例如，叫中心操作员、同译员和电脑收银机操作员使用的应用程序通常需要这种功能。

使应用程序能够动态切换语言比比启动时加载单个翻译文件多做一些工作，但并不困难。必须执行的操作如下：

- 提供一种让用户可以切换语言的方法。
- 对于每个控件或对话框，将其所有可翻译字符串放在放在单独的函数中（通常称为 `retranslateUi()`），并在语言更改时调用此函数。

让我们回顾一下“呼叫中心”应用程序源代码的相关部分。该应用程序提供了一个语言菜单（如图 18.1 所示），允许用户在运行时设置语言。默认语言是英语。

# 图 18.1. 动态语言菜单

![](img/5a524abdf0b0d58fa99d30abb4463611_696_0.png)
