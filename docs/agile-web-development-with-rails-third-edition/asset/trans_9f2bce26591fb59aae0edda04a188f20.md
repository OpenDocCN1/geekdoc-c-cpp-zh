

405 ActiveResource::MethodNotAllowed
409 ActiveResource::ResourceConflict
422 ActiveResource::ResourceInvalid
401..499 ActiveResource::ClientError

- 你可以通过在 ActiveResource 基类中重写验证方法来提供客户端验证。这与 ActiveRecord 中的验证行为相同。服务器端验证失败会导致响应代码为 422，并且你可以以相同的方式访问此类失败。有关更多详细信息，请参阅第 20.1 节、验证，第 397 页。
- 尽管默认格式是 XML，但你也可以使用 JSON 作为替代。只需在你的客户端类中将 self.format 设置为 :json 即可。请注意，如果这样做，你的客户端会将日期视为 ISO 8601/RFC 3339 格式的字符串，并将十进制数视为 Float 实例。
- 除了 self.site 之外，你还可以分别设置 self.user 和 self.password。
- self.timeout 使你能够指定 Web 服务请求在放弃并引发 Timeout::Error 之前应等待多长时间，以秒为单位。

## Part IV

## Securing and Deploying Your Application

本章是对 Andreas Schwarz 关于 Rails 安全性的在线手册的改编和扩展。该手册可在 http://manuals.rubyonrails.com/read/book/8 上获取（但在印刷时该网站似乎已关闭）。

## Chapter 27

## Securing Your Rails Application

Web 上的应用程序[content]

405 ActiveResource::MethodNotAllowed
409 ActiveResource::ResourceConflict
422 ActiveResource::ResourceInvalid
401..499 ActiveResource::ClientError

- 你可以通过在 ActiveResource 基类中重写验证方法来提供客户端验证。这与 ActiveRecord 中的验证行为相同。服务器端验证失败会导致响应代码为 422，并且你可以以相同的方式访问此类失败。有关更多详细信息，请参阅第 20.1 节、Validation，第 397 页。
- 尽管默认格式是 XML，但你也可以使用 JSON 作为替代。只需在你的客户端类中将 self.format 设置为 :json 即可。请注意，如果这样做，你的客户端会将日期视为 ISO 8601/RFC 3339 格式的字符串，并将十进制数视为 Float 实例。
- 除了 self.site 之外，你还可以分别设置 self.user 和 self.password。
- self.timeout 使你能够指定 Web 服务请求在放弃并引发 Timeout::Error 之前应等待多长时间，以秒为单位。

## Part IV

## Securing and Deploying Your Application

本章是对 Andreas Schwarz 关于 Rails 安全性的在线手册的改编和扩展。该手册可在 http://manuals.rubyonrails.com/read/book/8 上获取（但在印刷时该网站似乎已关闭）。

## Chapter 27

## Securing Your Rails Application

Web 上的应用程序处于持续攻击之下。Rails 应用程序也不例外。

安全性是一个很大的主题——足以写成整本书的主题。我们在仅一章中无法做到公正。在将应用程序放到可怕、险恶的网络上之前，你可能需要做一些研究。关于 Web 安全性的一个很好的阅读起点是开放 Web 应用程序安全项目（OWASP），网址为 http://www.owasp.org/。这是一个志愿者团体，他们整理了与安全相关的“免费、专业质量、开源文档、工具和标准”。一定要查看他们关于 Web 应用程序安全问题的十大列表。如果你遵循一些基本准则，你可以使你的 Rails 应用程序更加安全。

### 27.1 SQL Injection

SQL 注入是许多 Web 应用程序中排名第一的安全问题。那么，什么是 SQL 注入，它是如何工作的？

假设一个 Web 应用程序从不可靠的来源（如 Web 表单字段的数据）获取字符串，并将这些字符串直接用于 SQL 语句中。如果应用程序没有正确引用任何 SQL 元字符（如反斜杠或单引号），攻击者就可以控制在你的服务器上执行的 SQL，使其返回敏感数据、创建包含无效数据的记录，甚至执行任意 SQL 语句。

想象一个具有搜索功能的 Web 邮件系统。用户可以在表单上输入一个字符串，应用程序将列出所有主题包含该字符串的电子邮件。在我们应用程序的模型中，可能存在如下查询：

```
Email.find(:all,
    :conditions => "owner_id = 123 AND subject = '#{params[:subject]}'")
```

这是危险的。想象一个恶意用户手动发送字符串 "' OR 1 --" 作为 subject 参数。Rails 将其替换到为 find 方法生成的 SQL 后，结果语句将如下所示：¹

```
select * from emails where owner_id = 123 AND subject = '' OR 1 --'
```

OR 1 条件始终为真。两个减号开始一个 SQL 注释；其后的所有内容将被忽略。我们的恶意用户将获得数据库中所有电子邮件的列表。²

## Protecting Against SQL Injection

