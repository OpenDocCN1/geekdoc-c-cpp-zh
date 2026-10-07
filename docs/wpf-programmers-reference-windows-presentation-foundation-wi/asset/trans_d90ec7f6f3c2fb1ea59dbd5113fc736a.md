

## 512 | 附录 I XPATH

```xml
<Item Quantity="1" UnitPrice="13.95">Rechargeable Batteries</Item>
</Order>
<Customer CustomerName="Emily Pickle">
  <Order OrderDate="4/1/2010">
    <Item Quantity="1" UnitPrice="13.95">Rechargeable Batteries</Item>
    <Item Quantity="2" UnitPrice="2.99">Duct Tape</Item>
  </Order>
  <Order OrderDate="4/26/2010">
    <Item Quantity="2" UnitPrice="1.90">Highlighter</Item>
    <Item Quantity="1" UnitPrice="99.90">Flash Drive</Item>
    <Item Quantity="2" UnitPrice="0.10">Pencils</Item>
  </Order>
  <Order OrderDate="4/27/2010">
    <Item Quantity="1" UnitPrice="1.25">Soda</Item>
  </Order>
</Customer>
```

图 1 中的 `CustomerOrders` 示例使用 ListBox 来显示数据的不同视图。

### 绑定到 XML 数据

通常，绑定到 XML 数据的项需要一个项源来告诉它从哪里获取数据，以及一个项模板来告诉它如何显示项（有关绑定的更多详细信息请参见第 18 章）。例如，以下代码显示了 `CustomerOrders` 程序如何显示图 1 所示的数据：

```xml
<ListBox>
  <ListBox.ItemsSource>
    <Binding Source="{StaticResource customers}" XPath="Order" />
  </ListBox.ItemsSource>
  <ListBox.ItemTemplate>
    <DataTemplate>
      <StackPanel Orientation="Horizontal">
        <TextBlock Text="Ordered on " />
        <TextBlock Text="{Binding ../OrderDate}" FontWeight="Bold" />
        <TextBlock Text=" by " />
        <TextBlock Text="{Binding ../CustomerName}" FontWeight="Bold" />
      </StackPanel>
    </DataTemplate>
  </ListBox.ItemTemplate>
</ListBox>
```

`CustomerOrders` 的 `ListBox.ItemsSource` 属性告诉控件从 `StaticResource` customers 获取数据。XPath 值 "Order" 告诉控件选择数据中的所有项。`ListBox.ItemTemplate` 告诉控件如何显示它选择的对象。此模板包含一个包含多个 `TextBlock` 的 `StackPanel`。第一个 `TextBlock` 包含一个显示为 "Ordered on " 的简单字符串。第二个 `TextBlock` 使用绑定从所选的 Order 对象中提取数据：`@OrderDate` 属性。第三个 `TextBlock` 显示文本 "by "。最后一个 `TextBlock` 使用绑定 `../CustomerName` 从 Order 的父节点（即 Customer）中选择 `CustomerName` 属性。接下来的章节描述了 XPath 的两种用法：用于选择数据对象，以及用于确定对象显示的内容。

### 选择

要在 XML 中选择节点，您需要构建一个类似于目录的路径，该路径从根节点开始穿过数据。例如，在之前的数据中，路径 `/Customers/Order/Item` 意味着从根元素开始路径，进入 Customer 对象，进入 Order 对象，最后选择 Item 对象。表 I-1 总结了 XPath 符号。

#### 表 I-1:

| 符号 | 用途 |
| :--- | :--- |
| node_name | 选择具有给定名称的子节点。 |
| / | 在 XPath 的开头，选择根节点。在 XPath 中间，分隔节点名称。 |
| // | 匹配任意数量的节点。例如，`//Item` 匹配数据中所有的所有 Item 节点。 |
| . | 匹配当前节点。 |
| .. | 移动到父节点。 |
| @ | 选择属性。 |
| * | 匹配任意单个节点。 |
| @* | 匹配任意单个属性。 |

### 谓词

谓词放在 XPath 的方括号中，用于限制选择。谓词通常引用节点值或属性。例如，以下 XPath 匹配所有 `UnitPrice` 属性大于 5.00 的 Item 节点：

```xpath
//Item[@UnitPrice>5.00]
```

您可以使用 `|` 符号组合多个选择语句。例如，以下绑定选择了父节点为 Customer 且其 `CustName` 属性等于 'Bob Farkle' 或 'Emily Pickle' 的 Order 对象。（请注意，空格会被忽略，因此此示例在 `Source="StaticResource customers"` 中使用了额外的空间以便排版整齐。）

```xml
<Binding Source="StaticResource customers"
  XPath="//Customer[@CustName='Bob Farkle']/Order | //Customer[@CustName='Emily Pickle']/Order"/>
```

### 约束函数

XPath 提供了几种函数，您可以在谓词中使用它们来限制结果。例如，`contains` 函数在第一个参数包含第二个参数作为子字符串时选择节点。以下 XPath 语句选择了项的值（由符号 `.` 指定）包含字符 `p` 的 Item 节点：

```xpath
//Item[contains(.,'p')]
```

表 I-2 总结了最有用的约束函数。

#### 表 I-2:

| 函数 | 用途 |
| :--- | :--- |
| ceiling | 返回大于或等于输入参数的最小整数 |
| concat | 连接两个或多个字符串。 |
| contains | 如果第一个参数包含第二个作为子字符串，则返回 True。注意比较是大小敏感的。 |
| count | 返回参数的计数。例如，XPath 语句 `//Order[count()>2]` 选择具有两个以上项的 Order。 |
| floor | 返回小于或等于输入参数的最大整数 |
| name | 返回节点的名称。 |
| normalize-space | 移除字符串前后的空格。 |
| position | 返回节点在其父节点中的位置。 |
| round | 将数字四舍五入到最近整数。 |
| string-length | 返回字符串的长度。 |
| substring | 返回字符串的一部分。 |
| substring-after | 返回指定子字符串之后的子字符串。 |
| substring-before | 返回指定子字符串之前的子字符串。 |
| text | 选择文本节点。 |
| translate | 根据映射替换字符串中的字符。 |

