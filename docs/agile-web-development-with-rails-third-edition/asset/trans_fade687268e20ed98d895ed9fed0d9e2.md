

<html>
  <head>
    <title>User: <%= controller.action_name %></title>
    <%= stylesheet_link_tag 'scaffold' %>
    <%= javascript_include_tag :defaults %>
  </head>
  <body>
    <p style="color: green"><%= flash[:notice] %></p>
    <%= image_tag 'loading.gif', :id=>'spinner', :style=>"display:none; float:right;" %>
    <%= yield :layout %>
  </body>
</html>

当此模板被渲染到浏览器时，结果将是静态 HTML 和 JavaScript 代码的组合。以下是使用 observe_field 辅助方法生成的实际输出：

```
<input id="search" name="search" type="text" value="" />
<script type="text/javascript">
//<![CDATA[ 
new Form.Element.Observer('search', 0.5, function(element, value) {
  Element.show('spinner');
  new Ajax.Updater('ajaxwrapper',
    '/user/search',
    { onComplete:function(request){ Element.hide('spinner'); },
      parameters: 'search=' + encodeURIComponent(value)
    })
})
//]]>
```

现在，当用户在文本字段中输入时，字段的值将被发送到 User 控制器的 search 动作。请记住，由于我们提供了 update 参数，JavaScript 代码会将服务器返回的内容设置为目标元素的 innerHTML 属性的值。那么，search 做了什么？

```
def search
  unless params[:search].blank?
    @users = User.paginate :page => params[:page],
      :per_page => 10,
      :order => order_from_params,
      :conditions => User.conditions_by_like(params[:search])
    logger.info @users.size
  else
    list
  end
  render :partial=>'search', :layout=>false
end
```

## conditions_by_like

方法 User.conditions_by_like(params[:search]) 并不是 Active Record 的一部分。它实际上是从 Streamlined 框架中提取的代码。它提供了一种快速搜索模型中所有字段的方法。以下是完整的实现：

Download pragforms/vendor/plugins/relevance_extensions/lib/active_record_extensions.rb

```
def conditions_by_like(value, *columns)
  columns = self.user_columns if columns.size==0
  columns = columns[0] if columns[0].kind_of?(Array)
  conditions = columns.map {|c|
    c = c.name if c.kind_of? ActiveRecord::ConnectionAdapters::Column
    "#{c} LIKE " + ActiveRecord::Base.connection.quote("%#{value}%")
  }.join(" OR ")
end
```

如果 search 参数被传递给 search 动作，动作将基于对数据库的查询进行分页，查找与搜索值匹配的项目。否则，动作会调用 list 动作，该动作使用完整的表集填充 @users 和 @user_pages 值。最后，动作渲染 partial _search.html.erb，它仅返回值的表格，就像非 Ajax 版本一样。请注意，我们在渲染 partial 时明确禁用了任何布局。这可以防止递归的布局内布局问题。

## Using Prototype Helpers

Rails 提供了一整套 Prototype 辅助方法，为你的应用程序提供各种各样的 Ajax 解决方案。它们都需要你在页面中包含 prototype.js 文件。Rails 自带了该文件的一个版本，你可以使用 javascript_include_tag 辅助方法将其包含在页面中：

```
<%= javascript_include_tag "prototype" %>
```

许多应用程序将 Prototype 包含在默认布局中；如果你在整个应用程序中大量使用 Ajax，这是有意义的。如果你更关心带宽限制，你可能会选择更谨慎地仅在需要时包含它。如果你遵循标准的 Rails 生成器风格，你的 application.html.erb 文件将包含以下声明：

```
<%= javascript_include_tag :defaults %>
```

这将包含 Prototype、Script.aculo.us 以及用于应用程序特定 JavaScript 的生成的 application.js 文件。在任何一种情况下，一旦页面包含 Prototype，你就可以使用各种 Prototype 辅助方法向页面添加 Ajax。

## Common Options

在我们检查不同的辅助方法及其用途之前，让我们花一点时间了解我们可以传递给许多辅助方法的一些常见选项。由于大多数辅助方法最终会使用 XHR 向服务器发出调用，因此它们共享大量用于控制调用方式以及在调用前后做什么的选项。

## Synchronicity

大多数时候，你希望 Ajax 调用是异步的。这意味着用户可以继续与页面交互，而页面中的 JavaScript 在请求传输和处理期间可以继续执行操作。有时，你可能会发现需要同步 Ajax 调用（尽管我们强烈不建议这样做）。如果是这样，你可以传递 :type 选项，它有两个可能的值：:asynchronous（默认值）和 :synchronous：

