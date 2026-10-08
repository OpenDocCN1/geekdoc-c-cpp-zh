
查看图 6 的 UML 图。

![](img/6a52d1dde3a219cfa39d548e31d0e6ce_592_0.png)

图 6
继承和聚合的 UML 符号

你需要能够区分继承、接口实现、聚合和依赖的 UML 符号。

UML 记法中的箭头可能会令人混淆。表 1 显示了我们使用的 UML 符号摘要。

UML 符号

![](img/6a52d1dde3a219cfa39d548e31d0e6ce_593_0.png)

- 6. 考虑问题中的名词。哪些是类？
- 7. 考虑问题中的名词。它们是如何相互相关的？
- 8. 考虑类类。它依赖哪些类？
- 9. 为什么应该最小化耦合？
- 10. 在图书馆系统中，哪些依赖关系会导致聚合？
- 11. 在图书馆管理系统中，哪些书被借出了？
- 12. 它是另一个类的特化吗？
- 13. 现在尝试章节末的练习题。

## 多重性 (Multiplicities)

有些设计师喜欢在聚合关系的末尾写多重性，以表示聚合的对象数量。常见的多重性表示法如下：

- *任意数量（零或多个）；*
- 一个或多个：`1..*`
- 零或一个：`0..1`
- 恰好一个：`1`

下例显示一个客户拥有一个或多个银行账户。

![](img/6a52d1dde3a219cfa39d548e31d0e6ce_595_0.png)

## 聚合、关联与组合

有些设计师发现聚合或*拥有（*has-a** 这种术语并不令人满意。例如，银行的客户。银行“拥有”客户吗？是客户“拥有”银行账户，还是银行“拥有”这些账户？在这些“拥有”关系中，哪一个关系应该用聚合来建模？这种思维方式导致我们做出了过早的实现决策。

在设计阶段早期，定义类之间的关系是很有用的，这种关系被称为*关联（*association**）。如果你可以*从*一个类*导航到*另一个类的对象，那么这两个类之间就是关联关系。例如，对于一个银行对象，你可以通过访问实例变量或进行数据库查询来导航到客户对象。

关联关系的 UML 表示法是一条实线，并带有可选的箭头，显示你可以在哪些方向导航该关系。你还可以在线上添加单词来进一步解释关系的性质。下例显示你可以从银行对象导航到客户对象，但不能反向导航。也就是说，在这个特定的设计中，`Customer` 类没有机制来确定哪家银行存放了它的钱。

![](img/6a52d1dde3a219cfa39d548e31d0e6ce_595_1.png)

UML 标准还认可一种更强的聚合形式，称为*组合（*composition**），在这种情况下，被聚合的对象不独立于包含对象存在。例如，组合模拟了银行与其账户之间的关系。如果一家银行关闭，账户对象也将消失。在 UML 表示法中，组合看起来像是带有实心菱形的聚合。

## 12.2 类之间的关系 561

![](img/6a52d1dde3a219cfa39d548e31d0e6ce_596_0.png)

## 组合关系

坦率地说，聚合、关联和组合之间的区别即使对经验丰富的设计师也可能令人困惑。如果你觉得区分很有帮助，尽管可以使用你认为最合适的关系。但不要花时间去思考这些概念之间细微的区别。从 Java 程序员的实用角度来看，重要的是知道一个类的对象何时拥有另一个类对象的引用。聚合或“拥有”关系准确地描述了这种现象。

## 编程贴士 12.1

### 将并行数组转换为对象数组

有时，你会发现自己在使用相同长度的数组或列表，每个列表存储的是概念上应该是对象的一部分。在这种情况下，重新组织你的程序并使用一个元素为对象的单个数组或数组列表是一个好主意。

例如，假设一张发票包含系列描述和价格。解决方案是保留两个数组：

```java
String[] descriptions;
double[] prices;
```

每个数组的长度相同，第 i 个切片（由 `descriptions[i]` 和 `prices[i]` 组成）包含需要一起处理的数据。这些数组被称为并行数组（见图 7）。

并行数组在大型程序中会变成头疼的问题。程序员必须确保数组长度相同，并且每个切片填充的值实际上属于在一起。此外，任何对切片操作的方法都必须获取切片的所有值作为参数，这在编写程序时非常繁琐。

补救方法很简单。查看切片并找到它所代表的概念。然后将该概念转换为一个类。在这个示例中，每个切片包含一个物品的描述和价格；将其转换为：

```java
public class Item
{
    private String description;
    private double price;
    ...
}
```

![](img/6a52d1dde3a219cfa39d548e31d0e6ce_596_1.png)

`descriptions = prices =`
`[i]`
`[i]` 一个切片

> 通过将并行数组转换为对象数组来避免并行数组。

