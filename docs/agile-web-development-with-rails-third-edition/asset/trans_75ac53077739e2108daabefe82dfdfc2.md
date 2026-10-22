

所有聚合函数都接受一个选项哈希，与可以传递给 find 的哈希非常相似。（count 函数是个例外——我们会单独讨论它。）

:conditions
将函数限制为匹配的行。条件可以以与 find 方法相同的格式指定。

:joins
指定要连接的附加表。

:limit
将结果集限制为给定数量的行。这仅在分组结果时才有用（我们稍后会讨论）。

:order
对结果集进行排序（仅在与 :group 一起使用时有用）。

:having
指定 SQL HAVING ... 子句。

:select
指定要在聚合中使用的列（但这可以简单地作为聚合函数的第一个参数指定）。

:distinct （仅限 count）
仅统计列中的不同值。

这些选项可以组合使用：

```
Order.minimum :amount
Order.minimum :amount, :conditions => "amount > 20"
```

这些函数对值进行聚合。默认情况下，它们返回单个结果，例如，返回满足某些条件的订单的最小订单金额。但是，如果你包含 :group 子句，函数将改为产生一系列结果，为分组表达式具有相同值的每组记录产生一个结果。例如，以下代码计算每个州的最大销售额：

```
result = Order.maximum :amount, :group => "state"
puts result  #=> [["TX", 12345], ["NC", 3456], ...]
```

此代码返回一个有序哈希。你可以使用分组元素（在我们的示例中为 "TX"、"NC"...）对其进行索引。你也可以使用 each 按顺序遍历条目。每个条目的值是聚合函数的值。

使用分组时，:order 和 :limit 参数才真正发挥作用。

作用域也可以组合。查找最近一周通过支票支付的订单同样简单：

```
orders = Orders.checks.last_n_days(7)
```

除了使应用程序代码更易于编写和阅读之外，命名作用域还可以使代码更高效。例如，前面的语句被实现为单个 SQL 查询。

可以使用 scope 命名作用域创建匿名作用域：

```
in_house = Orders.scoped(:conditions => 'email LIKE "%@pragprog.com"')
```

当然，匿名作用域也可以组合：

```
in_house.checks.last_n_days(7)
```

作用域不限于条件；我们可以在 find 调用中做的几乎所有事情都可以在作用域中做：:limit、:order、:join 等等。只需注意 Rails 不知道如何处理多个 order 或 limit 子句，因此请确保在每个调用链中仅使用一次。

Rails 甚至提供了一个名为 all 的作用域，其功能等同于 find(:all)。

## 重新加载数据

在一个数据库可能被多个进程（或多个应用程序）访问的应用程序中，始终存在获取的模型对象可能已过时的可能性——有人可能已将更新的副本写入数据库。

在某种程度上，这一问题通过事务支持得到解决（我们在第 418 页描述）。然而，仍会有需要手动刷新模型对象的时候。Active Record 使这变得很容易——只需调用其 reload 方法，对象的属性就会从数据库中刷新：

```
stock = Market.find_by_ticker("RUBY")
loop do
  puts "Price = #{stock.price}"
  sleep 60
  stock.reload
end
```

在实践中，reload 在单元测试的上下文之外很少使用。

## 更新现有行

在讨论了这么多 finder 方法之后，你会很高兴知道，使用 Active Record 更新记录并没有太多可说的。

如果你有一个 Active Record 对象（可能代表我们 orders 表中的一行），你可以通过调用其 save 方法将其写入数据库。如果此对象

## 删除行

Active Record 支持两种行删除样式。首先，它有两个类级方法，delete 和 delete_all，它们在数据库级别操作。delete 方法接受单个 id 或 id 数组，并删除底层表中对应的行（行）。delete_all 删除匹配给定条件的行（如果未指定条件则删除所有行）。两次调用的返回值取决于适配器，但通常是受影响的行数。如果在调用前行不存在，则不会抛出异常。

```
Order.delete(123)
User.delete([2,3,4,5])
Product.delete_all(["price > ?", @expensive_price])
```

destroy 方法是 Active Record 提供的第二种行删除形式。这些方法都通过 Active Record 模型对象工作。

destroy 实例方法从数据库中删除对应于特定模型对象的行。然后它冻结该对象的内容，防止未来对属性的更改。

```
order = Order.find_by_name("Dave")
order.destroy
# ... order is now frozen
```

有两个类级销毁方法，destroy（接受 id 或 id 数组）和 destroy_all（接受条件）。两者都将数据库表中的对应行读入模型对象，并调用这些对象的实例级 destroy 方法。两种方法都不返回有意义的值。

```
Order.destroy_all(["shipped_at < ?", 30.days.ago])
```

为什么我们需要 delete 和 destroy 这两种类方法？delete 方法绕过了各种 Active Record 回调和验证函数，而 destroy 方法确保它们都被调用。（我们从第 407 页开始讨论回调。）通常，如果你希望确保数据库根据模型类中定义业务规则保持一致，最好使用 destroy 方法。

## 18.6 聚合和结构化数据

（本节包含可在首次阅读时安全跳过的材料。）

## 存储结构化数据

有时将包含任意 Ruby 对象的属性直接存储到数据库表中会很有帮助。Active Record 支持的一种方式是将 Ruby 对象序列化为字符串（YAML 格式），并将该字符串存储在对应于该属性的数据库列中。在模式中，此列必须定义为 text 类型。

由于 Active Record 通常将字符或文本列映射为普通的 Ruby 字符串，因此如果你想利用此功能，需要告诉 Active Record 使用序列化。例如，我们可能想记录客户最近五次购买。我们将创建一个包含用于保存此信息的文本列的表：

```
create_table :purchases, :force => true do |t|
  t.string :name
  t.text   :last_five
end
```

在包装此表的 Active Record 类中，我们将使用 serialize 声明告诉 Active Record 将对象编组到此列并从此列编组出来：

```
class Purchase < ActiveRecord::Base
  serialize :last_five
  # ...
end
```

当我们创建新的 Purchase 对象时，我们可以将任何 Ruby 对象分配给 last_five 列。在本例中，我们将其设置为字符串数组：

```
purchase = Purchase.new
purchase.name = "Dave Thomas"
purchase.last_five = [ 'shoes', 'shirt', 'socks', 'ski mask', 'shorts' ]
purchase.save
```

当我们稍后读取它时，该属性会被设置回数组：

```
purchase = Purchase.find_by_name("Dave Thomas")
pp purchase.last_five
pp purchase.last_five[3]
```

此代码输出以下内容：

```
["shoes", "shirt", "socks", "ski mask", "shorts"]
"ski mask"
```

尽管功能强大且方便，但如果我们以后需要在 Ruby 应用程序之外使用序列化列中的信息，这种方法是有问题的。除非该应用程序理解 YAML 格式，否则列内容对它来说是不透明的。特别是，很难在 SQL 查询中使用这些列中的结构。出于这些原因，使用组合进行对象聚合通常是更好的方法。