```
<%= link_to_remote "Wait for it...",
    :url => {:action => 'synchronous_action'},
    :update => 'results_div',
    :type => :synchronous %>
```

## Updating the Page

Ajax 调用可能导致几种不同的响应。服务器可能会发送以下任何一种内容：

- *Nothing:* 服务器响应中没有内容，只有 HTTP 头。
- *HTML:* 要注入到页面中的 HTML 片段。
- *Data:* 结构化数据（JSON、XML、YAML、CSV 等）供 JavaScript 处理。
- *JavaScript:* 由浏览器执行的代码。

如果你的 Ajax 调用从服务器返回 HTML 片段，你可以指示大多数 Prototype 辅助方法使用 :update 选项将此 HTML 直接注入到页面中。你可以发送的可能值如下：

- *A DOM id:* 页面上元素的 id；JavaScript 将使用返回的值重置其 innerHTML 属性。
  <%= link_to_remote "Show me the money!",
      :url => {:action => 'get_the_money'},
      :update => 'the-money' %>
- *A hash:* 与调用成功或失败关联的 DOM 元素的 id。Prototype 识别两种状态：success 和 failure，其中 failure 定义为 HTTP 状态不是“200 Ok”的任何响应。使用此方法在成功完成时更新目标元素，但在出错时向另一个元素发送警告。

## 将进酒

## ——唐 · 李白

## 一首饯行的歌

《将进酒》是一首劝酒歌，大约是唐玄宗天宝年间李白离京后漫游梁、宋时期所作。

当时李白与友人岑勋在嵩山另一好友元丹丘的颍阳山居做客，三人登高饮宴，人生快慰，李白借此题抒写怀抱。

## 创作背景

这首诗作于唐玄宗天宝十一年（752年）。李白当时与友人岑勋在嵩山另一好友元丹丘的颍阳山居做客，三人登高饮宴，人生快慰，诗人借此题抒写怀抱。诗中表达了诗人对怀才不遇的感叹，又抱着乐观、通达的情怀，也流露了人生几何当及时行乐的消极情绪。全诗洋溢着豪情逸兴，具有出色的艺术成就。

我们之前介绍过的所有常见选项都可用于 link_to_remote。
看这个更详细的例子：

```
<div id="inbox_status">Unknown</div>
<%= link_to_remote 'Check Status...',
    :url => {:action => 'get_inbox_status',
             :user_id => @user.id},
    :update => 'inbox_status',
    :condition => "$('inbox_status').innerHTML == 'Unknown'",
    :before => "Element.show('progress_indicator')",
    :complete => "Element.hide('progress_indicator')" %>
```

此版本只有在目标元素当前值为“Unknown”时才会触发 XHR 请求，从而防止用户重复请求数据。它使用 :before 和 :complete 选项来打开和关闭进度指示。

## periodically_call_remote

与其依赖用户发起远程调用，你可能希望以固定的间隔定期调用服务器以检查更改。例如，在基于 Web 的聊天应用程序中，你希望每隔几秒询问服务器是否有新的聊天消息到达。这是一种常见的分布式状态检查方式，也是真正的“推送”通信技术的替代方案。

periodically_call_remote 方法为你处理了这个问题。它几乎与 link_to_remote 完全相同，只是它不接受用作链接文本的字符串值，而是接受一个间隔值，告诉它在向服务器发送请求之间等待多长时间。让我们修改之前的示例，每六十秒显示一次用户的收件箱状态：

```
<div id="inbox_status">Unknown</div>
<%= periodically_call_remote :url => {:action => 'get_inbox_status',
                                 :user_id => @user.id},
    :update => 'inbox_status',
    :frequency => 60,
    :condition => "$('inbox_status').innerHTML == 'Unknown'",
    :before => "Element.show('progress_indicator')",
    :complete => "Element.hide('progress_indicator')" %>
```

periodically_call_remote 接受与 link_to_remote 相同的选项（以及 :frequency 选项）。这意味着你可以为 :confirm 选项提供值。请在此处非常小心。不仅会出现一个模态对话框，要求用户批准一个原本完全透明的事件，而且在对话框显示在屏幕上时，管理 periodically_call_remote 的计时器仍在滴答作响并触发确认请求。这意味着你很容易陷入确认对话框堆积的情况，每次你点击 OK 或 Cancel 对话框消失时，立即又被另一个对话框取代。

