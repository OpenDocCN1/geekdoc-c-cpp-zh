
这是一个好主意——以防你的程序用户需要选择具有非标准扩展名的文件。但是，如果你想取消“所有文件”过滤器，请调用

```java
chooser.setAcceptAllFileFilterUsed(false)
```

> **警告：** 如果同一个文件选择器要重复用于加载和保存不同类型的文件，请先调用
>
> `chooser.resetChoosableFilters()`
>
> 来清除任何旧的过滤器，然后再添加新的过滤器。

最后，你可以通过为文件选择器显示的每种文件类型提供特殊的图标和文件描述来自定义文件选择器。具体做法是提供一个扩展 javax.swing.filechooser 包中 FileView 类的类的对象。这绝对是一项高级技术。通常，你不需要提供文件视图——可插拔外观会为你提供一个。但如果你想为特殊文件类型显示不同的图标，则可以安装自己的文件视图。你需要扩展 FileView 类并实现五个方法：

```
Icon getIcon(File f)
String getName(File f)
String getDescription(File f)
String getTypeDescription(File f)
Boolean isTraversable(File f)
```

然后，使用 setFileView 方法将你的文件视图安装到文件选择器中。

文件选择器会为每个要显示的文件或目录调用你的方法。如果你的方法对图标、名称或描述返回 null，文件选择器会查阅外观的默认文件视图。这很好，因为你只需处理那些想要有所不同的文件类型。

文件选择器调用 isTraversable 方法来决定当用户点击目录时是否打开该目录。请注意，这个方法返回的是一个 Boolean 对象，而不是 boolean 值！这看起来有点奇怪，但实际上很方便——如果你不想偏离默认文件视图，只需返回 null。文件选择器会转而查阅默认文件视图。换句话说，这个方法返回一个 Boolean，允许你在三个选项中进行选择：true（Boolean.TRUE）、false（Boolean.FALSE）或不在乎（null）。

示例程序包含一个简单的文件视图类。只要文件与某个文件过滤器匹配，该类就显示一个特定图标。我们用它在所有图像文件旁显示一个调色板图标。

```java
class FileIconView extends FileView
{
    private FileFilter filter;
    private Icon icon;

    public FileIconView(FileFilter aFilter, Icon anIcon)
    {
        filter = aFilter;
        icon = anIcon;
    }

    public Icon getIcon(File f)
    {
        if (!f.isDirectory() && filter.accept(f))
            return icon;
        else return null;
    }
}
```

使用 setFileView 方法将此文件视图安装到你的文件选择器中：

```java
chooser.setFileView(new FileIconView(filter,
    new ImageIcon("palette.gif")));
```

文件选择器随后会在所有通过过滤器的文件旁边显示调色板图标，并使用默认文件视图显示所有其他文件。自然，我们使用的是在文件选择器中设置的那个过滤器。

最后，你可以通过添加一个*附件*组件来自定义文件对话框。例如，图 11.34 显示了文件列表旁边的一个预览附件。该附件显示当前所选文件的缩略图。

附件可以是任何 Swing 组件。在我们的示例中，我们扩展了 JLabel 类，并将其图标设置为图形图像的缩放副本：

```java
class ImagePreviewer extends JLabel
{
    public ImagePreviewer(JFileChooser chooser)
    {
        setPreferredSize(new Dimension(100, 100));
        setBorder(BorderFactory.createEtchedBorder());
    }

    public void loadImage(File f)
    {
        var icon = new ImageIcon(f.getPath());
        if(icon.getIconWidth() > getWidth())
            icon = new ImageIcon(icon.getImage().getScaledInstance(
                getWidth(), -1, Image.SCALE_DEFAULT));
        setIcon(icon);
        repaint();
    }
}
```

![](img/127bccebb2cfadea3f02579edaad63c3_755_0.png)

**图 11.34** 带有预览附件的文件对话框

这里只有一个挑战。当用户选择不同的文件时，我们希望更新预览图像。文件选择器使用“JavaBeans”机制，在其某个属性发生变化时通知感兴趣的监听器。所选文件是一个属性，你可以通过安装 PropertyChangeListener 来监视它。下面是你截获这些通知所需的代码：

