

哦，不。我们的登录未被识别，并且我们被重定向到了登录页面。此时我们需要了解一些关于 HTTP 认证的知识，因为我们的客户端显然无法理解我们设置的表单。事实上，客户端（在本例中为单行命令和我们创建的存根）并不理解 cookie 或会话。

HTTP 基本认证并不复杂，而且从 Rails 2.0 开始，Rails 就为其提供了直接支持。我们的认证逻辑位于 app/controllers/application.rb 中，因此我们将用以下内容替换 unless 子句的主体：

```
authenticate_or_request_with_http_basic('Depot') do |username, password|
  user = User.authenticate(username, password)
  session[:user_id] = user.id if user
end
```

有了这段代码，我们再试一次：

```
depot_client> ruby script/console
Loading development environment (Rails 2.2.2)
>> Product.find(2).title
=> "Pragmatic Project Automation"
```

成功！

请注意，我们所做的更改会影响用户界面。管理员将不再看到登录表单；他们将看到浏览器提供的弹出窗口。流程会自动变得“友好”，因为一旦提供正确的用户名和密码，你就会直接进入请求的页面，而不会重定向。

一个缺点是注销不再按预期工作。是的，会话被清空了，但下次访问页面时，大多数浏览器会自动提供之前的凭据，登录将自动发生。部分解决方案是使用会话来指示用户已注销，然后在这种情况下使用原始登录表单：

```
class AdminController < ApplicationController
  # just display the form and wait for user to
  # enter a name and password
  def login
    if request.post?
      user = User.authenticate(params[:name], params[:password])
      if user
        session[:user_id] = user.id
        redirect_to(:action => "index")
      else
        flash.now[:notice] = "Invalid user/password combination"
      end
    end
  end
end
```

让我们更大胆一点。何不为这本书提供 5 美元的折扣呢？

```
depot_client> ruby script/console
Loading development environment (Rails 2.2.2)
>> p = Product.find(2)
=> #<Product:0x282e7ac @prefix_options={}, ... >
>> puts p.price
29.95
=> nil
>> p.price -= 5
=> #<BigDecimal:0x282b958,'0.2495E2',8(16)>
>> p.save
=> true
```

这看起来似乎太好了而不真实。但我们可以通过简单地在浏览器中访问商店来非常容易地验证这一点：

![](img/a160fc3a330a0b3b2a764d41d614e688_630_0.png)

我们不知道你怎么想，但对我们来说，Active Resource 看起来是一种如此精妙、先进的技术，以至于与魔法无法区分。

## 26.3 关系和集合

在 Products 上取得成功后，让我们继续进行 Orders。我们先写一个存根：

Download `depot_client/app/models/order.rb`

```
class Order < ActiveResource::Base
  self.site = 'http://dave:secret@localhost:3000/'
end
```

看起来不错。让我们试试：

```
depot_client> ruby script/console
>> Order.find(1).name
=> "Dave Thomas"
>> Order.find(1).line_items
NoMethodError: undefined method `line_items' for #<Order:0x2818970>
```

好吧，此时，我们需要了解幕后是如何工作的。回到理论，但不用担心，没多少。

魔法的运作方式是利用脚手架提供的所有 REST 和 XML 接口。要获取产品列表，它会访问 http://localhost:3000/products.xml。要获取产品 #2，它将 GET http://rubymac:3000/products/2.xml。要保存对产品 #2 的更改，它将把更新后的产品 PUT 到 http://rubymac:3000/products/2.xml。

所以，这就是魔法的本质——生成 URL，很像第 21 章 Action Controller: Routing and URLs 中讨论的那样，第 425 页。以及生成（和消费）XML，很像第 12 章 Task G: One Last Wafer-Thin Change 中讨论的那样，第 181 页。让我们看看实际效果。首先我们将 line items 作为 order 的嵌套资源。我们通过编辑服务器应用程序中的 `config/routes.rb` 文件来做到这一点：

```
map.resources :orders, :has_many => :line_items
```

添加此项后，我们需要重新启动服务器。

现在更改 line items 控制器，使其查找 params 中的 :order_id 并将其视为 line item 的一部分：

```
def create
  params[:line_item][:order_id] ||= params[:order_id]
  @line_item = LineItem.new(params[:line_item])

  respond_to do |format|
    if @line_item.save
      flash[:notice] = 'LineItem was successfully created.'
      format.html { redirect_to(@line_item) }
      format.xml  { render :xml => @line_item, :status => :created,
                    :location => @line_item }
    else
      format.html { render :action => "new" }
      format.xml  { render :xml => @line_item.errors,
                    :status => :unprocessable_entity }
    end
  end
