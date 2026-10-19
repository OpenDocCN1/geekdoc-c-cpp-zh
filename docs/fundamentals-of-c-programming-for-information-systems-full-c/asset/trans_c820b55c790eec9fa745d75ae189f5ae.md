

## KeyValuePair 集合

字典（Dictionary）中的每一项都属于 KeyValuePair 类型，并且是 KeyValuePair 集合的成员。KeyValuePair 由一个键和一个值组成。图 9-17 显示了使用 foreach 循环遍历 KeyValuePair 集合来显示每个键和值的代码。

图 9-17：使用 KeyValuePair 保存字典中的每一项

```
53
54    private void btnDisplayAll_Click(object sender, EventArgs e)
55    {
56        string fmtStr = "{0,-10}{1,8:C}";
57        lstDisplay.Items.Add(string.Format(fmtStr, "Product#", "Price"));
58
59        foreach (KeyValuePair<string, float> kvp in prices)
60        {
61            lstDisplay.Items.Add(string.Format(fmtStr, kvp.Key, kvp.Value));
62        }
63    }
```

### 第 59 行：foreach (KeyValuePair<string, float> kvp in prices)

字典中的每一项都属于 KeyValuePair 类型。第 59 行将变量 kvp 声明为 KeyValuePair 类型，其中键为 string 类型，值为 float 类型。foreach 循环从 prices 中逐个获取每个 KeyValuePair 并将其赋给变量 kvp。

### 第 61 行：lstDisplay.Items.Add(string.Format(fmtStr, kvp.Key, kvp.Value));

KeyValuePair 类型变量 kvp 的 Key 和 Value 属性用于在 ListBox 中显示键和值，如下所示：

| 产品编号 | 价格 |
| "1033" | $89.95 |
| "1009" | $21.50 |
| "1014" | $159.00 |
| "1005" | $2.50 |
| "1001" | $55.70 |
| "1025" | $33.45 |

步骤 2-7：将图 9-17 中第 59–62 行的代码添加到 btnDisplayAll 的 Click 事件处理程序中。运行窗体并测试代码。

## Keys 集合与 Values 集合

Keys 集合是字典中所有项的键的集合。类似地，还有一个单独的 Values 集合，它是所有项的值的集合。图 9-18 显示了字典中两个集合的前几项。

### 图 9-18：Keys 集合和 Values 集合

| Keys 集合 | Values 集合 |
|---|---|
| "1033" | 89.95 |
| "1009" | 21.50 |
| "1014" | 159.00 |
| "1005" | 2.5 |

你可以使用 foreach 循环直接访问每一项中的键或值，而不必使用 KeyValuePair 来访问整个项。图 9-19 显示了使用 foreach 循环从 Values 集合中访问每个价格并计算平均价格的代码。

### 图 9-19：使用 Values 集合访问每个价格并计算平均价格

```
64
65 private void btnAvgPrice_Click(object sender, EventArgs e)
66 {
67     float totalPrice = 0;
68     foreach (float price in prices.Values)
69         totalPrice += price;
70
71     float avgPrice = totalPrice / prices.Count;
72     lstDisplay.Items.Add("Average Price: " + avgPrice.ToString("c2"));
73 }
```

### 第 68 行：foreach (float price in prices.Values)

totalPrice += price;

从 Values 集合中逐个获取价格，并计算总和。

### 步骤 2-8：将图 9-19 中第 68–71 行的代码添加到 btnAvgPrice 的 Click 事件处理程序中。运行窗体并测试代码。

你可以使用同样的方法从 Keys 集合中访问每个键。

以下是使用字典（Dictionary）的完整代码，其中产品编号为键，价格为值。

