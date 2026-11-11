
### 表 11.1 默认渲染操作

| 类型 | 渲染为 |
|---|---|
| 布尔值 | 复选框 |
| 图标 | 图像 |
| 对象 | 字符串 |

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_645_0.png)

图 11.5 包含行星数据的表格

## 11.1.3.2 访问表列

JTable 类将有关表列的信息存储在 TableColumn 类型的对象中。TableColumnModel 对象管理这些列。（图 11.6 显示了最重要的表类之间的关系。）如果你不想动态插入或删除列，就不会太多地使用列模型。列模型最常见的用途就是获取一个 TableColumn 对象：

```java
int columnIndex = . . . ;
TableColumn column = table.getColumnModel().getColumn(columnIndex);
```

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_646_0.png)

图 11.6 表类之间的关系

## 11.1.3.3 调整列大小

TableColumn 类让你可以控制列的大小调整行为。你可以使用以下方法设置首选宽度、最小宽度和最大宽度：

```java
void setPreferredWidth(int width)
void setMinWidth(int width)
void setMaxWidth(int width)
```

表组件使用这些信息来布局各列。

使用以下方法

```java
void setResizable(boolean resizable)
```

控制是否允许用户调整列的大小。

你可以通过以下方法以编程方式调整列的大小：

```java
void setWidth(int width)
```

当调整某一列的大小时，默认情况下表的总体大小保持不变。当然，被调整列的宽度增减必须分配到其他列上。默认行为是更改被调整列右侧所有列的大小。这是一个很好的默认设置，因为它允许用户从左到右将所有列调整到所需宽度。

你可以使用以下方法设置表 11.2 中的另一种行为：

```java
void setAutoResizeMode(int mode)
```

这是 JTable 类的方法。

### 表 11.2 调整大小模式

| 模式 | 行为 |
|---|---|
| `AUTO_RESIZE_OFF` | 不调整其他列的大小；更改表宽度。 |
| `AUTO_RESIZE_NEXT_COLUMN` | 仅调整下一列的大小。 |
| `AUTO_RESIZE_SUBSEQUENT_COLUMNS` | 平均调整所有后续列的大小；这是默认行为。 |
| `AUTO_RESIZE_LAST_COLUMN` | 仅调整最后一列的大小。 |
| `AUTO_RESIZE_ALL_COLUMNS` | 调整表中的所有列；这不是一个好的选择，因为它会阻止用户将多列调整到所需大小。 |

## 11.1.3.4 调整行大小

行高由 JTable 类直接管理。如果你的单元格高于默认高度，可能需要设置行高：

```java
table.setRowHeight(height);
```

默认情况下，表中所有行具有相同高度。你可以通过以下调用设置各单独行的高度：

```java
table.setRowHeight(row, height);
```

实际行高等于用这些方法设置的行高减去行边距。默认行边距为 1 像素，但你可以通过以下调用更改它：

```java
table.setRowMargin(margin);
```

红色。当你单击 Color 列时，会看到蓝色行星移到表格底部。这是通过以下调用实现的：

```java
sorter.setComparator(COLOR_COLUMN, new Comparator<Color>()
{
   public int compare(Color c1, Color c2)
   {
      int d = c1.getBlue() - c2.getBlue();
      if (d != 0) return d;
      d = c1.getGreen() - c2.getGreen();
      if (d != 0) return d;
      return c1.getRed() - c2.getRed();
   }
});
```

如果没有为某一列指定比较器，则排序顺序按如下方式确定：

- 1. 如果列类是 `String`，则使用 `Collator.getInstance()` 返回的默认排序器。它按照适合当前区域设置的方式对字符串排序。（有关区域设置和排序器的更多信息，请参见第 7 章。）
- 2. 如果列类实现了 `Comparable`，则使用其 `compareTo` 方法。
- 3. 如果已为排序器设置 `TableStringConverter`，则使用默认排序器对转换器的 `toString` 方法返回的字符串进行排序。如果你想使用这种方法，请按如下方式定义转换器：

    ```java
    sorter.setStringConverter(new TableStringConverter()
    {
       public String toString(TableModel model, int row, int column)
       {
          Object value = model.getValueAt(row, column);
          convert value to a string and return it
       }
    });
    ```

- 4. 否则，对单元格值调用 `toString` 方法，并使用默认排序器对它们进行排序。

