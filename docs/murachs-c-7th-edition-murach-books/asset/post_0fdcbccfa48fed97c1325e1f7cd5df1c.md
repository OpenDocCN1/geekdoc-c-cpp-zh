
## The code for the Product Maintenance form

```csharp
public partial class frmProductMain : Form
{
    public frmProductMain()
    {
        InitializeComponent();
    }

    private List<Product> products = null;

    private void frmProductMain_Load(object sender, EventArgs e)
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

    private void btnAdd_Click(object sender, EventArgs e)
    {
        frmNewProduct newProductForm = new frmNewProduct();
        Product product = newProductForm.GetNewProduct();
        if (product != null)
        {
            products.Add(product);
            ProductDB.SaveProducts(products);
            FillProductListBox();
        }
    }

    private void btnDelete_Click(object sender, EventArgs e)
    {
        int i = lstProducts.SelectedIndex;
        if (i != -1)
        {
            Product product = products[i];
            string message = "Are you sure you want to delete "
                + product.Description + "?";
            DialogResult button =
                MessageBox.Show(message, "Confirm Delete",
                MessageBoxButtons.YesNo);
            if (button == DialogResult.Yes)
            {
                products.Remove(product);
                ProductDB.SaveProducts(products);
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

Figure 12-13  The code for the Product Maintenance form

## The code for the Validator class

```csharp
public static class Validator
{
    private static string lineEnd = "\n";

    public static string LineEnd
    {
        get
        {
            return lineEnd;
        }
        set
        {
            lineEnd = value;
        }
    }

    public static string IsPresent(string value, string name)
    {
        string msg = "";
        if (value == "")
        {
            msg += name + " is a required field." + LineEnd;
        }
        return msg;
    }

    public static string IsDecimal(string value, string name)
    {
        string msg = "";
        if (!Decimal.TryParse(value, out _))
        {
            msg += name + " must be a valid decimal value." + LineEnd;
        }
        return msg;
    }
}
```

### Note

- The code for the IsInt32() and IsWithinRange() methods isn’t shown here because these methods aren’t used by the Product Maintenance application.

## More skills for creating a class

In addition to the skills you’ve already learned in this chapter for creating classes, the topics that follow present some additional skills that you should know about.

### How to code auto-implemented properties

If you look back at the Code property in figure 12-7, you’ll see that the get and set accessors simply return the value of an instance variable and assign the value parameter to the instance variable. When that’s the case, you can code the property as an auto-implemented property as shown in figure 12-16. Auto-implemented properties provide a shorthand for coding simple properties. The auto-implemented property in the first example in this figure, for example, is equivalent to the Code property shown in figure 12-7.

When you use an auto-implemented property, you should know that the compiler creates a private instance variable for you. Because of that, this property is only accessible through the get and set accessors. You should also know that you can create a read-only auto-implemented property by omitting the set keyword as shown in the second example in this figure. However, you can’t create write-only auto-implemented properties.

The second example also shows that you can assign an initial value to an auto-implemented property. That’s particularly useful for a read-only property, since its value can’t be set in any other way.

The third and fourth examples in this figure show statements that set and get the value of the auto-implemented property in the first example. If you compare these statements with the statements in figure 12-7 that set and get the value of a property, you’ll see that they’re identical.

Note that if you want to convert a property that doesn’t use auto-implemented properties to one that does, you can use refactoring to do that. Just place the cursor anywhere in the property, press Ctrl + period (.), and select Use Auto Property from the Quick Actions menu that appears. Note that this deletes the private instance variable that’s associated with the property. In addition, if a value is assigned to the instance variable, that value is assigned to the property.

With C# 9.0 and later, you can use the init keyword instead of the set keyword to create an init-only setter. In this figure, the fifth example shows how to create an init-only setter for the Code property. When you use this type of setter, you can only assign a value to the property when the object is being initialized by a constructor or an object initializer. In this figure, the sixth example shows how to use an object initializer to set the value of the Code property. However, you could also use a constructor like the one shown in figure 12-4.

### The syntax for coding an auto-implemented property

```csharp
public type PropertyName { get; [set;] } [= value]
```

### An auto-implemented property with both get and set accessors

```csharp
public string Code { get; set; }
```

### An auto-implemented property with a get accessor and an initial value

```csharp
public string Code { get; } = "C#";
```

### A statement that sets the value of an auto-implemented property

```csharp
product.Code = txtProductCode.Text;
```

### A statement that gets the value of an auto-implemented property

```csharp
string code = product.Code;
```

### An auto-implemented property with an init-only setter (C# 9.0 and later)

```csharp
public string Code { get; init; }
```

### A statement that uses an object-initializer to set the init-only property

```csharp
var product2 = new Product { Code = "C#" };
```

### Description

- If the get accessor for a property simply returns the value of its instance variable and the set accessor simply assigns a value to its instance variable, you can create an *auto-implemented property*. Auto-implemented properties were introduced with C# 6.0.
- When you create an auto-implemented property, a corresponding private instance variable is created automatically, and that variable is only accessible through the property.
- An auto-implemented property can consist of both the get and set keywords or just a get keyword.
- You can initialize the value of the private instance variable for an auto-implemented property by coding an equals sign and the value following the closing brace for the property.
- You can use refactoring to convert a standard property to an auto-implemented property.
- With C# 9.0 and later, you can use the init keyword instead of the set keyword to create an init-only setter. Then, you can only set the value of the property when the object is being initialized by a constructor or by an object initializer as described in figure 12-4.

### A read-only property

```csharp
public decimal DiscountAmount
{
    get
    {
        return subtotal * discountPercent;
    }
}
```

### The same property using an expression body

```csharp
public decimal DiscountAmount => subtotal * discountPercent;
```

### A read/write property for a private instance variable

```csharp
public string Code
{
    get
    {
        return code;
    }
    set
    {
        code = value;
    }
}
```

### The same property using expression-bodied get and set accessors

```csharp
public string Code
{
    get => code;
    set => code = value;
}
```

### Description

- If a property is read-only and simply returns the value of an expression, you can code it as an expression-bodied property. Expression-bodied properties were introduced with C# 6.0.
- To code an expression-bodied property, you code the access modifier, return type, and property name, followed by the lambda operator (=>) and the expression to be returned.
- If the get accessor for a property simply returns an expression and the set accessor executes a single statement, the accessors can be coded as expression-bodied accessors. Expression-bodied get and set accessors were introduced with C# 7.0.
- To code an expression-bodied get accessor, you code the get keyword, followed by the lambda operator and the expression to be returned.
- To code an expression-bodied set accessor, you code the set keyword, followed by the lambda operator and the statement to be executed.
- You can use refactoring to convert read-only properties and get and set accessors that use code blocks to properties and accessors that use expression bodies.

Figure 12-17  How to code expression-bodied properties and accessors
