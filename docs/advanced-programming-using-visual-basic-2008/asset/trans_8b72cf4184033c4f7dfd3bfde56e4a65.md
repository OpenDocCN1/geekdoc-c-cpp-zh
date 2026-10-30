

## TableAdapter 和 TableAdapterManager

尽管用户可以在内存中对数据集进行更改，但在执行 TableAdapter 的 Update 方法或 TableAdapterManager 的 UpdateAll 方法之前，原始数据源不会发生任何更改。您可以选择在每次更改后执行更新，也可以在程序终止时一次性执行。

TableAdapterManager 是 Visual Studio 2008 的新功能，用于管理多个相关表的更新。对于单个表，例如我们首先要更新的表，只需要 TableAdapter 即可。如果您使用 Update Wizard 更新在早期版本的 Visual Basic 中创建的数据库应用程序，则不会生成 TableAdapterManager，并且更新会通过 TableAdapter.Update 方法执行。默认情况下，在使用 Visual Studio 2008 创建的新数据库应用程序中，创建 TableAdapter 时也会创建 TableAdapterManager。

本章后面在“Updating Related Tables”部分，您将学习到使用 TableAdapterManager 执行的层级更新。您可以通过在将任何表或字段拖到窗体之前将数据集的 HierarchicalUpdate 属性设置为 false，来防止在单表应用程序中自动添加 TableAdapterManager。

TableAdapter.Update 和 TableAdapter.UpdateAll 方法都会将数据集中的更改保存到原始数据源。

## The Update and UpdateAll Methods—General Form

```
TableAdapter.Update(DataSet.table)
TableAdapterManager.UpdateAll(DataSet)
```

请注意，TableAdapterManager.UpdateAll 方法仅指定数据集名称；如果 TableAdapter 只有一个表，TableAdapter.Update 方法也可以仅指定数据集名称；否则您必须提供 DataSetName.TableName。

## The Update and UpdateAll Methods—Examples

```
PublishersTableAdapter.Update(ContactsDataSet.Publishers)
PublishersTableAdapter.Update(ContactsDataSet)
TableAdapterManager.UpdateAll(ContactsDataSet)
```

您可以决定何时执行更新方法。您可以在每次添加、编辑或删除发生时保存更改，也可以在程序终止时等待。或者结合这两种技术，通过在菜单或按钮上提供 Save 选项，然后在程序终止时提示未保存的更改。这种技术与 Office 应用程序相匹配：您可以随时保存文档，但如果尝试在未保存更改的情况下关闭，会显示对话框。

substantial network traffic. 您必须考虑应用程序和数据的位置、可以进行更改的用户数量，以及数据源是否需要始终保持最新非常重要。

最好等待程序终止时保存所有更改。（但是，断电可能会导致所有更改丢失。）要提示未保存的更改，请将更新方法放在窗体的 FormClosing 事件处理程序中。FormClosing 事件在 Me.Close 执行时发生，这应该发生在用户从菜单或按钮中选择 Exit 时，或用户单击窗体的 Close 按钮甚至退出 Windows 时。

要询问用户在已进行更改时是否保存数据集，请检查 HasChanges 方法的返回值。如果已进行更改，请显示消息“Do you want to save the changes?”。以下代码属于窗体的 FormClosing 事件处理程序：

```
Private Sub ContactForm_FormClosing(ByVal sender As Object, _
ByVal e As System.Windows.Forms.FormClosingEventArgs) _
Handles Me.FormClosing
    ' Check for unsaved changes.
    Dim AnswerDialogResult As DialogResult

    If ContactsDataSet.HasChanges() Then
        ' Query the user to save the changes.
        AnswerDialogResult = MessageBox.Show(
            "Do you want to save the changes?", "Unsaved Changes", _
            MessageBoxButtons.YesNoCancel, MessageBoxIcon.Question, _
            MessageBoxDefaultButton.Button2)
        Select Case AnswerDialogResult
            Case Windows.Forms.DialogResult.Yes
                ' Save the DataSet.
                PublishersBindingSource.EndEdit()
                PublishersTableAdapter.Update(ContactsDataSet)
            Case Windows.Forms.DialogResult.Cancel
                ' Cancel the closing.
                e.Cancel = True
        End Select
    End If
End Sub
```

