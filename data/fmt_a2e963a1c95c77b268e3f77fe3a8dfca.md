
```ruby
huddle3/test/functional/projects_controller_test.rb
test "project timeline index should be sorted correctly" do
  set_current_project(huddle)
  get show, id: assign(huddle).id
  expected_keys = assign(reports).keys.map { |id| id.to_s(:db) }
  assert_equal(["2009-01-06", "2009-01-07"], expected_keys)
  assert_equal(
    [status_reports(one_tue).id, status_reports(two_tue).id],
    assigns(reports)[Date.parse("2009-01-06").map(&:id)]
  )
end
```

第 4-5 行断言创建一个名为 `@reports` 的对象，其键是报告的日期。第 6-8 行断言每个键包含其报告，并按用户名排序（准确来说，是用户的邮箱——我们并没有使用用户字段）。

该测试自然会失败，因为 `assigns(reports)` 为 `nil`。

转向控制器测试，让我们只验证对模型的赋值。在 `app/controllers/projects_controller.rb` 中：

```ruby
huddle3/app/controllers/projects_controller.rb
def show
  @project = Project.find(params[:id])
  @reports = @project.reports_grouped_by_day
  respond_to do
    format.html # show.html.erb
    format.xml # render xml => @project
  end
end
```

这意味着我们有一个模型测试 `test/unit/project_test.rb`：

```ruby
huddle3/test/unit/project_test.rb
test "should be able to retrieve projects by day" do
  actual = project(huddle)
  expected_keys = actual.keys.map { |id| id.to_s(:db) }
  assert_equal(["2009-01-06", "2009-01-07"], expected_keys)
  assert_equal([status_reports(one_tue).id, status_reports(two_tue).id],
    actual[Date.parse("2009-01-06").map(&:id)])
end
```

`div` 可能过于具体了——这些可能是行或正在转换的内容。计数测试是为了防止出现多余的内容，而这仅通过测试已知标签的存在是无法捕获的。在这种情况下，我们还测试了恰好有两天的报告，且每天都有两份报告。这是为了匹配我们设置的固件数据（fixture data）而校准，并快速展示了固件的一个弱点——对该固件数据的更改可能会破坏此测试。

此外，为了让其生效，请在 `test/test_helper.rb` 的类定义内部添加此行：

```
huddle3/test/test_helper.rb
include ActionController::RecordIdentifier
```

这允许我们能够在测试中使用 `dom_id` 方法，这非常方便。[26]

暂不考虑视图代码可能有数亿种方式通过此测试的字面要求但违背其精髓，这里是一个通过测试视图的基本结构，`app/views/projects/show.html.erb`：

```
huddle3/app/views/projects/show.html.erb
<h2>Status Reports for <%= @project.name %></h2>
<% @reports.keys.sort_by(&:date).each do |date| %>
<div id="<%= date.to_s(:db) %>-day">
  <h3>Reports for <%= date.to_s(:long) %></h3>
<% @reports[date].each do |report| %>
  <div id="<%= dom_id(report) %>">
Yesterday I: <%= report.yesterday %>
Today I will: <%= report.today %>
  </div>
  <% end %>
</div>
<% end %>
```

这为每个日期提供了一个 `div`，并为每个单独的报告提供了嵌套的 `div`。

# 到目前为止一切良好

此时，我们已经完成了对 Rails 测试驱动开发（TDD）的初步导览。你应该能够为 Rails 应用程序添加测试；使用固件数据；测试你的控制器、模型和视图；并对 TDD 快速测试/代码反馈循环如何在实践中运作有了感觉。

书的其余根据测试的应用部分进行划分。第二部分处理测试 ActiveRecord 模型，通过固件和工厂（factories）为测试获取数据，以及其他数据相关主题。第三部分讨论测试控制器、视图和辅助方法（helpers），每个部分都有一些特殊机制来使过程变得更容易。

大型第三方测试框架 Shoulda 和 RSpec 在第四部分进行讨论，而第五部分涵盖了集成测试，两者都使用了 Rails 本身以及使用了如 Webrat 和 Cucumber 等外部工具。最后，第六部分讨论了如何使用覆盖率工具评估和改进你的测试、管理性能以及排除故障。

`assert_select` 的一个方便特性是它可以解析 HTML 标记，如果 HTML 格式不正确，它会抛出警告 [21]——例如，如果缺少结束标签。

另一种方法是说这些测试应该直接跟踪名称，例如 assert_select [22] "textarea[name = ?],status_report[today]"。

