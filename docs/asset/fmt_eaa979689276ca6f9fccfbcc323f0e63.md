
输出:
产品信息 - 产品代码: C101, 产品名称: Camera, 产品价格 15.75

语句 #3 定义了一个字符串类型、名为 `Code` 的属性。该属性具有 `get` 和 `set`（访问器和修改器）方法。每当在任何语句中访问 `code` 成员时，都会自动调用相应方法。例如，语句 #1 调用了在语句 #5 中定义的 `set` 方法。要赋值给 `code` 成员的值会被赋给参数 `value`，然后将其赋给成员 `code`。

同样，当如语句 #2 所示访问 `code` 成员时，会调用 `get` 访问器（在语句 #4 中），返回成员 `code` 中的值并显示在屏幕上。

## 在结构体中定义数组

你在上一章中学习了数组。现在你将发现如何将它们作为结构体成员。列表 6.12 显示的 `ArrayInstruct.cs` 文件展示了名为 `Product` 的结构体中的关于产品信息。`Product` 结构体有两个成员：字符串类型的 `code` 和一个名为 `product_info` 的字符串数组。`product_info` 数组存储了产品的名称、价格和制造日期。

## 第 6 章 方法与结构体

### 列表 6.12 ArrayStruct.cs 中的程序代码

```csharp
using System;

struct Product {

    public string code;

    public string[] product_info;

}

class ArrayStruct {

    static void Main() {

        Product p1 = new Product();

        p1.product_info = new string[3];

        p1.code = "C101";

        p1.product_info[0] = "Cell Phone";

        p1.product_info[1] = "12.99";

        p1.product_info[2] = "11/07/2013";

        Console.WriteLine("Information of the product - Product Code: {0}, Product Name: {1}, Product Price: {2}, Date of Manufacturing: {3}", p1.code, p1.product_info[0], p1.product_info[1], p1.product_info[2]);

    }

}
```

输出:
产品信息为 - 产品代码: C101, 产品名称: Cell Phone, 价格: 12.99, 制造日期: 11/07/2013

你可以看到 `Product` 结构体是由两个字段定义的：`code` 和 `product_info`。`product_info` 数组只是在结构体中声明了而并没有定义。实例化了 `Product` 结构体，创建了变量 `p1`。`code` 字段被设置为值 `C101`。为 `product_info` 数组分配了三个内存块。换句话说，定义了 `product_info` 数组，允许该数组存储三个字符串。产品名称、价格和制造日期作为字符串元素存储在 `product_info` 数组中。最后，访问了结构体成员 `code` 和 `product_info` 中的信息并将其显示在屏幕上。

列表 6.13 显示的程序 `ArrayStructInit.cs` 使用结构体中的数组来存储产品信息。该程序演示了包含数组成员的结构体在实例化时是如何初始化的。

### 列表 6.13 ArrayStructInit.cs 文件中的程序代码

```csharp
using System;

struct Product {

    public string code;

    public string[] product_info;

    public Product(string c, string[] pfo) {

        code = c;

        product_info = new string[3];

        product_info[0] = pfo[0];

        product_info[1] = pfo[1];

        product_info[2] = pfo[2];

    }

}

class ArrayStructInit {

    static void Main() {

        string[] pfo = new string[3];

        pfo[0] = "Cell Phone";

        pfo[1] = "12.99";

        pfo[2] = "11/07/2013";

        Product pl = new Product("C101", pfo);

        Console.WriteLine("Information of the product - Product Code: {0}, Product Name: {1}, Price: {2}, Date of Manufacturing: {3}", pl.code, pl.product_info[0], pl.product_info[1], pl.product_info[2]);

    }

}
```

输出:
产品信息 - 产品代码: C101, 产品名称: Cell Phone, 价格: 12.99, 制造日期: 11/07/2013

你可以看到 `Product` 结构体包含两个字段：`code` 和 `product_info`。`product_info` 数组只是在结构体中声明了而并没有定义。`code` 字段被赋值为 `C101`。为 `product_info` 数组分配了三个内存块。换句话说，定义了 `product_info` 数组，允许该数组存储三个字符串。产品名称、价格和制造日期作为字符串元素存储在 `product_info` 数组中。最后，访问了结构体成员 `code` 和 `product_info` 中的信息并将其显示在屏幕上。

