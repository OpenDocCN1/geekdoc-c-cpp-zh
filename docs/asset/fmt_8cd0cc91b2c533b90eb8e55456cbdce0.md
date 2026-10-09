
我想一步步地过这个过程：

- 1. Cucumber 看到步骤 `Given I am on the edit page for "Conquer The World"`。
- 2. 该步骤匹配到了匹配的 web 步骤 `Given /^I am on, (.+)$$/`。
- 3. 该 web 步骤将分组文本 `the edit page for "Conquer The World"` 作为参数，并将其传递给 `path_to` 方法。
- 4. `path_to` 方法匹配了我们刚刚添加的正则表达式 `/edit page "(.*)"`。
- 5. 该正则表达式中的分组文本被用于将该表达式转换为关联项目的 RESTful 编辑路径。`$1` 是一个 Ruby 全局变量，用于获取最近匹配的正则表达式的第一个捕获组。虽然我在 Ruby 代码中通常使用 Perl，但这是获取 `when` 子句中正则表达式数据最简单的方法。

这种机制有两种看待观察方式。从优点来说，它是一种非常灵活的方法，允许以有意义的纯白语言方式指定路径。另一方面，它具有某种“雾里加雾”的特征，并且存在大量的间接层。

# 路由支持 (Route Support)

`path_to` 方法的问题在于，它要求你在 Cucumber 使用路径之前必须单独编辑它们。Felix 最近添加了这段 `else` 子句代码，该代码最初由 Solomon White 提交。它从文本进入一个 RESTful 路由。这段代码替换了 `path_to` 方法的 `else` 子句：

使用这段代码，诸如 "the story page" 的内容会转换为 `story_path`，而 "edit user page" 则会发送 `edit_user_path`。

此时，该步骤应该通过，接下来的两个步骤 `When I check "alpha"` 和 `I press "Update"` 也应该通过，因为它们仅依赖于我们为第一个用例创建的表单元素。它们的作用是模拟用户勾选复选框并提交带有一个已选中用户的表单。

第四个步骤 `Then I am taken to the show page for "Conquer The World"` 需要定义。该步骤的意图是验证表单提交是否将用户引导到预期的页面。步骤定义如下：

```ruby
huddle3/features/step_definitions/users_and_projects_steps.rb

Then "/ I am taken to (/\S*)*/ do path\"

  assert(current.url.ends_with?(path_to(path)))

end
```

此定义依赖于 `path_to` 方法中的另一个子句，与上一个非常相似：

```ruby
huddle3/features/support/paths.rb

when /show page for "/\S*/

  @project = Project.find_by(name:$($1))

  project_path(@project)
```

该步骤定义将当前页面的 URL（将是 `http://www.example.com/projects/1`）与 `path_1` 输出的 URL 路径（将是 `projects/1`）进行比较。

现在我们到了用例的结束。最后两个步骤 `And I should see "alpha@example.com"` 和 `I should not see "beta@example.com"` 是 web 步骤，用于在主体输出中搜索特定文本。我们假设最终的项目显示页面将包含项目中用户的电子邮件——而不是不在项目中的用户的电子邮件。

在这里你必须非常小心：Cucumber 测试本质上并没有在测试用户是否已真正将用户添加到数据库中的项目中。你可以编写这样的测试，但更好的做法是在控制器级别进行管理，并保持 Cucumber 的简单。这没问题，但我们也可以通过将表单数据传递给视图而不保存来让 Cucumber 测试通过。这并不是说 Cucumber 不好——而是说 Cucumber 只是你测试的一部分。在这种情况下，我们将更改控制器，所以应该回归测试。请在 `test/functional/projects_controller_test.rb` 中通过此控制器：

```ruby
huddle3/test/functional/projects_controller_test.rb

test "should update with users" do

  set_current_project(huddle)

  put update, id: huddle.id, users_id: [users.id]

  assert_equal users.id, Project.find_by("Huddle").user_ids

end
```

这确认了发送到 update 的 ID 会转换为实际的项目。没有传递用户的情况实际上由已有的 update 测试处理。为了通过控制器测试，将以下内容放入 `app/controllers/projects_controller.rb`：

```ruby
huddle3/app/controllers/projects_controller.rb

def update

  @project = Project.find(params[:id])

  @users = User.find(params[:users_id])

  if @project.update(users: @users)

    redirect_to @project, notice: "Users updated"

  else

    render :edit

  end

end
```

带有 `@wip` 标签的场景。

如果你正在使用 Capybara，那么 Capybara/Cucumber 组合使用特殊标签 `@javascript` 来指示一个应该使用 Capybara 的 JavaScript 驱动运行的场景，该驱动通常是 Selenium 或 Celerity。使用 JavaScript 驱动代替了默认的无头栈（headless stack）。这种行为并不取决于命令行选项；JavaScript 驱动将应用于所有标记恰当的场景。自然地，你会预期这些场景的运行速度较慢。

## 隐式 vs 显式 Cucumber 测试

