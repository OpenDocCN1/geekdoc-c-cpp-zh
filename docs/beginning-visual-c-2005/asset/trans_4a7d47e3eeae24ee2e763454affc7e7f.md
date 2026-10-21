

| 属性 | 描述 |
|---|---|
| Alignment | 该值决定单元格内容的对齐方式。值由 DataGridViewAlignment 枚举定义，因此值可以是以下常量中的任意一个：
BottomCenter, BottomLeft, BottomRight,
MiddleCenter, MiddleLeft, MiddleRight,
TopCenter, TopLeft, TopRight, NotSet
默认值是 NotSet。 |
| WrapMode | 该值决定当文本过长无法容纳在单元格中时是否换行。值是 DataGridViewTriState 枚举定义的一组常量中的一个，可以是：
True, False, NotSet
默认值是 NotSet。 |
| Padding | 该值是类型为 System::Windows::Forms::Padding 的对象，决定单元格内容与单元格边缘之间的空间。Padding 类构造函数需要一个类型为 int 的参数，表示以像素为单位的填充量。默认值对应单元格中无填充。 |
| Format | 该值是一个格式字符串，决定字符串内容的格式化方式。这与你在 Console::WriteLine() 函数中使用的格式化方式相同。默认值是一个空字符串。 |

这不是 DataGridViewCellStyle 对象的属性的详尽列表，只是与单元格外观相关的那些属性。

特定单元格外观的确定方式相当复杂，因为你可以在 DataGridView 控件中设置多个不同的属性，所有这些属性都决定给定单元格或一组单元格的显示方式，并且其中几个可能在任何给定时间同时生效。例如，你可以设置属性值来指定一行单元格的外观，或一列单元格的外观，或控件中所有单元格的外观，并且这些都可以同时生效。显然，由于行和列总会相交，这三种可能性都适用于任何给定单元格，因此存在明显的冲突。

DataGridView 控件中的每个单元格都由一个 System::Windows::Forms::DataGridViewCell 对象表示，任何给定单元格的外观，包括标题单元格，由其 InheritedStyle 属性的值决定。单元格的 InheritedStyle 属性的值是通过查看所有返回适用于该单元格的 DataGridViewCellStyle 对象的可能属性，然后按优先级顺序考虑这些属性得出的；序列中第一个被发现已设置的属性即为生效的属性。行和列的标题单元格的 InheritedStyle 属性值的确定方式与其他单元格的 InheritedStyle 属性不同，因此我将分别讨论它们，先从标题单元格开始。

## 自定义标题单元格

控件中每个标题单元格的 `InheritedStyle` 属性值是通过按顺序考虑以下属性的值来确定的：

- 表示该单元格的 `DataGridViewCell` 对象的 `Style` 属性。
- 控件对象的 `ColumnHeadersDefaultCellStyle` 属性或 `RowHeadersDefaultCellStyle` 属性。
- 控件对象的 `DefaultCellStyle` 属性。

因此，如果单元格对象的 `Style` 属性值已被设置，则单元格的 `InheritedStyle` 属性采用该值并决定单元格的外观。如果没有，则在该值已被设置的情况下，下一个候选属性生效。如果第二个选择未被设置，则应用控件的 `DefaultCellStyle` 属性。

不要忘记 `InheritedStyle` 属性的值是类型为 `DataGridViewCellStyle` 的对象，而它本身具有决定单元格外观各个方面的属性。遍历优先级序列的过程适用于 `DataGridViewCellStyle` 对象的每个属性，因此总体上可能来自优先级序列中的多个属性的贡献。

## 自定义非标题单元格

控件中每个非标题单元格的 `InheritedStyle` 属性值（非标题单元格即包含数据的单元格）是从 `DataGridView` 对象中的以下属性按顺序确定的：

