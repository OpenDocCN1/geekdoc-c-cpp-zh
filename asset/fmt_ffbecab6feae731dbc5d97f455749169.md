
你甚至可以链式调用 `returns` 和 `raises`：

```
stubby.stubs(:user_count).returns(1).then(raises(Exception))
```

另一个常见用法是如果类的所有实例都使用类方法来响应同一个存桩。这通过 `any_instance` 管理，后跟着你可以执行的任何 `returns` 或 `raises` 预期。如下所示：

```
Project.any_instance.stubs(:save).returns(false)
```

通过这一点，你可以修正标准 Rails scaffolds（脚手架）中一个令人烦恼的问题。虽然结构松散（至少就本文而言），但为标准 `script/generate_scaffold` 控制器生成的 Rails 测试并没有覆盖 100% 的控制器方法。具体来说，对 `create` 和 `update` 响应的失败条件没有被覆盖。我一直认为（在没有真实理由的情况下），这一遗漏是因为测试此点的最简单方法是使用 mock 工具包，而 Rails 团队不想强制要求某一个特定的包。

既然已经提到了 mock 工具包，这里有几个使用 `any_instance` 调用来验证 `create` 和 `edit` 错误行为的示例测试。

这是针对 Mocha 的 `Project` 类——你需要对你的类进行细微调整：

```
huddle stubby/mocha/test/functional/projects_controller_test.rb

Line 1 test "fail create gracefully" do

  - assert_no_difference('Project.count') do

    - Project.any_instance.stubs(:save).returns(false)

    - post_create, project = {:name => 'Project Runway'}

    - assert_template('new')

  end
```

```
test "fail update gracefully" do

  Project.any_instance.stubs(:update_attributes).returns(false)

  put_update, id = projects

  assert_template('edit')

  actual = Project.find(id)

  assert_equal("Project Greenlight", actual.name)

end
```

使用声明可以通过多种方式变得更加复杂——坦率地说，我对其中某些的实际应用场景并不熟悉，但我们会快速过一遍。

最通用的情况下，我们可以向 `with` 传递一个块（block）而不是参数：

```ruby
proj = Project.new()

proj.stubs(status).with {value % 2 == 0}.returns("Active")

proj.stubs(status).with {value % 3 == 0}.returns("Asleep")
```

当调用存根的方法时，如果块返回 `true`，则认为预期匹配成功：

```ruby
>> proj.status(2)
=> "Active"
```

如果一个或多个块返回了 `true`，似乎最后一个声明的胜出：

```ruby
>> proj.status(3)
=> "Asleep"
>> proj.status(6)
=> "Asleep"
```

如果没有任何块返回 `true`，我们就会得到一个意外的调用错误（unexpected invocation error），正如我们刚才所看到的。

Mocha 还定义了一系列参数匹配器（parameter matchers），让行为更加灵活。以下是最实用的匹配器不完整列表。请注意，并非所有行为都可以使用块语法实现。

使用 `instance_of` 匹配器以及它的近亲 `is_a` 可以匹配任何传入的参数是否属于给定的类。使用 `instance_of`：

```ruby
proj = Project.new()

proj.stubs(tasks_before).with(instance_of(Date)).returns(3)

proj.stubs(tasks_before).with(instance_of(String)).raises(Exception)
```

任何 Mocha 匹配器都可以通过 `Not` 方法进行取反（注意，它的首字母是大写的，以避免与关键字冲突）。

```ruby
proj = Project.new()

proj.stubs(tasks_before).with(Not(instance_of(Date))).returns(3)
```

我们可以使用 `any_of` 匹配器为多个可能的参数应用存根：

```ruby
proj.stubs(thing).with(any_of('a', 'b')).returns('ababab')
```

我们还可以将 `any_of` 嵌套其他匹配器，尽管这会让语法变得复杂：

```ruby
proj.stubs(thing).with(any_of(instance_of(String), instance_of(Integer))).returns("Argh")
```

另一个有匹配器是 `regexp_matches`，它允许我们通过正则表达式进行匹配：

```ruby
proj.stubs(thing).with(regexp_matches(/user*/)).returns("A User!")
```

可以使用 `has_entry` 匹配器与特定的键值对匹配：

```ruby
proj.stubs(:options).with(has_entry(verbose => true))
```

此片段中的存根不会匹配任何包含 `:verbose => true` 的哈希参数，无论哈希的内容是什么。

