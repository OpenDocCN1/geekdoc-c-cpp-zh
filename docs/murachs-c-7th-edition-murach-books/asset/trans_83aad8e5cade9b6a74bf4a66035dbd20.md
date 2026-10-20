

# ProductList 类的代码

```
public class ProductList : List<Product>
{
    // Modify the behavior of the Add method of the List<Product> class
    public new void Add(Product p) => base.Insert(0, p);

    // Provide two additional methods
    public void Fill()
    {
        List<Product> products = ProductDB.GetProducts();
        foreach (Product product in products)
            base.Add(product);
    }

    public void Save() => ProductDB.SaveProducts(this);
}
```

## 说明

- 此版本的 ProductList 类继承了 .NET 的 List<> 类。因此，它不需要定义 List<> 实例变量，因为该类本身就是一种 List<> 类。

# Product Maintenance 窗体的代码

图 14-11 展示了此版本 Product Maintenance 窗体的代码。你首先应注意 FillProductListBox() 方法的代码。你可能还记得，第 13 章的 Product Maintenance 窗体中，该方法的代码必须使用 for 循环配合 ProductList 类的索引器来处理产品列表。相比之下，由于本章的 ProductList 类继承了 List<Product> 类，因此可以使用 foreach 循环来处理产品列表。下一章你将更深入地了解支持以这种方式处理集合的特性。

在这个 foreach 循环中，你还可以看到多态性的作用。此处，将文本添加到列表框的 Items 集合中的语句会为每个产品调用 GetDisplayText() 方法。由于 GetDisplayText() 是一个虚方法，被 Book 和 Software 类都重写了，因此这段代码对 Book 对象调用 Book 类的 GetDisplayText() 方法，对 Software 对象调用 Software 类的 GetDisplayText() 方法。要确认这一点，可以回顾图 14-9 查看这两个方法之间的差别，也可以回顾图 14-8 查看最终显示结果之间的差别。

# Product Maintenance 窗体的代码

```
public partial class frmProductMain : Form
{
	public frmProductMain()
	{
		InitializeComponent();
	}

	private ProductList products = new ProductList();
	private void frmProductMain_Load(object sender, EventArgs e)
	{
		products.Fill();
		FillProductListBox();
	}

	private void FillProductListBox()
	{
		lstProducts.Items.Clear();
		foreach (Product p in products)
			lstProducts.Items.Add(p.GetDisplayText("\t"));
	}

	private void btnAdd_Click(object sender, EventArgs e)
	{
		frmNewProduct newForm = new frmNewProduct();
		Product product = newForm.GetNewProduct();
		if (product != null)
		{
			products.Add(product);
			products.Save();
			FillProductListBox();
		}
	}

	private void btnDelete_Click(object sender, EventArgs e)
	{
		int i = lstProducts.SelectedIndex;
		if (i != -1)
		{
			Product product = products[i];
			string message = "Are you sure you want to delete " + product.Description + "?";
			DialogResult button = MessageBox.Show(message, "Confirm Delete", MessageBoxButtons.YesNo);
			if (button == DialogResult.Yes)
			{
				products.Remove(product);
				products.Save();
				FillProductListBox();
			}
		}
	}

	private void btnExit_Click(object sender, EventArgs e)
	{
		this.Close();
	}
}
```

# New Product 窗体的代码

```
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

    private void rbBook_CheckedChanged(object sender, EventArgs e)
    {
        if (rbBook.Checked)
        {
            lblAuthorOrVersion.Text = "Author: ";
            txtAuthorOrVersion.Tag = "Author";
        }
        else
        {
            lblAuthorOrVersion.Text = "Version: ";
            txtAuthorOrVersion.Tag = "Version";
        }
        txtCode.Focus();
    }

    private void btnSave_Click(object sender, EventArgs e)
    {
        if (IsValidData())
        {
            if (rbBook.Checked)
                product = new Book(txtCode.Text, txtDescription.Text,
                    txtAuthorOrVersion.Text,
                    Convert.ToDecimal(txtPrice.Text));
            else
                product = new Software(txtCode.Text, txtDescription.Text,
                    txtAuthorOrVersion.Text,
                    Convert.ToDecimal(txtPrice.Text));
            this.Close();
        }
    }

    private bool IsValidData()
    {
        return Validator.IsPresent(txtCode) &&
            Validator.IsPresent(txtDescription) &&
            Validator.IsPresent(txtAuthorOrVersion) &&
            Validator.IsPresent(txtPrice) &&
            Validator.IsDecimal(txtPrice);
    }

    private void btnCancel_Click(object sender, EventArgs e)
    {
        this.Close();
    }
}
```

