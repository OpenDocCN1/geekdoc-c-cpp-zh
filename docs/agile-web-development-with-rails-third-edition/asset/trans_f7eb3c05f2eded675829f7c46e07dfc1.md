

```
part :content_type => "text/html",
    :body => render_message("sent", :order => order)

order.line_items.each do |li|
  image = li.product.image_location
  content_type = case File.extname(image)
  when ".jpg", ".jpeg";  "image/jpeg"
  when ".png";            "image/png"
  when ".gif";            "image/gif"
  else;                    "application/octet-stream"
  end

  attachment :content_type => content_type,
             :body          => File.read(File.join("public", image)),
             :filename      => File.basename(image)
end
end
```

注意这次我们显式地使用 part 指令渲染消息，强制其类型为 text/html，主体为渲染模板的结果。³ 然后我们遍历订单中的行项目。对于每个项目，我们确定图像文件的名称，根据文件扩展名构造 MIME 类型，并将文件作为内联附件添加。

## 25.2 接收电子邮件

Action Mailer 使编写处理传入电子邮件的 Rails 应用变得容易。不幸的是，你还需要找到一种方法从服务器环境获取适当的电子邮件并将其注入到应用中；这需要做更多的工作。

在应用内部处理电子邮件是容易的部分。在你的 Action Mailer 类中，编写一个名为 receive 的实例方法，它接受一个参数。该参数将是一个 TMail::Mail 对象，对应于传入的电子邮件。你可以提取字段、正文文本和/或附件，并在应用中使用它们。

例如，一个 bug 跟踪系统可能会通过电子邮件接受故障单。从每封电子邮件中，它构造一个包含基本票据信息的 Ticket 模型对象。如果电子邮件包含附件，每个附件都将被复制到一个新的 TicketCollateral 对象中，该对象与新票据关联。

3. 在撰写本文时，Rails 中存在一个小错误（ticket 3332）。如果消息有附件，Rails 在你使用 xxx.text.html.erb 命名约定命名它时不会渲染消息的默认模板。使用 part 显式添加内容可以正常工作。该错误已修复。

```
RUBY=/Users/dave/ruby1.8/bin/ruby
TICKET_APP_DIR=/Users/dave/Work/BS2/titles/RAILS/Book/code/e1/mailer
HANDLER='IncomingTicketHandler.receive(STDIN.read)'

:0 c
* ^Subject:.*Bug Report.*
| cd $TICKET_APP_DIR && $RUBY script/runner $HANDLER
```

receive 类方法可用于所有 Action Mailer 类。它接受电子邮件文本，将其解析为 TMail 对象，创建接收者类的一个新实例，并将 TMail 对象传递给该类中的 receive 实例方法。这就是我们在第 620 页编写的方法。结果是，从外部世界收到的电子邮件最终会创建一个 Rails 模型对象，进而在数据库中存储一个新的故障单。

## 25.3 测试电子邮件

电子邮件测试有两个层次。在单元测试层面，你可以验证 Action Mailer 类是否正确生成电子邮件。在功能层面，你可以测试应用是否在你期望发送电子邮件时发送这些电子邮件。

### 单元测试电子邮件

当我们使用 generate 脚本创建订单邮件程序时，它自动在应用的 test/unit 目录中构造了对应的 order_mailer_test.rb 文件。如果你查看该文件，会发现它相当复杂。那是因为它允许你从 fixture 文件读取电子邮件的预期内容，并将此内容与邮件程序类生成的电子邮件进行比较。然而，这是一种相当脆弱的测试。只要你更改用于生成电子邮件的模板，就需要更改对应的 fixture。

如果对电子邮件内容的精确测试对你很重要，那么请使用预生成的测试类。在 test/fixtures 目录的子目录中创建预期内容，该子目录以测试命名（因此我们的 OrderMailer fixtures 将位于 test/fixtures/order_mailer 中）。使用生成代码中包含的 read_fixture 方法读取特定 fixture 文件并将其与模型生成的电子邮件进行比较。

