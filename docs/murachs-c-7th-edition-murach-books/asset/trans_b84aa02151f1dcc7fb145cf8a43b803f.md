

# 客户维护表单

![](img/844f608d10a44654833ea5efc8a2e7a7_691_0.png)

# 添加/修改客户表单

![](img/844f608d10a44654833ea5efc8a2e7a7_691_1.png)

# 显示以确认删除操作的对话框

![](img/844f608d10a44654833ea5efc8a2e7a7_691_2.png)

# 描述

- 要添加新客户，用户在客户维护表单上单击添加按钮以显示空白的添加客户表单。然后，用户输入新客户的数据并单击接受按钮返回客户维护表单。
- 要修改现有客户的数据，用户输入客户 ID 并单击获取客户按钮以显示该客户的信息。然后，用户单击修改按钮以显示修改客户表单，进行适当的修改，并单击接受按钮返回客户维护表单。
- 要删除现有客户，用户输入客户 ID 并单击获取客户按钮以显示该客户的信息。然后，用户单击删除按钮并响应显示以确认删除操作的对话框。

图 20-17 客户维护应用程序的用户界面

# 客户维护表单的代码

图 20-18 显示了客户维护表单的代码。在默认构造函数之后（此处未显示），它声明了两个类变量。第一个存储表单使用的 DB 上下文对象的实例，第二个存储当前在表单上显示的客户。

由于此表单不包含 Load 事件处理程序，因此在表单首次加载时不会显示任何数据。然后，用户可以输入客户 ID 并单击获取客户按钮以检索客户的数据，或单击添加按钮以添加新客户。

获取客户按钮的 Click 事件处理程序首先调用 IsValidData() 方法。该方法反过来调用名为 Validator 的类中的 IsInt32() 方法，以检查用户是否对客户 ID 输入了整数。该类包含与第 12 章中的 Validator 类中类似的方法。

如果客户 ID 为整数，则使用它从数据库中获取用户输入的 ID 的客户。为此，代码调用 Customers 实体集合的 Find() 方法。如果找到指定 ID 的客户，此方法将返回一个 Customers 对象。否则，它将返回 null。

调用 Find() 方法的语句在 try-catch 语句中编码。这是因为如果 DB 上下文不再可用或找不到数据库，Find() 方法将抛出异常。因此，此事件处理程序应捕获该异常。为处理此异常，catch 块将 Exception 对象传递给本代码列表第 4 页所示的 HandleGeneralError() 方法。

在执行 Find() 方法后，事件处理程序检查 Customers 对象是否包含 null 值。如果包含，则显示一条消息，指出未找到客户，并调用名为 ClearControls() 的方法。此方法在第 2 页介绍，它清除表单控件上的数据并将焦点移至客户 ID 文本框，以便用户可以输入另一个 ID。

如果 Customers 对象包含值，事件处理程序将检查该客户的 States 对象是否已加载。如果已加载，则表示同一州的另一个客户的数据已显示。如果未加载，则调用 Load() 方法将其加载。

最后，事件处理程序调用 DisplayCustomer() 方法。此方法在第 2 页介绍，它在表单上显示从数据库检索到的数据。

# 客户维护表单的代码
第 1 页

```csharp
public partial class frmCustomerMaintenance : Form
{
    // default constructor
    private MMABooksContext context = new MMABooksContext();
    private Customers selectedCustomer;
    private void btnGetCustomer_Click(object sender, EventArgs e)
    {
        if (IsValidData())
        {
            int customerID = Convert.ToInt32(txtCustomerID.Text);
            try
            {
                selectedCustomer = context.Customers.Find(customerID);
                if (selectedCustomer == null)
                {
                    MessageBox.Show("No customer found with this ID. " +
                        "Please try again.", "Customer Not Found");
                    this.ClearControls();
                }
                else
                {
                    if (!context.Entry(selectedCustomer)
                        .Reference("StateNavigation").IsLoaded)
                    {
                        context.Entry(selectedCustomer)
                            .Reference("StateNavigation").Load();
                    }
                    this.DisplayCustomer();
                }
            }
            catch (Exception ex)
            {
                this.HandleGeneralError(ex);
            }
        }
    }
    private bool IsValidData()
    {
        bool success = true;
        string errorMessage = "";
        errorMessage = Validator.IsInt32(txtCustomerID.Text,
            txtCustomerID.Tag.ToString());
        if (errorMessage != "")
        {
            success = false;
            MessageBox.Show(errorMessage, "Entry Error");
            txtCustomerID.Focus();
        }
        return success;
    }
}
```

