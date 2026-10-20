

## 客户维护表单的代码

第 3 页

```
private void btnModify_Click(object sender, EventArgs e)
{
    var addModifyForm = new frmAddModifyCustomer {
        AddCustomer = false,
        Customer = selectedCustomer,
        States = context.States.OrderBy(s => s.StateName).ToList()
    };
    DialogResult result = addModifyForm.ShowDialog();

    if (result == DialogResult.OK)
    {
        selectedCustomer = addModifyForm.Customer;
        try {
            context.SaveChanges();
            DisplayCustomer();
        }
        catch (DbUpdateConcurrencyException ex) {
            this.HandleConcurrencyError(ex);
        }
        catch (DbUpdateException ex) {
            this.HandleDataError(ex);
        }
        catch (Exception ex) {
            this.HandleGeneralError(ex);
        }
    }
}

private void btnDelete_Click(object sender, EventArgs e)
{
    DialogResult result =
        MessageBox.Show(
            $"Delete {selectedCustomer.Name}?",
            "Confirm Delete", MessageBoxButtons.YesNo,
            MessageBoxIcon.Question);

    if (result == DialogResult.Yes) {
        try {
            context.Customers.Remove(selectedCustomer);
            context.SaveChanges();
            this.ClearControls();
        }
        catch (DbUpdateConcurrencyException ex) {
            this.HandleConcurrencyError(ex);
        }
        catch (DbUpdateException ex) {
            this.HandleDataError(ex);
        }
        catch (Exception ex) {
            this.HandleGeneralError(ex);
        }
    }
}
```

## 客户维护表单的代码

第 4 页

```
private void HandleConcurrencyError(DbUpdateConcurrencyException ex)
{
    ex.Entries.Single().Reload();

    var state = context.Entry(selectedCustomer).State;
    if (state == EntityState.Detached)
    {
        MessageBox.Show("Another user has deleted that customer.",
            "Concurrency Error");
        this.ClearControls();
    }
    else
    {
        string message = "Another user has updated that customer.\n" +
            "The current database values will be displayed.";
        MessageBox.Show(message, "Concurrency Error");
        this.DisplayCustomer();
    }
}

private void HandleDataError(DbUpdateException ex)
{
    string errorMessage = "";
    var sqlException = (SqlException)ex.InnerException;
    foreach (SqlError error in sqlException.Errors)
    {
        errorMessage += "ERROR CODE:  " + error.Number + " " +
            error.Message + "\n";
    }
    MessageBox.Show(errorMessage);
}

private void HandleGeneralError(Exception ex)
{
    MessageBox.Show(ex.Message, ex.GetType().ToString());
}

private void btnExit_Click(object sender, EventArgs e)
{
    this.Close();
}
}
```

## 添加/修改客户表单的代码

图 20-19 显示了添加/修改客户表单的代码。此表单首先声明了三个公共属性，用于从客户维护表单获取数据并向其提供数据。

当此表单首次加载时，Load 事件处理程序首先调用 LoadStatesComboBox() 方法来配置 State 组合框。为此，该方法将组合框绑定到客户维护表单分配给此表单的 States 属性的 States 对象集合。

如果正在添加新客户，Load 事件处理程序将继续设置表单的 Text 属性为“Add Customer”，并初始化 State 组合框，使其不选择任何状态。否则，它将表单的 Text 属性设置为“Modify Customer”，并调用 DisplayCustomerData() 方法。此方法使用表单的 Customer 属性在表单上显示客户的数据。当 Load() 方法完成后，用户可以输入新客户的数据或修改现有客户的数据。

## 添加/修改客户表单的代码

```
public partial class frmAddModifyCustomer : Form
{
    // default constructor

    public Customers Customer { get; set; }
    public List<States> States { get; set; }
    public bool AddCustomer { get; set; }

    private void frmAddModifyCustomer_Load(object sender, EventArgs e)
    {
        this.LoadStatesComboBox();
        if (this.AddCustomer)
        {
            this.Text = "Add Customer";
            cboStates.SelectedIndex = -1;
        }
        else
        {
            this.Text = "Modify Customer";
            this.DisplayCustomerData();
        }
    }

    private void LoadStatesComboBox()
    {
        try
        {
            cboStates.DataSource = this.States;
            cboStates.DisplayMember = "StateName";
            cboStates.ValueMember = "StateCode";
        }
        catch (Exception ex)
        {
            MessageBox.Show(ex.Message, ex.GetType().ToString());
        }
    }

    private void DisplayCustomerData()
    {
        txtName.Text = Customer.Name;
        txtAddress.Text = Customer.Address;
        txtCity.Text = Customer.City;
        cboStates.SelectedValue = Customer.State;
        txtZipCode.Text = Customer.ZipCode;
    }
}
```