## Feedback 3.1

编写语句以使用 NorthwindTableAdapter 保存 CustomerDataSet 的所有更改。

## The BindingSource Object

当您使用绑定控件时，例如网格、列表、文本框或标签，绑定的表数据由 BindingSource 对象管理。绑定源控制表中记录的位置，并负责确保窗体上的所有绑定控件显示来自同一记录的数据。您可以使用绑定源的属性来确定当前记录并从一条记录导航到下一条记录。

## Binding Source Properties and Methods

您可以使用 BindingSource 对象的属性和方法来显示记录号并进行导航。

## Displaying the Record Number

BindingSource 的 Position 属性保存当前行号（从零开始），而 Count 属性表示表中的记录数。

```
PublishersBindingSource.Position
PublishersBindingSource.Count
```

使用这些属性，您可以在窗体的标签或状态栏中显示记录号：“Record 5 of 200”。

请注意，您必须将 1 加到 Position 属性上，因为它是从零开始的。

```
With PublishersBindingSource
    RecordPositionLabel.Text = "Record " & _
        (.Position + 1).ToString() & " of " & .Count.ToString()
End With
```

表 5.3 显示了 BindingSource 类的一些有用属性和方法。

## Useful Properties and Methods of the BindingSource Class

| Property/method | Purpose |
|---|---|
| Current property | Retrieves the current row. |
| Position property | Index of the current row. |
| Count property | Number of rows in the table. |

## Navigating Using BindingSource Methods

您可以使用绑定源进行记录导航。例如，您可能有 Next Record、Previous Record、First Record 和 Last Record 按钮。修改 Position 属性会更改记录位置；如果您有绑定字段或网格，则新的当前记录会显示。表 5.4 显示了导航方法。

## Navigation Methods of the BindingSource Class

| Method | Purpose |
|---|---|
| MoveFirst | Moves to the first row. |
| MoveNext | Moves to the next row. |
| MoveLast | Moves to the last row. |
| MovePrevious | Moves to the previous row. |

您应该检查以确保不会尝试移动到超出最后一条记录或在第一条记录之前的记录。请记住，记录位置或索引从 0 开始，使最后一条记录的位置为 Count 减一。

```
' Move to the next record.
With PublishersBindingSource
    If .Position = .Count - 1 Then
        .MoveFirst()
    Else
        .MoveNext()
    End If
End With

' Move to the previous record.
With PublishersBindingSource
    If .Position = 0 Then
        .MoveLast()
    Else
        .MovePrevious()
    End If
End With

' Move to the first record.
PublishersBindingSource.MoveFirst()

' Move to the last record.
PublishersBindingSource.MoveLast()
```

## Binding Source Update Methods

您可以使用绑定源的方法来维护表数据（表 5.5）。使用 AddNew 方法开始向数据集中添加新记录的操作。当您为网格中显示的数据执行 AddNew 方法时，网格中的最后一行（带星号的那一行）会被激活，以便用户可以输入新行。如果您为单独绑定的字段执行 AddNew，字段内容将被清除，以便用户可以输入新记录。当用户离开新记录时，EndEdit 方法会自动执行；或者您也可以显式执行该方法，也许响应按钮单击。如果用户希望取消添加或编辑，您可以调用 CancelEdit 方法。您也可以对正在进行的添加使用 CancelNew，其效果与 CancelEdit 相同。但请始终记住数据集是断开连接的，因此任何新记录都添加到内存中的数据集，而不是在执行 Update 或 UpdateAll 方法之前保存到原始数据源。

## Editing Methods of the BindingSource Object

### Table 5.5

| Method | Purpose |
|---|---|
| AddNew | Clears bound fields to allow new data to be entered. Adds a new row to the table. |
| Insert | Adds a record at the specified index. |
| CancelNew | Cancels the record being added. |
| CancelEdit | Cancels the edit currently being processed. |
| EndEdit | Completes the current edit and saves the changes in the dataset. |
| RemoveAt | Deletes the row at the specified index from the table. |
| RemoveCurrent | Deletes the current record. |

