

这段代码等价于之前的示例：

```
article = Article.create(:name => "Join Models")
article.users.create!(:name => "dave")
```

请注意，使用这种方法无法在中间表中设置属性。

## 扩展关联

关联声明（belongs_to、has_xxx）是对模型对象之间业务关系的陈述。相当频繁地，与该特定关联相关联的是额外的业务逻辑。在之前的示例中，我们定义了文章与其读者之间的关系，称为 Reading。该关系包含了用户对刚读过的文章的评分。给定一个用户，我们如何获取他们评分在三颗星或更高的所有文章的列表？四颗星或更高？

我们已经看到了一种方法：我们可以构建新的关联，使结果集满足某些额外条件。我们在上一页的 happy_users 关联中就是这样做的。然而，这种方法受限——我们无法参数化查询，让调用者决定什么评分算作“happy”。

另一种方法是让使用我们模型的代码在查询本身上添加额外的条件：

```
user = User.find(some_id)
user.articles.find(:all, :conditions => [ 'rating >= ?', 3])
```

这可行，但会轻微破坏封装：我们真的希望将基于评分查找文章的想法封装在 articles 关联内部。Rails 允许我们通过向任何 has_many 声明添加一个块来实现这一点。在此块中定义的任何方法都将成为关联的方法。

以下代码向 user 模型中的 articles 关联添加了 finder 方法 rated_at_or_above：

```
class User < ActiveRecord::Base
  has_many :readings
  has_many :articles, :through => :readings do
    def rated_at_or_above(rating)
      find :all, :conditions => ['rating >= ?', rating]
    end
  end
end
```

给定一个 user 模型对象，我们现在可以调用此方法来检索他们高度评分的文章列表：

```
user = User.find(some_id)
good_articles = user.articles.rated_at_or_above(4)
```

合并到单个数据库表中。该表包含层次结构中所有类的所有属性的列。它还额外包含一个列，按惯例称为 type，用于标识任何特定行所代表的特定类。这在第 19.2 图中有所说明，见下一页。

在 Active Record 中使用单表继承非常简单。在模型类中定义你需要的继承层次结构，并确保对应于层次结构基类的表包含该层次结构中所有类的所有属性的列。表还必须额外包含一个 type 列，用于区分相应模型对象的类。

在定义表时，请记住子类的属性只会出现在对应于这些子类的表行中；例如，员工没有 balance 属性。因此，你必须定义表以允许任何不在所有子类中出现的列为空值。以下是创建第 19.2 图中所示表的迁移，见下一页：

```
create_table :people, :force => true do |t|
  t.string :type

  # common attributes
  t.string :name
  t.string :email

  # attributes for type=Customer
  t.decimal :balance, :precision => 10, :scale => 2

  # attributes for type=Employee
  t.integer :reports_to
  t.integer :dept

  # attributes for type=Manager
  # -- none --
end
```

我们可以定义我们的模型对象层次结构：

```
class Person < ActiveRecord::Base
end

class Customer < Person
end

class Employee < Person
  belongs_to :boss, :class_name => "Manager", :foreign_key => :reports_to
end
```

```
Customer.create(:name => 'Bert Public', :email => "b@public.net", :balance => 12.45)

barney = Employee.new(:name => 'Barney Rub', :email => "barney@here.com", :dept => 23)

barney.boss = wilma
barney.save!
```

```
manager = Person.find_by_name("Wilma Flint")
puts manager.class      #=> Manager
puts manager.email      #=> wilma@here.com
puts manager.dept       #=> 23
```

```
customer = Person.find_by_name("Bert Public")
puts customer.class    #=> Customer
puts customer.email    #=> b@public.net
puts customer.balance  #=> 12.45
```

注意我们如何要求基类 Person 查找一行，但在一种情况下返回对象的类是 Manager，在另一种情况下是 Customer；Active Record 通过检查行的 type 列并创建适当的对象来确定类型。

还请注意我们在 Employee 类中使用的一个小技巧。我们使用 belongs_to 创建了一个名为 boss 的属性。该属性使用 reports_to 列，该列指向 people 表。这就是让我们能够说 barney.boss = wilma 的原因。

使用单表继承时有一个相当明显的限制。两个子类不能具有名称相同但类型不同的属性，因为这两个属性将映射到底层模式中的同一列。

还有一个不太明显的限制。属性 type 也是内置 Ruby 方法的名称，因此直接访问它以设置或更改行的类型可能会导致奇怪的 Ruby 消息。相反，通过创建适当类的对象隐式访问它，或通过模型对象的索引接口访问它，使用类似以下内容：

```
person[:type] = 'Manager'
```

## 多态关联

STI 的一个主要缺点是存在一个单一的底层表，其中包含继承树中所有子类的所有属性。我们可以使用 Rails 的第二种异构聚合形式——多态关联——来克服这个问题。

## Joe 提问...

## 如果我们想要真正的继承怎么办？

单表继承很聪明——只要我们子类化一个 Active Record 类，它就会自动启用。但如果我们想要真正的继承怎么办？如果我们想通过定义一个抽象基类和一组子类来在 Active Record 类的集合之间共享某些行为怎么办？

答案是在我们的抽象基类中定义一个名为 abstract_class? 的类方法。该方法应返回 true。这有两个效果。首先，Active Record 将永远不会尝试查找对应于此抽象类的数据库表。其次，此类的所有子类都将被视为独立的 Active Record 类——每个类都映射到自己的数据库表。

当然，更好的做法可能是使用包含共享功能的 Ruby 模块，并将此模块混入需要该行为的 Active Record 类中。

多态关联依赖于外键列只是一个整数这一事实。虽然有一个约定，即名为 user_id 的外键引用 users 表中的 id 列，但没有法律强制执行这一点。³

在计算机科学中，多态是一种机制，允许你抽象出某物接口的本质，而不管其底层实现如何。例如，加法方法就是多态的，因为它适用于整数、浮点数，甚至字符串。

在 Rails 中，多态关联是一种关联到不同类型对象的关联。假设这些对象都共享一些共同特征，但它们会有不同的表示。

为了具体说明，让我们看一个简单的资产管理系统。我们在简单的目录中索引我们的资产。每个目录条目包含一个名称、获取日期，以及对实际资源的引用：文章、图像、声音等等。不同资源类型对应不同的数据库表和不同的 Active Record 模型，但它们都是资产，并且都被编目。

3. 如果你指定数据库应强制执行外键约束，多态关联将无法工作。

