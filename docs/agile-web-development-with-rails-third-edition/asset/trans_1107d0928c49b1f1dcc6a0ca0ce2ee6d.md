

```
:too_long      => "is too long (maximum is %d characters)",
:too_short      => "is too short (minimum is %d characters)",
:wrong_length  => "is the wrong length (should be %d characters)",
:taken          => "has already been taken",
:not_a_number   => "is not a number",
:greater_than   => "must be greater than %d",
:greater_than_or_equal_to => "must be greater than or equal to %d",
:equal_to       => "must be equal to %d",
:less_than      => "must be less than %d",
:less_than_or_equal_to => "must be less than or equal to %d",
:odd            => "must be odd",
:even           => "must be even"
```

要更改唯一性验证失败时返回的消息，你可以在你的 config/locales/en.yml 文件中编写如下代码：

```
en:
  activerecord:
    errors:
      taken: "is in use"
```

## 20.2 回调

Active Record 控制着模型对象的生命周期——它创建模型对象，在它们被修改时进行监控，保存和更新它们，并目送它们被销毁。通过回调，Active Record 让我们的代码能够参与到这个监控过程中来。我们可以编写代码，在对象生命周期中的任何重要事件发生时被调用。借助这些回调，我们可以执行复杂的验证，在列值进出数据库时进行映射，甚至可以阻止某些操作完成。

Active Record 定义了二十个回调。其中十八个形成 before/after 对，环绕对 Active Record 对象的某个操作。例如，before_destroy 回调会在 destroy 方法被调用之前被调用，而 after_destroy 会在之后被调用。两个例外是 after_find 和 after_initialize，它们没有对应的 before_xxx 回调。（这两个回调在其他方面也有所不同，我们稍后会看到。）

在图 20.1 中（见下页），我们可以看到这十八个成对回调是如何环绕模型对象的基本 create、update 和 destroy 操作的。也许令人惊讶的是，验证前后的调用并不是严格嵌套的。

除了这十八个调用之外，after_find 回调会在任何 find 操作之后被调用，而 after_initialize 会在一个 Active Record 模型对象被创建之后被调用。

要让你的代码在回调期间执行，你需要编写一个处理器，并将其与相应的回调关联起来。

![](img/a160fc3a330a0b3b2a764d41d614e688_407_0.png)

## 图 20.1：Active Record 回调的顺序

实现回调有两种基本方式。

```
class Order < ActiveRecord::Base
  # ...
  def before_save
    self.payment_due ||= Time.now + 30.days
  end
end
```

定义回调的第二种基本方式是声明处理器。处理器可以是方法或块。¹ 你可以使用以事件命名的类方法将处理器关联到特定事件。要关联一个方法，请将其声明为 private 或 protected，并在处理器声明中将其名称指定为符号。要指定一个块，只需在声明后添加它。这个块会接收模型对象作为参数。

```
class Order < ActiveRecord::Base

  before_validation :normalize_credit_card_number

  after_create do |order|
    logger.info "Order #{order.id} created"
  end
```

1. 处理器也可以是包含要 eval 的代码的字符串，但这已弃用。

要完全禁用此行为，请使用以下代码：

```
ActiveRecord::Base.record_timestamps = false
```

## 回调对象

作为直接在模型类中指定回调处理器的一种变体，你可以创建单独的处理器类来封装所有回调方法。这些处理器可以在多个模型之间共享。处理器类就是一个定义了回调方法（before_save、after_create 等）的类。在 app/models 中为这些处理器类创建源文件。

在使用处理器的模型对象中，你创建该处理器类的一个实例，并将该实例传递给各种回调声明。几个例子会让这一点更清楚。

```
class CreditCardCallbacks
  # Normalize the credit card number
  def before_validation(model)
    model.cc_number.gsub(/[-\s]/, '')
  end
end
```

现在，在我们的模型类中，我们可以安排调用这个共享回调：

```
class Order < ActiveRecord::Base
  before_validation CreditCardCallbacks.new
  # ...
end
```

```
class Subscription < ActiveRecord::Base
  before_validation CreditCardCallbacks.new
  # ...
end
```

在这个例子中，处理器类假设信用卡号存储在名为 cc_number 的模型属性中；Order 和 Subscription 都会有一个该名称的属性。但我们可以推广这个思路，使处理器类不那么依赖于使用它的类的实现细节。

现在我们可以安排从 orders 模型内部调用 Encrypter 类：

```
require "encrypter"

class Order < ActiveRecord::Base
  encrypter = Encrypter.new([:name, :email])

  before_save  encrypter
  after_save   encrypter
  after_find   encrypter

  protected
    def after_find
    end
end
```

我们创建一个新的 Encrypter 对象，并将其连接到 before_save、after_save 和 after_find 事件。这样，就在一个订单被保存之前，encrypter 中的 before_save 方法会被调用，依此类推。

那么，为什么我们要定义一个空的 after_find 方法呢？记住，我们说过出于性能原因，after_find 和 after_initialize 会被特殊对待。这种特殊对待的一个后果是，Active Record 只有在模型类中看到一个实际的 after_find 方法时，才会知道调用 after_find 处理器。我们必须定义一个空的占位符才能使 after_find 处理生效。

这一切都很好，但每个想要使用我们的加密处理器的模型类都需要包含大约八行代码，就像我们对 Order 类所做的那样。我们可以做得更好。我们将定义一个完成所有工作的辅助方法，并让该辅助方法可用于所有 Active Record 模型。为此，我们将它添加到 ActiveRecord::Base 类中：

```
Download e1/ar/encrypt.rb

class ActiveRecord::Base
  def self.encrypt(*attr_names)
    encrypter = Encrypter.new(attr_names)

    before_save  encrypter
    after_save   encrypter
    after_find   encrypter

    define_method(:after_find) { }
  end
end
```

有了这个，我们现在可以通过一次调用来为任何模型类的属性添加加密。

```
Download e1/ar/encrypt.rb
class Order < ActiveRecord::Base
  encrypt(:name, :email)
end
```

一个简单的驱动程序让我们可以对此进行实验：

```
Download e1/ar/encrypt.rb
o = Order.new
o.name = "Dave Thomas"
o.address = "123 The Street"
o.email = "dave@pragprog.com"
o.save
puts o.name

o = Order.find(o.id)
puts o.name
```

在控制台上，我们在模型对象中看到客户的名字（纯文本）：

```
ar> ruby encrypt.rb
Dave Thomas
Dave Thomas
```

然而，在数据库中，姓名和电子邮件地址被我们的工业级加密所掩盖：

```
depot> sqlite3 -line db/development.sqlite3 "select * from orders"
  id = 1
  user_id =
  name = Dbwf Tipnbt
  address = 123 The Street
  email = ebwf@qsbhq sph.dpn
```

## 观察者

回调是一种很好的技术，但它们有时会导致模型类承担与模型本质并不真正相关的责任。例如，在第 408 页，我们创建了一个在订单创建时生成日志消息的回调。该功能并不是基本 Order 类的一部分——我们把它放在那里是因为回调在那个位置执行。

Active Record 观察器克服了这一限制。观察器会透明地将自身链接到模型类中，就像它是模型的一部分一样注册回调，但不需要对模型本身进行任何更改。下面是我们之前使用观察器编写的日志记录示例：

```
Download e1/ar/observer.rb
class OrderObserver < ActiveRecord::Observer
  def after_save(an_order)
    an_order.logger.info("Order #{an_order.id} created")
  end
end
```