```
private Dictionary<string, float> prices = new Dictionary<string, float>();

private void DictionaryValueType_Load(object sender, EventArgs e)
{
    string currentline;
    string[] fields = new string[2];
    //Create StreamReader
    StreamReader PriceReader = new StreamReader("Price.txt");

    //Read each line from the file, split and store in an array.
    while (PriceReader.EndOfStream == false)
    {
        currentline = PriceReader.ReadLine(); // Read product# & price
        fields = currentline.Split(',');
        // Add the key (Prod#) and value (price) to the Dictionary:
        prices.Add(fields[0], float.Parse(fields[1]));
        cboProdNumber.Items.Add(fields[0]); // Add product# to ComboBox
    }
    PriceReader.Close();
}

private void cboProdNumber_SelectedIndexChanged(object sender, EventArgs e)
{
    string fmtStr = "{0,-10}{1,8:C}";
    lstDisplay.Items.Clear();
    lstDisplay.Items.Add(string.Format(fmtStr, "Product#", "Price"));

    string selectedProduct = cboProdNumber.SelectedItem.ToString();
    // Use the key (Product#) to get the value (price).
    float price = prices[selectedProduct];
    lstDisplay.Items.Add(string.Format(fmtStr, selectedProduct, price));
}

private void btnDisplayAll_Click(object sender, EventArgs e)
{
    string fmtStr = "{0,-10}{1,8:C}";
    lstDisplay.Items.Add(string.Format(fmtStr, "Product#", "Price"));

    foreach (KeyValuePair<string, float> kvp in prices)
    {
        lstDisplay.Items.Add(string.Format(fmtStr, kvp.Key, kvp.Value));
    }
}

private void btnAvgPrice_Click(object sender, EventArgs e)
{
    float totalPrice = 0;
    foreach (float price in prices.Values)
        totalPrice += price;

    float avgPrice = totalPrice / prices.Count;
    lstDisplay.Items.Add("Average Price: " + avgPrice.ToString("C2"));
}
```

现在开始练习！完成练习 9.2。

## 以数组作为值的 Dictionary

接下来，我们看一个以数组作为值的 Dictionary 示例。

## 教程 3：以 Product# 作为键、以销售数组作为值的 Dictionary

在此应用程序中，你将一个 string 类型的产品编号作为键，并将包含四个季度销售额的数组作为值存储在 Dictionary 中。产品编号及对应的季度销售额从图 9-20 所示的 Sales.txt 文件中读取，并存储在 Dictionary `sales<string, Array>` 中。

图 9-20：Sales.txt 文件

1033, 16, 32, 23, 40
1009, 144, 182, 169, 205
1014, 54, 49, 72, 63
1005, 38, 62, 55, 77
1001, 7, 9, 8, 15
1025, 98, 110, 105, 130

图 9-21 显示了包含产品编号和销售额的 Dictionary。

图 9-21：sales Dictionary<string, array> 的键和值示例数据

| 键 | 值 |  |  |  |
|---|---|---|---|---|
| 1033 | 16 | 32 | 23 | 40 |
| 1009 | 144 | 182 | 169 | 205 |
| 1014 | 54 | 49 | 72 | 63 |
| 1005 | 38 | 62 | 55 | 77 |
| 1001 | 7 | 9 | 8 | 15 |
| 1025 | 98 | 110 | 105 | 130 |

从 ComboBox 中选择产品编号，然后在 ListBox 中显示总销售额，如图 9-22 所示。

图 9-25 显示了通过使用产品编号作为键来查找所选产品编号的季度销售额的代码。

### 图 9-25：查找产品销售数据的代码

```
45
46 private void cboProdNumber_SelectedIndexChanged(object sender, EventArgs e)
47 {
48     string fmtStr = "{0,-10}{1,8}";
49     lstDisplay.Items.Clear();
50     lstDisplay.Items.Add(string.Format(fmtStr, "Product#", "Annual Sales"));
51
52     string selectedProduct = cboProdNumber.SelectedItem.ToString();
53     // Use the key (Product#) to get the value (quarterly sales array).
54     string[] salesArray = sales[selectedProduct];
55
56     int annualSales = 0;
57     foreach (string qtrSale in salesArray)
58         annualSales = annualSales + int.Parse(qtrSale);
59     // Or, you may use a for loop:
60     //for (int quarter = 0; quarter <= 3; quarter++)
61     //    annualSales = annualSales + int.Parse(salesArray[quarter]);
62     lstDisplay.Items.Add(string.Format(fmtStr, selectedProduct, annualSales));
63 }
```