end
```

让我们获取数据，只为看看它是什么样子的：

```
<?xml version="1.0" encoding="UTF-8"?>
<line-items type="array">
  <line-item>
    <created-at type="datetime">2008-09-10T11:44:25Z</created-at>
    <id type="integer">1</id>
    <order-id type="integer">1</order-id>
    <product-id type="integer">3</product-id>
    <quantity type="integer">1</quantity>
    <total-price type="decimal">22.8</total-price>
    <updated-at type="datetime">2008-09-10T11:48:27Z</updated-at>
  </line-item>
  <line-item>
    <created-at type="datetime">2008-09-10T11:47:49Z</created-at>
    <id type="integer">2</id>
    <order-id type="integer">2</order-id>
    <product-id type="integer">2</product-id>
    <quantity type="integer">2</quantity>
    <total-price type="decimal">59.9</total-price>
    <updated-at type="datetime">2008-09-10T11:47:49Z</updated-at>
  </line-item>
  <line-item>
    <created-at type="datetime">2008-09-10T11:48:27Z</created-at>
    <id type="integer">3</id>
    <order-id type="integer">1</order-id>
    <product-id type="integer">2</product-id>
    <quantity type="integer">1</quantity>
    <total-price type="decimal">0.0</total-price>
    <updated-at type="datetime">2008-09-10T11:48:27Z</updated-at>
  </line-item>
</line-items>
```

现在让我们给 Dave 的首次购买提供 20% 的折扣：

```
>> li = LineItem.find(:all, :params => {:order_id=>1}).first
=> #<LineItem:0x2823334 @prefix_options={:order_id=>1}, ... >
>> puts li.total_price
28.5
=> nil
>> li.total_price *= 0.8
=> 22.8
>> li.save
=> true
```

所以，这里的一切都按预期工作。一件事需要注意的是 :params 的使用。这正如你对 URL 生成所期望的那样进行处理。与 ActiveResource 类提供的站点模板匹配的参数将被替换。而剩余的参数将被附加为查询参数。服务器使用 URL 进行路由，并将参数作为 `params` 数组提供。

最后，让我们在订单中添加一个 line item：

```
>> li2 = LineItem.new(:order_id=>1, :product_id=>2, :quantity=>1,
>> :total_price=>0.0)
=> #<LineItem:0x28142bc @prefix_options={:order_id=>1},
@attributes={"quantity"=>1, "product_id"=>2, "total_price"=>0.0}>
>> li2.save
=> true
```

## 26.4 整合一切

虽然 ActiveResource 起初看起来像是一种魔法，但它只是大量依赖于本书前面描述的概念。以下是一些提示：

- 认证使用你的网站已支持的底层认证机制，并且不会违背 Web 的原则，就像某些其他协议倾向于做的那样。无论如何，没有人能用 Active Resource 做任何他们以前不能做的事情。

  请注意，如果你使用基本认证，你希望使用 TLS/SSL（又名 HTTPS）来确保密码不会被嗅探。

- 虽然 Active Resource 没有有效地使用会话或 cookie，但这并不意味着你的服务器不再继续生成它们。你希望为 Active Resource 使用的接口关闭会话，或者你希望确保使用基于 cookie 的会话。否则，服务器最终会管理大量永远不需要的会话。有关更多详细信息，请参阅第 22.2 节 Rails Sessions，第 477 页。

- 在第 21.3 节 Adding Your Own Actions，第 451 页中，我们描述了集合和成员。ActiveResource 为处理集合定义了四个类方法，为处理成员定义了四个实例方法。这些方法的名称为 get、post、put 和 delete。方法名称决定了使用的底层 HTTP 方法。

  这些方法中的每一个的第一个参数是集合或成员的名称。此信息只是用于构造 URL。你可以指定额外的 :params，这些参数要么与 self.site 中的值匹配，要么作为查询参数添加。

  你可能会发现自己比预期更频繁地使用它。不是获取所有订单，你可能希望提供一个仅获取最近订单或逾期订单的接口。你可以在这些方法中做的事情仅受你的想象力的限制。

- Active Resource 将 HTTP 状态码映射为异常：

  | HTTP 状态码 | 异常 |
  | --- | --- |
  | 301, 302 | ActiveResource::Redirection |
  | 400 | ActiveResource::BadRequest |
  | 401 | ActiveResource::UnauthorizedAccess |
  | 403 | ActiveResource::ForbiddenAccess |
  | 404 | ActiveResource::ResourceNotFound |

