

# 428 | 附录 B 内容

# 表格 B-3 (续)

| 对象 | 目的 |
|---|---|
| 图形 (Figure) | 在带有周围文本的独立区域显示内容。你可以设置其在流式内容中的对齐方式，它可以跨越多个列。 |
| 用户界面元素 | 位于 `FlowDocument` 中的文本框（TextBox）、按钮（Button）和其他元素。 |
| 三维对象 | 显示 3D 输出。 |

# FlowDocument 对象示例

以下 XML 包含了 `FlowDocument` 中最常见对象的简单示例：

```
<FlowDocument FontFamily="Arial" FontSize="12" Background="Lime" Foreground="Black">
  <!-- 一个包含使用不同字体 Run 的段落。 -->
  <Paragraph>
    <Run FontStyle="Italic" Foreground="Red" FontWeight="Bold">simple</Run>
    包含一个 Run 的段落。
  </Paragraph>

<!-- 一个具有两行的表格。第一行具有具有不同的样式
       （可能用作页头） -->
  <Table Border="Black" BorderThickness="1" FontSize="12">
    <Columns>
      <TableColumn Width="25%" />
      <TableColumn Width="75%" />
    </Columns>
    <TableRow>
      <TableRow Background="LightGray" FontSize="15">
        <TableCell>
          <Paragraph>Item</Paragraph>
        </TableCell>
        <TableCell>
          <Paragraph>Purpose</Paragraph>
        </TableCell>
      </TableRow>
      <TableRow>
        <TableCell>
          <Paragraph>List</Paragraph>
        </TableCell>
        <TableCell>
          <Paragraph>在列表中显示项目</Paragraph>
        </TableCell>
      </TableRow>
    </TableRow>
  </Table>

  <!-- 一个包含用户界面元素的块容器。 -->
  <BlockUIContainer>
    <Button Name="btnBlockUI" Width="100" Height="50"
            Content="Block UI Button" />
  </BlockUIContainer>
</FlowDocument>
```

```
</BlockUIContainer>

<!-- 一个包含内联控件的段落。 -->
<Paragraph>
  一些内联内容：
  <Button Name="btnButton">A Button</Button>
  <TextBlock Text="A Box"/></TextBlock>
  <Ellipse Width="50" Height="30" 
    Fill="Yellow" Stroke="Red" StrokeThickness="5" />
</Paragraph>

<!-- 一个定义浮动控件 (Floater) 的段落。 -->
<Paragraph>
  <Floater HorizontalAlignment="Right">
    <Paragraph BorderBrush="Black" BorderThickness="1*">
      <StackPanel Margin="2,2,2,2">
        <Ellipse Fill="Yellow" Width="40" Height="20"/>
        <TextBlock Margin="5" FontStyle="Italic">
          图 1. 一个浮动的椭圆。
        </TextBlock>
      </StackPanel>
    </Paragraph>
  </Floater>
</Paragraph>

<!-- 另一个可以位于浮动控件旁边的段落。 -->
<Paragraph>
  浮动控件持有可以浮动到其他位置的内容。
</Paragraph>

<!-- 一个列表。 -->
<List>
  <ListItem>
    <Paragraph>
      Ellipse
      <Ellipse Width="20" Height="20" Stroke="Black" StrokeThickness="1*"/>
    </Paragraph>
  </ListItem>
  <ListItem>
    <Paragraph>
      Triangle
      <Polygon
        Stroke="Black" StrokeThickness="1"
        Points="0,0 20,0 10,20" />
    </Paragraph>
  </ListItem>
</List>
</FlowDocument>
```

`Paragraph` 对象通常构成了 `FlowDocument` 大部分内容。此对象除了 `Background` 和 `Foreground` 之外，拥有一套字体属性。

关于 `FlowDocuments` 的更多信息，请参阅第 21 章。

# FLOWDOCUMENTVIEWER

`FlowDocumentViewer` 在页面模式下显示 `FlowDocument`。在这种模式下，它看到单页，并使用属性来决定。

示例 FlowDocumentViewer

要使用 `FlowDocumentViewer`，请将 `FlowDocument` 放入其中：

