

# 产品维护应用程序的代码

图 12-14 到 12-16 显示了产品维护表单、新产品表单以及 Validator 类的代码。由于你已经在图 12-3 中见过 Product 类的代码，我将不再重复它。此外，由于你不需要了解 ProductDB 类的实现就能理解此应用程序的工作原理，我也不会展示该类的代码。如果你感兴趣，可以在第 21 章和第 22 章找到该类的三种不同实现。

图 12-14 显示的产品维护表单代码首先声明了一个类型为 `List<>` 的类变量名为 products。接下来，在表单的 `Load` 事件处理器中，调用了 `ProductsDB` 类的 `GetProducts` 方法，用从 Products 文件中的数据中创建的 Product 对象填充此列表。然后，调用 `FillProductListBox` 方法。该方法使用 `foreach` 循环将每个产品 `GetDisplayText` 方法返回的字符串添加到列表框中。注意传递给该方法的是一个制表符，以便产品如图 12-12 所示显示。

如果用户点击 Add（添加）按钮，将创建一个新产品表单实例，并调用该表单的 `NewProduct` 方法。如果此方法返回的 Product 对象不为空，则将该产品添加到 products 列表中。然后，调用 `ProductDB` 类的 `SaveProducts` 方法来更新文件，并调用 `FillProductListBox` 方法刷新列表框以便创建新产品。

如果用户在列表中选择一个产品并点击 Delete（删除）按钮，将显示一个确认对话框。然后，如果用户确认删除，该产品将从列表中移除，更新 Products 文件，并刷新列表框。

新产品表单的代码在图 12-14 所示。它声明了一个名为 product 的私有 Product 对象。然后，从产品维护表单调用的 `NewProduct` 方法开始以对话框的形式显示新产品表单。如果用户点击此对话框中的 Save（保存）按钮，将调用 `IsValidData` 方法来验证数据。该方法会对表单上的每个文本框调用 `Validator` 类的 `IsPresent` 方法。此外，它还会价格框文本调用 `IsDecimal` 方法。

如果所有值都有效，则将根据用户输入的值创建一个 New 对象，关闭对话框，并将 Product 对象返回给产品维护表单。相比之下，如果用户点击 Cancel（取消）按钮，对话框关闭，并将初始化为 null 的 product 变量返回给产品维护表单。

图 12-16 显示的 Validator 类的代码不应该让你意外。事实上，你已经在图 12-10 中见过与此代码类似的代码。唯一的区别是这个版本的 Validator 类包含一个 `IsDecimal` 方法以及一个 `IsPresent` 方法。注意，产品维护应用程序没有使用 `IsInt32` 或 `IsWithinRange` 方法，因此我在该图中省略了这些方法。

# 产品维护表单的代码

```csharp
public partial class frmProductMain : Form
{
    public frmProductMain()
    {
        InitializeComponent();
    }
    private List<Product> products = null;
    private void frmProductMain_Load(object sender, System.EventArgs e)
    {
        products = ProductDB.GetProducts();
        FillProductListBox();
    }
    private void FillProductListBox()
    {
        lstProducts.Items.Clear();
        foreach (Product p in products)
        {
            lstProducts.Items.Add(p.GetDisplayText("\t"));
        }
    }
    private void btnAdd_Click(object sender, System.EventArgs e)
    {
        frmNewProduct frmProduct = new frmNewProduct();
        Product product = frmProduct.GetNewProduct();
        if (product != null)
        {
            products.Add(product);
            ProductDB.SaveProducts(products);
            FillProductListBox();
        }
    }
    private void btnDelete_Click(object sender, System.EventArgs e)
    {
        int i = lstProducts.SelectedIndex;
        if (i != -1)
        {
            Product product = products[i];
            string message = "Are you sure you want to delete " + product.Description + " ?";
            DialogResult result = MessageBox.Show(message);
            if (result == DialogResult.Yes)
            {
                products.Remove(product);
                ProductDB.SaveProducts(products);
                FillProductListBox();
            }
        }
    }
}
```
图 12-14 产品维护表单的代码

# 新产品表单的代码

```csharp
public partial class frmNewProduct : Form
{
    public frmNewProduct()
    {
        InitializeComponent();
    }
    private Product product = null;
    public Product GetNewProduct()
    {
        this.ShowDialog();
        return product;
    }
    private void btnSave_Click(object sender, System.EventArgs e)
    {
        if (IsValidData())
        {
            product = new Product(txtCode.Text, txtDescription.Text, decimal.Parse(txtPrice.Text));
            this.Close();
        }
    }
    private bool IsValidData()
    {
        return Validator.IsPresent(txtCode) && 
               Validator.IsPresent(txtDescription) && 
               Validator.IsDecimal(txtPrice);
    }
    private void btnCancel_Click(object sender, System.EventArgs e)
    {
        this.Close();
    }
}
```
图 12-15 新产品表单的代码

# Validator 类的代码

```csharp
public static class Validator
{
    private static string title = "Entry Error";
    public static string Title {
        get {
            return title;
        }
        set {
            title = value;
        }
    }
    public static bool IsPresent(TextBox textBox)
    {
        if (string.IsNullOrEmpty(textBox.Text))
        {
            MessageBox.Show(textBox.Tag + " is a required field.", Title);
            textBox.Focus();
            return false;
        }
        return true;
    }
    public static bool IsDecimal(TextBox textBox)
    {
        try {
            decimal.Parse(textBox.Text);
            return true;
        } catch (FormatException) {
            MessageBox.Show(textBox.Tag + " must be a decimal number.", Title);
            textBox.Focus();
            return false;
        }
    }
}
```

# 注意

- IsInt32 和 IsWithinRange 方法的代码没有在此显示，因为这些方法没有被产品维护应用程序使用。

# 使用类视图和类图

现在你已经看到了一个使用类的完整应用程序，准备好学习如何使用类视图和类图了。虽然你可以不使用这些功能来创建应用程序，但它们通常能让你更容易可视化并处理项目中的类。

# 使用类视图窗口

类视图窗口是一个与解决方案资源管理器窗口一起显示的选项页窗口。如图 12-17 所示，此窗口包含解决方案中类的分级查看器，以及每个类的成员。简而言之，类视图提供了应用程序结构的整体视图。

此图中的解决方案是图 12-12 到 12-16 所示的产品维护应用程序。在这里，我展开了类视图窗口上方格中的项目，并点击了 Product 类以便在下方格中显示其成员。正如你所见，该类的成员包括 GetDisplayText 方法的两个签名；两个构造函数；Code、Description 和 Price 属性；以及名为 code、description 和 price 的私有字段。图标上的锁表示这些字段无法从类外部访问。

你还可以使用类视图窗口在代码编辑器中显示任何成员的代码。要这样做，只需双击类视图窗口下方格中的成员即可。例如，在此图中，你可以看到当我双击 Price 属性时显示的代码。