# 对象类型与类型转换

既然你已经学习了继承的基础知识，并看到了一个使用继承的应用程序示例，接下来可以学习一些在使用继承时经常需要的其他技巧，其中包括对象类型转换（casting）以及获取对象类型的信息。

## 如何使用 Type 类获取对象类型的信息

如你所知，System.Object 类包含一个 GetType() 方法，可用于获取表示 .NET 对象类型的 Type 对象。图 14-13 列出了 Type 类中一些可用于获取对象信息的成员。例如，可以使用 Name 属性获取类型的名称，如“Product”或“Book”；可以使用 Namespace 属性获取包含某个类型的命名空间的名称，如“ProductMaintenance”；还可以使用 FullName 属性获取类型的完全限定名称，如“ProductMaintenance.Book”。此外，还可以使用 BaseType 属性获取表示某个类型所继承的类的 Type 对象。

该图中的第一个示例展示了如何使用这些属性来显示对象的信息。此处，GetType() 方法用于获取通过 Product 类型变量访问的 Book 对象的信息。请注意，即使变量的类型是 Product，GetType() 方法返回的 Type 对象所表示的也是 Book 对象。

第二个示例展示了如何编写 if 语句来测试对象的类型。此处，我使用了 typeof 运算符来获取 Book 类的 Type 对象，然后将此 Type 对象与 Product 对象的 GetType() 方法返回的 Type 对象进行比较。

第三个示例展示了测试对象类型的另一种方法。此处，在调用 Product 对象的 GetType() 方法之后，我使用 Name 属性获取生成的 Type 对象的名称，然后将该名称与 Book 类的 nameof 运算符返回的名称进行比较。请注意，你也可以将 Product 对象的名称与字符串字面量进行比较，如下所示：

```
if (p.GetType().Name == "Book")
```

不过，使用 nameof 运算符的好处在于，编译器可以检查该类型是否有效。此外，如果你更改了类型名称，可以使用重构功能来更改所有出现的类型名称。

尽管此示例仅展示了如何使用 nameof 运算符获取类型的名称，但你应知道，还可以使用它获取任何变量或成员的名称。有关更多信息，请参阅 Visual Studio 中关于此运算符的文档。

请记住，从第 12 章可知，你还可以使用 C# 7.0 及更高版本的模式匹配来测试对象的类型。不过，如果需要获取某个类型的信息，你仍需使用 Type 类的成员，如图所示。

## Type 类

| 属性 | 说明 |
|---|---|
| Name | 返回包含类型名称的字符串。 |
| FullName | 返回包含类型的完全限定名称的字符串，其中包括命名空间名称和类型名称。 |
| BaseType | 返回表示某个类型所继承的类的 Type 对象。 |
| Namespace | 返回包含某个类型的命名空间名称的字符串。 |
| 方法 | 说明 |
| GetType() | 返回表示对象类型的 Type 对象。 |

## 使用 Type 类获取对象信息的代码

```
Product p;
p = new Book("C#", "Murach's C#", "Anne Boehm", 59.50m);
Type t = p.GetType();
Console.WriteLine("Name: " + t.Name);
Console.WriteLine("Namespace: " + t.Namespace);
Console.WriteLine("FullName: " + t.FullName);
Console.WriteLine("BaseType: " + t.BaseType.Name);
```

## 控制台上显示的结果

```
Name: Book
Namespace: ProductMaintenance
FullName: ProductMaintenance.Book
BaseType: Product
```

## 如何测试对象的类型

```
if (p.GetType() == typeof(Book))
```

## 测试对象类型的另一种方法

```
if (p.GetType().Name == nameof(Book))
```

## 说明

- 每个对象都有一个 GetType() 方法，该方法返回与对象类型对应的 Type 对象。
- 可以使用 Type 类的属性获取任何对象类型的信息，例如类型的名称及其基类的名称。
- 上面显示的属性和方法只是 Type 类的 90 多个属性和方法中的一部分。
- 测试对象类型最简单的方法是将对象的 GetType() 方法返回的 Type 对象与某个类型的 typeof 运算符返回的 Type 对象进行比较。
- 测试对象类型的另一种方法是将对象类型的名称与某个类型的 nameof 运算符返回的名称进行比较。nameof 运算符从 C# 6.0 开始可用。