```
<FlowDocumentViewer>
  <!-- 插入 FlowDocument -->
</FlowDocumentViewer>
```

关于 `FlowDocument` 的信息。

# FLOWDOCUMENTREADER

`FlowDocumentReader` 在 `Page`、`Scroll` 或 `TwoPage` 模式下显示 `FlowDocument`。

模式值

表格 B-4：模式

| 模式 | 含义 |
| --- | --- |
| Page | 像页 |
| Scroll | 滚动 |
| TwoPage | 像双页 |

示例 FlowDocumentReader

要使用 `FlowDocumentReader`，请将 `FlowDocument` 放入其中：

```
<FlowDocumentReader Mode="Page">
  <!-- 插入 FlowDocument -->
</FlowDocumentReader>
```

关于 `FlowDocument` 的信息。

# FLOWDOCUMENTSCROLLER

`FlowDocumentScrollView` 在滚动模式下显示 `FlowDocument`。在这种模式下，它看到单页，并使用属性来决定。

示例 FlowDocumentScrollView

```
<FlowDocumentScrollView Mode="Scroll">
  <!-- 插入 FlowDocument -->
</FlowDocumentScrollView>
```

关于 `FlowDocument` 的信息。

# GROUPBOX

`GroupBox` 显示带有页头的单页内容。`Foreground` 属性决定文本。

表格 B-5：GroupBox 的属性

| 属性 | 目的 |
| --- | --- |
| Background | 填充控件的颜色 |
| BorderBrush | 控件边缘的颜色 |
| BorderThickness | 控件边缘的厚度 |
| Foreground | 显示文本的颜色 |
| Header | 顶部的文本 |

示例 GroupBox 和 "Grid"

以下代码定义了一个包含 `Grid` 的简单 `GroupBox`：

```
<GroupBox Width="300" Height="200"
Header="Customer Address" BorderBrush="Red" Foreground="Blue">
    <Grid>
        <!-- 在此处插入控件 -->
    </Grid>
</GroupBox>
```

# IMAGE

`Image` 显示图片。关键属性列在表格 B-6。

表格 B-6：Image 的属性

| 属性 | 目的 |
|---|---|
| Source | 存储的位置。可以是文件名或绝对路径。 |
| Stretch | 如何拉伸。可以是 None、Uniform。 |

示例加载图像

以下代码创建了两个 `Image`。第一个从项目加载图像。第二个从网络地址加载。

```
<Image Width="200" Stretch="Uniform" Source="MadScientist.jpg"/>
<Image Width="200" Stretch="Uniform" Source="http://example.com/image.jpg"/>
```

# LABEL

`Label` 显示用户可以读取但无法修改的文本。关键属性见表格 B-7。

表格 B-7：Label 的属性

| 属性 | 目的 |
| Background | 文本后的颜色 |
| BorderBrush | 控件边缘的颜色 |
| BorderThickness | 控件边缘的厚度 |
| Content | 控件的内容，通常是简单文本 |
| FontFamily | 字体族名称，如 Times Roman、Arial 或 Segoe（读作 go） |
| FontSize | 文本的大小。附加 cm、in、px 或 pt 来指定厘米、英寸、像素（默认）或磅（1/72 英寸），例如 "0.25in" 或 "12pt"。 |
| TextStyle | 可以是 Normal、Italic 或 Oblique（模拟没有斜体的字字体）。 |
| FontWeight | 文本的粗细。可以是 Thin、ExtraLight、Light、Normal、Medium、SemiBold、Bold、ExtraBold、Black 和 ExtraBlack。 |
| Foreground | 用于绘制文本的颜色 |

示例简单 Label

以下代码创建了一个简单的 `Label`：

```
<Label Content="First Name:" FontSize="20" FontWeight="Bold"/>
```

# LISTVIEW

*ListView* 以几种布局中的一种显示数据项。*GridView* 最常用的。关键属性见表格 B-8。

表格 B-8：ListView 的属性

| 属性 | 目的 |
| --- | --- |
| Background | 文本后的颜色 |
| BorderBrush | 控件边缘的颜色 |
| BorderThickness | 控件边缘的厚度 |