- 表示该单元格的 `DataGridViewCell` 对象的 `Style` 属性。
- 表示包含该单元格的行对象的 `DataGridViewRow` 对象的 `DefaultCellStyle` 属性。你通常通过索引控件对象的 `Rows` 属性来引用 `DataGridViewRow` 对象。
- 控件对象的 `AlternatingRowsDefaultCellStyle` 属性；这仅适用于行索引为奇数的单元格。
- 控件对象的 `RowsDefaultCellStyle` 属性。
- 包含该单元格的 `DataGridViewColumn` 对象的 `DefaultCellStyle` 属性。你通常通过索引控件对象的 `Columns` 属性来访问 `DataGridViewColumn` 对象。
- 控件对象的 `DefaultCellStyle` 属性。

理论上你可以为每个单元格拥有不同的 `DataGridViewCellStyle` 对象，但为了效率，你需要将此类对象的数量保持在最小。

下一个 Try It Out 在一个示例中探讨了这些可能性中的一些，在该示例中你自行设置 `DataGridView` 对象。

## 第 22 章

## Try It Out — 设置控件的外观

使用 Windows Forms 模板创建一个新的 CLR 项目，名称为 Ex22_02。将一个 `DataGridView` 控件添加到表单的设计选项卡中，并将其 (Name) 属性更改为 dataGridView。这是类中引用控件对象的句柄的名称。你也可以将表单的 Text 属性更改为 "My Other Book List。" 对于其余示例，你将使用构造函数中的代码。

你显示的数据与前一个示例类似，但为了稍微扩展可能性，你将在每一行的开头添加一个日期条目，指定一本书，因此第一列的单元格将包含类型为 `System::DateTime` 的对象的引用，其余列将为字符串。DateTime 类定义了一个时间点，你通常将其指定为日期加上一天中的时间。在示例中，仅日期是感兴趣的，因此你将使用一个仅接受三个参数的构造函数：年、月和日。

## 设置数据

第一步是创建要显示的数据。在 `Form1` 构造函数中，在调用 `InitializeComponent();` 之后添加以下代码：

// Create book data, one book per array
array<Object^>^ book1 = {gcnew DateTime(1999,11,5), L"0-09-174271-4",
                         L"Wonderful Life", L"Stephen Jay Gould", L"Hutchinson Radius"};
array<Object^>^ book2 = {gcnew DateTime(2001,10,25), L"0-09-977170-5",
                         L"The Emperor's New Mind", L"Roger Penrose", L"Vintage"};
array<Object^>^ book3 = {gcnew DateTime(1993,1,15), L"0-14-017996-8",
                         L"Metamagical Themes", L"Douglas R. Hofstadter", L"Penguin"};
array<Object^>^ book4 = {gcnew DateTime(1994,2,7), L"0-201-36080-2",
                         L"The Meaning Of It All", L"Richard P. Feynman", L"Addison-Wesley"};
array<Object^>^ book5 = {gcnew DateTime(1995,11,6), L"0-593-03449-X",
                         L"The Walpole Orange", L"Frank Muir", L"Bantam Press"};
array<Object^>^ book6 = {gcnew DateTime(2004,7,16), L"0-439-99358-X",
                         L"The Amber Spyglass", L"Philip Pullman", L"Scholastic Children's Books"};
array<Object^>^ book7 = {gcnew DateTime(2002,9,18), L"0-552-13461-9",
                         L"Pyramids", L"Terry Pratchett", L"Corgi Books"};
array<Object^>^ book8 = {gcnew DateTime(1998,2,27), L"0-7493-9739-X",
                         L"Made In America", L"Bill Bryson", L"Minerva"};

// Create array of books
array<array<Object^>^>^ books = {book1, book2, book3, book4,
                                 book5, book6, book7, book8};

其基本机制与前一个示例相同。这里的差异是由于每本书的规范中多了一个类型为 `DateTime` 的项目，因此数组元素是类型为 `Object^`。你会回忆起 Object 类是每个 C++/CLI 类的基类，因此你可以在类型为 `Object^` 的元素中存储对任何类类型对象的句柄。

你可以在构造函数中添加以下语句：

```
array<String^>^ headers = {L"Date", L"ISBN", L"Title", L"Author", L"Publisher"};
```

