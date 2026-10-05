

# 增强型发票总表表

![](img/3148667e42d4db35b3d08576aaa1fa01_150_0.png)

# 类变量和两个事件程序的代码

```
int numberOfInvoices = 0;
decimal totalOfInvoices = 0m;
decimal invoiceAverage = 0m;

private void btnCalculate_Click(object sender, EventArgs e)
{
    decimal subtotal = Convert.ToDecimal(txtEnterSubtotal.Text);
    decimal discountPercent = .25m;
    decimal discountAmount = Math.Round(subtotal * discountPercent, 2);
    decimal invoiceTotal = subtotal - discountAmount;
    txtSubtotal.Text = subtotal.ToString("c");
    txtDiscountPercent.Text = discountPercent.ToString("P");
    txtDiscountAmount.Text = discountAmount.ToString("c");
    txtTotal.Text = invoiceTotal.ToString("c");

    numberOfInvoices += (int)invoiceTotal;
    totalOfInvoices += invoiceTotal;
    invoiceAverage = totalOfInvoices / numberOfInvoices;

    txtNumberOfInvoices.Text = numberOfInvoices.ToString();
    txtOfInvoices.Text = totalOfInvoices.ToString("c");
    txtInvoiceAverage.Text = invoiceAverage.ToString("c");

    txtEnterSubtotal.Text = "";
    txtEnterSubtotal.Focus();
}

private void btnCalculateTotals_Click(object sender, System.EventArgs e)
{
    numberOfInvoices = 0;
    totalOfInvoices = 0m;
    invoiceAverage = 0m;

    txtNumberOfInvoices.Text = "";
    txtOfInvoices.Text = "";
    txtInvoiceAverage.Text = "";

    txtEnterSubtotal.Focus();
}
```

图 4-17 增强型发票总表应用程序

# 观点

如果你理解了增强型发票总表应用程序的代码，说明你已经迈出了很远的一步。如果没有，在完成本章的练习时，你应该更好地理解此应用程序是如何工作的。一旦你理解了它，你就准备好学习如何编写选择和迭代语句了，以便为你的应用程序添加逻辑操作。

## 术语

- 内置数据类型
- 位
- 字节
- 整数
- Unicode 字符集
- ASCII 字符集
- 布尔值
- 变量
- 常量
- 声明
- 初始化
- 驼峰命名法
- Pascal 命名法
- 字面量常量
- 科学计数法
- 算术表达式
- 算术运算符
- 操作数
- 二元运算符
- 一元运算符
- 前置操作数
- 后置操作数
- 赋值语句
- 赋值运算符
- 优先级
- 强制转换
- 隐式转换
- 宽化转换
- 显式转换
- 窄化转换
- 严格的类型语义
- 静态方法
- 参数
- 精度
- 银行家舍入法
- 字符串
- 字符串字面量
- 空值
- 空字符串
- 拼接
- 追加
- 转义序列
- 逐字字字符串字面量
- 结构
- 值类型
- 引用类型
- 作用域
- 类作用域
- 类变量
- 方法作用域
- 寿命
- 枚举
- 成员
- 可空类型

# 练习 4-1 修改发票总表应用程序

在练习中，你将修改本章中介绍的发票总表应用程序。

# 打开发票总表应用程序

- 1. 打开位于 C:\C# 2010\Chapter 04\InvoiceTotal 目录下的应用程序。这是图16 所示的应用程序。

# 修改并测试发票总表应用程序的代码

- 2. 生成并运行应用程序，输入一个有效的小金额以验证是否取了正确的折扣。然后，输入一个像 225.50 的有效小金额，这将产生一个超过两位小数的折扣金额，并确保折扣金额和总额仅显示两位小数。

- 3. 为小金额输入“$1000”并点击计算按钮。此时应该发生一个异常，Visual Studio 将进入断点模式，异常助手程序将显示一条消息，指示输入字符串格式不正确。

- 4. 注意高亮的语句。这表明赋值语句无法将输入的字符串转换为 decimal 类型。接下来，将鼠标指针悬停在 `txtSubtotal.Text` 上，你可以看到数据提示显示当前值为 $1000。然后，点击调试工具栏上的停止调试按钮结束应用程序。

# 对代码进行实验

- 5. 修改 `btnCalculate_Click` 方法的第一条语句，将发票总额加到 `totalOfInvoices` 中。
- 6. 修改代码以确保折扣金额仅显示两位。
- 7. 保存项目。

# 练习 4-2 增强发票总表应用程序

本练习将引导你增强发票总表应用程序。这将让你获得开发练习。

# 打开发票总表应用程序并增强表单

- 1. 打开 C:\C# 2010\Chapter 04\InvoiceTotal 中的应用程序。
- 2. 使用你在第三章中学的技术添加新控件。
- 3. 设置每个控件的属性。

# 添加增强代码

- 4. 为 `btnCalculate_Click` 添加代码，以计算并显示新数据。
- 5. 为 `btnCalculateTotals_Click` 事件添加代码。
- 6. 测试应用程序。

# 添加更多控件和代码

- 7. 在表单右侧添加两个标签和两个文本框。标签应为“最大发票”和“最小发票”。
- 8. 添加查找最大和最小发票总额的代码。（提示：要查找最小发票总额，使用 `Math.Min` 方法将每张发票总额与包含截至目前最小总额的变量进行比较。为了让第一张发票正常工作，可以将此变量初始化为 `Decimal.MaxValue`）。
- 9. 测试应用程序。