图 20-18 客户维护表单的代码（第 1 部分，共 4 部分）

图 20-18 第 2 页顶部的 DisplayCustomer() 方法将 selectedCustomer 对象的相应属性分配给文本框的 Text 属性。对于州文本框，值是从 selectedCustomer 对象的导航属性使用相关的 States 对象检索的。这就是为什么必须加载客户的 States 对象。并且，这就是表单能够显示州名而不是州代码的方式。最后，该方法启用修改和删除按钮，以便用户可以选择更新或删除所选客户。

ClearControls() 方法将空字符串分配给表单上的文本框并禁用修改和删除按钮。最后，它将焦点移至客户 ID 文本框，以便用户可以输入另一个 ID。

添加按钮的 Click 事件处理程序将添加/修改客户表单作为对话框显示。但首先，它创建该表单的一个实例并将其公共 AddCustomer 属性设置为 true。这样，表单就知道正在添加新客户。并且，它将 States 对象的集合分配给表单的公共 States 属性。为此，它使用 DB 上下文的 States 集合并按名称对州进行排序。

如果客户成功添加，则从添加/修改客户表单的 Customer 属性中检索新客户。然后，在 try 子句内，调用 DB 上下文的 Add() 方法将该 Customers 对象添加到 Customers 集合中。接下来，执行 SaveChanges() 方法将客户添加到数据库。

在 try 子句之后，catch 子句处理可能抛出的异常。如果抛出 DbUpdateException，则将其传递给名为 HandleDataError() 的方法。如果抛出任何其他异常，则将其传递给名为 HandleGeneralError() 的方法。这两种方法均在代码列表第 4 页介绍。为了使这些 catch 子句正常工作，DbUpdateException 对象的子句必须首先编码。这是因为 DbUpdateException 对象比 Exception 对象更具体。

# 客户维护表单的代码
# 第 2 页

```csharp
private void DisplayCustomer()
{
    txtCustomerID.Text = selectedCustomer.CustomerId.ToString();
    txtName.Text = selectedCustomer.Name;
    txtAddress.Text = selectedCustomer.Address;
    txtCity.Text = selectedCustomer.City;
    txtState.Text = selectedCustomer.StateNavigation.StateName;
    txtZipCode.Text = selectedCustomer.ZipCode;
    btnModify.Enabled = true;
    btnDelete.Enabled = true;
}

private void ClearControls()
{
    txtCustomerID.Text = "";
    txtName.Text = "";
    txtAddress.Text = "";
    txtCity.Text = "";
    txtState.Text = "";
    txtZipCode.Text = "";
    btnModify.Enabled = false;
    btnDelete.Enabled = false;
    txtCustomerID.Focus();
}

private void btnAdd_Click(object sender, EventArgs e)
{
    var addModifyForm = new frmAddModifyCustomer {
        AddCustomer = true,
        States = context.States.OrderBy(s => s.StateName).ToList()
    };
    DialogResult result = addModifyForm.ShowDialog();

    if (result == DialogResult.OK)
    {
        selectedCustomer = addModifyForm.Customer;
        try
        {
            context.Customers.Add(selectedCustomer);
            context.SaveChanges();
            this.DisplayCustomer();
        }
        catch (DbUpdateException ex)
        {
            this.HandleDataError(ex);
        }
        catch (Exception ex)
        {
            this.HandleGeneralError(ex);
        }
    }
}
```

