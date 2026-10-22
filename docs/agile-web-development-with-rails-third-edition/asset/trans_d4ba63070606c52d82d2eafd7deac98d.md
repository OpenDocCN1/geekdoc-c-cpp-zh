
## 大卫说...

### 选择好的夹具名称

就像一般变量的命名一样，你希望夹具的名称尽可能自解释。当你断言 orders(:valid_order_for_fred) 确实是 Fred 的有效订单时，这能提高测试的可读性。这也让你更容易记住要针对哪个夹具进行测试，而无需再去查 p1 或 order4。夹具越多，选择好的夹具名称就越重要。因此，尽早这样做会让你以后更轻松。

但对于那些不容易像 valid_order_for_fred 这样获得自解释名称的夹具，我们该怎么办呢？选择那些更容易与角色关联的自然名称。例如，不要使用 order1，而使用 christmas_order；不要使用 customer1，而使用 fred。一旦你养成了使用自然名称的习惯，很快你就能编出一个小故事：fred 先用他的 invalid_credit_card 为他的 christmas_order 付款，然后用他的 valid_credit_card 付款，最后选择把一切都运送给 aunt_mary。

基于关联的故事是轻松记住大量夹具世界的关键。

显然，一种方法是使用模型中的查找方法来读取数据。不过，Rails 提供了更简便的方式。对于加载到测试中的每个夹具，Rails 都会定义一个与夹具同名的方法。你可以用这个方法访问包含该夹具数据的预加载模型对象：只需向其传递 YAML 夹具文件中定义的行名，它就会返回一个包含该行数据的模型对象。以我们的产品数据为例，调用 products(:ruby_book) 会返回一个包含我们在夹具中定义的数据的 Product 模型。让我们用这个来测试产品标题唯一性的验证：

下载：depot_r/test/unit/product_test.rb

```
test "unique title" do
  product = Product.new(:title      => products(:ruby_book).title,
                        :description => "yyy",
                        :price      => 1,
                        :image_url  => "fred.gif")

  assert !product.save
  assert_equal "has already been taken", product.errors.on(:title)
end
```

该测试假设数据库中已经包含了一行 Ruby 书的数据。它使用以下方式获取该现有行的标题：

```
products(:ruby_book).title
```

然后它创建一个新的 Product 模型，将其标题设置为该现有标题。它断言尝试保存此模型会失败，并且 title 属性关联了正确的错误。

如果你想避免为 Active Record 错误使用硬编码字符串，可以将响应与其内置的错误消息表进行比较：

```
test "unique title1" do
  product = Product.new(:title      => products(:ruby_book).title,
                        :description => "yyy",
                        :price      => 1,
                        :image_url  => "fred.gif")

  assert !product.save
  assert_equal I18n.translate('activerecord.errors.messages.taken'),
               product.errors.on(:title)
end
```

（要查看这些内置错误消息的列表，请在 Active Record gem 中查找 validations.rb 文件。在下一页的图 14.1 中，我们可以看到本章编写时的错误列表，但当你阅读时它可能已经发生了变化。）

## 测试购物车

我们的 Cart 类包含一些业务逻辑。当我们向购物车添加产品时，它会检查该产品是否已经在购物车的商品列表中。如果是，则增加该商品的数量；如果不是，则为该产品添加一个新商品。让我们为这个功能编写一些测试。

Rails generate 命令创建了源文件，用于存放我们应用中数据库支持模型的单元测试。但购物车呢？我们是手工创建 Cart 类的，在单元测试目录中没有与之对应的文件。别绝望！我们只需创建一个。只需将另一个测试文件中的样板代码复制到一个新的 cart_test.rb 文件中（记得将类重命名为 CartTest）：

```
require 'test_helper'

class CartTest < ActiveSupport::TestCase
  fixtures :products
end
```

```
{
  :inclusion => "is not included in the list",
  :exclusion => "is reserved",
  :invalid => "is invalid",
  :confirmation => "doesn't match confirmation",
  :accepted => "must be accepted",
  :empty => "can't be empty",
  :blank => "can't be blank",
  :too_long => "is too long (maximum is %d characters)",
  :too_short => "is too short (minimum is %d characters)",
  :wrong_length => "is the wrong length (should be %d characters)",
  :taken => "has already been taken",
  :not_a_number => "is not a number",
  :greater_than => "must be greater than %d",
  :greater_than_or_equal_to => "must be greater than or equal to %d",
  :equal_to => "must be equal to %d",
  :less_than => "must be less than %d",
  :less_than_or_equal_to => "must be less than or equal to %d",
  :odd => "must be odd",
  :even => "must be even"
}
```

