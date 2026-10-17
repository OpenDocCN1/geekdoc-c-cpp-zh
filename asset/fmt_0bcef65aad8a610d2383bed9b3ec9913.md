
`WebReference.WebServiceInstance = new WebReference.WebService();`

在此实例化后，就可以使用此实例建立客户端项目与我们的 Web 服务之间的连接。该方法的伪代码如下：

- A. 使用上述协议创建一个新的 Web 服务实例 `wsSelect`。
- B. 同样创建一个新的 `wsSQLResult`，它可以作为在 Web 服务中开发的的真实对象的映射。我们可以轻松地访问 Web 方法来执行数据查询，并通过将结果分配给映射对象来从返回的对象中选取结果。
- C. 创建一个新的 `DataSet` 对象，并将其用于调用返回 `DataSet` 的 Web 方法。
- D. 根据用户使用 `Query Method` 组合框选择的方法，可以使用不同的 Web 方法来执行数据查询。
- E. 将存储在真实对象中的返回数据分配给我们的映射对象，可以从该对象检索每条信息并显示在我们的图形用户界面中。
- F. 如果使用了 `DataSet` 方法，则将返回的 `DataSet` 对象分配给我们的映射 `DataSet`，并调用 `fillFacultyDataSet()` 方法将从 `DataSet` 提取的信息填充到客户端表单的文本框中。

现在我们开始编写 `Faculty Form` 构造函数的代码。

### 9.3.10.3.1 开发 FacultyForm 类构造函数的代码

现在我们开始开发 `FacultyForm` 类构造函数的代码，以完成上述 1 中的初始化工作。

- 打开 `FacultyForm` 类的构造函数，并将图 9.33 所示的以下代码输入此方法。

| WinClientSelectFacultyForm | FacultyForm() |
|---|---|
| public FacultyForm() { |
| InitializeComponent(); |
| ComboName.Items.Add("Ying Bar"); |
| ComboName.Items.Add("David Blair"); |
| ComboName.Items.Add("Black Anderson"); |
| ComboName.Items.Add("Steve Johnson"); |
| ComboName.Items.Add("Geneney King"); |
| ComboName.Items.Add("Alice Brown"); |
| ComboName.Items.Add("Debby Angles"); |
| ComboName.Items.Add("Jeff Henry"); |
| ComboName.SelectedIndex = 0; |
| ComboMethod.Items.Add("Object Method"); |
| ComboMethod.Items.Add("Stored Procedure Method"); |
| ComboMethod.Items.Add("DataSet Method"); |
| ComboMethod.SelectedIndex = 0; |
| } | |
| A | B |

图 9.33 FacultyForm 类构造函数的代码。

## ASP.NET Web Services

让我们仔细观察这段代码，看看它是如何工作的。

- A. 使用 `Add()` 方法向组合框控件 `ComboName` 中添加了 8 个默认成员，这将允许用户从该组合框控件中选择一个所需的故障项，以便对项目运行执行数据查询。通过将 `SelectedIndex` 设置为 0，默认选中第一个故障项。
- B. 在另一个组合框控件 `ComboMethod` 中也添加了三个方法，允许用户通过我们的 Web 服务执行关联的数据查询。默认选择第一个方法。

接下来，让我们来编写返回（Back）按钮的 `Click` 方法代码。

### 9.3.10.3.2 开发 Back Click 方法的代码

这段代码非常简单；只需在表单窗口中双击 Back 点击方法，并在其中输入以下单行代码：

```
Application.Exit();
```

该行代码的作用是在用户点击此按钮时终止我们的项目。接下来，让我们编写选择（Select）按钮的 `Click` 方法代码。

### 9.3.10.3 开发 Select Click 事件过程的代码

打开 Select 按钮的点击方法，并将图 9.34 所示的代码输入到方法中。让我们仔细观察这段代码，看看它是如何工作的。

- A. 在此方法的开头创建了一些数据对象，包括：使用上述协议创建的 `Web Service SQLResult`；一个新的 `SQLResult` 对象，作为我们在 Web 服务中开发的实际 `SQLResult` 的映射，可以轻松地访问 Web 方法执行数据查询，并通过将其赋值给该映射对象从返回的对象获取结果；以及一个用于调用返回 `DataSet` 的 Web 方法的新型 `DataSet` 对象。

