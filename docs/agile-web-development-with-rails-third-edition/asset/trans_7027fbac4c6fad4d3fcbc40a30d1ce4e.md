
图 19.1：向 has_one 关系添加内容

## has_many 声明

has_many 定义一个行为类似于子对象集合的属性：

```
class Order < ActiveRecord::Base
  has_many :line_items
end
```

| 声明 | 外键 | 目标类 | 目标表 |
|---|---|---|---|
| has_many :line_items | order_id（在 line_items 中） | LineItem | line_items |

你可以将子对象作为数组访问、查找特定子对象以及添加新子对象。例如，以下代码向订单添加了一些订单项：

```
order = Order.new
params[:products_to_buy].each do |prd_id, qty|
  product = Product.find(prd_id)
  order.line_items << LineItem.new(:product => product,
                                  :quantity => qty)
end
order.save
```

追加运算符（<<）不仅仅是将一个对象追加到订单内部的列表中。它还会将这些订单项关联回当前订单，方法是将它们的外键设置为当前订单的 id，并在父订单保存时自动保存这些订单项。

我们可以遍历 has_many 关系的子对象——该属性充当数组：

```
order = Order.find(123)
total = 0.0

order.line_items.each do |li|
  total += li.quantity * li.unit_price
end
```

与 has_one 一样，你可以通过向 has_many 提供选项哈希来修改 Active Record 的默认行为。:class_name、:foreign_key 和 :conditions 选项的工作方式与它们在 has_one 方法中的工作方式相同。

:dependent 选项可以取 :destroy、:nullify 和 :delete_all 这些值——它们的含义与 has_one 中相同，只是应用于所有子行。

:dependent => :destroy 的工作方式是遍历子表，对每一行调用 destroy，这些行的外键引用父表中正在被删除的行。

然而，如果子表仅由父表使用（也就是说，它没有其他依赖项），并且没有在删除时执行任何操作的钩子方法，你可以改用 :dependent => :delete_all。此选项会在单个 SQL 语句中删除子行（这会更快）。

你可以通过设置 :finder_sql 和 :counter_sql 选项来覆盖 Active Record 用于获取和统计子行的 SQL。当仅使用 :conditions 选项添加 where 子句不够用时，这很有用。例如，你可以为特定产品创建所有订单项的集合：

```
class Order < ActiveRecord::Base
  has_many :rails_line_items,
    :class_name => "LineItem",
    :finder_sql => "select l.* from line_items l, products p " +
                   " where l.product_id = p.id " +
                   "       and p.title like '%rails%'"
end
```

:counter_sql 选项用于覆盖 Active Record 在统计行数时使用的查询。如果指定了 :finder_sql 而未指定 :counter_sql，Active Record 会通过将 finder SQL 的 select 部分替换为 select count(*) 来生成 counter SQL。

如果你希望在遍历集合时按特定顺序排列，则需要指定 :order 选项。你提供的 SQL 片段就是出现在 select 语句中 order by 子句之后的文本。它由一列或多列名称组成。集合将根据列表中的第一列排序。如果两行在该列中具有相同的值，则排序将使用列表中的第二项来决定它们的顺序，依此类推。每列的默认排序顺序为升序——在列名后面加上关键字 DESC 可反转此顺序。

以下代码可能用于指定订单的订单项按数量排序（数量最小的在前）：

```
class Order < ActiveRecord::Base
  has_many :line_items,
    :order => "quantity, unit_price DESC"
end
```

如果两个订单项数量相同，则单价最高的将排在前面。

之前讨论 has_one 时，我们提到它也支持 :order 选项。这似乎很奇怪——如果一个父对象只与一个子对象关联，那么获取该子对象时指定排序有什么意义呢？

事实证明，Active Record 可以在底层数据库不存在 has_one 关系的情况下创建这种关系。例如，一个客户可能有许多订单，这是一种 has_many 关系。但该客户只有一个最近订单。我们可以使用 has_one 结合 :order 选项来表达这一点：

