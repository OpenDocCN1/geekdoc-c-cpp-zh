

## FIGURE 4.4

终于达到第一范式！

![](img/1e45673ab6eca9d20e67635ff5b9b318_136_0.png)

图 4.4 中的表包含与图 4.2 和图 4.3 中所示相同的数据。然而，新的排列使得处理数据变得容易得多。例如，可以轻松构建查询以返回客户订购的特定书籍的总数量，或确定哪些标题已被特定书店订购。

> Tip
> 你的表应始终处于第一范式。确保表的每个单元格都包含一个单一值，不要在单元格内混合值，并且不要有重复组（如你在图 4.3 中看到的那样）。

此时表设计优化尚未完成。然而，仍需对 BookOrders 数据和本应用程序中的其他表做很多工作。特别是，图 4.4 中显示的表包含冗余信息。书籍标题在客户每次订购同一本书时都会重复，而订单号和订单日期则对订单的所有行重复。

一个更微妙的问题是，OrderID 不再能用作表的键。因为 OrderID 对订单中的每个书籍标题重复，所以它不能用于标识表中的单个记录。相反，OrderID 字段现在是表的键字段，可用于定位与特定订单相关的所有记录。优化的下一步纠正了这种情况。

## Second normal form

通过将 tblBookOrders 中的数据拆分为多个表来实现第二范式（2NF），可以获得更高效的设计。规范化的第二条规则说明如下：

Data not directly dependent on the table's primary key is moved into another table.

这条规则意味着表应包含代表单个实体的數據。因为我们正在逐步将一个未规范化的表转换为规范化的数据，tblBookOrders3 没有主键。我们暂时忽略这一事实，将表中的每一行视为一个实体。该行中不是实体不可分割部分的全部数据都移至另一个表。在 tblBookOrders3 中，Customer 字段和 Title 字段都不是订单的不可分割部分，应移至不同的表。

### Identifying entities

但客户不是订单不可分割的一部分吗？是的，他们是。然而，存储在 tblBookOrders3 的 Customer 字段中的数据是客户姓名。如果客户更改姓名，并不会从根本上改变订单。同样，虽然书籍对订单很重要，但书籍的标题却不是。

为了解决这个问题，我们需要为客户和书籍分别创建表。首先，创建一个名为 tblBookstores 的新表，如图 4.5 所示。

要创建 tblBookstores，请执行以下步骤：

- 1. 点击功能区的“创建”选项卡上的“表设计”。
- 2. 添加一个名为 BookstoreID 的自动编号字段。
- 3. 点击功能区“表工具 设计”选项卡上的“主键”。
- 4. 添加一个名为 StoreName 的简短文本字段。
- 5. 将 StoreName 的“字段大小”设置为 50。
- 6. 将表保存为 tblBookstores。

我们可以想象，我们希望存储有关客户的更多信息，例如他们的邮寄地址和电话号码。目前，我们通过将不是订单不可分割部分的数据移至其自己的表，从而将数据置于 2NF。

接下来通过执行以下步骤为书籍创建表：

- 1. 点击功能区的“创建”选项卡上的“表设计”。
- 2. 添加一个名为 BookID 的自动编号字段。
- 3. 点击功能区“表工具 设计”选项卡上的“主键”。
- 4. 添加一个名为 BookTitle 的简短文本字段。
- 5. 将表保存为 tblBooks。

## FIGURE 4.5

将客户数据移至其自己的表。

![](img/1e45673ab6eca9d20e67635ff5b9b318_138_0.png)

客户和书籍仍然是订单不可分割的一部分（只是不是姓名和标题），我们需要一种方法将表相互关联。虽然客户可能会更改姓名，但客户不能更改 BookstoreID，因为我们创建了它并且我们控制它。同样，出版商可能会更改书籍的标题，但不会更改 BookID。tblBookstores 和 tblBooks 的主键是可靠的指针，指向它们标识的对象，无论其他信息可能如何更改。

图 4.6 显示了我们的三个表，但 tblBookOrders4 现在包含其在 tblBookstores 和 tblBooks 中相关记录的主键，而不是客户姓名和书籍标题。当一个表的主键用作另一个表中的字段时，它被称为外键。