图 7
并行数组

你现在可以消除并行数组了。
`Item[] items;`

![](img/6a52d1dde3a219cfa39d548e31d0e6ce_597_0.png)

## 一致性

在本章中，你学习了提高代码质量的标准。当你有一组方法时，你应该注意一致性。在这个示例中，我们使用：

```java
String[] descriptions;
double[] prices;
```

为了显示对话框，使用：

```java
JOptionPane.showMessageDialog(null,
prompt, messageString)
```

这样的不一致性并不致命，但它们会令人苦恼。

## 12.3 应用：打印发票

在本书中，我们讨论了一个特别适合初学者的五部分开发流程：

- 1. 收集需求。
- 2. 使用 CRC 卡片寻找类、职责和协作者。
- 3. 使用 UML 图记录关系。
- 4. 使用 Javadoc 文档行为。
- 5. 实现你的程序。

## 12.3 应用：打印发票

学习很多表示法确实不容易。但 UML 图画起来很简单。当然，随着项目的变得复杂，你可能想学习形式的设计方法。有很多方法可以描述对象场景、程序的整体结构等，这些对项目非常有益。《统一建模语言用户指南》对这些技术提供了很好的概述。

在本节中，我们将通过一个简单的示例演示面向对象的设计。在这种情况下，这种方法论可能会让人压力很大，但它是对每一步机制的良好介绍。你将准备好应对更复杂的程序。

### 12.3.1 需求

在设计解决方案之前，你应该用纯白英语收集程序的所有需求。写下你的程序应该做什么。除了通用描述外，包含典型场景是有帮助的。

示例程序的任务是打印发票。发票描述了数量产品的费用。（我们省略了日期、时间、发票号和客户号等复杂性。）程序简单地打印账地址、所有项目和总金额。每个行项目包含产品的描述、单价、数量和总价。

![](img/6a52d1dde3a219cfa39d548e31d0e6ce_598_0.png)

发票列出了每个项目的费用和总金额。

# 发票

Sam 的小电器
100 Main Street
Anytown, CA 98765

| 描述 | 数量 | 总计 |
| --- | --- | --- |
| 烤面包机 | 29.95 | 3 | 89.85 |
| 吹风机 | 24.95 | 1 | 24.95 |
| 吸尘器 | 19.99 | 2 | 39.98 |

金额：$154.78

此外，为了简单起见，我们不提供用户界面。我们只是使用一个向发票添加项目并展示它们的测试程序。

### 12.3.2 CRC 卡

在设计面向对象的程序时，你需要发现类。类对应于需求规范中的名词。在这个问题中，哪些名词是显而易见的：

## 564 第 12 章 面对象设计

（课程，烤面包机不计入——它是对 `LineItem` 对象的描述，包含一个数据值，而不是类的名称。）
描述和价格是 `Product` 类的属性。那么数量呢？
数量不是 `Product` 的属性。就像在打印好的发票上一样，让我们创建一个 `LineItem` 类，用来记录产品和数量（例如“3 台烤面包机”）。
总计和金额是计算出来的——并没有存储在任何地方。因此，它们不会产生类。

经过这个排除法过程，我们剩下四个可以作为类的候选对象：

- `Invoice`（发票）
- `Address`（地址）
- `LineItem`（行项目）
- `Product`（产品）

它们中的每一个都代表一个实用的概念，所以让我们先创建一个发票。然而，`Invoice` 类并不知道应该将输出显示在 `System.out`、文本框还是文件中。因此，让我们稍微放宽任务，让发票负责发票的格式化。其结果是一个字符串（包含多行），可以被打印出来或显示。在 CRC 卡片上记录这一职责：

| Invoice |
| :--- |
| 格式化发票 |
| | |
| | |
| | |
| | |

发票如何格式化自己？它必须格式化账单地址、格式化所有行项目，然后加上金额。发票如何格式化地址？它不——那实际上是 `Address` 类的职责。这引出了第二张 CRC 卡片：

| Address |
| :--- |
| 格式化地址 |
| | |
| | |
| | |
| | |
| |

同样，行项目的格式化是 `LineItem` 类的职责。

## 12.3 应用：打印发票 565

`Invoice` 类的 `format` 方法调用了 `Address` 和 `LineItem` 类的 `format` 方法。每当一个方法使用另一个类时，你就将该类列为协作类。换句话说，`Address` 和 `LineItem` 是 `Invoice` 的协作类：

| Invoice |
| :--- | :--- |
| 格式化发票 | Address |
| | LineItem |
| | |
| | |
| | |
| | |

在格式化发票时，发票还需要计算应付金额。为了获得该金额，它必须询问每个行项目该项目的总价。
行项目如何获取该总价？它必须向 `product` 请求单价，并乘以数量。这意味着，`Product` 类必须公开单价，并且它是 `LineItem` 类的协作类。

