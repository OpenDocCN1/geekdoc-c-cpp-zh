
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

## 注意

- `IsInt32` 和 `IsWithinRange` 方法的代码没有在此显示，因为这些方法没有被产品维护应用程序使用。

# 使用类视图和类图

现在你已经看到了一个使用类的完整应用程序，准备好学习如何使用类视图和类图了。虽然你可以不使用这些功能来创建应用程序，但它们通常能让你更容易可视化并处理项目中的类。

## 使用类视图窗口

类视图窗口是一个与解决方案资源管理器窗口一起显示的选项页窗口。如图 12-17 所示，此窗口包含解决方案中类的分级查看器，以及每个类的成员。简而言之，类视图提供了应用程序结构的整体视图。

此图中的解决方案是图 12-12 到 12-16 所示的产品维护应用程序。在这里，我展开了类视图窗口上方格中的项目，并点击了 `Product` 类以便在下方格中显示其成员。正如你所见，该类的成员包括 `GetDisplayText` 方法的两个签名；两个构造函数；`Code`、`Description` 和 `Price` 属性；以及名为 `code`、`description` 和 `price` 的私有字段。图标上的锁表示这些字段无法从类外部访问。

你还可以使用类视图窗口在代码编辑器中显示任何成员的代码。要这样做，只需双击类视图窗口下方格中的成员即可。例如，在此图中，你可以看到当我双击 `Price` 属性时显示的代码。

### 类视图窗口

![](img/3148667e42d4db35b3d08576aaa1fa01_404_0.png)

#### 描述

- 类视图窗口允许你浏览解决方案中的类。
- 在顶部窗格中，类视图窗口显示项目的类。在底部窗格中，类视图窗口显示选中类的成员，包括属性、方法、事件和字段。
- 要显示类视图，点击与解决方案资源管理器（Solution Explorer）分组的类视图选项卡，或使用“视图->类视图”命令。
- 要显示项目的类，请展开顶部窗格中的项目。
- 要在此下方窗格中显示类的成员，请点击顶部窗格中的该类。
- 要在此代码编辑器中显示成员的 C# 代码，请双击类视图窗口中的该成员。

图 12-17 如何使用类视图窗口

## 如何使用类图和类详细窗口

12–18 显示了一个类图，其中包含了“产品维护”`Product Maintenance`应用程序中的两个类。在这里，你可以看到组成这些类的成员。例如，`Product` 类的成员包括名为 `code`、`description` 和 `price` 的私有字段；`Code`、`Description` 和 `Price` 属性；重载的 `GetDisplayText` 方法以及重载的 `Product` 构造函数。在这里，私有字段图标上的锁表示这些字段无法从类外部访问。此外，`Validator` 类周围的虚线表示这是一个静态类。

你可以通过在解决方案资源管理器中右键点击项目名称，并在弹出的菜单中选择“类图”命令来创建这样的类图。这将创建一个包含项目中每个类的类图。然后，你可以通过点击类并按 `Delete` 键从图中删除任何类。你还可以通过从解决方案资源管理器将其拖到图中来添加新类。

创建类图的另一种方法是在解决方案资源管理器中右键点击一个类并选择“查看类图”命令。这将创建一个只包含一个类的类图。然后，你可以通过从解决方案资源管理器拖入其他类来图中图中。

在创建类图后，你可以使用类工具栏来调整图表。例如，你可以点击 `a:T` 按钮显示类中每个成员的名称和类型，可以点击 `( )` 按钮显示每个成员的名称、类型和签名。

当你选择类图中的一个类时，可以使用位于图下方的类详细窗口（Class Details window）查看该类成员或该类中选中成员的详细信息。例如，图中类图中选中了 `Code` 属性，因此它在类详细窗口中也被高亮显示。

要导航到选中类的任何成员的代码，请在类图或类详细窗口中双击该成员的图标。然后，Visual Studio 将代码编辑器中打开该类（如果尚未打开）并跳转到所选成员的代码。

要为新属性、方法、字段和事件生成初始代码，请点击类详细窗口中的相应行或按钮。例如，你可以点击类详细窗口中的 `<add property>` 行或“新属性”`New Property`按钮来开始创建一个新属性。然后，你在“修改”`modify`行中输入名称和类型。要跳转到代码编辑器以完成属性的代码编写，请双击该行的图标。像这样使用类详细窗口是开发类中所有成员初始代码的快速方法。

最后，要从类中删除成员，可以在类图或类详细窗口中选中该成员时按 `Delete` 键。这不仅会从类图和类详细窗口中删除该成员，还会删除代码编辑器中该成员的代码。

# 第 12 章 如何创建和使用类

## 类图显示项目中的两个类

![](img/3148667e42d4db35b3d08576aaa1fa01_406_0.png)

### 描述

- 类图是一个或多个类的方法、属性、字段和事件的视觉表示。要创建类图，请右键点击项目。

### Express 版限制

- 类图是一个或多个类的方法、属性、字段和事件的视觉表示。要创建类图，请右键点击项目。