如果你只使用预定义的 Active Record 函数（如 attributes、save 和 find）并且在调用这些方法时不添加自己的 conditions、limits 和 SQL，那么 Active Record 会为你处理数据的危险字符的引用。例如，以下调用是安全的，不会受到 SQL 注入攻击：

```
order = Order.find(params[:id])
```

即使 id 值来自传入的请求，find 方法也会处理元字符的引用。恶意用户能做的最坏的事情就是引发 Not Found 异常。

但如果你的调用确实包含 conditions、limits 或 SQL，并且这些数据中的任何部分来自外部来源（即使是间接的），你必须确保此外部数据不包含任何 SQL 元字符。一些潜在不安全的查询包括以下内容：

```
Email.find(:all,
  :conditions => "owner_id = 123 AND subject = '#{params[:subject]}'")
```

```
Users.find(:all,
  :conditions => "name like '%#{session[:user].name}%'")
```

```
Orders.find(:all,
  :conditions => "qty > 5",
  :limit      => #{params[:page_size]})
```

抵御这些 SQL 注入攻击的正确方法是永远不要使用常规的 Ruby #{...} 机制将任何内容替换到 SQL 语句中。相反，使用 Rails 绑定变量设施。例如，你希望将 Web 邮件搜索查询重写如下：

```
subject = params[:subject]
Email.find(:all,
  :conditions => ["owner_id = 123 AND subject = ?", subject ])
```

1. 实际使用的攻击取决于数据库。这些示例基于 MySQL。
2. 当然，在实际应用程序中，owner id 会被动态插入；这里省略是为了保持示例简单。

如果 find 的参数是数组而不是字符串，Active Record 将为第一个元素中的每个 ? 占位符插入第二个、第三个和第四个（以及以后）元素的数值。它会在元素为字符串时添加引号，并引用 Email 模型使用的数据库适配器对具有特殊含义的所有字符。

除了使用问号和值数组之外，你还可以使用命名绑定值并传递哈希。我们从第 330 页开始讨论这两种形式的占位符。

## Extracting Queries into Model Methods

如果需要在代码的多个位置执行具有类似选项的查询，你应该在模型类中创建一个封装该查询的方法。例如，你的应用程序中可能存在一个常见的查询，如下所示：

```
emails = Email.find(:all,
  :conditions => ["owner_id = ? and read='NO'", owner.id])
```

最好将其封装在 Email 模型的类方法中：

```
class Email < ActiveRecord::Base
  def self.find_unread_for_owner(owner)
    find(:all, :conditions => ["owner_id = ? and read='NO'", owner.id])
  end
  # ...
end
```

在应用程序的其他部分中，你可以在需要查找任何未读电子邮件时调用此方法：

```
emails = Email.find_unread_for_owner(owner)
```

如果你以这种方式编码，就不必担心元字符——所有安全问题都在模型内部的较低级别封装。你应该确保这种模型方法即使使用不受信任的参数调用也不会破坏任何东西。

还请记住，Rails 会为模型中的所有属性自动生成查找方法，并且这些查找方法对 SQL 注入攻击是安全的。如果你想搜索具有给定 owner 和 subject 的电子邮件，你可以简单地使用 Rails 自动生成的方法：

```
list = Email.find_all_by_owner_id_and_subject(owner.id, subject)
```

### 27.2 Creating Records Directly from Form Parameters

假设你想实现一个用户注册系统。你的 users 表看起来像这样：

```
create_table :users do |t|
  t.string :name
  t.string :password
  t.string :role,      :default => "user"
  t.integer :approved, :default => 0
end
```

role 列包含 admin、moderator 或 user 之一，并定义此用户的权限。approved 列在管理员批准此用户访问系统后设置为 1。

相应的注册表单的 HTML 如下所示：

```
<form method="post" action="http://website.domain/user/register">
  <input type="text" name="user[name]" />
  <input type="text" name="user[password]" />
</form>
```

在我们应用程序的控制器中，从表单数据创建用户对象的最简单方法是直接将表单参数传递给 User 模型的 create 方法：

```
def register
  User.create(params[:user])
end
```

但如果有人决定将注册表单保存到磁盘并通过添加一些字段来玩弄它会怎样？也许他们手动提交如下所示的网页：

```
<form method="post" action="http://website.domain/user/register">
  <input type="text" name="user[name]" />
  <input type="text" name="user[password]" />
  <input type="text" name="user[role]"      value="admin" />
  <input type="text" name="user[approved]" value="1" />
</form>
```

尽管我们控制器中的代码仅打算为新用户初始化 name 和 password 字段，但此攻击者还给了自己管理员状态并批准了自己的帐户。

Active Record 提供了两种方法来防止敏感属性被更改表单的恶意用户覆盖。第一种方法是将要保护的属性列为 attr_protected 方法的参数。任何被标记为受保护的属性都不会通过 create 和 new 方法的模型属性批量赋值来分配。