| WinSelectProject | cmdSelect_Click(object sender, EventArgs e) |
| :--- | :--- |
| A | void cmdSelect_Click(object sender, EventArgs e) { SQLSelect.WebServiceSelect wsSelect = new SQLSelect.WebServiceSelect(); SQLSelect.SQLResult wsResult = new WS_SQLSelect.SQLResult(); DataSet wsData = new DataSet(null); if (ComboMethod.Text == "Object Method") { try(wsResult = SQLSelect.GetSelectObject(ComboName.Text)); } catch (Exception err) { MessageBox.Show("Web service is wrong: " + err.Message); } ProcessObject(ref wsResult); } else if (ComboMethod.Text == "Stored Procedure Method") { try { wsResult = SQLSelect.GetSelectSP(ComboName.Text); } catch (Exception err) { MessageBox.Show("Web service is wrong: " + err.Message); } ProcessObject(ref wsResult); } else { try { wsData = SQLSelect.GetSelectDataSet(ComboName.Text); } catch (Exception err) { MessageBox.Show("Web service is wrong: " + err.Message); } FillDataDataSet(ref wsData); } } |

图 9.34 选择按钮方法的代码。

- B. 如果用户从 `ComboMethod` 中选择了“对象方法”，则使用 `try-catch` 块通过实例化的引用类调用我们在 Web 服务中开发的 Web 方法 `GetSqlClient()` 以执行数据查询。选定的设施位于 `ComboName` 组合框的 `Text` 属性中，并作为参数传递给此调用。
- C. `catch` 语句用于收集调用过程中发生的任何异常，并使用消息框显示错误信息。
- D. 如果没有发生异常，则执行返回的自定义方法 `ProcessObject()`，从返回的对象中提取所有检索到的信息并在窗口中显示。
- E. 如果用户选择了“存储过程方法”，则通过 Web 引用类的实例调用我们在 Web 服务中开发的 Web 方法 `GetSqlClientSelect()` 来执行数据查询。
- F. `catch` 语句用于收集调用过程中发生的任何异常，并使用消息框显示错误信息。
- G. 同样，执行自定义方法 `ProcessObject()`（其代码将在稍后编写），从返回的对象中提取所有检索到的信息并在窗口中显示。
- H. 如果用户选择“DataSet 方法”，则通过 Web 引用类的实例调用 Web 方法 `GetSqlClientDataSet()`，该方法返回包含我们所需设施信息的 `DataSet`。
- I. `catch` 语句用于收集调用过程中发生的任何异常，并使用消息框显示错误信息。
- J. 调用另一个自定义方法 `FillFacilityDataSet()`（其代码将在后开发），从返回的 `DataSet` 中提取所有检索到的信息并在窗口中显示。

接下来，让我们处理所有自定义方法的代码开发。

### 9.10.3.4 开发所有自定义方法的代码

自定义方法 `ProcessObject()` 和 `FillFacilityObject()` 的代码如图 9.35 所示。这两个方法都使用调用的 `SQLResult` 作为传递参数的数据类型，因为返回的对象是该类的一个实例。

这段代码的功能是：

- A. 如果存储在我们的类或返回对象中的成员 `SQLRequestOK` 被设置为 `True`，则意味着我们的 Web 方法执行成功，将调用并执行自定义方法 `FillFacilityObject()`。
- B. 否则，不调用自定义方法。
- C. `FillFacilityObject()` 方法用于在窗口中显示设施信息。
- D. `ProcessObject()` 方法用于在窗口中显示检索到的信息。
- E. 两个方法都通过显示消息来处理潜在错误。

## 9.35 自定义方法的代码

## ASP.NET Web Services

## WinSelectProject

## ProcessObject()

```cs
void ProcessObject(ref SQLSelect.SQLResult wsResult) {
    if (wsResult.SQLRequestOK) {
        FillFacilityObject(wsResult);
    } else {
        MessageBox.Show("Web service is wrong: " + wsResult.Message);
    }
}
```

## FillFacilityObject()

```cs
void FillFacilityObject(DataSet wsData) {
    for (int i = 0; i < wsData.Tables[0].Rows.Count; i++) {
        ComboName.Items.Add(wsData.Tables[0].Rows[i]["FacilityName"]);
        ComboName.Text = wsData.Tables[0].Rows[i]["FacilityName"];
    }
}
```

## FillFacilityDataSet()

```cs
void FillFacilityDataSet(ref DataSet wsData) {
    for (int i = 0; i < wsData.Tables[0].Rows.Count; i++) {
        ComboName.Items.Add(wsData.Tables[0].Rows[i]["FacilityName"]);
        ComboName.Text = wsData.Tables[0].Rows[i]["FacilityName"];
    }
}
```
