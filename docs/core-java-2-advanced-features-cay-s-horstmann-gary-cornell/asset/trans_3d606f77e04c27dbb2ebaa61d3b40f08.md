

## javax.swing.JTable 1.2（续）

- `void moveColumn(int from, int to)`  
  移动表格索引为`from`的列，使其索引变为`to`。仅影响视图。
- `void removeColumn(TableColumn column)`  
  从视图中移除指定列。
- `int convertRowIndexToModel(int index)`
- `int convertColumnIndexToModel(int index)`  
  返回具有给定索引的行或列的模型索引。当行被排序或过滤，或列被移动或移除时，该值不同于索引。
- `void setRowSorter(RowSorter<? extends TableModel> sorter)`  
  设置行排序器。

## javax.swing.table.TableColumnModel 1.2

- `TableColumn getColumn(int index)`  
  获取描述具有给定视图索引的列的表格列对象。

## javax.swing.table.TableColumn 1.2

- `TableColumn(int modelColumnIndex)`  
  构造一个表格列，用于查看具有给定索引的模型列。
- `void setPreferredWidth(int width)`
- `void setMinWidth(int width)`
- `void setMaxWidth(int width)`  
  将此表格列的首选宽度、最小宽度和最大宽度设置为`width`。
- `void setWidth(int width)`  
  将此列的实际宽度设置为`width`。
- `void setResizable(boolean b)`  
  如果`b`为true，则列可调整大小。

## javax.swing.RowFilter<M, I> 1.6（续）

- `static <M,I> RowFilter<M,I> numberFilter(RowFilter.ComparisonType type, Number number, int... indices)`  
  返回一个过滤器，包含那些值在与给定数字或日期进行给定比较时匹配的行。比较类型为EQUAL、NOT_EQUAL、AFTER或BEFORE之一。如果指定了任何列模型索引，则仅搜索这些列；否则，搜索所有列。对于数字过滤器，单元格值的类必须与数字的类匹配。
- `static <M,I> RowFilter<M,I> dateFilter(RowFilter.ComparisonType type, Date date, int... indices)`  
  返回一个过滤器，包含那些值在与给定数字或日期进行给定比较时匹配的行。比较类型为EQUAL、NOT_EQUAL、AFTER或BEFORE之一。如果指定了任何列模型索引，则仅搜索这些列；否则，搜索所有列。对于日期过滤器，单元格值的类必须与日期的类匹配。
- `static <M,I> RowFilter<M,I> regexFilter(String regex, int... indices)`  
  返回一个过滤器，包含具有匹配给定正则表达式的字符串值的行。如果指定了任何列模型索引，则仅搜索这些列；否则，搜索所有列。注意，匹配的是RowFilter.Entry的getStringValue方法返回的字符串。
- `static <M,I> RowFilter<M,I> andFilter(Iterable<? extends RowFilter<? super M, ? super I>> filters)`
- `static <M,I> RowFilter<M,I> orFilter(Iterable<? extends RowFilter<? super M, ? super I>> filters)`  
  返回一个过滤器，包含由所有过滤器包含的条目，或由至少一个过滤器包含的条目。
- `static <M,I> RowFilter<M,I> notFilter(RowFilter<M,I> filter)`  
  返回一个过滤器，包含给定过滤器未包含的条目。

## javax.swing.RowFilter.Entry<M, I> 1.6

- `I getIdentifier()`  
  返回此行条目的标识符。
- `M getModel()`  
  返回此行条目的模型。
- `Object getValue(int index)`  
  返回此行指定索引处存储的值。
- `int getValueCount()`  
  返回此行中存储的值的数量。
- `String getStringValue()`  
  返回此行指定索引处存储的值，并将其转换为字符串。TableRowSorter生成的条目的getStringValue会调用排序器的字符串转换器。

![](img/7dd923a566750151a3aab0dacd0cdaa5_647_0.png)

图10.12 一个带有单元格渲染器的表格

```
table.setDefaultRenderer(Color.class, new ColorTableCellRenderer());
```

该渲染器现在用于此表中所有给定类型的对象。

如果你想基于其他标准选择渲染器，则需要继承JTable类并重写getCellRenderer方法。

