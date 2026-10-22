
# 是的，这令人困惑……

你可能已经注意到，通过 `has_many` 添加到 Active Record 类中的方法存在相当多的重复（或几乎重复）。例如，`count`、`size` 和 `length` 之间的差异，或者 `clear`、`destroy_all` 和 `delete_all` 之间的差异，都很微妙。这主要是因为 Active Record 中的功能随着时间的推移逐渐累积。随着新选项的加入，现有方法不一定能及时更新。我们猜测在某个时候这个问题会得到解决，这些方法将会被统一。值得研究一下在线的 Rails API 文档，因为本书出版后 Rails 很可能已经发生了变化。

让我们看看除了商店应用之外的另一个例子来说明“habtm”。也许我们正在使用 Rails 编写一个社区网站，用户可以阅读文章。有许多用户和许多文章，任何用户都可以阅读任何文章。为了跟踪目的，我们想知道阅读每篇文章的人以及每个人阅读过的文章。我们还想知道用户最后一次查看某篇特定文章的时间。我们将用一个简单的连接表来实现这一点。在 Rails 中，连接表的名字是两个被连接表的名字按字母顺序拼接而成：

![](img/a160fc3a330a0b3b2a764d41d614e688_370_0.png)

我们将两个模型类设置为通过这个表相互关联：

```
class Article < ActiveRecord::Base
  has_and_belongs_to_many :users
  # ...
end
```

```
class User < ActiveRecord::Base
  has_and_belongs_to_many :articles
  # ...
end
```

这允许我们执行诸如列出阅读过文章 123 的所有用户以及 pragdave 阅读过的所有文章等操作：

```
# Who has read article 123?
article = Article.find(123)
readers = article.users
```

```
# What has Dave read?
dave = User.find_by_name("pragdave")
articles_that_dave_read = dave.articles
```

```
# How many times has each user read article 123
counts = Article.find(123).users.count(:group => "users.name")
```

当我们的应用注意到有人阅读了一篇文章时，它将他们的用户记录与文章关联起来。我们将在 User 类中使用一个实例方法来实现这一点：

```
class User < ActiveRecord::Base
  has_and_belongs_to_many :articles

  # This user just read the given article
  def just_read(article)
    articles << article
  end

  # ...
end
```

如果我们想要在用户与文章之间的关联中记录更多信息，比如记录用户阅读文章的时间，那该怎么办？在这种情况下，你应该改用常规的 Active Record 模型作为连接表（请记住，在“habtm”中，连接表不是一个 Active Record 模型）。我们将在下一节讨论这种方案。

与其他关系方法一样，“habtm”支持一系列覆盖 Active Record 默认值的选项。`:class_name`、`:foreign_key` 和 `:conditions` 的工作方式与其他 `has_` 方法中的相同（`:foreign_key` 选项设置在连接表中指向该表的外键列的名称）。此外，“habtm”还支持覆盖连接表名称、连接表中外键列名称以及用于查找、插入和删除两个模型之间链接的 SQL 的选项。详情请参阅 API 文档。

## 关联集合回调

我们还可以定义 `before_add`、`after_add`、`before_remove` 和 `after_remove` 回调，这些回调在我们向关联集合添加对象或从中移除对象时触发：

```
class User < ActiveRecord::Base
  has_and_belongs_to_many :articles, :after_add => :categorize

  def categorize(article)
    # ...
  end
end
```

也可以通过传递数组来定义多个回调。如果任何一个 `before_add` 或 `before_remove` 回调抛出异常，该对象将不会被添加或移除。

## 使用模型作为连接表

目前 Rails 的思路是保持连接表的纯净——连接表应该只包含一对外键列。每当你觉得需要向这种表添加更多数据时，你实际上是在创建一个新模型，因为连接表从简单的链接机制变成了应用业务中一个成熟的参与者。让我们回顾之前关于文章和用户的例子。

在简单的“habtm”实现中，连接表记录了一篇文章被用户阅读的事实。连接表中的行没有独立的存在。但很快我们发现自己想向这个表添加信息。我们想记录读者何时阅读了文章，以及阅读完成后给了多少颗星。连接表突然有了自己的生命，值得拥有自己的 Active Record 模型。我们称之为 Reading。其模式如下所示：

