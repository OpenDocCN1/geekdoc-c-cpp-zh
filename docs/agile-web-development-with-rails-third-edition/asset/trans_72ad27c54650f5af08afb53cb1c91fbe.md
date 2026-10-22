

查看 ActiveRecord::Errors 的 API 文档，你会发现许多其他方法。其中大部分已被更高级的验证辅助方法取代。

## 验证辅助方法

某些验证是常见的：这个属性不能为空，那个属性必须在 18 到 65 之间，等等。Active Record 提供了一组标准的辅助方法，可以将这些验证添加到你的模型中。每个都是类级方法，名称都以 validates_ 开头。每个方法接受一个属性名列表，后面可选地跟着一个验证配置选项的散列。

例如，我们可以将之前的验证写成如下形式：

```
class User < ActiveRecord::Base
  validates_format_of :name,
    :with     => /\A\w+$/,
    :message => "is missing or invalid"

  validates_uniqueness_of :name,
    :on       => :create,
    :message => "is already being used"
end
```

大多数 validates_ 方法接受 :on 和 :message 选项。:on 选项决定验证何时应用，可以取 :save（默认）、:create 或 :update 之一。:message 参数可用于覆盖生成的错误消息。

当验证失败时，辅助方法会向 Active Record 模型对象添加一个错误对象。该错误对象将与正在验证的字段关联。验证后，你可以通过查看模型对象的 errors 属性来访问错误列表。当 Active Record 用作 Rails 应用程序的一部分时，此检查通常分两步完成：

1. 控制器尝试保存 Active Record 对象，但由于验证问题而失败（返回 false）。控制器重新显示包含错误数据的表单。
2. 视图模板使用 error_messages_for 方法显示模型对象的错误列表，用户有机会修复这些字段。

我们将在第 536 页的 23.5 节“错误处理与模型对象”中介绍表单和模型的交互。

接下来的页面列出了你可以在模型对象中使用的验证辅助方法。

## validates_confirmation_of

验证一个字段与其孪生字段是否具有相同的内容。

```
validates_confirmation_of attr... [ options... ]
```

许多表单要求用户输入两次某些信息，第二次输入作为第一次没有输错的确认。如果你使用命名约定，即第二个字段的名称是属性名加上 _confirmation 后缀，那么你可以使用 validates_confirmation_of 来检查两个字段是否具有相同的值。第二个字段不必存储在数据库中。

例如，视图可能包含以下内容：

```
<%= password_field "user", "password" %><br />
<%= password_field "user", "password_confirmation" %><br />
```

在 User 模型中，你可以使用以下代码验证两个密码是否相同：

```
class User < ActiveRecord::Base
  validates_confirmation_of :password
end
```

### 选项

| 选项 | 类型 | 描述 |
|------|------|------|
| :if | 代码 | 参见第 406 页的讨论。 |
| :unless | 代码 | 参见第 406 页的讨论。 |
| :message | 文本 | 默认为“doesn't match confirmation.” |
| :on | :save、:create 或 :update。 | |

## validates_each

使用块验证一个或多个属性。

```
validates_each attr... [ options... ] { |model, attr, value| ... }
```

对每个属性调用该块（如果 :allow_nil 为 true，则跳过值为 nil 的属性）。传入正在验证的模型、属性名和属性值。如下例所示，如果验证失败，该块应向模型的错误列表中添加错误：

```
class User < ActiveRecord::Base
  validates_each :name, :email do |model, attr, value|
    if value =~ /groucho|harpo|chico/i
      model.errors.add(attr, "You can't be serious, #{value}")
    end
  end
end
```

### 选项

| 选项 | 类型 | 描述 |
|------|------|------|
| :allow_nil | 布尔 | 如果 :allow_nil 为 true，值为 nil 的属性将不会传入块中。默认情况下会传入。 |
| :if | 代码 | 参见第 406 页的讨论。 |
| :unless | 代码 | 参见第 406 页的讨论。 |
| :on | :save、:create 或 :update。 | |