| Product |
| :--- |
| 获取描述 |
| 获取单价 |
| | |
| | |
| | |
| | |
| | |

| LineItem |
| :--- | :--- |
| 格式化项目 | Product |
| 获取总价 |
| | |
| | |
| | |
| | |
| | |

最后，发票必须填充产品和数量，这样格式化结果才才有意义。这也是 `Invoice` 类的职责。

## 第 12 章 面对象设计

| Invoice | |
| :--- | :--- |
| 格式化发票 | Address |
| 添加产品和数量 | LineItem |
| Product | |

我们现在有了一组完成 CRC 卡片过程的 CRC 卡片。

### 12.3.3 UML 图

- 使用 UML 图记录类之间的关系。

在你通过 CRC 卡片发现类以及它们之间的关系之后，你应该将你的发现记录在 UML 图中。依赖关系源于它与之协作的类。在我们的示例中，`Invoice` 类与 `Address`、`LineItem` 和 `Product` 类协作。`LineItem` 类与 `Product` 类协作。
问问自己，这些依赖关系实际上是聚合（aggregation）吗？发票如何知道它所协作的地址、行项目和产品对象？发票对象必须持有对这些对象的引用。发票对象持有地址、行项目和产品对象的引用。`LineItem` 类持有 `Product` 对象的引用。

# 570 第12 章 面向对象设计

无法立即找到一个完美的解决方案，并且可能需要回过重新组织你的类和职责。这是正常现象，也是在预料之中的。面向对象设计过程目的是在设计阶段解决这些问题，此时这些问题还容易纠正，而不是在实现阶段，因为那时候的重新组织将更加困难且耗费时间。

## section_3/InvoicePrinter.java

```java
/**
 * 此程序通过打印示例发票来演示
 * 发票类。
 */
public class InvoicePrinter {
    public static void main(String[] args) {
        Address samsAddress = new Address("Sam's Small Appliances", "100 Main Street", "Anytown", "CA", "98765");

        Invoice samsInvoice = new Invoice(samsAddress);

        samsInvoice.add(new Product("Toaster", 29.95, 3));
        samsInvoice.add(new Product("Hair dryer", 24.95, 1));
        samsInvoice.add(new Product("Car vacuum", 19.99, 2));

        System.out.println(samsInvoice.format());
    }
}
```

## section_3/Invoice.java

```java
/**
 * 描述一组购买产品的发票。
 */
public class Invoice {
    private Address billingAddress;
    private ArrayList<LineItem> items;

    /**
     * 构造一个发票。
     * @param address 账单地址
     */
    public Invoice(Address address) {
        items = new ArrayList<LineItem>();
        billingAddress = address;
    }

    /**
     * 为发票添加一个产品的费用。
     * @param product 客户订购的产品
     * @param quantity 产品的数量
     */
    public void add(Product aProduct, int quantity) {
        LineItem anItem = new LineItem(aProduct, quantity);
        items.add(anItem);
    }

    /**
     * 格式化发票。
     * @return 格式化后的发票
     */
    public String format() {
        String r = "INVOICE E\n\n"
            + billingAddress.format()
            + String.format("\n%3s%-30s%8s%8s%s\n",
            "Description", "Price", "Qty", "Total:");

        for (LineItem item : items) {
            r = r + item.format() + "\n";
        }

        r += String.format("\nAMOUNT DUE: $%8.2f", getAmount());
        return r;
    }

    /**
     * 计算应付总额。
     * @return 应付金额
     */
    private double getAmount() {
        double amountDue = 0;
        for (LineItem item : items) {
            amountDue = amountDue + item.getTotalPrice();
        }
        return amountDue;
    }
}
```

```java
/**
 * 描述要购买的商品数量。
 */
public class LineItem {
    private int quantity;
    private Product theProduct;

    /**
     * 根据产品和数量构造一个项目。
     * @param aProduct 产品
     * @param quantity 项目数量
     */
    public LineItem(Product aProduct, int aQuantity) {
        theProduct = aProduct;
        quantity = aQuantity;
    }

    /**
     * 计算此行项目的总成本。
     * @return 总价
     */
    public double getTotalPrice() {
        return theProduct.getPrice() * quantity;
    }

    /**
     * 格式化此项目。
     * @return 此行项目的格式化字符串
     */
    public String format() {
        return String.format("%-30s$%.2f%8d$%.2f",
            theProduct.getDescription(), theProduct.getPrice(),
            quantity, getTotalPrice());
    }
}
```

## section_3/Product.java

```java
/**
 * 描述一个具有描述和价格的产品。
 */
public class Product {
    private String description;
```