### 图 14.1：标准 Active Record 验证消息

注意，我们已将现有的 products 夹具包含在此测试中。这是一种常见做法：我们经常希望在多个测试用例之间共享测试数据。在这种情况下，购物车测试需要访问产品数据，因为我们将向购物车添加产品。

因为我们需要测试向购物车添加不同的产品，所以需要至少再往我们的 products.yml 夹具中添加一个产品。完整的文件现在看起来像这样：

下载：depot/test/fixtures/products.yml

```
ruby_book:
  title: Programming Ruby
  description: Dummy description
  price: 1234
  image_url: ruby.png

rails_book:
  title: Agile Web Development with Rails
  description: Dummy description
  price: 2345
  image_url: rails.png
```

下载：depot_r/test/unit/cart_test.rb

```
require 'test_helper'

class CartTest < ActiveSupport::TestCase
  fixtures :products

  def setup
    @cart = Cart.new
    @rails = products(:rails_book)
    @ruby = products(:ruby_book)
  end

  def test_add_unique_products
    @cart.add_product @rails
    @cart.add_product @ruby
    assert_equal 2, @cart.items.size
    assert_equal @rails.price + @ruby.price, @cart.total_price
  end

  def test_add_duplicate_product
    @cart.add_product @rails
    @cart.add_product @rails
    assert_equal 2*@rails.price, @cart.total_price
    assert_equal 1, @cart.items.size
    assert_equal 2, @cart.items[0].quantity
  end
end
```

这种设置对特定的测试有用吗？两种观点都有道理。但是，当我们看功能测试时，我们会发现 setup 方法可以在保持测试一致性方面发挥关键作用。

## 单元测试支持

在编写单元测试时，你最终可能会使用下面列表中的大部分断言：

```
assert(boolean,message)
    Fails if boolean is false or nil.
    assert(User.find_by_name("dave"), "user 'dave' is missing")
```

```
assert_equal(expected, actual,message)
assert_not_equal(expected, actual,message)
    Fails unless expected and actual are/are not equal.
    assert_equal(3, Product.count)
    assert_not_equal(0, User.count, "no users in database")
```

## 14.3 控制器的功能测试

控制器掌控全局。它们接收传入的 Web 请求（通常是用户输入），与模型交互以收集应用程序状态，然后通过让适当的视图向用户显示内容来作出响应。因此，在测试控制器时，我们要确保给定的请求能得到适当的响应。我们仍然需要模型，但单元测试已经覆盖了它们。

Rails 将测试单个控制器的测试称为功能测试。Depot 应用有四个控制器，每个控制器都有许多动作。这里有很多东西可以测试，但我们会挑一些重点来讲解。让我们从用户开始的地方开始——登录。

### 管理员

如果任何人都能来管理 Depot 应用，那就不妙了。虽然我们可能没有复杂的安全系统，但我们希望确保 admin 控制器至少能挡住那些不速之客。

由于 AdminController 是用 generate controller 脚本创建的，Rails 在 test/functional 目录中为我们准备了一个测试桩：

下载：depot_r/test/functional/admin_controller_test.rb

```
require 'test_helper'

class AdminControllerTest < ActionController::TestCase
  # Replace this with your real tests.
  test "the truth" do
    assert true
  end
end
```

功能测试的关键是 ActionController::TestCase 父类。它初始化了每次功能测试所需的三个实例变量。

- @controller 包含被测控制器的一个实例。
- @request 包含一个请求对象。在运行中的实际应用程序里，请求对象包含传入请求的所有细节和数据，包括 HTTP 头信息、POST 或 GET 数据等。在测试环境中，我们使用请求对象的一个特殊测试版本，它无需真实传入的 HTTP 请求即可初始化。
- @response 包含一个响应对象。虽然在编写应用程序时我们还没有见过响应对象，但我们一直在使用它们。每次处理来自浏览器的请求时，Rails 都会在幕后填充一个响应对象。模板将数据渲染到响应对象中，我们想要返回的状态码记录在