然而，我们更喜欢更简单的方法。就像我们不会测试模板生成的网页的每个字节一样，我们通常也不会费心测试生成的电子邮件的全部内容。相反，我们测试最可能出错的部分：动态内容。这简化了单元测试代码，并使其对模板的小改动更具弹性。

这是一个典型的电子邮件单元测试：

Download e1/mailer/test/unit/order_mailer_test.rb

```
require 'test_helper'

class OrderMailerTest < ActionMailer::TestCase
  tests OrderMailer

  def setup
    @order = Order.new(:name => "Dave Thomas", :email => "dave@pragprog.com")
  end

  def test_confirm
    response = OrderMailer.create_confirm(@order)
    assert_equal("Pragmatic Store Order Confirmation", response.subject)
    assert_equal("dave@pragprog.com", response.to[0])
    assert_match(/Dear Dave Thomas/, response.body)
  end
end
```

setup 方法为邮件发送者创建一个订单对象。在测试方法中，我们让邮件类创建（但不发送）一封电子邮件，并使用断言验证动态内容是否符合预期。注意使用 assert_match 来验证正文内容的一部分。

### 电子邮件的功能测试

现在我们知道可以为订单创建电子邮件，我们希望确保应用在正确的时间发送正确的电子邮件。这是功能测试的工作。

让我们开始为我们的应用生成一个新的控制器：

```
depot> ruby script/generate controller Order confirm
```

我们将实现单个 action confirm，它为新订单发送确认电子邮件：

Download e1/mailer/app/controllers/order_controller.rb

```
class OrderController < ApplicationController
  def confirm
    order = Order.find(params[:id])
    OrderMailer.deliver_confirm(order)
    redirect_to(:action => :index)
  end
end
```

我们在第 14.3 节《控制器的功能测试》，第 224 页看到了 Rails 如何为生成的控制器构造 stub 功能测试。我们将把邮件测试添加到此生成的测试中。

Action Mailer 在测试环境中不会投递电子邮件。相反，它将生成的每封电子邮件添加到数组 ActionMailer::Base.deliveries 中。我们将使用它

来获取控制器生成的电子邮件。我们将在生成的测试的 setup 方法中添加几行代码。一行将此数组别名为更易管理的名称 emails。第二行在每次测试开始时清空该数组。

```
Download e1/mailer/test/functional/order_controller_test.rb

@emails = ActionMailer::Base.deliveries
@emails.clear
```

我们还需要一个包含示例订单的 fixture。我们将在 test/fixtures 目录中创建一个名为 orders.yml 的文件：

```
Download e1/mailer/test/fixtures/orders.yml

daves_order:
  id: 1
  name: Dave Thomas
  address: 123 Main St
  email: dave@pragprog.com
```

现在我们可以为我们的 action 编写测试。以下是测试类的完整源代码：

```
Download e1/mailer/test/functional/order_controller_test.rb

require 'test_helper'

class OrderControllerTest < ActionController::TestCase

  fixtures :orders

  def setup
    @controller = OrderController.new
    @request    = ActionController::TestRequest.new
    @response   = ActionController::TestResponse.new

    @emails     = ActionMailer::Base.deliveries
    @emails.clear
  end

  def test_confirm
    get(:confirm, :id => orders(:daves_order).id)
    assert_redirected_to(:action => :index)
    assert_equal(1, @emails.size)
    email = @emails.first
    assert_equal("Pragmatic Store Order Confirmation", email.subject)
    assert_equal("dave@pragprog.com", email.to[0])
    assert_match(/Dear Dave Thomas/, email.body)
  end
end
```

它使用 emails 别名访问自测试开始运行以来 Action Mailer 生成的电子邮件数组。在检查列表中恰好有一封电子邮件后，它随后验证内容是我们期望的。

我们可以通过使用 rake 的 test_functional 目标或直接执行脚本来运行此测试：

```
depot> ruby test/functional/order_controller_test.rb
```
