

与其让产品表变得杂乱，我们将它保存在一个辅助的详情表中：

```
class CreateDetails < ActiveRecord::Migration
  def self.up
    create_table :details do |t|
      t.integer :product_id
      t.string :sku
      t.string :manufacturer
    end
  end

  def self.down
    drop_table :details
  end
end
```

模型同样简单：

```
class Detail < ActiveRecord::Base
  belongs_to :product
  validates_presence_of :sku
end
```

视图使用 form_for 来捕获产品模型的字段，并在该表单中使用 fields_for 调用来捕获详情模型的数据：

```
<% form_for :product, :url => { :action => :create } do |form| %>
  <%= error_messages_for :product %>
  Title: <%= form.text_field :title %><br/>
  Description: <%= form.text_area :description, :rows => 3 %><br/>
  Image url: <%=form.text_field :image_url %><br/>

  <fieldset>
    <legend>Details...</legend>
    <%= error_messages_for :details %>
    <% fields_for :details do |detail| %>
      SKU: <%= detail.text_field :sku %><br/>
      Manufacturer: <%= detail.text_field :manufacturer %>
    <% end %>
  </fieldset>
  <%= submit_tag %>
<% end %>
```

我们可以查看生成的 HTML 来了解其工作原理：

```
<form action="/products/create" method="post">
  Title:
  <input id="product_title" name="product[title]" size="30" type="text" /><br/>
  Description:
  <textarea cols="40" id="product_description"
    name="product[description]" rows="3"></textarea><br/>
```

```
Image url:
<input id="product_image_url" name="product[image_url]" size="30" type="text" /></br>

<fieldset>
<legend>Details...</legend>
SKU:
<input id="details_sku" name="details[sku]" size="30" type="text" /></br>
Manufacturer:
<input id="details_manufacturer" name="details[manufacturer]" size="30" type="text" />
</fieldset>

<input name="commit" type="submit" value="Save changes" />
</form>
```

注意详情模型的字段是如何被恰当地命名的，确保其数据会以正确的子哈希形式返回在 params 中。

用于初始渲染此表单的新建 action，仅仅创建两个新的模型对象：

Download e1/views/app/controllers/products_controller.rb

```
def new
  @product = Product.new
  @details = Detail.new
end
```

create action 负责接收表单数据并将模型保存回数据库。它比单个模型保存复杂得多。这是因为它必须考虑两个因素：

- 如果任一模型包含无效数据，则不应保存任一模型。
- 如果两个模型都包含验证错误，我们希望显示来自两个模型的错误信息——也就是说，我们不想在发现一个模型有问题时就停止检查错误。

我们的解决方案使用事务和异常处理器：

Download e1/views/app/controllers/products_controller.rb

```
def create
  @product = Product.new(params[:product])
  @details = Detail.new(params[:details])

  Product.transaction do
    @product.save!
    @details.product = @product
    @details.save!
    redirect_to :action => :show, :id => @product
  end

```
```
rescue ActiveRecord::RecordInvalid => e
  @details.valid?  # force checking of errors even if products failed
  render :action => :new
end
```

这应该足以让你入门。对于需要更多的人，请参阅 *Advanced Rails Recipes* [Cla08] 中的 Recipe 13。

## 错误处理和模型对象

我们迄今为止在本章中看到的各种辅助小部件都知道 Active Record 模型。它们可以从模型对象的属性中提取所需的数据，并且以模型可以从请求参数中提取的方式命名其参数。

辅助对象以另一种重要方式与模型交互；它们知道每个模型中保存的 errors 结构，并会使用它来标记验证失败的属性。

在为模型中的每个字段构造 HTML 时，辅助方法会调用该模型的 errors.on(field) 方法。如果返回任何错误，生成的 HTML 将被包裹在 class="fieldWithErrors" 的 <div> 标签中。如果你将适当的样式表应用到你的页面上（我们在第 520 页见过如何做），你就可以突出显示任何出错的字段。例如，以下 CSS 片段取自脚手架生成的代码使用的样式表，会在验证失败的字段周围放置红色边框：

```
.fieldWithErrors {
  padding:        2px;
  background-color:  red;
  display:        table;
}
```

除了突出显示出错的字段，你可能还想显示错误信息的文本。Action View 为此提供了两个辅助方法。error_message_on 返回与特定字段关联的错误文本：