```
class Customer < ActiveRecord::Base
  has_many :orders
  has_one  :most_recent_order,
    :class_name => 'Order',
    :order      => 'created_at DESC'
end
```

此代码在客户模型中创建了一个新属性 most_recent_order。它将引用具有最新 created_at 时间戳的订单。我们可以使用该属性来查找客户最近的订单：

```
cust = Customer.find_by_name("Dave Thomas")
puts "Dave last ordered on #{cust.most_recent_order.created_at}"
```

这之所以有效，是因为 Active Record 实际上使用如下 SQL 获取 has_one 关联的数据：

```
SELECT * FROM orders
WHERE  customer_id = ?
ORDER  BY created_at DESC
LIMIT  1
```

limit 子句意味着只返回一行，满足 has_one 声明中的“一”部分。order by 子句确保该行是最新的一行。

在探讨更高级的 Active Record 主题时，我们将介绍 has_many 支持的其他一些选项。

## has_many() 添加的方法

与 belongs_to 和 has_one 一样，has_many 会向其宿主类添加许多与属性相关的方法。同样，这些方法的名称以属性名开头。在接下来的描述中，我们将列出该声明添加的方法：

```
class Customer < ActiveRecord::Base
  has_many :orders
end
```

- orders(force_reload=false)
  返回与此客户关联的订单数组（如果没有，则可能为空）。结果会被缓存，如果之前已获取过订单，则不会再次查询数据库，除非传入 true 作为参数。

- orders << order
  将 order 添加到此客户关联的订单列表中。

- orders.push(order1, ...)
  将一个或多个 order 对象添加到此客户关联的订单列表中。concat 是此方法的别名。

- orders.replace(order1, ...)
  用新的集合替换与此客户关联的订单集合，并检测当前子集合与新集合之间的差异，从而优化相应的数据库更改。

- orders.delete(order1, ...)
  从此客户关联的订单列表中移除一个或多个 order 对象。如果关联被标记为 :dependent => :destroy 或 :delete_all，则每个子对象都会被销毁。否则，它会将其 customer_id 外键设为 null，从而断开关联。

- orders.delete_all
  对所有子行调用关联的 delete 方法。

- orders.destroy_all
  对所有子行调用关联的 destroy 方法。

- orders.clear
  取消所有订单与此客户的关联。与 delete 类似，这会断开关联，但仅当订单被标记为 :dependent 时才会从数据库中删除这些订单。

- orders.find(options...)
  发出常规 find 调用，但结果被限制为仅返回与此客户关联的订单。这适用于 id、:all 和 :first 形式。

- orders.count(options...)
  返回子对象数量。如果你指定了自定义 finder 或 count SQL，则使用该 SQL。否则，使用标准的 Active Record count，并限制为具有相应外键的子行。可以提供 count 的任何可选参数。

- orders.size
  如果你已经加载了关联（通过访问它），则返回该集合的大小。否则，通过查询数据库返回数量。与 count 不同，size 方法会遵循传给 has_many 的任何 :limit 选项，并且不使用 finder_sql。

- orders.length
  强制重新加载关联，然后返回其大小。

- orders.empty?
  等同于 orders.size.zero?。

- orders.sum(options...)
  等同于对关联中的行调用常规的 Active Record sum 方法（见第 338 页）。请注意，这是使用 SQL 函数对数据库中的行进行操作，而不是遍历内存中的集合。

- orders.uniq
  返回具有唯一 id 的子对象数组。

- orders.build(attributes={})
  构造一个新的 order 对象，使用给定属性初始化，并与客户关联。该对象不会被保存。

- orders.create(attributes={})
  构造并保存一个新的 order 对象，使用给定属性初始化，并与客户关联。

## has_and_belongs_to_many 声明

has_and_belongs_to_many（以下简称 “habtm”，以节省我们可怜的打字手指）在很多方面与 has_many 类似。“habtm” 创建一个本质上为集合的属性。该属性支持与 has_many 相同的方法。此外，“habtm” 允许你在关联两个对象时向连接表添加信息（尽管，我们稍后将看到，这种功能已逐渐不受青睐）。