```java
chooser.addPropertyChangeListener(event -> {
    if (event.getPropertyName() == JFileChooser.SELECTED_FILE_CHANGED_PROPERTY)
    {
        var newFile = (File) event.getNewValue();
        // update the accessory
        ...
    }
});
```

## javax.swing.JFileChooser 1.2

- `JFileChooser()`
  创建一个可用于多个窗口的文件选择器对话框。
- `void setCurrentDirectory(File dir)`
  设置文件对话框的初始目录。
- `void setSelectedFile(File file)`
- `void setSelectedFiles(File[] file)`
  为文件对话框设置默认的文件选择。
- `void setMultiSelectionEnabled(boolean b)`
  设置或取消多选模式。
- `void setFileSelectionMode(int mode)`
  让用户只能选择文件（默认）、只能选择目录，或同时选择文件和目录。mode 参数是 `JFileChooser.FILES_ONLY`、`JFileChooser.DIRECTORIES_ONLY` 和 `JFileChooser.FILES_AND_DIRECTORIES` 之一。
- `int showOpenDialog(Component parent)`
- `int showSaveDialog(Component parent)`
- `int showDialog(Component parent, String approveButtonText)`
  显示一个对话框，其中“批准”按钮的标签为 “Open”、“Save” 或 approveButtonText 字符串。返回 `APPROVE_OPTION`、`CANCEL_OPTION`（如果用户选择了取消按钮或关闭了对话框），或 `ERROR_OPTION`（如果发生了错误）。
- `File getSelectedFile()`
- `File[] getSelectedFiles()`
  获取用户选择的文件或文件数组（如果用户没有选择任何文件，则返回 null）。
- `void setFileFilter(FileFilter filter)`
  设置文件对话框的文件过滤器。所有 filter.accept 返回 true 的文件都会显示。此外，还会将该过滤器添加到可选择的过滤器列表中。
- `void addChoosableFileFilter(FileFilter filter)`
  向可选择的过滤器列表中添加一个文件过滤器。
- `void setAcceptAllFileFilterUsed(boolean b)`
  在过滤器组合框中包含或取消“所有文件”过滤器。
- `void resetChoosableFileFilters()`
  清除可选择过滤器的列表。除非被显式取消，否则仅保留“所有文件”过滤器。
- `void setFileView(FileView view)`
  设置一个文件视图，以提供关于文件选择器显示的文件的各项信息。
- `void setAccessory(JComponent component)`
  设置附件组件。

### javax.swing.filechooser.FileFilter 1.2

- `boolean accept(File f)`
  如果文件选择器应显示此文件，则返回 true。
- `String getDescription()`
  返回此文件过滤器的描述——例如，“图像文件 (*.gif,*.jpeg)”。

### javax.swing.filechooser.FileNameExtensionFilter 6

- `FileNameExtensionFilter(String description, String... extensions)`
  构造一个具有给定描述的文件过滤器，该过滤器接受所有目录以及所有名称以句点后跟给定扩展名字符串之一结尾的文件。

### javax.swing.filechooser.FileView 1.2

- `String getName(File f)`
  返回文件 f 的名称；如果没有，则返回 null。通常，此方法直接返回 `f.getName()`。
- `String getDescription(File f)`
  返回文件 f 的可读性描述；如果没有，则返回 null。例如，如果 f 是一个 HTML 文档，此方法可能会返回它的标题。
- **String getTypeDescription(File f)**
  返回文件 f 类型的可读性描述；如果没有，则返回 null。例如，如果 f 是一个 HTML 文档，此方法可能会返回字符串 "Hypertext document"。
- **Icon getIcon(File f)**
  返回文件 f 的图标；如果没有，则返回 null。例如，如果 f 是一个 JPEG 文件，此方法可能会返回一个缩略图图标。
- **Boolean isTraversable(File f)**
  如果 f 是用户可打开的目录，则返回 Boolean.TRUE。如果目录在概念上是一个复合文档，此方法可能返回 Boolean.FALSE。与所有 FileView 方法一样，该方法可以返回 null，表示文件选择器应改为查阅默认视图。

关于 Swing 编程的讨论到此结束。有关更高级的 Swing 组件和复杂的图形技术，请参阅卷 II。