![](img/a160fc3a330a0b3b2a764d41d614e688_372_0.png)

使用我们在本章中到目前为止看到的 Rails 工具，我们可以用以下方式对此建模：

```
class Article < ActiveRecord::Base
  has_many :readings
end
```

```
class User < ActiveRecord::Base
  has_many :readings
end
```

```
class Reading < ActiveRecord::Base
  belongs_to :article
  belongs_to :user
end
```

当用户阅读文章时，我们可以记录该事实：

```
reading = Reading.new
reading.rating  = params[:rating]
reading.read_at = Time.now
reading.article = current_article
reading.user    = session[:user]
reading.save
```

然而，与“habtm”解决方案相比，我们失去了一些东西。我们不再能轻松地询问一篇文章有哪些读者，或询问一个用户阅读了哪些文章。这就是 `:through` 选项的用武之地。让我们更新我们的文章和用户模型：

```
class Article < ActiveRecord::Base
  has_many :readings
  has_many :users, :through => :readings
end
```

```
class User < ActiveRecord::Base
  has_many :readings
  has_many :articles, :through => :readings
end
```

两个新的 `has_many` 声明上的 `:through` 选项告诉 Rails，`readings` 表可以用于从（例如）一篇文章导航到阅读过该文章的多个用户。现在我们可以编写如下代码：

```
readers = an_article.users
```

在幕后，Rails 构造必要的 SQL 来返回所有在 `readers` 表中被引用的用户行，这些 `readers` 行引用了原始文章。（呼！）

`:through` 参数指定在原始模型类中要导航通过的关联。因此，当我们这样说时：

```
class Article < ActiveRecord::Base
  has_many :readings
  has_many :users, :through => :readings
end
```

`:through => :readings` 参数告诉 Active Record 使用 `has_many :readings` 关联来查找名为 Reading 的模型。

我们给关联起的名字（此处为 `:users`）然后告诉 Active Record 使用哪个属性来查找用户（`user_id`）。你可以通过向 `has_many` 声明添加 `:source` 参数来更改这一点。例如，到目前为止，我们称阅读过文章的人为 `users`，仅仅因为这是 Reading 模型中关联的名字。然而，我们可以很容易地改称他们为 `readers`——我们只需要覆盖所使用的关联名称：

```
class Article < ActiveRecord::Base
  has_many :readings
  has_many :readers, :through => :readings, :source => :user
end
```

事实上，我们还可以更进一步。这仍然是一个 `has_many` 声明，所以它会接受所有 `has_many` 参数。

例如，让我们创建一个关联，返回所有给我们文章打了四星或更高评分的用户：

```
class Article < ActiveRecord::Base
  has_many :readings
  has_many :readers, :through => :readings, :source => :user
  has_many :happy_users, :through => :readings, :source => :user,
    :conditions => 'readings.rating >= 4'
end
```

## 去除重复

`has_many :through` 返回的集合只是跟随底层连接关系的结果。如果某个用户阅读了一篇特定文章三次，那么向那篇文章询问其用户列表将返回该用户模型的三个副本（连同其他阅读过该文章的用户）。有两种方法可以去除这些重复。

首先，我们可以向 `has_many` 声明添加 `:uniq => true` 限定符：

```
class Article < ActiveRecord::Base
  has_many :readings
  has_many :users, :through => :readings, :uniq => true
end
```

这完全在 Active Record 内部实现；数据库返回完整的一组行，然后 Active Record 处理它并消除任何重复的对象。

还有一种技巧可以让我们在数据库中去重。我们可以覆盖 Active Record 生成的 SQL 的 `select` 部分，添加 `distinct` 限定符。我们必须记得添加表名，因为生成的 SQL 语句中包含一个连接。

```
class Article < ActiveRecord::Base
  has_many :readings
  has_many :users, :through => :readings, :select => "distinct users.*"
end
```

我们可以使用 `<<` 方法（别名为 `push`）创建新的 `:through` 关联。关联的两端都必须事先保存，这样才行。

```
class Article < ActiveRecord::Base
  has_many :readings
  has_many :users, :through => :readings
end
```

```
user = User.create(:name => "dave")
article = Article.create(:name => "Join Models")

article.users << user
```

我们还可以使用 `create!` 在关联的远端创建一行。
