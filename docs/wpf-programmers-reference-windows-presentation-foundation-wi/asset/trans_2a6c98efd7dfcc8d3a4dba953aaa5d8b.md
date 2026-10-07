

# GridSplitter 46

```xml
<ColumnDefinition Width="*" />
<ColumnDefinition Width="*" />
<ColumnDefinition Width="*" />
</Grid.ColumnDefinitions>
<RowDefinitions>
<RowDefinition Height="*" />
<RowDefinition Height="*" />
<RowDefinition Height="*" />
</Grid.RowDefinitions>
<GridSplitter Grid.Column="1" Grid.RowSpan="10"
HorizontalAlignment="Left"
VerticalAlignment="Stretch"
Background="Blue"
ShowsPreview="False"
Width="5" />
<GridSplitter Grid.Column="1" Grid.RowSpan="10"
HorizontalAlignment="Right"
VerticalAlignment="Stretch"
Background="Red"
ShowsPreview="False"
Width="5" />
</Grid>
```

以下代码为上一个示例中使用的 Grid 创建了水平的 GridSplitters：

```xml
<Grid>
<Grid.ColumnDefinitions>
<ColumnDefinition Width="*" />
<ColumnDefinition Width="*" />
<ColumnDefinition Width="*" />
</Grid.ColumnDefinitions>
<RowDefinitions>
<RowDefinition Height="*" />
<RowDefinition Height="*" />
<RowDefinition Height="*" />
</Grid.RowDefinitions>
<GridSplitter Grid.Row="1" Grid.ColumnSpan="20"
HorizontalAlignment="Stretch"
VerticalAlignment="Top"
Background="Blue"
ShowsPreview="False"
Height="5" />
<GridSplitter Grid.Row="1" Grid.ColumnSpan="20"
HorizontalAlignment="Stretch"
VerticalAlignment="Bottom"
Background="Red"
ShowsPreview="False"
Height="5" />
<Image Source="baseball.jpg" Grid.Row="1" Grid.Column="1" />
</Grid>
```

# 留出空间

在 Grid 内部放置其他对象时，务必为拆分器留出空间。例如，如果你在第二列的左边缘放置一个 5 像素宽的 GridSplitter，那么该列中的任何其他控件都应该具有至少 5 像素的左边距，以免它们与拆分器重叠。

# LISTBOX

ListBox 显示项目列表并允许用户选择一个或多个。

该控件应包含持有选项的 ListBoxItems。SelectedIndex、SelectedItem 和 SelectedValue 属性允许你获取和设置当前选的项目。

**表格 D-14**: ListBox的关键属性

| 属性 | 用途 |
| --- | --- |
| HorizontalContentAlignment | 决定 ListboxItems 的对齐方式。可以是 Center（居中）、Left（左对）、Right（右对）或 Stretch（拉伸）。 |
| SelectedIndex | 决定当前选中项目的索引。 |
| SelectedItems | 返回当前选的项目。（如果选中多个项目，无法使用 SelectedIndex、SelectedItem 或选择属性来查看哪些项目被选中。） |
| SelectionMode | 决定用户可以选择多少项目。可以是 Single（单选，仅限一项）、Multiple（多选，可以通过单独点击选择多个项目）或 Extended（扩展，可以使用 [Shift]+点击和 [Ctrl]+点击选择多个项目）。 |

**表格 D-15**: ListBox 的关键事件

| 事件 | 用途 |
| --- | --- |
| SelectionChanged | 当选中项发生变化时触发。 |

ListBox 内部的 ListBox 对象还提供了一些实用的事件（参见表 D-16）。

# 表格 D-16:

| 事件 | 用途 |
|---|---|
| Selected | 当项目被选中时触发。 |
| Unselected | 当项目被取消选中时触发。 |

# 使用 ListBox 的示例

以下 XML 代码构建了一个 ListBox，列出太阳系行星名称。它还显示了一个 Label，显示当前选中行星的名称。

```xml
<StackPanel>
  <ListBox Names="listPlanets" SelectedIndex="2">
    <ListBoxItem Content="Mercury" />
    <ListBoxItem Content="Venus" />
    <ListBoxItem Content="Earth" />
    <ListBoxItem Content="Mars" />
    <ListBoxItem Content="Jupiter" />
    <ListBoxItem Content="Saturn" />
    <ListBoxItem Content="Uranus" />
    <ListBoxItem Content="Neptune" />
    <ListBoxItem Content="Pluto" />
  </ListBox>
  <Label Content="{Binding ElementName=listPlanets, Path=SelectedItem.Content}"/>
</StackPanel>
```