程序 `ArrayStructInit.cs` 使用结构体中的数组来存储产品信息。该程序演示了包含数组成员的结构体在实例化时是如何初始化的。

你可以看到 `Product` 结构体包含两个字段：`code` 和 `product_info`。`product_info` 数组只是在结构体中声明了而并没有定义。`Product` 结构体被实例化，创建了变量 `pl`（此处为p1）。`code` 字段被赋值为 `C101`。为 `product_info` 数组分配了三个内存块。换句话说，定义了 `product_info` 数组，允许该数组存储三个字符串。产品名称、价格和制造日期作为字符串元素存储在 `product_info` 数组中。最后，访问了结构体成员 `code` 和 `product_info` 中的信息并将其显示在屏幕上。

（注：原文中此处 `pl` 似乎是 `p1` 的笔误，翻译时保持代码逻辑）

输出:
产品信息 - 产品代码: C101, 产品名称: Cell Phone, 价格: 12.99, 制造日期: 11/07/2013

该程序演示了包含数组成员的结构体在实例化时是如何初始化的。

（注：原文中此处 `pl` 似乎是 `p1` 的笔误，翻译时保持代码逻辑）

## 第6章 方法与结构

```csharp
class ArrayOfStructs {
    static void Main() {
        Product[] p = { new Product("C101", "Camera", 9.99), new Product("L102", "Laptop", 30), new Product("T103", "Tablet", 15.99) };
        Console.WriteLine("Information of products:");
        for (int i = 0; i<p.Length; i++) {
            Console.WriteLine("Product Code: {0}, Product Name: {1}, Product Price: {2}", p[i].code, p[i].product_name, p[i].price);
        }
    }
}
```

输出：

Information of products:

Product Code: C101, Product Name: Camera, Product Price 9.99

Product Code: L102, Product Name: Laptop, Product Price 30

Product Code: T103, Product Name: Tablet, Product Price 15.99

在这里，使用了构造函数来初始化三个字段：`code`、`product_name` 和 `price`。在 `Main` 方法中，定义了结构体数组 `p` 并用三个 `Product` 结构体对象对其初始化。在你定义并初始化结构体数组后，存储在其中的三个产品的信息将显示在屏幕上。

## 嵌套结构体

在 C# 中，结构体可以嵌套另一个结构体内部。嵌套结构体作为父结构体的一个成员。在声明嵌套结构体时使用的访问修饰符定义了它的可见性。将 C# 结构体嵌套在彼此内部有两种方法。第一种方法是将结构体的整个声明嵌套在另一个结构体内部，如下所示：

```csharp
struct S1 {
    // struct S1 的公共成员变量
    public struct S2 {
        // struct S2 的公共成员变量
    }
}
```

在上述语法中，你看到整个结构体 S2 被声明在结构体 S1 的主体体内部。嵌套结构体的第二种方法是将结构体作为另一个结构体的成员变量，如下所示：

```csharp
struct S1
{
    // 公共成员变量
}
struct S2
{
    // 公共成员变量
    public S1 s; // 声明为 struct S2 成员变量的 struct S1
}
```

列表 6.16 显示的 NestedStruct.cs 程序演示了结构体的嵌套。定义了一个 `Product` 结构体，它包含三个成员：字符串类型的 `code`、字符串类型的 `product_name` 以及双精度类型的 `price`。嵌套在 `Product` 内部的是另一个名为 `Specifications` 的结构体。`Specifications`结构体由三个字符串类型的成员组成：`color`、`weight` 和 `size`。

### 列表 6.16 NestedStruct.cs 文件中的程序代码

```csharp
using System;
struct Product {
    public string code;
    public string product_name;
    public double price;
    public struct Specifications {
        public string color;
        public string weight;
        public string size;
    }
}
class NestedStruct {
    static void Main() {
        Product p1;
        p1.code="L102";
        p1.product_name="Laptop";
        p1.price=800;
        Product.Specifications spec;
        p1.spec.color="silver";
        p1.spec.weight=".25 pound";
        p1.spec.size="8 inches";
    }
}
```

## 第6章 方法与结构

```csharp
Console.WriteLine("Information of the product - Product Code: {0}, Product Name: {1}, Product Price {2}", p1.code, p1.product_name, p1.price);
Console.WriteLine("Product Color: {0}, Weight: {1}, Size: {2}", spec.color,
spec.weight, spec.size);
}
```