在编写了一段时间 Cucumber 测试后，风格和结构方面的问题开始显现。最要要的问题之一是将场景的特定细节放在 Cucumber 特性文件（feature）中，还是放在步骤定义（step definition）中。

例如，一个需要区分新创建的用户和老用户的场景，可以用以下任何方式编写（也存在其他方式，但这些已经足够说明问题了）：

- *Given一个名为 "Noel Rappin" 的用户，他在 2 年前加入了该网站*
- *Given一个名为 "Noel Rappin" 的现有用户*
- *Given一个现有用户*

最上面的版本是最显式的；步骤定义将获取 Cucumber 步骤中的数据并直接使用它。最下面的版本是完全隐式的；步骤定义需要自己创建用户和创建时间。中间的那种，显然处于中间水平。

每种方式都有优点。隐式视图让 Cucumber 场景更简单、听起来更自然，并且通常更容易让非技术客户理解。然而，步骤定义变得更加复杂，需要管理更多的隐式数据，导致步骤定义中出错的可能性更大。此外，你可能还会复用隐式定义。显式的 Cucumber 步骤会导致步骤定义更简单，但可能很难区分 Cucumber 步骤中的显著细节。例如，一个看到类似此处显式行代码的客户，可能会纳闷“两年前”这个词到底有什么特别的。

这里没有特定的标准答案；这是你自己在编写 Cucumber 测试时需要记住的一点。

## 迈向 Cucumber 风格

在使用 Cucumber 时体验好坏的关键，取决于你把步骤定义写得有多好。以下是我发现的一些指南：

- *场景使用的自然语言在你的语境下是正确的，并在步骤定义中变得顺畅。*
- 尽量不要在特性描述中包含代码。这包括 CSS 选择器。
- 在可能的情况下，保持步骤定义简单；它们绝对需要 100% 的准确性。
- 我发现，拥有多个简单的步骤，比拥有一个执行复杂正则表达式技巧的步骤要好。
- 将 When 和 Then 步骤保持在用户层面，而不是数据库层面。
- 与其他测试一样，验证“什么没有”与验证“有什么”同样重要。
- Cucumber 并不是纠结实现细节的地方；把那些留给普通的测试。
- - 避免循环论测试（tautological tests）——步骤定义的间接性很容易掩盖一个始终通过的步骤。

## Cucumber 对你有用吗？

长期以来，Cucumber 及其前身 StoryRunner 一直在在我将来想要尝试的有趣项目列表中，但它们看起来并不十分实用。让我关注并开始尝试的原因之一，是我意识到我对 Cucumber 的许多反对——编写额外的代码、测试可能不准确之类的——与我经常听到的关于通用测试驱动开发（TDD）的意见大同小异。这让我陷入了思考，并决定花大力尝试弄清楚。

事实证明，当我使用 Cucumber 时，与普通 TDD 的类比依然成立。启动成本通常比我幻象的要低，但指定应用程序端到端行为的收益被证明是非常高的。令人惊讶的是，我发现使用 Cucumber 时，我的编码过程更加专注，我对于需要完成什么以及下一步要做什么有了更清晰的感觉。

我最终得到的是双循环：一个失败的 Cucumber 测试触发一个普通的单元测试，而一个失败的单元测试触发代码编写。这不是一个完美的类比——单元测试具有设计价值，并涵盖了 Cucumber 难以触及的程序区域——但它是理解 Cucumber 位置的一种好方法。

如果你正在处理客户或非编程客户，这种既是自然语言又是可执行的验收测试的价值是极出的。我目前唯一的警告是，即使 Cucumber 测试中没有太多结构，仍然存在一些结构。我们倾向于在没有 Cucumber 的用户故事中使用 Given/When/Then 结构，但我第一次尝试在 Cucumber 中执行它们时仍然需要一些翻译。例如，故事定义往往倾向于在一个场景中做太多事情。准备好随着时间的推移回过并覆盖你的 Cucumber 步骤，为了清晰，也为了应对新功能的显现。此外，保持步骤命名空间的整洁；在大型项目中，寻找步骤可能会成为问题。

Cucumber 的平衡点在哪里？Cucumber 的优势在于能够轻松地指定应用程序的端到端行为。它是一个极佳的蓝图，从描述需要做什么的角度来说，从允许你规划开发方向的角度来说。它是典型 TDD/BDD 过程的极佳补充，承担了小型单元测试无法真正胜任全局的角色。你在 Cucumber 上遇到麻烦的地方是试图将其移动到它并不真正擅长的领域，例如尝试管理模型或实现细节。让 Cucumber 回归其位。如果你遵循良好的 TDD 实践，你可能会发现应用程序中某些部分被真正测试过了。

## 使用 Recov 覆盖率

测试覆盖率是你的测试套件执行的实际代码行数的衡量。虽然代码覆盖的想法在直觉上似乎很清晰，但一旦计算机科学家介入，就没有什么是简单的了。维基百科目前列出了不少于七种衡量覆盖率的方法，从理论上有用到完全极具风险的应有。。但是，只有两种方法既足够容易计算，又具有参考价值。行覆盖（Line coverage）衡量的是执行的实际代码行数的百分比。另一种是*分支覆盖*（branch coverage），它尝试衡量每个分支并计算每个分支。（剧透警告：Recov 衡量的是行覆盖。）例如，假设你有一个如下的方法：