# MENU

Menu 为窗口显示菜单。虽然你可以在 Menu 中放置 Labels、Buttons 和 TextBoxes 等控件，但 Menu 通常包含 MenuItem 对象，这些对象包含窗口的顶层菜单（参见表 D-17 到 D-19）。

MenuItem 的 Header 属性决定了它的显示内容。MenuItem 可以包含其他 MenuItem 以构建菜单层次结构。

# 表格 D-17:

| 属性 | 用途 |
|---|---|
| IsMainMenu | 决定该控件是否为主菜单。如果一个窗口包含多个菜单，所有其他菜单都应将此设置为 False，这样当用户按下 [Alt] 键或 [F10] 时，它们就不会收到通知。 |

# 附录 D 用户交互控件

表格 D-18:
| 属性 | 用途 |
|---|---|
| Command | 决定与菜单项相关的命令。 |
| CommandParameter | 决定传递给 Command 的参数。 |
| CommandTarget | 决定引发 Command 的对象。 |
| IsCheckable | 决定菜单项是否可以被勾选。如果为 True，则该项会自动勾选和取消勾选。 |
| IsChecked | 决定控件当前是否被勾选。 |
| IsSubOpen | 决定菜单是否打开。 |

表格 D-19:
| 事件 | 用途 |
|---|---|
| Checked | 当控件被勾选时触发。 |
| Click | 当控件被点击时触发。 |
| SubmenuOpened | 当子菜单打开时触发。 |
| Unchecked | 当控件被取消勾选时触发。 |

# 使用 Menu 的示例

以下 XML 代码构建了一个带有若干 MenuItem 的 Menu。

```xml
<Menu>
  <MenuItem Header="File">
    <MenuItem Header="New" />
    <MenuItem Header="Open" />
  </MenuItem>
  <MenuItem Header="Edit">
    <MenuItem Header="Copy" />
    <MenuItem Header="Paste" />
  </MenuItem>
</Menu>
```

# PASSDBOX

PasswordBox 是一个隐藏文本的文本框，显示点、星号或其他字符（参见表 21）。

表格 D-20: PasswordBox 的关键属性

| 属性 | 用途 |
|---|---|
| Password | 以明文确定当前密码。 |
| PasswordChar | 决定输入时显示的字符。 |
| SecurePassword | 以 SecureString 返回当前密码。 |

表格 D-21: PasswordBox 的关键事件

| 事件 | 用途 |
|---|---|
| PasswordChanged | 当密码变化时触发。 |

# 使用 Password 的示例

以下代码创建两个 PasswordBox。第一个使用默认字体和 PasswordChar，因此显示圆圈。第二个使用 Wingdings 字体和 PasswordChar="N"。

```xml
<PasswordBox Password="Secret" />
<PasswordBox Password="Secret" FontFamily="Wingdings" PasswordChar="N" />
```

# RADIOBUTTON

RadioButton 允许用户从一组互斥选项中选择一个（参见表 D-22）。当用户选择一个 RadioButton 时，同一容器内的其他选项都会取消。（对比 CheckBox，可以同时选择多个。）

ComboBox 也允许用户从一系列选择中选择一个，因此你可以考虑使用 ComboBox 而不是 RadioButton，特别是当你节省空间时。

可以通过将它们放在不同的容器中或使用 GroupName 属性创建多个 RadioButton 组。

表格 D-22:
| 属性 | 用途 |
|---|---|
| IsChecked | 决定控件当前是否被选中。 |
| GroupName | 定义 RadioButton 组。共享非空 GroupName 值的 RadioButton 属于同一组，即使它们位于不同的容器中。 |
| IsThreeState | 决定控件是否在三个值之间循环——选中（IsChecked = True）、未选中（IsChecked = False）和不确定（IsChecked = null）。 |

只有代码可以将 RadioButton 设置为不确定状态。用户只能选中或取消选中 radioButton。
当 RadioButton 处于不确定状态时，如果用户选择了组内的另一个 RadioButton，它不会取消选中（参见表 D-23）。

表格 D-23:
| 事件 | 用途 |
|---|---|
| Checked | 当控件被选中时触发。 |
| Unchecked | 当控件被取消选中时触发。 |
| Click | 当控件被选中或取消选中时触发。 |