输出：

Information of the product - Product Code: L102, Product Name: Laptop, Product Price 800

Product Color: silver, Weight: .25 pound, Size: 8 inches

你可以看到 `Specifications` 结构体被声明在 `Product` 结构体内部。`Product` 结构体是父结构体。在 `Main` 方法中，创建了一个 `Product` 类型的变量 `p1`。`Product` 结构体的 `code`、`product_name` 和 `price` 成员被初始化为 L102、Laptop 和 800。随后，创建了 `Product.Specifications` 类型的变量 `spec`。通过指定父结构体后跟点（.）来访问嵌套结构体。`Specifications` 体的 `color`、`weight` 和 `size` 成员被初始化为 silver、.25 pound 和 8 inches。最后，`Product` 和 `Specifications` 成员变量的值将显示在屏幕上。

你可能在想在初始化结构体时是否可以初始化嵌套结构体的成员。答案是定的。

列表 6.17 显示的 NestedStruct.cs 程序演示了如何在初始化时初始化父结构体和嵌套结构体的成员。

## 列表 6.17 NestedStruct.cs 文件中的程序代码

## 日期时间结构

传递给构造函数的值用于初始化 `Product` 结构体的成员，其余三个值则用于调用 `Specifications` 结构体的构造函数，以初始化其颜色、重量和大小成员。分配给这两个结构体成员的值将显示在屏幕上。

现在你已经如何在 C# 程序中工作和使用结构体。`DateTime` 结构体是 C# 提供的一个常用内置结构体。从它的名称可以看出，`DateTime` 用于存储日期和时间。下一节将对其进行详细介绍。

## 日期时间结构

`DateTime` 结构表示日期和时间。它是一个值类型结构，而不是引用类型。`DateTime` 的值处于公元 0001 年1 月 1 日午 12:00:00 到 9999 年12 月 31 日 11:59:59 之间。你可以使用以下任何方法创建 `DateTime` 对象：

```
DateTime today_date = DateTime.Today; // 从当前日期时间值创建 DateTime 实例
DateTime custom_date1 = new DateTime(2012, 11, 5); // 创建仅包含日期的 DateTime 实例
DateTime custom_date2 = new DateTime(2012, 11, 5, 10, 30, 15); // 从提供的日期时间值创建 DateTime 实例
string dateStr = "11/5/2013 10:30 AM";
DateTime custom_date3 = DateTime.Parse(dateStr); // 从给定字符串提供的日期时间值创建 DateTime 实例
DateTime custom_date4 = new DateTime(1000000); // 从提供的 Ticks 数量创建 DateTime 实例
```

一个 tick（刻度）代表百纳秒，或者一秒的千万分之一。

## 注意

> 如果在指定日期时没有指定时间，`DateTime` 构造函数会将时间设置为午夜 12:00。

`DateTime` 对象将日、月、年、时、分和毫秒值存储为单独属性，允许通过属性（Properties）单独访问每个值。

## 使用 DateTime 属性和方法

`DateTime` 属性从 `DateTime` 结构包含的日期和时间中返回所需的组件。表 6.2 提供了 `DateTime` 属性的简要描述。

## 第 6 章 方法与结构体

| 属性 | 说明 |
|---|---|
| Hour, Minute, Second, Millisecond, Year, Month, and Day | 属性名称本身描述了它返回的组件。 |
| DayOfWeek | 显示星期（周一、二、三、四、五、六或日）。 |
| DayOfYear | 返回一年的天数。 |
| TimeOfDay | 返回 `DateTime` 结构中的时间元素。 |
| Date | 返回 `DateTime` 结构中的日期组件。时间值设置为午夜 12（00:00:00）。 |
| Day, Month, Year | 从提供的 `DateTime` 对象返回日、月、年的值。 |
| Now | 返回当前的日期时间值。例如：7/3/2013 9:43:16 AM |
| Today | 以 `DateTime` 实例的形式获取当前日期。它不包含时间信息。时间值设置为 12:00:00。例如：7/2/2013 12:00:00 AM |
| Ticks | 返回 `DateTime` 结构中的 tick 数量。 |
| UtcNow | 返回协调世界时 (UTC) 的 `DateTime`。 |