在我们将客户数据拆分到其自己的表之前，如果 Uptown Books 将其名称更改为 Uptown Books and Periodicals，我们将不得不识别 tblBookOrders3 中所有客户为 Uptown Books 的行，并为每个识别出的行更改字段值。

在该过程中遗漏客户姓名的实例称为更新异常，会导致与数据库中其他记录不一致的记录。从数据库的角度来看，Uptown Books 和 Uptown Books and Periodicals 是两个完全不同的组织，即使我们知道它们是同一家商店。检索 Uptown Books and Periodicals 放置的所有订单的查询将遗漏 Customer 字段中仍为 Uptown Books 的任何记录，因为存在更新异常。

## FIGURE 4.6

使我们的表达到 2NF 的第一步。

![](img/1e45673ab6eca9d20e67635ff5b9b318_139_0.png)

从订单表中删除客户姓名的另一个优点是，姓名现在仅存在于数据库中的一个位置。如果 Uptown Books 将其名称更改为 Uptown Books and Periodicals，我们现在只需更改 tblBookstores 表中的条目。这一单一更改会反映在整个数据库中，包括使用客户姓名信息的所有窗体和报表。

识别单独的实体并将其数据放入单独的表中，是实现第二范式的重要第一步。但我们还未完全完成。我们的订单表仍然没有我们可以用作主键的唯一字段。OrderID 字段具有重复值，这表明需要做更多工作才能达到 2NF。

### Less obvious entities

客户和书籍是物理对象，很容易识别为单独的实体。下一步有点抽象。我们的订单表，现在称为 tblBookOrders4，仍然包含有关两个单独但相关的实体信息。订单是一个实体，而订单明细（订单上的各个行）也是各自的实体。

## Chapter 4: Understanding Table Relationships

图 4.6 中显示的 tblBookOrders4 的前三个记录包含相同的 OrderID、OrderDate 和 BookStoreID。这三个字段是整个订单的特征，而不是订单上每个单独行的特征。Quantity 和 BookID 字段在那三个第一个记录中包含不同的值。Quantity 和 BookID 是订单上特定行的特征。

> **TIP**
> 
> 在多个记录中重复的值，例如图 4.6 中 tblBookOrders4 中的 OrderID，是表明你的数据尚未处于第二范式的迹象。某些数据，例如外键，旨在重复。其他数据，例如日期和数量，自然重复，并不表示存在问题。

将我们的订单数据置于第二范式的最后一步是将与整个订单相关的信息放入与订单每行信息不同的表中。创建一个名为 tblBookOrderDetails 的新表，其中包含字段 BookOrderDetailID、Quantity 和 BookID。BookOrderDetailID 是一个自动编号字段，将用作主键，而 BookID 是一个外键字段，我们用它来关联两个表。图 4.7 显示了我们的新订单表 tblBookOrders5 和我们的新明细表 tblBookOrderDetails。

tblBookOrders5 中的 OrderID 字段已被删除，并创建了一个新的自动编号字段 OrderID。现在我们有了订单表中的唯一字段，我们可以将 OrderID 设置为主键。tblBookOrders5 的每个记录中的所有数据都直接与订单实体相关。或者，用 2NF 的语言来说，所有数据都直接依赖于主键。

tblBookOrderDetails 中的 OrderID 字段是外键，用于将两个表关联在一起。图 4.7 显示 tblBookOrderDetails 中的前三条记录显示 OrderID 为 1，对应于 tblBookOrders5 的第一条记录。

tblBookOrderDetails 中的所有字段都直接依赖于主键 BookOrderDetailID。第一条记录中的数量 10 直接与订单上的行项目相关。它仅通过间接方式与整个订单相关，就像接下来两条记录中的数量 5 和 7 一样。这种间接关系是通过在记录中包含 OrderID 外键创建的。

原始表 tblBookOrders1 的每个记录都包含有关多个不同实体的数据。通过一系列步骤，我们将数据拆分为四个表——tblBookOrders5、tblBookOrderDetails、tblBookStores 和 tblBooks——每个表都包含有关一个实体的数据。我们的數據最终处于第二范式。

将一个表分解为多个单独的表，每个表描述数据的某个方面，被称为分解。分解是规范化过程中的一个非常重要的部分。即使表看起来比原始表小（参见图 4.2），表中的数据与之前相同。

