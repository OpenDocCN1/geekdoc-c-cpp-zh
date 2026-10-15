

Table 11.17: 显示 RichTextBox 控件的编辑命令

| Editing Command | Key Gesture |
|---|---|
| AlignLeft | CTRL+L |
| AlignRight | CTRL+R |
| Delete | DELETE |
| DeleteNextWord | CTRL+DELETE |
| DeletePreviousWord | CTRL+BACKSPACE |
| EnterLineBreak | SHIFT+ENTER |
| EnterParagraphBreak | ENTER |
| MoveDownByLine | DOWN |
| MoveDownByPage | PAGEDOWN |
| MoveDownByParagraph | CTRL+DOWN |
| MoveToLineEnd | END |
| MoveToLineStart | HOME |
| MoveUpByLine | UP |
| MoveUpByPage | PAGEUP |
| TabBackward | SHIFT+TAB |
| TabForward | TAB |
| ToggleBold | CTRL+B |
| ToggleItalic | CTRL+I |
| ToggleUnderline | CTRL+U |

RichTextBox 控件的继承层次结构如下：

```
System.Object
    System.Windows.Threading.DispatcherObject
    System.Windows.DependencyObject
    System.Windows.Media.Visual
        System.Windows.UIElement
        System.Windows.FrameworkElement
        System.Windows.Controls.Control
        System.Windows.Controls.Primitives.TextBoxBase
            System.Windows.Controls.RichTextBox
```

你可以在 WPF 应用程序中添加一个 RichTextBox 控件，如以下代码片段所示：

```
<RichTextBox>
    <!--Document-->
</RichTextBox>
```

RichTextBox 控件值得注意的属性在表 11.18 中列出：

Table 11.18: 显示 RichTextBox 控件的值得注意的属性

| Property | Description |
|---|---|
| AcceptsReturn | Gets or sets a value that indicates how the text editing control responds when a user presses the ENTER key |
| AcceptsTab | Gets or sets a value that indicates how the text editing control responds when a user presses the TAB key |
| AutoWordSelection | Gets or sets a value that determines whether to select the whole word when a user starts selecting that word |
| CanRedo | Retrieves a value that indicates whether or not the most recent undo action can be redone |
| CanUndo | Retrieves a value that indicates whether or not the most recent action can be undone |
| CaretPosition | Gets or sets the position of the input inserted into text |
| Document | Gets or sets the Flow document that represents the content of RichTextBox |
| ExtentHeight | Retrieves the vertical size of the visible content area |
| ExtentWidth | Retrieves the horizontal size of the visible content area |
| HorizontalOffset | Gets or sets the horizontal scroll position |
| IsDocumentEnabled | Gets or sets a value that indicates whether a user can interact with the UIElement and ContentElement objects within RichTextBox |
| IsReadOnly | Gets or sets a value that indicates whether a user can edit the text in this control |
| IsUndoEnabled | Gets or sets a value that indicates whether undo support is enabled for the text-editing control |
| Selection | Retrieves the selection state of the current selection in RichTextBox |
| SpellCheck | Retrieves a SpellCheck object that provides access to spelling errors in the text of RichTextBox |
| UndoLimit | Retrieves or sets the number of actions stored in the undo queue |

## Flow Content Elements

在 WPF 中，流内容元素提供了创建适合托管在 FlowDocument 中的流内容的构建块。流内容元素可以归为两个大类：Block 和 Inline。派生自 Block 类的类用于包含对象，例如段落和列表，而派生自 Inline 类的类包含在文档中显示的对象，例如换行和跨度。Block 和 Inline 类是从 TextElement 类派生的抽象类。TextElement 类的继承层次结构如下：

```
System.Object
  System.Windows.Threading.DispatcherObject
    System.Windows.DependencyObject
      System.Windows.ContentElement
        System.Windows.FrameworkContentElement
          System.Windows.Documents.TextElement
```

TextElement 类的属性在表 11.19 中列出：

Table 11.19: 显示 TextElement 类的属性