图 20-19 的第 2 页首先介绍了 Accept 按钮的 Click 事件处理程序。此代码首先调用 IsValidData() 方法来确定表单上的数据是否有效。如果有效并且正在添加客户，则会创建一个新客户。之后，调用 LoadCustomerData() 方法以使用新的或修改后的客户数据更新 Customer 属性。最后，将表单的 DialogResult 属性设置为 DialogResult.OK，并且添加/修改表单保持打开状态，以便用户可以更正其输入。

IsValidData() 方法测试用户是否已输入姓名、地址、城市、州和邮政编码。如果用户已输入这些数据，该方法将返回 true 值。否则，它将在对话框中显示适当的错误消息并返回 false 值。

LoadCustomerData() 方法将用户输入到文本框和组合框中的值分配给表单的 Customer 属性的相应属性。在这里，SelectedValue 属性用于获取 State 组合框的值。然后，调用 ToString() 方法将该属性返回的对象转换为字符串。

Cancel 按钮的 Click 事件处理程序的工作方式与客户维护表单中 Exit 按钮的 Click 事件处理程序类似。它包含一个单一语句，调用 Close() 方法关闭表单。但是，这不会退出应用程序。相反，它会关闭添加/修改表单并将焦点返回到客户维护表单。

## 添加/修改客户表单的代码

```
private void btnAccept_Click(object sender, EventArgs e)
{
    if (this.IsValidData())
    {
        if (this.AddCustomer){
            this.Customer = new Customers();
        }
        this.LoadCustomerData();
        this.DialogResult = DialogResult.OK;
    }
}

private bool IsValidData()
{
    string errorMessage = "";
    errorMessage += Validator.IsPresent(txtName.Text, txtName.Tag.ToString());
    errorMessage += Validator.IsPresent(txtAddress.Text, txtAddress.Tag.ToString());
    errorMessage += Validator.IsPresent(txtCity.Text, txtCity.Tag.ToString());
    errorMessage += Validator.IsPresent(cboStates.Text, cboStates.Tag.ToString());
    errorMessage += Validator.IsPresent(txtZipCode.Text, txtZipCode.Tag.ToString());

    bool success = true;
    if (errorMessage != "")
    {
        MessageBox.Show(errorMessage, "Entry Error");
        success = false;
    }
    return success;
}

private void LoadCustomerData()
{
    Customer.Name = txtName.Text;
    Customer.Address = txtAddress.Text;
    Customer.City = txtCity.Text;
    Customer.State = cboStates.SelectedValue.ToString();
    Customer.ZipCode = txtZipCode.Text;
}

private void btnCancel_Click(object sender, EventArgs e)
{
    this.Close();
}
```

## 视角

在本章中，您学习了如何使用 Database First 开发从现有数据库创建实体数据模型。您还学习了如何使用 LINQ to Entities 将数据加载到模型中，并学习了如何使用 EF 插入、更新和删除数据以及检查异常。有了这些技能，您应该能够开发允许用户显示和维护数据的应用程序。

请记住，关于 EF 的学习内容远不止于此。特别是，如果应用程序将要工作的数据库尚不存在，您需要了解如何使用 Code First 开发从您创建的模型生成数据库。有关如何执行此操作的更多信息，您可以参考在线文档或获取一本关于 EF 的单独书籍。

## 术语

|  |  |
|---|---|
| Entity Framework (EF) Core | cascading deletes |
| Object Relational Mapping (ORM) framework | foreign key property |
| Object Services | lazy loading |
| Entity Client Data Provider | eager loading |
| conceptual model | query path |
| storage model | explicit loading |
| mappings | cascading updates |
| NuGet Package Manager | concurrency conflict |
| Code First development | concurrency control |
| Database First development | last in wins |
| database (DB) context class | optimistic concurrency |
| entity class | pessimistic concurrency |
| method chaining | concurrency exception |
| navigation property | concurrency token |
|  | rowversion property |

## 练习 20-1 构建产品维护应用程序

对于此练习，您将开发一个应用程序来显示、修改、插入和删除产品。为了让您更容易完成，我们将为您提供表单和项目的部分代码。

## 查看代码并运行应用程序

- 1. 在 C:\C#\Chapter 20\ProductMaintenance 目录中打开应用程序。
- 2. 查看设计器中的两个表单，然后显示每个表单的代码并查看该代码。
- 3. 运行应用程序并单击一些按钮。请注意，它们目前还不做太多事情，尽管添加和修改按钮确实会显示添加/修改