第 54 行：`sales[selectedProduct]` 使用 selectedProduct 作为键来获取值，该值是一个数组。返回的数组存储在 salesArray 中。

第 57-58 行使用 foreach 循环将 salesArray 的所有四个元素相加。

步骤 3-5：将图 9-25 中第 54-58 行的代码添加到 ComboBox 的 SelectedIndexChanged 事件中，以查找所选产品编号的销售额。运行窗体并测试代码。

现在开始练习！完成练习 9.3。

## 复习题

9.5 Dictionary 与 List 有何不同？

## 练习

图 9-26 显示了存储在 Ch9_Collections 项目目录 Debug 文件夹中的 Vendor.txt 文件的数据。

### 图 9-26：Vendor.txt 文件（vendor#、名称、街道、城市、州、邮政编码、电话）

1,FCC,445 12th Street SW, Washington,DC,20554,888-225-5322
2,U.S.Copyright Office,101 Independence Ave, Washington,DC,20559,202-707-3000
3,CDC,1600 Clifton Road,Atlanta,GA,30333,800-232-4636
4,White House, 1600 Pennsylvania Avenue NW, Washington,DC,20500,202-456-1111
5,Labor Statistics,Postal Sq Bldg,2 Mass Ave,Washington,DC,20212,800-877-8339
6,AMTRAK,60 Massachusetts Avenue NE, Washington,DC,20002,800-523-6590
7,U.S. Air Force,1690 Air Force Pentagon,Washington,DC,20330-1670,800-423-8723
8,National Guard,111 South George Mason Dr,Arlington,VA,22204,800-864-6264
9,Office of Govt Ethics,1201 New York Ave,Washington,DC,20005,202-482-9300
10,IRS,1111 Constitution Ave NW, Washington, DC,20224,800-829-1040

### 练习 9-1：List

创建一个名为 VendorsList 的窗体，使用户能够查找并显示任何指定供应商的邮政编码和电话号码，如下所示：

从 Vendor.txt（图 9-26）读取供应商记录，并将其加载到名为 vendors 的数组列表（List of arrays）中，同时将供应商名称添加到已排序的 ComboBox 中。

当用户从 ComboBox 中选择供应商名称时，在 ListBox 中查找并显示该名称及对应的邮政编码和电话号码。

### 练习 9-2：Dictionary

创建一个名为 VendorsDictionary1 的窗体，使用户能够查找并显示任何指定供应商的电话号码，如下所示：

从 Vendor.txt 文件（图 9-26）中读取每条供应商记录。将名称作为键，电话号码作为值添加到名为 vendorPhones 的 Dictionary 中。将名称添加到已排序的 ComboBox 中。

当用户从 ComboBox 中选择供应商名称时，在 ListBox 中查找并显示该名称及对应的电话号码。

### 练习 9-3：Dictionary

创建一个名为 VendorsDictionary2 的窗体，使用户能够查找并显示任何指定供应商的邮政编码和电话号码，如下所示：

从 Vendor.txt 文件（图 9-26）中读取每条供应商记录，将其拆分并存储到数组中。将邮政编码和电话号码复制到另一个数组（可以使用 Array.Copy）。将名称作为键，将包含邮政编码和电话号码的数组作为值添加到名为 vendors 的 Dictionary 中。将名称添加到已排序的 ComboBox 中。

当用户从 ComboBox 中选择供应商名称时，在 ListBox 中查找并显示该名称及对应的邮政编码和电话号码。