## validates_exclusion_of

验证属性不在一组值中。

```
validates_exclusion_of attr..., :in => enum [ options... ]
```

验证没有任何一个属性出现在 enum 中（支持 include? 谓词的任何对象）。

```
class User < ActiveRecord::Base
  validates_exclusion_of :genre,
    :in => %w{ polka twostep foxtrot },
    :message => "no wild music allowed"
  validates_exclusion_of :age,
    :in => 13..19,
    :message => "cannot be a teenager"
end
```

### 选项

| 选项 | 类型 | 描述 |
|------|------|------|
| :allow_nil | 布尔 | 如果为 true，nil 属性被视为有效。 |
| :allow_blank | 布尔 | 如果为 true，空白属性被视为有效。 |
| :if | 代码 | 参见第 406 页的讨论。 |
| :unless | 代码 | 参见第 406 页的讨论。 |
| :in（或 :within） | 可枚举 | 一个可枚举对象。 |
| :message | 文本 | 默认为“is not included in the list.” |
| :on | :save、:create 或 :update。 | |

## validates_format_of

根据模式验证属性。

```
validates_format_of attr..., :with => regexp [ options... ]
```

通过将每个属性的值与 regexp 匹配来验证该属性。

```
class User < ActiveRecord::Base
  validates_format_of :length, :with => /\d+(in|cm)/
end
```

### 选项

| 选项 | 类型 | 描述 |
|------|------|------|
| :if | 代码 | 参见第 406 页的讨论。 |
| :unless | 代码 | 参见第 406 页的讨论。 |
| :message | 文本 | 默认为“is invalid.” |
| :on | :save、:create 或 :update。 | |
| :with |  | 用于验证属性的正则表达式。 |

## validates_inclusion_of

验证属性属于一组值。

```
validates_inclusion_of attr..., :in => enum [ options... ]
```

验证每个属性的值是否出现在 enum 中（支持 include? 谓词的任何对象）。

### 选项（validates_uniqueness_of 的延续）

| 选项 | 类型 | 描述 |
|------|------|------|
| :message | 文本 | 默认为“has already been taken.” |
| :on | :save、:create 或 :update。 | |
| :scope | 属性 | 将检查限制为在列中具有与正在检查的行相同值的行。 |

## 条件验证

所有验证声明都接受一个可选的 :if 或 :unless 参数，该参数标识要运行的代码。参数可以是以下任何一种：

- 一个符号，在这种情况下，将调用相应的方法，并将当前 Active Record 对象传递给它
- 一个字符串，它会被（通过调用 eval）求值
- 一个 Proc 对象，它会被调用，并将当前 Active Record 对象传递给它

对于在 :if 参数上指定的代码，如果返回的值为 false，则跳过此特定验证。对于在 :unless 参数上指定的代码，如果返回的值为 true，则跳过此特定验证。

:if 选项通常与 Ruby proc 一起使用，因为 proc 允许你编写代码，其执行会延迟到验证执行时。例如，你可能想检查密码是否已指定，以及它是否与其确认密码（你要求用户输入的重复密码）匹配。但是，如果第一个验证失败，你不想执行确认检查。你可以通过仅在密码不为空白时运行确认检查来实现这一点。

```
validates_presence_of :password
```

```
validates_confirmation_of :password,
  :message => "must match confirm password",
  :if => Proc.new { |u| !u.password.blank? }
```

## 验证错误消息

验证返回的默认错误消息内置于 Active Record 中。但是，你可以通过编程方式更改它们。这些消息存储在一个以符号为键的散列中。可以这样访问：

```
I18n.translate('activerecord.errors.messages')
```

撰写本文时的值如下：

```
:inclusion     => "is not included in the list",
:exclusion      => "is reserved",
:invalid        => "is invalid",
:confirmation   => "doesn't match confirmation",
:accepted       => "must be accepted",
:empty          => "can't be empty",
:blank          => "can't be blank",
```

