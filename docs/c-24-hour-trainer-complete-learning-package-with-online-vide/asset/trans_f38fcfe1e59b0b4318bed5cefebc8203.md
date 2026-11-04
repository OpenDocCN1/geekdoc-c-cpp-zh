
## 编程数据库，第 2 部分

上一课中描述的简单程序几乎算不上商业级别的数据库应用程序，但它们确实能让你用极少的代码执行基本的数据库操作。

在本课中，你将学习如何为第 34 课中描述的程序添加一些新功能。你将学习如何为程序添加搜索、过滤和排序功能，以使查找数据变得更容易。

### 搜索

在大型数据库中，定位特定值可能很困难。程序可以通过使用 BindingContext 的 Find 方法来简化查找记录的过程。此方法将要搜索的字段名称和应查找的值作为参数。它返回具有所需值的第一个记录的索引。

例如，以下代码在名为 contactsBindingSource 的 BindingSource 中的数据中搜索 FirstName 值等于 Kim 的记录：

```
int recordNumber = contactsBindingSource.Find("FirstName", "Kim");
```

找到目标记录的索引后，你可以以某种方式突出显示它以供用户查看。例如，请回忆 BindingSource 的 CurrencyManager 控制数据中的当前位置。以下代码使当前记录成为 Find 找到的记录，因此显示数据的任何控件都会显示该记录：

```
contactsBindingSource.CurrencyManager.Position = recordNumber;
```

> **警告** 如果 Find 找不到目标字符串，则返回 -1。请注意不要尝试对记录号 -1 执行任何显式操作，否则程序可能会崩溃。这意味着上一行代码实际上应该是
>
> ```
> if (recordNumber != -1)
>     contactsBindingSource.CurrencyManager.Position = recordNumber;
> ```

如果程序在网格中显示数据，则焦点会移动到找到的记录的行。如果程序在字段控件中显示数据，则这些控件现在显示找到的记录的数据。

### 过滤

Find 方法有些受限。它只在单个字段中搜索完全匹配，并且只返回第一个匹配记录的索引。通常你可能更喜欢更灵活的搜索，例如可以检查条件（age >= 21）、查找部分匹配（LastName begins with S）并组合多个测试（state is VA or DC）的搜索。也许看到满足条件的全部记录而不是仅第一个记录会更好。

过滤器让你执行这类搜索。过滤器测试 BindingSource 数据中的每条记录并选择满足测试的记录。附加到 BindingSource 的任何显示控件只显示所选记录。

要使用过滤器，将 BindingSource 的 Filter 属性设置为描述要选择的记录的字符串。过滤器将每条记录的字段与值进行比较并选择匹配的记录。例如，子句 State='FL' 选择 State 字段值为 FL 的记录。

字符串值应使用单引号或双引号分隔。（单引号通常更容易输入到本身由双引号分隔的字符串中。）数值不应有分隔符。

表 35-1 列出了可用于比较字段和值的运算符。

**表 35-1**

| 操作符 | 用途 |
| --- | --- |
| = | 等于 |
| <> | 不等于 |
| < | 小于 |
| > | 大于 |
| <= | 小于或等于 |
| >= | 大于或等于 |
| LIKE | 匹配模式 |
| IN | 在值列表中 |

LIKE 运算符执行模式匹配。使用 * 或 % 作为通配符，匹配零个或多个字符。

你可以使用 AND、OR 和 NOT 逻辑运算符来组合多个比较的结果。如有必要，使用括号来确定求值顺序。

表 35-2 列出了一些示例过滤器。

**表 35-2**

| 过滤器 | 选择 |
| --- | --- |
| LastName = 'Johnson' | LastName 为 Johnson 的记录 |
| FirstName = 'Ann' OR FirstName = 'Anne' | FirstName 为 Ann 或 Anne 的记录 |
| FirstName LIKE 'Pam%' | FirstName 以 Pam 开头的记录 |
| State IN('NY','NC','NJ') | State 为 NY、NC 或 NJ 的记录 |
| (Balance < -50) OR ((Balance < 0) AND (DaysOverdue > 30)) | 账户透支超过 $50 或账户透支任何金额超过 30 天的记录 |

你可以使用 BindingSource 的 RemoveFilter 方法移除过滤器并再次显示所有记录。