## 11.3.7 过滤行

除了对行排序之外，`TableRowSorter` 还可以有选择地隐藏行——这一过程称为过滤。要激活过滤，请设置一个 `RowFilter`。例如，要包含所有至少有一颗卫星的行，请调用

```java
sorter.setRowFilter(RowFilter.numberFilter(ComparisonType.NOT_EQUAL, 0, MOONS_COLUMN));
```

这里，我们使用一个预定义的数字过滤器。要构造数字过滤器，请提供

- 比较类型（EQUAL、NOT_EQUAL、AFTER 或 BEFORE 之一）。
- Number 子类的对象（例如 Integer 或 Double）。只考虑与给定 Number 对象具有相同类的对象。
- 零个或多个列索引值。如果未提供索引值，则搜索所有列。

静态方法 RowFilter.dateFilter 以相同方式构造日期过滤器；你需要提供 Date 对象而不是 Number 对象。

最后，静态方法 RowFilter.regexFilter 构造一个过滤器，用于查找与正则表达式匹配的字符串。例如，

```java
sorter.setRowFilter(RowFilter.regexFilter(".*[^s]$", PLANET_COLUMN));
```

仅显示名称不以“s”结尾的行星。（有关正则表达式的更多信息，请参见第 2 章。）

你还可以使用 andFilter、orFilter 和 notFilter 方法组合过滤器。要过滤名称不以“s”结尾且至少有一颗卫星的行星，可以使用以下过滤器组合：

```java
sorter.setRowFilter(RowFilter.andFilter(List.of(
    RowFilter.regexFilter(".*[^s]$", PLANET_COLUMN),
    RowFilter.numberFilter(ComparisonType.NOT_EQUAL, 0, MOONS_COLUMN))));
```

要实现自己的过滤器，请提供 RowFilter 的子类，并实现 include 方法以指示应显示哪些行。这很容易做到，但 RowFilter 类那种宏大的通用性会让人有点望而生畏。

`RowFilter<M, I>` 类有两个类型参数——分别用于模型和行标识符的类型。处理表时，模型始终是 TableModel 的子类型，标识符类型是 Integer。（将来某个时候，其他组件也可能支持行过滤。例如，要在 JTree 中过滤行，可能会使用 `RowFilter<TreeModel, TreePath>`。）

行过滤器必须实现以下方法

```java
public boolean include(RowFilter.Entry<? extends M, ? extends I> entry)
```

`RowFilter.Entry` 类提供了获取模型、行标识符以及给定索引处值的方法。因此，你可以按行标识符和行内容进行过滤。

例如，这个过滤器每隔一行显示一行：

```java
var filter = new RowFilter<TableModel, Integer>()
{
    public boolean include(Entry<? extends TableModel, ? extends Integer> entry)
    {
        return entry.getIdentifier() % 2 == 0;
    }
};
```

如果你只想包含卫星数量为偶数的行星，则应改为检查

```java
((Integer) entry.getValue(MOONS_COLUMN)) % 2 == 0
```

在我们的示例程序中，我们允许用户隐藏任意行。我们将隐藏的行索引存储在一个集合中。该行过滤器显示索引不在该集合中的所有行。

过滤机制并非为条件随时间变化的过滤器而设计。在我们的示例程序中，每当隐藏行集合发生变化时，我们都会不断调用

```java
sorter.setRowFilter(filter);
```

设置过滤器会使其立即生效。

## 11.3.8 隐藏和显示列

如你在上一节中所见，你可以按表行的内容或行标识符来过滤表行。隐藏表列使用完全不同的机制。

JTable 类的 removeColumn 方法从表视图中移除一列。列数据实际上并未从模型中移除——它们只是从视图中隐藏。removeColumn 方法接受一个 TableColumn 参数。如果你有列号（例如，通过调用 getSelectedColumns 获得），则需要向表模型请求实际的表列对象：

```java
TableColumnModel columnModel = table.getColumnModel();
TableColumn column = columnModel.getColumn(i);
table.removeColumn(column);
```

如果你记得该列，稍后可以将其重新添加回来：

```java
table.addColumn(column);
```

此方法将列添加到末尾。如果你希望它出现在其他位置，请调用 moveColumn 方法。

你也可以通过添加新的 TableColumn 对象来添加一个与表模型中列索引对应的新列：