还有十几个左右类似的匹配器，许多在实际应用中似乎并不常用，我邀请你查看 [Mocha 文档](http://mocha.rubyforge.org) 获取列表。

一种可能的用法是使用 `mock_active_records` 方法来处理上一节提到的 ActiveRecord 对象。记住，问题在于来自控制器的数据库调用创建的 ActiveRecord 对象与你挂载存根的对象完全不同。但你可以深入 ActiveRecord 内部并在测试辅助函数中定义它：

```ruby
def mock_active_records(records)
  records.each do |record|
     class.stub.stubs(:instantiate).with(has_entry('id' => record.id.to_s)).returns(record)
     record.stubs(:reload).returns(record)
  end
end
```

这里的关键短语是第 3 行的 `stubs(:instantiate).with`。该方法通过一组键值对创建一个 ActiveRecord 对象。在第 4 行，Mocha 的 `has_entry` 装饰器被用来声明键值对包含匹配记录的 ID，然后直接返回该记录。由于 `instantiate` 方法是从 `ActiveRecord::Base::find` 用的，除非你请求的是某些已知对象，否则不会尝试从数据库检索此对象。`reload` 方法同样被存根了。

示例用法如下：

```ruby
test "My projects might be properly saved" do
  @bluebook = Project.make(name=> "Project Bluebook")
  @runway = Project.records(name=> "Project Runway")
  mock_active_records(@bluebook, @runway)
  @bluebook.stubs(save=> true)
  @runway.stubs(save=> false)
end
```

注意，你必须用 `mock_active_records` 方法标记你将使用的记录，因为你实际上对这些对象指定了任何 stub 或 mock。这里有几点需要注意，最明显的是测试中的 ActiveRecord 需要位于 `mock_active_records` 调用中，因为尝试用非匹配哈希调用 stub 会触发预期错误。在只定义几个对象的工厂环境中，这种限制可能很好接受。此外，ActiveRecord 的内部可能会发生变化，导致此机制失效。

如果你只有两个对象需要 mock 且测试的方法很简单，则有一个更简单的选项：

```ruby
test "My projects might be properly saved" do
  @bluebook = Project.make(name=> "Project Bluebook")
  Project.stub(find).return(@bluebook)
  @bluebook.stubs(save=> true)
  post_update, id=> @bluebook.id
end
```

以上所有都是让 `Project` 类在 `find` 被调用时始终返回 `@bluebook`。它确保了使用 `find` 查找对象的控制器方法返回你在测试中设置的同一个对象。这里有明显的局限性——基本上，我们假设测试只需要创建一个 `Project` 对象。但在许多情况下（例如简单的更新或创建方法），这种方法是有效的。

## Mock 对象与行为驱动开发

使用真正的 Mock 对象（模拟对象）有趣之处在于，它们的使用开启了一种完全不同的测试风格。我们在书中的大部分内容看到的测试都是验证计算结果的：它们是在测试一个过程的终点。然而，当使用 Mock 对象时，我们有机会在测试过程中测试过程的行为，而不是结果。

一个示例将有助于澄清这种区别。在之前的“测试视图（Testing the View）”章节中，Huddle 应用有一个控制器测试，它很大程度上基于对模型调用的结果。

如果没有 Mock 对象，测试看起来如下所示（来自 `test/functional/projects_controller_test.rb`）：

```ruby
huddle_mocha/test/functional/projects_controller_test.rb

test "project timeline index be sorted correctly" do
  set_current_project(huddle)
  get :show, :id => assign(reports).keys.map { |d| d.to_s(s) }
  assert_equal("2009-01-06", "2009-01-07", expected_keys)
  assert_equal(
    [status_reports(ben_true).id, status_reports(jerry_true).id],
    assigns(reports)[Date.parse("2009-01-06")].map&(:id)
  )
end
```

随着该章节中过程的执行，此测试中的断言最终将与这里被测试的控制器操作所做的模型调用几乎完全相同地复制。当时，我们提到过 Mock 对象包将是编写测试的另一种方式。Mock 版本的测试可能像下面这个通过测试：

```ruby
huddle_mocha/test/functional/controller_test.rb

test "mock show test" do
  set_current_project(huddle)
  Project.any_instance.expects(:reports_grouped_by_day).returns(
    [Date.today => status_reports(aaron_true)]
  )
  get :show, :id => projects(huddle)
  assert_not_nil assigns(reports)
end
```

乍看之下，这看起来荒谬地极简。它似乎并没有在实际断言任何东西。诀窍在于第 3-4 行设置的 Mock 期望，以及该系统中可能存在的其他测试的结合。此测试验证了控制器调用了将 `reports` 变量设置为某些值的模型方法。它还验证了控制器和视图运行没有错误，但那是次要的。该测试验证的是控制器方法的行为——即它调用了特定的模型方法，而不是执行该调用后产生的状态。

此测试并没有尝试验证那些实际上属于其他测试范畴的功能。那是模型方法的工作。视图层对该值进行的操作是视图测试的工作。此测试通过使用已知方法验证了特定的实例变量被设置，其理论基础是控制器方法的作用是产生一组已知的值供使用。但验证 `reports` 的确切值是毫无意义的（至少在这种情况下），因为该值完全是由 Mock 期望生成的。

在 във风格的测试中使用 Mock 对象既有优点也有缺点。速度是一个是一个巨大的优势：从 Mock 获取值将比从任何固定件（fixture）或工厂数据库获取值快得多。另一个优势是测试的封装。在在上一个示例中，如果模型对象中引入了 Bug，只有模型测试会失败——受 Mock 保护的控制器测试将是没问题的。然而，非 Mock 版本的控制器测试很容易受到模型方法结果的影响而失败。如果做得当，这种封装可以使其更容易诊断和修复失败。

然而，有几个需要注意的潜在问题。一个是 Mock 的返回值与真实方法之间的不匹配。在之前的一个控制器示例中，Mock 调用方法返回一个哈希表，其键是一个 `Date` 对象，值是 `StatusReport` 对象列表。然而，如果模型方法返回的键为字符串的哈希表，那么可能会出现控制器方法通过但这种情况，这个问题可以通过使用集成测试或验收测试来覆盖；请参见[使用集成测试测试工作流](https://example.com) 章节和[使用 Cucumber 进行验收测试](https://example.com) 章节。

## RSpec

N/A

## RR

```
sudo gem install rr
```

然后，在 `test_helper.rb` 的测试用例声明中添加以下内容：

```
include RR::Adapters::UnitTest
```

# 创建空桩 (Blank Stubs)

这些包中最基本的功能是创建一个简单的桩对象，在其中你可以指定一个或多个方法的返回值。当这些方法被调用时，将返回指定的值。如果方法没有被调用，则什么都不会发生。以下是创建一个与应用程序中任何现有对象连接的桩对象的语法。

## FlexMock

```
stub = flexmock("name",method => result)
```