> **提示：** 如果您的渲染器仅绘制文本字符串或图标，您可以扩展DefaultTableCellRenderer类。它会为您处理焦点和选择状态的渲染。

### 10.2.4.2 渲染表头

要在表头中显示图标，请设置表头值：

```
moonColumn.setHeaderValue(new ImageIcon("Moons.gif"));
```

然而，表头不够智能，无法为表头值选择合适的渲染器。你必须手动安装渲染器。例如，要在列标题中显示图像图标，请调用

```
moonColumn.setHeaderRenderer(table.getDefaultRenderer(ImageIcon.class));
```

### 10.2.4.3 编辑单元格

要启用单元格编辑，表格模型必须通过定义`isCellEditable`方法来表示哪些单元格可编辑。通常情况下，你会希望让某些列可编辑。在示例程序中，我们允许编辑四个列。

```java
public boolean isCellEditable(int r, int c)
{
    return c == PLANET_COLUMN || c == MOONS_COLUMN || c == GASEOUS_COLUMN || c == COLOR_COLUMN;
}
```

> **注意：** `AbstractTableModel`定义的`isCellEditable`方法总是返回`false`。`DefaultTableModel`会重写该方法，使其总是返回`true`。

如果你运行该程序（清单10.8至10.11），请注意你可以单击Gaseous列中的复选框来打开和关闭勾选标记。如果单击Moons列中的单元格，会出现一个组合框（见图10.13）。你很快就会看到如何安装这样一个组合框作为单元格编辑器。

![](img/7dd923a566750151a3aab0dacd0cdaa5_648_0.png)

图10.13 一个单元格编辑器

最后，单击第一列中的单元格。该单元格获得焦点。你可以开始输入，单元格内容会随之改变。

你刚刚在操作中看到的是`DefaultCellEditor`类的三种变体。可以用`JTextField`、`JCheckBox`或`JComboBox`构造一个`DefaultCellEditor`。`JTable`类会自动为Boolean单元格安装复选框编辑器，并为所有未提供自身渲染器的可编辑单元格安装文本字段编辑器。文本字段允许用户编辑通过对表格模型的`getValueAt`方法的返回值应用`toString`而得到的字符串。

编辑完成后，通过调用编辑器的`getCellEditorValue`方法获取编辑后的值。该方法应返回正确类型的值（即模型的`getColumnClass`方法返回的类型）。

要获得组合框编辑器，需手动设置单元格编辑器——`JTable`组件不知道哪些值可能适合特定类型。对于Moons列，我们希望用户能够选择0到20之间的任意值。以下是初始化组合框的代码：

```
JComboBox moonCombo = new JComboBox();
for (int i = 0; i <= 20; i++)
    moonCombo.addItem(i);
```

要构造`DefaultCellEditor`，请在构造函数中提供组合框：

```
TableCellEditor moonEditor = new DefaultCellEditor(moonCombo);
```

接下来，我们需要安装编辑器。与颜色单元格渲染器不同，该编辑器不依赖于对象类型——我们不一定希望将它用于所有`Integer`类型的对象。相反，我们需要将它安装到特定列中：

```
moonColumn.setCellEditor(moonEditor);
```

### 10.2.4.4 自定义编辑器

再次运行示例程序并单击一种颜色。会弹出一个颜色选择器，让你为行星选择新颜色。选择一种颜色并单击“确定”。单元格颜色会更新（见图10.14）。

颜色单元格编辑器不是标准的表格单元格编辑器，而是自定义实现。要创建自定义单元格编辑器，需要实现`TableCellEditor`接口。该接口有点繁琐，自Java SE 1.3起，提供了`AbstractCellEditor`类来负责事件处理的细节。

`TableCellEditor`接口的`getTableCellEditorComponent`方法请求一个组件来渲染单元格。它与`TableCellRenderer`接口的`getTableCellRendererComponent`方法完全相同，只是没有焦点参数。当单元格正在编辑时，假定它拥有焦点。编辑器组件在编辑进行时会临时替换渲染器。在我们的示例中，我们返回一个未着色的空白面板。这是向用户表明该单元格当前正在编辑。