另一种选项是使用集成测试或 Cucumber 验收测试来代替控制器测试。

像 Shoulda 这样的框架为关联关系提供了简单的单行测试——在这种情况下，可能 [24] 值得直接投入单行代码。

在 Rails 2.x 中，该代码将以 `named_scope` 而不是 `scope` 开始。在 Rails 3 中，这也可以被 [25] 写为普通的类 `find` 方法，因为 Rails 3 的 ActiveRecord 组件可以像 `named_scopes` 一样组合。

在 Rails 2.x 中，用此行 `include Action::Helpers::RecordIdentificationHelper` [26] 来包含该模块。

# 第二部分

## 测试应用程序数据

### 使用 Rails 单元测试测试模型

典型 Rails 应用程序中的绝大多数数据是通过连接到数据库的 ActiveRecord 对象访问的。这些对象通过模型测试进行测试。模型测试（Rails 称为单元测试）是 Rails 测试功能中最基础的层，我的意思是它们离 Ruby 的 `TestUnit` 最近，并且是构建控制器和视图结构的基础。Rails 中的模型测试仅仅是 `TestUnit` 加上设置固件数据的能力；用于设置（setup）和拆卸（teardown）的块（block）语法以及一些额外的断言方法。你编写的模型测试被放置在 `test/unit` 中。我们从模型测试开始 Rails 旅之旅，因为它们对 Rails 特有功能的依赖最少，通常是启动应用程序最简单的地方。稍后，我们将转向控制器测试、视图测试和集成测试。

### 名称之，第一部分

对 Rails 模型的测试通常被称为单元测试，但尽管我很固板且技术化，我更倾向于称它们为模型测试。我的基本问题是，“单元测试”取决于你如何看待具有特定的含义，要么包含功能测试，要么不包含。例如，Jay 认为测试并不是真正的单元测试，因为它们需要外部数据库。我个人认为，将“单元测试”作为所有测试的通用术语，将“模型测试”作为实际验证模型的测试会不那么困惑。

### 模型测试中可用的 Rails

Rails 模型的测试通常被称为单元测试，但尽管我很固板且技术化，我更倾向于称它们为模型测试。我的基本问题是，“单元测试”取决于你如何看待具有特定的含义，要么包含功能测试，要么不包含。例如，Jay 认为测试并不是真正的单元测试，因为它们需要外部数据库。我个人认为，将“单元测试”作为所有测试的通用术语，将“模型测试”作为实际验证模型的测试会不那么困惑。

模型测试是 `ActiveSupport::TestCase` 的子类，正如我们在测试控制器中将看到的：

- 从固件加载数据。
- 受 RSpec 启发的语法：`test "something" do`。
- 用于设置（setup）和拆卸（teardown）的块语法。
- 一些额外的断言方法：`assert_difference` 和 `assert_no_difference`。
- `assert_valid`，用于验证 ActiveRecord 模型是有效的。
- 几个数据库辅助方法：`assert_from_db`、`assert_sql` 和 `assert_no_queries`。
- `test_helper.rb`，所有测试所需的，它向 `ActiveSupport::TestCase` 注入了一些断言方法。

### 模型测试中测试什么

模型。下一个问题？

### 好的，什么是好的测试类？

目标是让每个模型的单独测试文件覆盖 100% 的代码。其他测试可能会接触模型，但并不是对模型测试的有效替代。测试应该尽可能接近所描述的代码。

你需要多少个测试？严格的测试驱动答案是，所有新逻辑都应该由失败的测试驱动，相反，每个新测试都应该失败并触发新的代码逻辑。一个典型的进展如下（如果你保持方法更小简单，你往往需要更少的测试）：

- 正常路径（happy-path）用例的测试。
- 代码中每个分支的测试。这里的重构通常会导致方法拆分成多个更小的方法。
- 至少一个已知错误用例的测试，例如传递空参数 [30]。我的立场可能有点固执，即只有当你你需要错误用例执行特定操作，或者怀疑预期错误没有真的被处理为错误时，才包含它。

保持每个单独测试简单。在很多情况下，你只需要为测试创建一个模型对象。你可能会发现，在编写测试之前列出所有想要测试的用例很有帮助。这很好，但你仍然需要逐一个编写并通过测试。

```ruby
story:stories(incomplete)
assert_difference "story.task_logs.count", 1 do
  story.complete!(users(quentin))
end
```

```ruby
assert story.completed?
assert story.blocked?
assert_equal(Date.today.to_s(:db), story.end_date)
assert_equal("completed", story.most_recent_log_end_state)
end
```

