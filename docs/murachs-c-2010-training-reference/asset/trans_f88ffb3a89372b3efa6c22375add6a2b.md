

# 客户维护表单代码

第2页

```c
private void DisplayCustomer()
{
    txtName.Text = customer.Name;
    txtAddress.Text = customer.Address;
    txtCity.Text = customer.City;
    txtState.Text = customer.State;
    txtZipCode.Text = customer.ZipCode;
    btnModify.Enabled = true;
    btnDelete.Enabled = true;
}
```

```c
private void btnAdd_Click(object sender, EventArgs e)
{
    frmAddModifyCustomer addCustomerForm = new frmAddModifyCustomer();
    addCustomerForm.customer = true;
    DialogResult result = addCustomerForm.ShowDialog();
    if (result == DialogResult.OK)
    {
        customer = addCustomerForm.customer;
        txtCustomerID.Text = customer.CustomerID.ToString();
        this.DisplayCustomer();
    }
}
```

```c
private void btnModify_Click(object sender, EventArgs e)
{
    frmAddModifyCustomer modifyCustomerForm = new frmAddModifyCustomer();
    modifyCustomerForm.customer = false;
    modifyCustomerForm.customer = customer;
    DialogResult result = modifyCustomerForm.ShowDialog();
    if (result == DialogResult.OK)
    {
        customer = modifyCustomerForm.customer;
        this.DisplayCustomer();
    }
    else if (result == DialogResult.Retry)
    {
        this.GetCustomer(customer.CustomerID);
        if (customer != null)
        {
            this.DisplayCustomer();
        }
        else
        {
            this.ClearControls();
        }
    }
}
```

图 20-12 客户维护表单代码（3部分中的第2部分）

如果用户点击删除按钮，该按钮的 Click 事件处理程序将首先显示一个对话框以确认删除操作。如果确认了操作，它将调用 `CustomerDB` 类的 `DeleteCustomer` 方法来删除客户。如果该方法返回 false，则会显示错误消息，指示该客户已被更新或删除，并重新检索客户。然后，如果找到了客户，将显示该客户的更新数据。否则，将清空表单。如果客户被成功删除，表单也会被清空。

第20章 如何使用 ADO.NET 编写自己的数据访问代码

# 添加/修改客户表单代码 第3页

```c
private void btnDelete_Click(object sender, EventArgs e)
{
    DialogResult result = MessageBox.Show("删除 " + customer.Name + "?",
    "确认删除", MessageBoxButtons.YesNo,
    MessageBoxIcon.Query);
    if (result == DialogResult.Yes)
    {
        try
        {
            if ((CustomerDB.DeleteCustomer(customer)))
            {
                MessageBox.Show("另一个用户更新或删除了" +
                "该客户。", "数据库错误");
                this.GetCustomer(customer.CustomerID);
                if (customer != null)
                {
                    this.DisplayCustomer();
                }
                else
                {
                    this.ClearControls();
                }
            }
            else
            {
                this.ClearControls();
            }
        }
        catch (Exception ex)
        {
            MessageBox.Show(ex.Message, ex.GetType().ToString());
        }
    }
}
private void btnExit_Click(object sender, EventArgs e)
{
    this.Close();
}
```

图 20-12 客户维护表单代码（3部分中的第3部分）

# 添加/修改客户表单代码

图 20-13 显示了添加/修改客户表单的代码。该表单首先声明了两个公共字段，这些字段也会被客户维护表单使用。

当表单首次加载时，Load 事件处理程序首先调用 `LoadStateComboBox` 方法。该方法使用 `StateDB` 类的 `GetStates` 方法来填充一个包含 `State` 对象的通用列表。然后，它将表单上的 `State` 组合框（combo box）进行绑定。

如果正在添加客户，Load 事件处理程序将继续将表单的 `Text` 属性设置为“添加客户”，并初始化 `State` 组合框以便不选择任何状态。否则，它将表单的 `Text` 属性设置为“修改客户”并调用 `DisplayCustomer` 方法。此后，用户可以为新客户输入数据或修改现有客户的数据。

如果用户点击接受（Accept）按钮，该按钮的 Click 事件处理程序将首先调用 `IsValidData` 方法。该方法为每个文本框调用 `Validator` 类的 `IsPresent` 方法以确定其是否包含数据。它还会调用 `State` 组合框的 `IsPresent` 方法以确保已选择了一个状态。

如果表单有效，事件处理程序继续检查是在添加客户还是修改客户。如果正在添加客户，则将 `customer` 字段设置为新的 `Customer` 对象并调用 `PutCustomerData` 方法。该方法将 `Customer` 对象的属性设置为用户在表单上输入的值。

接下来，事件处理程序执行 `CustomerDB` 类的 `AddCustomer` 方法，并将由此返回的新客户 ID 赋值给 `Customer` 对象的 `CustomerID` 属性。然后，如果没有发生 SQL 错误，则将表单的 `DialogResult` 属性设置为 `DialogResult.OK`，这将导致表单关闭并将控制权交回客户维护表单。否则，将捕获异常并显示错误消息。

如果正在修改客户，事件处理程序首先创建一个 `Customer` 对象并将其存储在 `newCustomer` 变量中。然后，它将 `newCustomer` 的 `CustomerID` 属性设置为当前 ID。接下来，它调用 `CustomerDB` 类的 `UpdateCustomer` 方法并传递旧、新 `Customer` 对象。如果发生并发错误，将返回 false。在这种情况下，将显示错误消息并将表单的 `DialogResult` 属性设置为 `DialogResult.Retry`。否则，将 `newCustomer` 赋值给 `customer` 对象并将 `DialogResult` 设置为 `DialogResult.OK`。在任何情况下，表单都会关闭。