```
<%= error_message_on(:product, :title) %>
```

脚手架生成的代码使用不同的模式；它突出显示出错的字段，并在表单顶部显示一个单一的框来显示表单中的所有错误。它使用 error_messages_for 来实现这一点，该方法将模型对象作为参数接收：

```
<%= error_messages_for(:product) %>
```

我们如何让 Rails 使用我们漂亮的新表单构建器？我们只需向 form_for 添加一个 :builder 参数即可：

```
Download e1/views/app/views/builder/new.html.erb
<% form_for :product, :url => { :action => :save },
  :builder => TaggedBuilder do |form| %>
  <%= form.text_field 'title' %>
  <%= form.text_area 'description' %>
  <%= form.text_field 'image_url' %>
  <%= submit_tag %>
<% end %>
```

如果我们计划在多个表单中使用新的构建器，我们可能希望定义一个辅助方法，它的作用与 form_for 相同，但会自动添加 builder 参数。因为它是一个常规辅助方法，我们可以把它放在 helpers/application_helper.rb 中（如果我们想使其全局可用）或放在特定控制器的 helper 文件中。

理想情况下，辅助方法看起来像这样：

```
# DOES NOT WORK
def tagged_form_for(name, options, &block)
  options = options.merge(:builder => TaggedBuilder)
  form_for(name, options, &block)
end
```

然而，form_for 有可变长度的参数列表——它接受一个可选的第二个参数，其中包含模型对象。我们需要考虑这一点，使得我们的最终辅助方法变得稍微复杂一些：

```
Download e1/views/app/helpers/builder_helper.rb
module BuilderHelper
  def tagged_form_for(name, *args, &block)
    options = args.last.is_a?(Hash) ? args.pop : {}
    options = options.merge(:builder => TaggedBuilder)
    args = (args << options)
    form_for(name, *args, &block)
  end
end
```

我们的最终视图文件现在非常优雅：

```
Download e1/views/app/views/builder/new_with_helper.html.erb
<% tagged_form_for :product, :url => { :action => :save } do |form| %>
  <%= form.text_field 'title' %>
  <%= form.text_area 'description' %>
  <%= form.text_field 'image_url' %>
  <%= submit_tag %>
<% end %>
```

表单构建器是 Rails 中默默无闻的英雄。你可以使用它们在整个应用程序中建立一致且 DRY 的外观和感觉，并且

你可以将它们在应用程序之间共享，以在你的用户交互上施加公司范围内的标准。它们在你需要遵循应用程序的可访问性指南时也会有所帮助。我们建议为所有 Rails 表单使用表单构建器。

## 包含集合的表单

如果你需要在一个表单中编辑来自同一模型的多个对象，请在传递给表单辅助方法的实例变量名称中添加打开和关闭的方括号。这告诉 Rails 将对象的 id 作为字段名称的一部分包含在内。例如，以下模板允许用户更改与产品列表关联的一个或多个图像 URL：

```
Download e1/views/app/views/array/edit.html.erb

<%= form_tag do %>
  <% for @product in @products %>
    <%= text_field("product[]", 'image_url') %><br />
  <% end %>
  <%= submit_tag %>
<% end %>
```

当表单提交到控制器时，params[:product] 将是一个哈希的哈希，其中每个键是模型对象的 id，对应的值是该对象在表单中的值。在控制器中，这可以用来更新所有产品行，例如这样：

```
Download e1/views/app/controllers/array_controller.rb

Product.update(params[:product].keys, params[:product].values)
```

## 23.7 使用非模型字段

到目前为止，我们一直专注于 Rails 中模型、控制器和视图之间的集成。但 Rails 也提供了创建没有对应模型的字段的支持。这些辅助方法记录在 FormTagHelper 中，它们都接受一个简单的字段名称，而不是模型对象和属性。当表单提交到控制器时，字段的内容将以该名称存储在 params 哈希中。这些非模型辅助方法的名字都以 _tag 结尾。

我们需要创建一个表单来使用这些字段辅助方法。到目前为止我们一直在使用 form_for 来实现这一点，但这假设我们在围绕模型对象构建表单，而这在使用低级辅助方法时不一定是这种情况。

我们本可以把 <form> 标签硬编码到我们的 HTML 中，但 Rails 有更好的方法：使用 form_tag 辅助方法创建一个表单。就像 form_for 一样，form_tag 应该