### 排序

如果你在 DataGridView 中显示数据，你可以单击列标题根据该列中的值对记录进行排序。再次单击会反转排序顺序。排序不会比这更简单了。

然而，如果你是在字段而不是网格中显示数据，则不会获得自动排序。幸运的是，你只需将 BindingSource 的 Sort 属性设置为要排序的字段的名称，即可使其排序。使用其 RemoveSort 方法取消排序并以原始顺序显示记录。

### 试一试

在本练习中，你为在网格中显示记录的程序添加过滤功能。你允许用户输入过滤器，并使程序仅显示匹配过滤器的记录。

### 课程要求

在本课中，你：

- 复制你在第 34 课 Try It 中构建的程序（或从书的网站下载第 34 课的版本）。
- 添加一个包含 TextBox 和 Button 的 ToolStrip。
- 当用户单击 Button 时，应用在 TextBox 中输入的过滤器。

> **注释** 你可以从网站 www.wrox.com/go/csharp24hourtrainer2e 下载本课的代码和资源。

### 提示

- 确保在用户输入无效过滤器时保护程序。

### 逐步操作

- 复制你在第 34 课 Try It 中构建的程序（或从书的网站下载第 34 课的版本）。
  - 1. 这很直接。
- 添加一个包含 TextBox 和 Button 的 ToolStrip。
  - 1. 这很直接。
- 当用户单击 Button 时，应用在 TextBox 中输入的过滤器。
  - 1. 使用类似以下的代码：

```
// Apply the filter.
private void filterButton_Click(object sender, EventArgs e)
{
    string filter = filterTextBox.Text.Trim();
    if (filter.Length == 0)
    {
        // No filter.
        contactsBindingSource.RemoveFilter();
    }
    else
    {
        // Add the filter.
        try
        {
            contactsBindingSource.Filter = filter;
        }
        catch (Exception ex)
        {
            MessageBox.Show(ex.Message);
        }
    }
}
```

### 练习

- 1. 复制你为 Try It 构建的程序，并用“State:”标签和 ComboBox 替换 ToolBar 的 TextBox 和 Button。使 ComboBox 列出数据库中存在的州缩写（只需硬编码）加上一个空白选项。当用户选择一个值时，使用所选州来过滤数据。

- 7. [WPF, Hard] 自然地，在 WPF 中过滤记录比在 Windows Forms 中更困难。复制你在练习 34-4 中编写的程序，并添加一个 ToolBar、“State:”标签和 ComboBox，就像你在练习 1 中所做的那样。（你可能希望重新排列程序的控件以使用 DockPanel。）使用以下代码来过滤数据：

```
// Filter with the selected state.
private void stateComboBox_SelectionChanged(object sender,
    SelectionChangedEventArgs e)
{
    // Get the dataset.
    ContactsDataSet contactsDataSet =
        (ContactsDataSet)this.FindResource("contactsDataSet");

    // Get the selected state.
    ComboBoxItem item = stateComboBox.SelectedItem as ComboBoxItem;
    string state = item.Content.ToString();
    Console.WriteLine("Filtering by state " + state);

    // Set the filter.
    CollectionViewSource contactsViewSource =
        (CollectionViewSource)FindResource("contactsViewSource");
    BindingListCollectionView view =
        (BindingListCollectionView)contactsViewSource.View;

    if (state.Length == 0) view.CustomFilter = "";
    else view.CustomFilter = "State = '" + state + "'";
}
```

- 8. [WPF, Hard] 复制你在练习 34-11 中构建的程序，并添加“State:”标签和 ComboBox，就像你在练习 7 中所做的那样。你还需要做两个额外的更改。首先，在更改过滤器后，你需要更新位置标签。其次，你需要更改显示当前记录位置的方式，使其使用所选记录而不是整个数据表。修改 ShowPosition 方法，使其使用以下代码来确定所选记录的数量：

```
// Get the number of records selected.
CollectionViewSource contactsViewSource =
    (CollectionViewSource)FindResource("contactsViewSource");
BindingListCollectionView view =
    (BindingListCollectionView)contactsViewSource.View;
int numselected = view.Count;
```

> **注释** 请在 www.wrox.com/go/csharp24hourtrainer2evideos 在线选择第 35 课的视频。