| Property | Description |
|---|---|
| ContentEnd | Retrieves a TextPointer that represents the end of the content in the text element |
| ContentStart | Retrieves a TextPointer that represents the start of the content in the text element |
| ElementEnd | Retrieves a TextPointer that represents the end position of the text element |
| ElementStart | Retrieves a TextPointer that represents the start position of the text element |
| TextEffects | Gets or sets a collection of text effects to apply to the content of the text element |
| Typography | Retrieves the currently effective typography variations for the content of the text element |

WPF 中不同的流内容元素如下：

- Block-level elements
- Inline elements
- InlineCollection and BlockCollection elements

### Block-level Elements

块级元素用于在共同父级下对元素进行分组或对一组应用通用属性。块级元素的实际实现在该章的 Immediate Solutions 部分中展示。不同的块级元素在表 11.20 中列出：

Table 11.20: 列出块级元素

| Element | Description |
|---|---|
| Paragraph | Groups the content into a paragraph |
| Section | Contains other block-level elements, such as List and Table |
| List | Creates a bulleted or numeric list |
| ListItem | Creates a particular content item in the list of elements |
| Table | Creates a table |
| BlockUIContainer | Enables UIElement, such as a Button, to be embedded in a block-derived flow content |

### Inline Elements

内联元素用作在屏幕上呈现内容的直接容器。继承 Inline 元素的元素要么包含在 Block 元素中，要么包含在另一个 Inline 元素中。你可以在该章的 Immediate Solutions 部分看到内联元素的实际实现。不同的内联元素在表 11.21 中列出：

Table 11.21: 列出内联元素

| Element | Description |
|---|---|
| LineBreak | Creates a line break in the flow content |
| Run | Contains unformatted text |
| Span | Groups other Inline elements together |
| Figure and Floater | Embeds the content in Flow documents with placement properties that can be customized independent of the primary content flow |
| InlineUIContainer | Enables UIElements, such as Button, to be embedded in an Inline content element |

### InlineCollection and BlockCollection Elements

InlineCollection 类表示一个内联元素的集合。InlineCollection 类的子元素是 Paragraph、Span 和 TextBlock。InlineCollection 类只能在拥有此类的元素内部创建，例如 TextBlock。它不能直接实例化，也没有默认或重载的构造函数。你可以在 XAML 中创建 InlineCollection 类的实例。InlineCollection 类的继承层次结构如下：

```
System.Object
  System.Windows.Documents.TextElementCollection
    System.Windows.Documents.InlineCollection
```

InlineCollection 类的属性在表 11.22 中列出：

Table 11.22: InlineCollection 类的属性

| Property | Description |
|---|---|
| Count | Retrieves the number of items currently in a collection |
| FirstInline | Retrieves the first Inline element within InlineCollection |
| IsReadOnly | Retrieves a value that indicates whether or not the collection is read-only |
| LastInline | Retrieves the last Inline element within InlineCollection |

BlockCollection 类表示 Block 元素的一个类。FlowDocument 中 BlockCollection 类的子元素是 Section、ListItem、TableCell、Floater 和 Figure。此类只能在拥有 BlockCollection 的元素内部创建，例如 FlowDocument。它不能直接实例化，也没有默认或重载的构造函数。你不能在 XAML 中创建此类的实例。你可以在代码隐藏文件中使用并创建 BlockCollection 类的实例。

BlockCollection 类的继承层次结构如下：

```
System.Object
    System.Windows.Documents.TextElementCollection
        System.Windows.Documents.BlockCollection
```

BlockCollection 类的属性在表 11.23 中列出：

Table 11.23: BlockCollection 类的属性

| Property | Description |
|---|---|
| Count | Retrieves the number of items currently in a collection |
| FirstBlock | Retrieves the first Block element within the instance of the BlockCollection class |
| IsReadOnly | Retrieves a value that indicates whether or not a collection is read-only |
| LastBlock | Retrieves the last Block element within the instance of the BlockCollection class |

让我们现在进入该章的 Immediate Solutions 部分。