相比之下，这里是每个测试版本包含一个断言的版本：

```ruby
test "mark a story complete and add a task log" do
  assert_difference "story.task_logs.count", 1 do
    stories(incomplete).complete!(users(quentin))
  end
endend
```

```ruby
test "mark a story complete and the story should be completed" do
  story = stories(incomplete)
  story.complete!
  assert story.completed?
end
```

以此此类推。公平地说，一次运行一个断言的测试之所以冗长，是因为我只使用了 Rails 的核心方法。通过上下文（contexts）和单行测试工具（Single-Line Test Tools），RSpec 也有在 RSpec 章节中描述类似的功能。使用这些工具编写的每个测试一个断言的版本（one-assertion-per-test）可能比合一测试版本更具可读性。

存在一种权衡：将所有断言放在一个测试方法中，你可以获得清晰度和内聚的处处，但会导致测试无法独立运行。在合一测试中，如果 `assert story.completed?` 失败了，你不需要检查 `assert story.blocked`。如果所有断言都在单独的测试中，一切都会独立运行，但很难确定测试之间的关系。（多测试测试的运行速度也更慢。）

尽管如此，当你编写覆盖方法不同分支或错误测试的独立测试时，它们应该是不同的测试方法（除非方法设置极其简单）：

```ruby
test "full names" do
  user = User.create(first_name: "Fred", last_name: "Flintstone")
  assert_equal("Fred Flintstone", user.full_name)
end
```

```ruby
test "full names with a middle initial" do
  user = User.create(first_name: "Fred", last_name: "Flintstone", middle_initial: "D")
  assert_equal("Fred D. Flintstone", user.full_name)
end
```

```ruby
test "full name where there's no first name" do
  user = User.create(last_name: "Flintstone")
  assert_equal("Flintstone", user.full_name)
end
```

在这种情况下，你确实希望每个测试都独立运行；尝试将所有分支挤进单个测试中，以后将非常难以阅读。

#### 断言差异，或不断言差异

添加到基础单元测试中的那两个断言是常见测试模式的强大替代方案。以下测试断言了在调用 create 之后，用户总数量比之前多了一个：

```ruby
test "creating a user" do
  pre = User.count
  User.create(first_name: "Noel")
  post = User.count
  assert_equal(pre + 1, post)
end
```

使用 `assert_difference`，测试可以无需重复调用 `User.count` 来编写：

```ruby
test "creating a user" do
  assert_difference 'User.count' do
    User.create(first_name: "Noel")
  end
end
```

`assert_difference` 的第一个参数是一个 Ruby 代码字符串。该字符串的值通过 `eval` 计算。块中的代码会被执行，然后字符串的值会被重新计算。默认情况下，预期是新值比旧值大，但你可以通过传递第二个参数来调整此，例如传递 `assert_difference("User.count", 0)` 以保持不变，或者传递 `assert_difference("User.count", -1)` 来断言用户被删除。

如果你想检查多个代码片段，你有两种选择。`assert_difference` 的调用可以嵌套：

```ruby
test "create a user and a log entry" do
  assert_difference 'User.count' do
    assert_difference 'LogEntry.count' do
      User.create(first_name: "Noel")
    end
  end
end
```

`assert_difference` 的第一个参数是一个 Ruby 代码字符串。该字符串的值通过 `eval` 计算。块中的代码会被执行，然后字符串的值会被重新计算。默认情况下，预期是新值比旧值大，但你可以通过传递第二个参数来调整此，例如传递 `assert_difference("User.count", 0)` 以保持不变，或者传递 `assert_difference("User.count", -1)` 来断言用户被删除。

如果你想检查多个代码片段，你有两种选择。`assert_difference` 的调用可以嵌套：

```ruby
test "create a user and a log entry" do
  assert_difference 'User.count' do
    assert_difference 'LogEntry.count' do
      User.create(first_name: "Noel")
    end
  end
end
```

`assert_difference` 的第一个参数是一个 Ruby 代码字符串。该字符串的值通过 `eval` 计算。块中的代码会被执行，然后字符串的值会被重新计算。默认情况下，预期是新值比旧值大，但你可以通过传递第二个参数来调整此，例如传递 `assert_difference("User.count", 0)` 以保持不变，或者传递 `assert_difference("User.count", -1)` 来断言用户被删除。

如果你想检查多个代码片段，你有两种选择。`assert_difference` 的调用可以嵌套：