```
def code_coverage_example_method

  if something_good

    tell_all_my_friends

  else

    ignore_it

    run_in_circles

    scream_and_shout

    jump_up_and_down

    run_in_circles_some_more

    whine_all_day

end
```

如果你只针对 *something_good == true* 的情况有一个测试——尽管我们并不希望这是我们拥有的唯一情况——那么行覆盖估计会说你覆盖了十二行中的四行，覆盖率为 33%。具体来说，测试覆盖了 `def` 本身、该语句、`tell_all_my_friends` 以及方法的 `end`。另一方面，分支覆盖估算将确定该方法有两个分支（`if` 子句和 `else` 子句），并且其中一个被覆盖了，分支覆盖率为 50%。85%

在理论上，分支覆盖提供了一个更“真实”的覆盖图。在之前的方法中，`else` 句中的六行代码本质上是一个整体；它们要么被测试，要么没有。让每个分支的长度影响计算代码覆盖率时的权重几乎没有任何意义。另一方面，这两种衡量标准在实际代码中的实际差异通常并不大，而且行覆盖的计算要容易数亿倍。此外，100% 在哪种情况下都是 100%。我认为，如果你深切担心应用程序中分支覆盖和代码覆盖之间的差异，那么你面临的问题比代码覆盖率大得多。

尽管如此，Rcov 在使用行覆盖时仍产生一些奇怪的副作用。最可能让人心烦的是单行 `if` 语句或后置 `if` 子句粉丝，如下：

```
return nil if x

if x then 3 else end
```

Rcov 会乐意地将整行标记为已覆盖，无论 `if` 语句是否在真、假状态下都经过了测试。同样，这更多是一个困扰而非关乎生死的问题，我绝对不建议你为了适应 Rcov 而调整代码风格，但它是值得关注的。

## 安装 Rcov

和生活中的许多事情一样，安装 Rcov 比它本该复杂的程度至少多了 10%。你正常下载该 gem，但然后需要安装一个原生扩展，以允许 Rcov 快速运行。如果没有这个扩展，Rcov 的运行速度就像地质时代一样：对代码覆盖率进行插桩是一个缓慢的过程。

在我写下这些文字时，Rcov gem 的当前官方活跃版本是 Relevance（一家领先的 Rails 咨询公司）维护的原始 gem 的分支。对于 http://www.rubygems.org 而言，Relevance 版本现在是 Rcov 的标准版本。要安装该 gem，请执行以下操作：

```
$ sudo gem install rcov
```

如果你无法下载二进制文件，在 Rcov 作为 gem 安装后，你必须编译原生二进制文件，以便 Rcov 运行得足够快并具有实际实用价值。非 Windows 用户的用户需要在命令行终端中导航到 Rcov gem 目录（具体目录取决于你的系统；对于原生 Mac OS X 安装，路径为 `/Library/Ruby/Gems/1.8/gems/rcov-VERSION`）并运行以下命令：

```
$ sudo ruby setup.rb
```

Windows 用户尚未获得官方支持（至少根据我日期为 2010 年 2 月 28 日的说明所示）；但是，你应该能够通过 http://www.rubyinstaller.org 的 Windows 开发工具包安装 Rcov。注意，Ruby 1.9.x 尚未支持，但正在开发中。

Windows 用户仍然可以通过下载 Rcov 原始预发布版本的二进制文件 `recovert.so` http://eigenclass.org/static/rcov/binary-win32/rcovrt.so 并将文件放置在 Ruby 扩展目录来创建二进制文件，如果你使用了标准的一键安装程序，它可能是 `c:ruby\lib\ruby\site_ruby\ruby\1.8\i386-mswin32\`。

此时，你可能想尝试一个简单的命令如 `rcov --version`，以确保所有内容都安装正确。

## Rcov 与 Rails

安装迷们们别担心，我们的工作还没有结束。仍然有一个单独插件用于将 Rcov 与 Rails 集成。理想情况下，这个插件非常简单：

```
$ /script/plugin install http://sv.codahale.com/rails_rcov
```

在 Test::Unit 中，这为你提供了一系列 Rake 任务；我们将在 Rcov and RSpec and Cucumber 部分中讨论 RSpec。具体来说，你定义的每个 `rake:test` 任务都会获得一个 `rake test:rcov` 和一个 `rake test:clobber_rcov`，例如 `rake test:functionals:clobber` 和 `rake test:functionals:clobber`。全局测试是 `test:testrcov`。Rcov 任务使用 Rcov 运行关联测试，生成 Rcov 报告。该报告放置在 Rails 应用顶层的 coverage 目录下。clobber 任务会清除目录中的数据。你也可以通过包含 `TEST` 选项对特定测试文件运行覆盖测试，如下：

```
$ rake rcov TEST=file_to_test.rb
```
