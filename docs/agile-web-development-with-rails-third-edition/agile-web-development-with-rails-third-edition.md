# Rails 敏捷Web开发 第三版





> Tous les jours, à tous points de vue, je vais de mieux en mieux.
>
> ► Émile Coué

## 第二版序言

自从我宣布本书第一版以来，已经过去了十八个月。在书出版之前，很明显 Rails 会很火，但我认为当时没有人意识到这个框架最终会变得多么重要。

在随后的那一年里，Rails 势头强劲。它被用作无数新颖、令人兴奋网站的基础。同样重要的是，许多大型企业（其中许多是家喻户晓的名字）开始将 Rails 用于内部和外部应用。Rails 也获得了业界好评。Rails 的创造者 David Heinemeier Hansson 在 OSCON 被评为年度黑客。Rails 赢得了 Jolt 奖最佳 Web 开发工具奖，本书第一版也获得了 Jolt 奖最佳技术图书奖。

但 Rails 核心团队并没有只是坐享其成，吸收赞美。相反，他们一直在埋头添加新功能和设施。Rails 1.0 在第一版上市几个月后发布，增加了诸如数据库迁移支持以及更新的 Ajax 集成等功能。Rails 1.1 于 2006 年春季发布，是一个重磅版本，与上一个版本相比有超过 500 处更改。其中许多更改都意义深远。例如，RJS 模板改变了开发人员编写 Ajax 启用应用的方式，而集成测试框架改变了这些应用的测试方式。大量工作投入到扩展和增强 Active Record，现在它包括多态关联、连接模型、更好的缓存等等。

是时候更新本书以反映所有这些优点了。而且，当我开始进行更改时，我意识到还有一些其他变化。自第一本书发布以来，我们所有人都对如何编写 Rails 应用有了更多的经验。一些看起来很棒的想法在实践中效果并不好，而其他最初看起来很边缘的功能却变得很重要。这些新实践意味着对本书的更改比我预期的要深入得多。我不再只是对文本进行表面修改，添加几个新 API。相反，我发现自己在重写内容。原版中的一些章节已被删除，并添加了新章节。许多其余章节已被

code，Rails 会自动为该功能创建测试存根。框架使测试应用变得容易，因此 Rails 应用往往会被测试。

Rails 应用是用 Ruby 编写的，一种现代的面向对象脚本语言。Ruby 简洁而不至于晦涩难懂——你可以用 Ruby 代码自然、清晰地表达想法。这导致程序易于编写，也同样重要的是，几个月后易于阅读。

Rails 将 Ruby 发挥到极致，以新颖的方式扩展它，使程序员的生活更轻松。这使我们的程序更短、更易读。它还允许我们将通常在外部配置文件中完成的工作在代码库内部完成。这使得更容易看到发生了什么。以下代码定义了项目的模型类。现在不要担心细节。只需思考几行代码中表达了多少信息。

```
class Project < ActiveRecord::Base
  belongs_to        :portfolio
  has_one           :project_manager
  has_many          :milestones
  has_many          :deliverables, :through => :milestones

  validates_presence_of   :name, :description
  validates_acceptance_of :non_disclosure_agreement
  validates_uniqueness_of :short_name
end
```

来到 Rails 的开发人员还发现了一个强有力的哲学基础。Rails 的设计由几个关键概念驱动：DRY 和约定优于配置。DRY 代表不要重复自己——系统中每条知识都应该只在一个地方表达。Rails 利用 Ruby 的强大功能将其付诸实践。你会在 Rails 应用中发现很少的重复；你在一个地方说出你需要说的话——这个地方通常由 MVC 架构的约定所建议——然后继续前进。对于习惯于其他 Web 框架的程序员来说，一个简单的模式更改可能涉及半打或更多的代码更改，这是一个启示。

约定优于配置也很重要。这意味着 Rails 对将你的应用组合在一起的几乎每个方面都有合理的默认值。遵循约定，你可以用比典型的 Java Web 应用在 XML 配置中使用的更少的代码编写 Rails 应用。如果你需要覆盖约定，Rails 也让这变得容易。

来到 Rails 的开发人员还发现了其他东西。Rails 是新的，其核心开发团队了解新的 Web。Rails 不是在追赶新的事实上的 Web 标准；它正在帮助定义它们。而且 Rails 使


与第一版一样，Rails 核心团队给予了极大的帮助，回答了问题、检查了代码片段并修复了错误。在此特别*感谢*以下各位：

Scott Barron (htonl)、Jamis Buck (minam)、Thomas Fuchs (madrobby)、Jeremy Kemper (bitsweat)、Michael Koziarski (nzkoz)、Marcel Molina Jr. (noradio)、Rick Olson (technoweenie)、Nicholas Seckar (Ulysses)、Sam Stephenson (sam)、Tobias Lütke (xal) 以及 Florian Weber (csshsh)

我们还要感谢为本书贡献各专业章节的朋友们：Leon Breedt、Mike Clark、James Duncan Davidson、Justin Gehtland 和 Andreas Schwarz。

## 来自 Sam Ruby

这项工作最终比我预想的更加艰难，也更有收获。之所以更艰难，是因为 Rails 的变化如此之大，需要学习的东西如此之多（包括 Rails 2.0、SQLite 3，以及要与不同的出版商、操作系统和工具集协作）。但我无法用言语表达我对 beta 图书计划的喜爱——迄今为止，这本书吸引来的读者都非常棒，他们的评论、问题和反馈都让我感激不尽。

Sam Ruby

2009 年 1 月

rubys@intertwingly.net

## 来自 Dave Thomas

我一直对自己发誓，每本书都将是最后一本，别的理由不说，光是每本书都会让我离开家人几个月这一点就够了。再次感谢：Juliet、Zachary 和 Henry——谢谢你们所做的一切。

Dave Thomas

2006 年 11 月

dave@pragprog.com

> “《Agile Web Development with Rails》……我在当地的书店发现了它，看起来非常棒！”
> ——Dave 的妈妈

## 第一部分

## 入门

### 第 2 章

### Rails 应用程序的架构

Rails 的一个有趣特性是，它对你构建 Web 应用程序的方式施加了相当严格的约束。令人惊讶的是，这些约束让创建应用程序变得更容易——容易得多。让我们来看看原因。

#### 2.1 模型、视图和控制器

早在 1979 年，Trygve Reenskaug 就提出了一种用于开发交互式应用程序的新架构。在他的设计中，应用程序被分为三种类型的组件：模型、视图和控制器。

*模型*负责维护应用程序的状态。有时这种状态是短暂的，只持续与用户的几次交互。有时状态是持久的，会存储在应用程序之外，通常存储在数据库中。

模型不仅仅是数据；它强制执行适用于该数据的所有业务规则。例如，如果折扣不适用于低于 20 美元的订单，模型将强制执行该约束。这是有道理的；通过在模型中实现这些业务规则，我们确保应用程序中的其他任何内容都不会使数据无效。模型既充当看门人，又充当数据存储。

*视图*负责生成用户界面，通常基于模型中的数据。例如，在线商店将会有要显示在目录屏幕上的产品列表。这个列表可以通过模型访问，但将由视图从模型中访问该列表并将其格式化给最终用户。尽管视图可能为用户提供各种输入数据的方式，但视图本身从不处理传入的数据。一旦数据被显示，视图的工作就完成了。可能会有许多视图访问相同的模型数据，通常出于不同的目的。在在线商店中，将会有

路由组件接收传入的请求并立即对其进行解析。在这个简单的例子中，它将路径的第一部分 `store` 作为控制器的名称，将第二部分 `add_to_cart` 作为操作的名称。路径的最后一部分 `123`，按照惯例被提取到一个名为 `id` 的内部参数中。经过所有这些分析，路由器知道它必须调用控制器类 `StoreController` 中的 `add_to_cart` 方法（我们将在第 268 页讨论命名约定）。

`add_to_cart` 方法处理用户请求。在这种情况下，它找到当前用户的购物车（这是一个由模型管理的对象）。它还要求模型查找产品 123 的信息。然后它告诉购物车将该产品添加到自身。（看看模型是如何被用来跟踪所有业务数据的？控制器告诉它做什么，而模型知道如何去做。）

现在购物车中包含了新产品，我们可以将其展示给用户。控制器调用视图代码，但在调用之前，它会安排视图能够访问模型中的购物车对象。在 Rails 中，这种调用通常是隐式的；同样，约定有助于将特定的视图与给定的操作关联起来。

这就是 MVC Web 应用程序的全部内容。通过遵循一组约定并适当地划分你的功能，你会发现你的代码更容易处理，你的应用程序也更容易扩展和维护。这看起来是一笔不错的交易。

如果 MVC 只是以特定方式划分代码的问题，你可能会想为什么需要一个像 Ruby on Rails 这样的框架。答案很简单：Rails 为你处理了所有底层的事务——所有那些你自己处理起来需要很长时间的繁琐细节——让你专注于应用程序的核心功能。让我们看看……

#### 2.2 Active Record：Rails 的模型支持

一般来说，我们希望 Web 应用程序将信息存储在关系数据库中。订单录入系统会将订单、订单行和客户详细信息存储在数据库表中。即使是通常使用非结构化文本的应用程序（如博客和新闻网站），也常常使用数据库作为其后端数据存储。

尽管从你用于访问关系数据库的 SQL² 中可能不会立即看出来，但关系数据库实际上是围绕数学集合论设计的。虽然从概念的角度来看这很好，但它使得将关系数据库与面向对象（OO）编程语言结合起来变得困难。对象关注的是数据和操作，而数据库关注的是

2. SQL，有人称之为结构化查询语言，是用于查询和更新关系数据库的语言。

一组值。在关系术语中容易表达的操作，有时在 OO 系统中却难以编码。反之亦然。

随着时间的推移，人们已经找到了调和公司数据的关系视图和 OO 视图的方法。让我们看看两种不同的方法。一种将你的程序围绕数据库来组织；另一种将数据库围绕你的程序来组织。

##### 以数据库为中心的编程

最早针对关系数据库编程的人使用 C 和 COBOL 等过程式语言进行编程。这些人通常将 SQL 直接嵌入到他们的代码中，要么作为字符串，要么使用预处理器将源代码中的 SQL 转换为对数据库引擎的低级调用。

这种集成意味着将数据库逻辑与整体应用程序逻辑交织在一起变得很自然。一个想要扫描订单并更新每个订单中销售税的开发者可能会写出非常丑陋的代码，例如：

```
EXEC SQL BEGIN DECLARE SECTION;
    int     id;
    float   amount;
EXEC SQL END DECLARE SECTION;

EXEC SQL DECLARE c1 AS CURSOR FOR select id, amount from orders;

while (1) {
    float tax;
    EXEC SQL WHENEVER NOT FOUND DO break;
    EXEC SQL FETCH c1 INTO :id, :amount;
    tax = calc_sales_tax(amount)
    EXEC SQL UPDATE orders set tax = :tax where id = :id;
}
EXEC SQL CLOSE c1;
EXEC SQL COMMIT WORK;
```

吓人吧？别担心。我们不会这样做，尽管这种编程风格在 Perl 和 PHP 等脚本语言中很常见。在 Ruby 中也可以这样做。例如，我们可以使用 Ruby 的 DBI 库来生成类似的代码（和前面的例子一样，这个也没有错误检查）：

方法定义
→ 第 668 页

```
def update_sales_tax
  update = @db.prepare("update orders set tax=? where id=?")
  @db.select_all("select id, amount from orders") do |id, amount|
    tax = calc_sales_tax(amount)
    update.execute(tax, id)
  end
end
```





这种方法简洁明了，而且确实被广泛使用。对于小型应用来说，它似乎是一个理想的解决方案。然而，问题也存在。像这样将业务逻辑和数据库访问混在一起，可能会使应用在将来难以维护和扩展。而且，即使只是开始编写应用，你也需要了解 SQL。

例如，假设我们开明的州政府通过了一项新法律，要求我们记录计算销售税的日期和时间。我们认为这不成问题。只需在循环中获取当前时间，向 SQL 更新语句中添加一列，然后将时间传递给 execute 调用即可。

但是，如果我们在应用中的许多不同位置都设置了销售税列，会发生什么？现在我们需要逐一找到所有这些位置，并更新每一处。我们有了重复的代码，而且（如果我们漏掉了设置该列的位置）就埋下了错误的隐患。

在常规编程中，面向对象告诉我们封装可以解决这类问题。我们会将与订单相关的所有内容封装到一个类中；当法规发生变化时，我们就有一个统一的更新位置。

人们已经将这些想法扩展到了数据库编程中。基本原理非常简单。我们将数据库访问封装在一层类后面。应用的其余部分使用这些类及其对象——它从不直接与数据库交互。这样，我们就将所有与模式相关的内容封装到一个层中，并将应用代码与数据库访问的低层细节解耦。在我们的销售税变更案例中，只需修改包装订单表的类，以便在销售税变更时更新时间戳。

在实践中，这个概念实现起来比看起来要难。现实中的数据库表是相互关联的（例如，一个订单可能包含多个订单项），我们希望将这些关系反映到对象中：订单对象应包含一组订单项对象。但这样我们就会开始遇到对象导航、性能和一致性问题。面对这些复杂性，业界做了它一贯做的事情：它发明了一个三个字母的缩写：ORM，即对象关系映射。Rails 就使用了 ORM。

##### 对象关系映射

ORM 库将数据库表映射到类。如果数据库有一个名为 orders 的表，我们的程序就会有一个名为 Order 的类。该表中的行对应类的对象——一个特定的订单表示为 Order 类的一个对象。在该对象内部，属性用于获取和设置各个列。我们的 Order 对象具有获取和设置金额、销售税等的方法。

此外，包装我们数据库表的 Rails 类提供了一组执行表级操作的类方法。例如，我们可能需要查找具有特定 id 的订单。这实现为一个类方法，返回对应的 Order 对象。在 Ruby 代码中，这可能看起来像这样：

```
order = Order.find(1)
puts "Customer #{order.customer_id}, amount=#{order.amount}"
```

有时这些类方法会返回对象集合：

```
Order.find(:all, :conditions => "name='dave'").each do |order|
  puts order.amount
end
```

最后，与表中单独行对应的对象具有对该行进行操作的实例方法。最常用的可能是 save，该操作将行保存到数据库：

```
Order.find(:all, :conditions => "name='dave'").each do |order|
  order.discount = 0.5
  order.save
end
```

因此，ORM 层将表映射到类，将行映射到对象，将列映射到这些对象的属性。类方法用于执行表级操作，实例方法对单独行执行操作。

在典型的 ORM 库中，您提供配置数据来指定数据库中的实体与程序中的实体之间的映射。使用这些 ORM 工具的程序员经常会发现自己在创建和维护大量 XML 配置文件。

##### Active Record

*Active Record* 是 Rails 附带的 ORM 层。它紧密遵循标准 ORM 模型：表映射到类，行映射到对象，列映射到对象属性。它与大多数其他 ORM 库的不同之处在于其配置方式。通过依靠约定和合理的默认值，Active Record 最大限度地减少了开发人员执行的配置量。为了说明这一点，下面是一个使用 Active Record 包装我们的 orders 表的程序：

```
require 'active_record'
```

```
class Order < ActiveRecord::Base
end
```

```
order = Order.find(1)
order.discount = 0.5
order.save
```

### 第 3 章

### 安装 Rails

#### 3.1 您的购物清单

要在您的系统上运行 Rails，您需要以下内容：

- 一个 Ruby 解释器。Rails 是用 Ruby 编写的，您也将用 Ruby 编写您的应用程序。Rails 团队现在推荐使用 Ruby 1.8.7 版本。
- Ruby on Rails。本书编写时使用的是 Rails 2 版本（具体来说是 2.2.2 Rails RubyGem）。¹
- 一些库。
- 一个数据库。本书使用的是 SQLite 3。

对于开发机器来说，这些就是您所需的一切（除了编辑器，我们将单独讨论编辑器）。但是，如果您要部署应用程序，您还需要安装一个生产 Web 服务器（至少），以及一些让 Rails 高效运行的支撑代码。我们有整整一章专门讨论这个问题，从第 651 页开始，所以这里就不再赘述。

那么，如何安装所有这些呢？这取决于您的操作系统……

#### 3.2 在 Windows 上安装

如果您使用 Windows 进行开发，您很幸运，因为 InstantRails 2.0 是一个单独的下载包，其中包含 Ruby、Rails、SQLite 3（编写本书时为 3.5.4 版本）以及让它们协同工作所需的所有组件。它甚至包含一个 Apache Web 服务器和支持代码，让您可以部署高性能的 Web 应用程序。

1. 它也已经定期用 Edge Rails 进行了测试，在那里也应该能工作，但由于 Edge 版本在任何时候都不确定，因此不能保证这一点。

- 创建一个文件夹来存放 InstantRails 安装文件。该文件夹的路径不能包含任何空格（因此 C:\Program Files 就是一个不好的选择）。
- 访问 InstantRails 网站，² 并点击链接下载最新的 .zip 文件。（大约 70MB，所以如果您的网速较慢，开始下载前先泡一壶茶。）将它放入您在步骤 1 中创建的目录中。
- 如果您的系统不能自动解压，您需要手动解压该压缩包。
- 导航到 InstantRails-2.0 目录，并通过双击 InstantRails 图标（那个大的红色 I）启动 InstantRails。
  - 如果看到一个弹出窗口询问是否重新生成配置文件，请选择“是”。
  - 如果看到一个安全警报，说 Apache 已被防火墙阻止，嗯……我们不打算告诉您应该阻止还是解除阻止。就本书而言，我们不打算使用 Apache，所以这无关紧要。最安全的做法是选择“保持阻止”。如果您知道自己在做什么，并且您的机器上没有运行 IIS，您可以解除端口阻止，稍后使用 Apache。

您应该会看到一个小型 InstantRails 窗口出现。您可以使用它来监控和控制 Rails 应用程序。但是，我们将比这更深入一些，因此我们将使用控制台窗口。要启动它，请单击 InstantRails 窗口左上角的 I 按钮（该按钮是一个黑色的 I，右下角有一个红点）。从菜单中选择 Rails 应用程序...，然后选择 打开 Ruby 控制台窗口。您应该会看到弹出一个命令窗口，并且您会位于 rails_apps 目录中，如第 2 页图 3.1 所示。您可以分别输入命令 ruby -v 和 rails -v 来验证 Ruby 和 Rails 的版本。

此时，您已经可以正常运行了。但是，在您跳到下一章之前，您需要知道三个重要的事实。

首先，也是最重要的，每当您想在控制台窗口中输入命令时，您必须使用从 InstantRails 菜单启动的控制台。按照我们之前使用的相同步骤（单击 I，等等）。如果您打开一个普通的 Windows 命令提示符，事情就行不通。（为什么？因为 InstantRails 是自包含的——它不会安装到您的全局 Windows 环境中。这意味着您需要的所有程序默认不在 Windows 的路径中。您可以稍微费点心思，将它们添加到路径中，然后使用常规命令窗口，但使用 InstantRails 的方式似乎也一样容易。）

2. http://instantrails.rubyforge.org/wiki/wiki.pl




Tiger 用户还需要升级 SQLite 3。这可以通过从源代码编译来完成（听起来比实际要吓人）。你可以在 http://www.sqlite.org/download.html 找到相关说明。

另一种安装 SQLite 3 的方式是通过流行的 MacPorts 包，你可以在 http://www.macports.org/install.php 找到它。虽然说明看起来有点吓人，但各个步骤其实相当直接：运行一个安装程序，再运行另一个安装程序，向文件添加两行，再运行一个安装程序，然后执行一条命令。这可能并不比你亲自从源代码编译更容易，但许多人认为这项投入是值得的，因为它让安装更多包变得像一条命令一样简单。所以，如果你已经安装了 ports，让我们升级你机器上的 SQLite 3 版本：

```
sudo port upgrade sqlite3
```

Tiger 和 Leopard 用户都可以使用以下命令来更新系统的其余部分。如果你刚刚安装了 MacPorts，请务必注意重要提示：打开一个新的 shell，并通过 env 命令验证你的路径和变量更改已生效。如果你还没有安装 Apple 的 XCode Developer Tools（Leopard 需要 3.1 或更高版本，Tiger 需要 2.4.1 或更高版本），可以在 Apple Developer Connection 网站或 Mac OS X 安装光盘/DVD 上找到。

```
sudo gem update --system
sudo gem install rails
sudo gem update rake
sudo gem install sqlite3-ruby
```

以下步骤很少有必要，但如果问题持续出现，它可能会有所帮助。你可以通过将以下代码作为独立程序运行、在 irb 中运行，或在 ruby script/console 中运行，来验证你的 sqlite3-ruby 接口绑定到哪个版本的 SQLite 3。

```
require 'rubygems'
require 'sqlite3'
tempname = "test.sqlite#{3+rand}"
db = SQLite3::Database.new(tempname)
puts db.execute('select sqlite_version()')
db.close
File.unlink(tempname)
```

#### 3.4 在 Linux 上安装

从你的平台自带的包管理系统开始，无论是 aptitude、dpkg、portage、rpm、rug、synaptic、up2date 还是 yum。

##### 升级 RubyGems

升级 RubyGems 有很多不同的方法。不幸的是，根据你安装的 RubyGems 版本和你运行的发行版，并非所有方法都有效。要有耐心。逐一尝试以下方法，直到找到适合你的那一种。

- 使用 gem update 系统：
  `sudo gem update --system`
- 使用专为更新问题系统而设计的 gem：
  `sudo gem install rubygems-update`
  `sudo update_rubygems`
- 使用 rubygems-update 附带的 setup.rb：
  `sudo gem install rubygems-update`
  `cd /var/lib/gems/1.8/gems/rubygems-update-*`
  `sudo ruby setup.rb`
- 最后，从源代码安装：
  `wget http://rubyforge.org/frs/download.php/45905/rubygems-1.3.1.tgz`
  `tar xzf rubygems-1.3.1.tgz`
  `cd rubygems-1.3.1`
  `sudo ruby setup.rb`

第一步是安装必要的依赖。以下说明适用于 Ubuntu 8.10（Intrepid Ibex）；你可以根据你的安装情况进行调整：

```
sudo aptitude update
sudo aptitude install build-essential libopenssl-ruby
sudo aptitude install ruby rubygems ruby1.8-dev libsqlite3-dev
```

在继续之前，务必确认 RubyGems 的版本至少是 1.3.1。你可以通过执行 `gem -v` 来查看版本。如何升级你的 RubyGems 版本在当前页面的侧边栏中有描述。

```
sudo gem install rails
sudo gem install sqlite3-ruby
```

在执行最后一条命令时，系统会提示你选择要为你的平台安装哪个 gem。只需选择最新的（最顶部的）在括号中包含 ruby 字样的 gem，系统就会为你构建原生扩展。

你可能还需要将 /var/lib/gems/1.8/bin 添加到你的 PATH 环境变量中。你可以通过在 .bashrc 文件中添加一行来实现：

```
export PATH=/var/lib/gems/1.8/bin:$PATH
```

#### 3.5 选择 Rails 版本

前面的说明帮助你安装了最新版本的 Rails。但有时你可能不想使用那个版本。也许本书出版后又有新版本的 Rails 发布，所以你希望绝对确信你在这里看到的示例与你正在运行的 Rails 版本完全匹配。或者，你可能在一台机器上开发，但打算部署到另一台包含你无法控制的 Rails 版本的机器上。

如果这两种情况中的任何一种适用于你，你需要了解一些事情。首先，你可以使用 gem 命令查看你安装的所有 Rails 版本：

```
gem list --local rails
```

你还可以使用 `rails --version` 命令来验证你默认运行的 Rails 版本。它应该返回 2.2.2 或更高版本。

安装另一个版本的 Rails 也是通过 gem 命令完成的。根据你的操作系统，你可能需要在命令前加上 sudo。

```
gem install rails --version 2.2.2
```

现在，如果无法选择其中一个版本，那么拥有多个 Rails 版本对任何人都没有好处。幸运的是，有办法。在任何 rails 命令中，你都可以通过在命令的第一个参数之前插入由下划线包围的完整版本号来控制使用哪个版本的 Rails：

```
rails _2.2.2_ --version
```

这在创建新应用程序时特别方便，因为一旦你使用特定版本的 Rails 创建了应用程序，它将继续使用该版本的 Rails——即使系统上安装了更新的版本——直到你决定升级。如何更改你的应用程序所使用的 Rails 版本在第 264 页的侧边栏中有描述。

最后，如果你决定使用 2.2.2 以外的版本，你并非完全孤立无援。你可以在 http://wiki.pragprog.com/changes-to-rails 找到会影响你的更改列表。

#### 3.6 开发环境

编写 Rails 程序的日常工作相当直接。每个人的工作方式都不同：以下是我们工作方式的介绍。

##### 我的 IDE 在哪里？

如果你是从 C# 和 Java 等语言转向 Ruby 和 Rails，你可能会想了解 IDE。毕竟，我们都知道，如果没有至少 100MB 的 IDE 来支持我们的每一次按键，就不可能编写现代应用程序。对于你们这些已经觉悟的人来说，这里是本书中我们建议你坐下来阅读的地方——理想情况下，两边各放一堆框架参考书和 1000 页的《轻松上手》书籍。

Ruby 或 Rails 没有功能完备的 IDE（尽管有些环境已经接近了）。相反，大多数 Rails 开发者使用普通的旧式编辑器。事实证明，这并不像你想象的那么成问题。对于其他表现力较弱的语言，程序员依赖 IDE 为他们完成大量繁重的工作：IDE 进行代码生成、辅助导航，并增量编译以提前预警错误。

然而，对于 Ruby，这些支持大多并不必要。像 TextMate 这样的编辑器能提供你从 IDE 获得的 90% 的功能，但重量要轻得多。唯一缺失的有用 IDE 功能几乎就是重构支持。*
* 我们倾向于使用一个编辑器处理所有事情。其他人则使用专门的编辑器来创建应用程序代码与（比如说）HTML 布局。对于后者，可以寻找 Dreamweaver 等流行工具的插件。

（TextMate 在从剪贴板粘贴代码时重新缩进的能力非常方便。）

- 支持插入常见的 Ruby 和 Rails 结构。你会编写大量短方法，如果 IDE 能通过一两次按键创建方法骨架，你就可以专注于内部有趣的内容。

- 良好的文件导航。正如你将看到的，Rails 应用程序分布在许多文件中。⁴ 你需要一个能帮助你在这些文件之间快速导航的环境。你会向控制器添加一行来加载一个值，切换到视图添加一行来显示它，然后切换到测试来验证你做得是否正确。像记事本那样，通过“文件打开”对话框遍历选择每个要编辑的文件，是行不通的。我们更喜欢侧边栏中的文件树视图、一组帮助我们在目录树中按名称查找文件的快捷键，以及一些内置的智能导航功能（例如在控制器动作和相应视图之间导航）。

4. 一个新创建的 Rails 应用程序包含四十八个文件，分布在三十七个目录中。这还只是在你写任何东西之前，……




+   - 名称补全。Rails 中的名称往往很长。好的编辑器会让你输入前几个字符，然后在按下一个键时为你建议可能的补全。

我们不愿推荐特定的编辑器，因为我们认真使用过的编辑器只有少数几个，而且我们肯定会遗漏某人的最爱编辑器。尽管如此，为了帮助你开始使用除 Notepad 之外的工具，这里有一些建议：

+   - Mac OS X 上 Ruby 和 Rails 首选的编辑器是 TextMate (http://macromates.com/)。
+   - Mac OS X 上的 XCode 3.0 具有 Organizer，可提供你可能需要的许多功能。关于在 Leopard 上开始使用 Rails 的教程可在 http://developer.apple.com/tools/developonrailsleopard.html 获取。
+   - 对于那些原本想使用 TextMate 但恰好使用 Windows 的人，E-TextEditor (http://e-texteditor.com/) 提供了“Windows 上的 TextMate 强大功能”。
+   - Aptana RadRails (http://www.aptana.com/rails/) 是一个在 Aptana Studio 和 Eclipse 中运行的集成 Rails 开发环境。它可在 Windows、Mac OS X 和 Linux 上运行。它在 2006 年获得了基于 Eclipse 的最佳开源开发工具奖，而 Aptana 于 2007 年成为该项目的家。
+   - NetBeans IDE 6.5 (http://www.netbeans.org/features/ruby/index.html) 支持 Windows、Mac OS X、Solaris 和 Linux。它可作为带 Ruby 支持的下载包提供，也可作为稍后下载的 Ruby 插件包提供。除了对 Rails 2.0、Rake 目标和数据库迁移的特定支持外，它还支持 Rails 代码生成器图形向导，以及从 Rails 动作快速导航到其对应的视图。
+   - jEdit (http://www.jedit.org/) 是一个功能齐全的编辑器，支持 Ruby。它具有广泛的插件支持。
+   - Komodo (http://www.activestate.com/Products/Komodo/) 是 ActiveState 为动态语言，包括 Ruby 提供的 IDE。
+   - Arachn0 Ruby (http://www.ruby-ide.com/ruby/ruby_ide_and_ruby_editor.php) 是 Ruby 的商业 IDE。

向使用你所用操作系统的经验丰富的开发者询问他们使用哪种编辑器。在确定之前，花一到一周的时间尝试不同的替代方案。而且，一旦你选择了编辑器，要以自豪为目标每天学习一个新功能。

##### 创建你自己的 Rails API 文档

你可以创建 Rails API 文档的本地合并版本。只需在命令提示符下输入以下命令（如果使用 InstantRails 或 Locomotive，请记住在 Rails 环境中启动命令窗口）：

```
rails_apps> rails dummy_app
rails_apps> cd dummy_app
dummy_app> rake rails:freeze:gems
dummy_app> rake doc:rails
```

最后一步需要一段时间。当它完成后，你将在从 doc/api 开始的目录树中拥有 Rails API 文档。我们建议将此文件夹移动到桌面，然后删除 dummy_app 树。

要查看 Rails API 文档，请用浏览器打开位置 doc/api/index.html。

##### 桌面

我们不会告诉你在使用 Rails 时如何组织桌面，但我们会描述我们的做法。

大部分时间，我们都在编写代码、运行测试，并在浏览器中查看应用程序。因此，我们的主要开发桌面始终打开一个编辑器窗口和一个浏览器窗口。我们还想关注应用程序生成的日志，因此我们保持一个终端窗口打开。在其中，我们使用 tail -f 来滚动日志文件的内容，因为它在更新。我们通常以非常小的字体运行此窗口，以便占用更少的空间——如果我们看到有意思的内容闪过，我们会放大以进行调查。

我们还需要访问 Rails API 文档，我们在浏览器中查看它。在介绍中，我们谈到了使用 gem server⁵ 命令运行包含 Rails 文档的本地 Web 服务器。这很方便，但不幸的是，它将 Rails 文档分散在多个单独的文档树中。如果你在线，可以使用 http://api.rubyonrails.org 在一个地方查看所有 Rails 文档的合并视图。

#### 3.7 Rails 和数据库

本书中的示例使用 SQLite 3 编写（版本 3.4.0 左右）。如果你想跟随我们的代码，最简单的方法也是使用 SQLite 3。如果你决定使用其他数据库，也不会有大问题。

5. 对于 RubyGems 0.9.5 之前的版本，请使用命令 gem server。

数据库驱动。你可以使用命令 which ruby 来确保你没有运行 /usr/bin 中的 Ruby。

以下是可用的数据库适配器及其各自主页的链接：

| Adapter | Home Page |
|---|---|
| DB2 | http://raa.ruby-lang.org/project/ruby-db2 or http://rubyforge.org/projects/rubyibm |
| Firebird | http://rubyforge.org/projects/fireruby/ |
| MySQL | http://www.tmtm.org/en/mysql/ruby |
| Oracle | http://rubyforge.org/projects/ruby-oci8 |
| Postgres | http://rubyforge.org/projects/ruby-pg |
| SQL Server | http://github.com/rails-sqlserver |
| SQLite | http://rubyforge.org/projects/sqlite-ruby |

Postgres 适配器的纯 Ruby 版本可用。从 Ruby-DBI 页面 http://rubyforge.org/projects/ruby-dbi 下载 postgres-pr。

MySQL 和 SQLite 适配器也可用作 RubyGems 下载（分别为 mysql 和 sqlite3-ruby）。

#### 3.8 保持最新

假设你使用 RubyGems 安装了 Rails，保持最新相对容易。发出以下命令：

```
rubys> gem update rails
```

RubyGems 将自动更新你的 Rails 安装。⁶（我们将在部署和生产章节中，从第 651 页开始，关于在生产环境中更新你的应用程序会有更多说明。）RubyGems 会保留它安装的库的先前版本。你可以用以下命令删除它们：

```
rubys> gem cleanup
```

安装新版本的 Rails 后，你可能还想更新 Rails 最初添加到你的应用程序中的文件（它用于 Ajax 支持的 JavaScript 库、各种脚本等）。你可以通过在应用程序的顶级目录中运行以下命令来做到这一点：

```
rubys> rake rails:update
```

#### 3.9 Rails 和 ISP

如果你想在共享托管环境中将 Rails 应用程序上线，你需要找到一个精通 Ruby 的 ISP。寻找支持 Ruby、具有你需要的 Ruby 数据库驱动程序，并提供 Phusion Passenger 和/或

6. 较早版本的 gem 可能需要 --include-dependencies 选项。

### 第 4 章

### 即时满足

让我们编写一个简单的应用程序，以验证我们是否已在机器上稳妥地安装了 Rails。在此过程中，我们将一窥 Rails 应用程序的工作方式。

#### 4.1 创建新应用程序

当你安装 Rails 框架时，你还会获得一个名为 rails 的新命令行工具，用于构建你编写的每个新的 Rails 应用程序。

我们为什么需要一个工具来做这件事？我们为什么不能只在我们最喜欢的编辑器中随意编写并从头创建应用程序的源代码？好吧，我们可以随意编写。毕竟，Rails 应用程序只是 Ruby 源代码。但 Rails 还在幕后做了很多魔法，以使我们的应用程序以最少的显式配置工作。为了使这种魔法发挥作用，Rails 需要找到应用程序的各个组件。正如我们稍后会看到的（第 15.2 节，目录结构，第 257 页），这意味着我们需要创建特定的目录结构，将我们编写的代码插入到适当的位置。rails 命令只是为我们创建此目录结构并用一些标准的 Rails 代码填充它。

要创建你的第一个 Rails 应用程序，打开一个 shell 窗口，并导航到文件系统中你想要创建应用程序目录结构的位置。在我们的示例中，我们将在名为 work 的目录中创建项目。在该目录中，使用 rails 命令创建一个名为 demo 的应用程序。这里要稍微小心一点——如果你已有名为 demo 的现有目录，将会询问你是否要覆盖任何现有文件。¹

```
rubys> cd work
work> rails demo
create
create  app/controllers
```

1. 另外，如果你想指定要使用的 Rails 版本（如第 3.5 节，选择 Rails 版本，第 36 页所述），现在就是这样做的时候。




```
create  app/helpers
create  app/models
:       :       :
create  log/development.log
create  log/test.log
work>
```

该命令创建了一个名为 demo 的目录。进入该目录并列出其内容（在 Unix 上使用 `ls`，在 Windows 下使用 `dir`）。你会看到一批文件和子目录：

```
work> cd demo
demo> ls -p
README           config/      lib/         script/      vendor/
Rakefile         db/          log/         test/
app/             doc/         public/      tmp/
```

所有这些目录（及其包含的文件）起初可能让人望而生畏，但我们现在可以先忽略其中大部分。在本章中，我们只会直接用到其中两个：`app` 目录，用于编写我们的应用程序；以及 `script` 目录，其中包含一些有用的实用脚本。

让我们从 `script` 子目录开始。其中包含的一个脚本名为 `server`。这个脚本会启动一个独立的 Web 服务器，可以在 WEBrick 下运行我们新创建的 Rails 应用程序。² 闲话少说，让我们启动演示应用程序：

```
demo> ruby script/server
=> Booting WEBrick...
=> Rails application started on http://0.0.0:3000
=> Ctrl-C to shutdown server; call with --help for options
[2006-01-08 21:44:10] INFO  WEBrick 1.3.1
[2006-01-08 21:44:10] INFO  ruby 1.8.2 (2004-12-30) [powerpc-darwin8.2.0]
[2006-01-08 21:44:11] INFO  WEBrick::HTTPServer#start: pid=10138 port=3000
```

正如启动跟踪信息的最后一行所示，我们刚刚在 3000 端口启动了一个 Web 服务器。³ 通过在浏览器中指向 URL http://localhost:3000，我们可以访问该应用程序。结果如图 4.1 所示。

如果你查看启动 WEBrick 的那个窗口，你会看到显示你正在访问该应用程序的跟踪信息。我们将让 WEBrick 在这个控制台窗口中继续运行。稍后，当我们编写应用程序代码并通过浏览器运行它时，

> 2. WEBrick 是一个纯 Ruby 编写的 Web 服务器，随 Ruby 1.8.1 及更高版本一起分发。由于它保证可用，Rails 将其用作开发 Web 服务器。然而，如果你的系统安装了 Mongrel Web 服务器（且 Rails 能找到它），`script/server` 命令将优先使用它而不是 WEBrick。你可以通过向以下命令提供一个选项来强制 Rails 使用 WEBrick：
> `demo>ruby script/server webrick`

> 3. 地址中的 0.0.0.0 部分表示 WEBrick 将接受所有接口上的连接。在 Dave 的 OS X 系统上，这意味着两个本地接口（127.0.0.1 和 ::1）以及他的局域网连接。

![](img/a160fc3a330a0b3b2a764d41d614e688_45_0.png)

# 图 4.1：新创建的 Rails 应用程序

此时，我们有一个新应用程序在运行，但它还没有包含我们的任何代码。让我们来纠正这种情况。

#### 4.2 你好，Rails！

我们忍不住——我们就是要写一个 “Hello, World!” 程序来尝试新系统。在 Rails 中，这相当于一个向浏览器发送我们欢快问候的应用程序。

正如我们在第 2 章 “Rails 应用程序架构”（第 22 页）中所见，Rails 是一个模型-视图-控制器框架。Rails 接受来自浏览器的传入请求，解码请求以找到控制器，并在该控制器中调用动作方法。然后控制器调用一个特定的视图来向用户显示结果。好消息是，Rails 处理了连接所有这些动作的大部分内部管道代码。要编写我们简单的 “Hello, World!” 应用程序，我们需要控制器和视图的代码。我们不需要模型的代码，因为我们不处理任何数据。让我们从控制器开始。

与我们使用 `rails` 命令创建新的 Rails 应用程序的方式相同，我们也可以使用生成器脚本为项目创建新的控制器。这个命令称为 `generate`，它位于我们创建的 demo 项目的 `script` 子目录中。因此，要创建一个名为 Say 的控制器，我们要确保在 demo 目录中，然后运行该脚本，并传入我们要创建的控制器名称。⁴

```
demo> ruby script/generate controller Say
exists  app/controllers/
exists  app/helpers/
create  app/views/say
exists  test/functional/
create  app/controllers/say_controller.rb
create  test/functional/say_controller_test.rb
create  app/helpers/say_helper.rb
```

该脚本会记录它检查的文件和目录，并注明何时向你的应用程序添加新的 Ruby 脚本或目录。目前，我们只对其中一个脚本以及（稍后）新的目录感兴趣。

我们将要查看的源文件是控制器。你可以在 `app/controllers/say_controller.rb` 文件中找到它。让我们来看一下：

```
Download work/demo1/app/controllers/say_controller.rb
```

```
class SayController < ApplicationController
end
```

相当简洁，是吧？SayController 是一个继承自 ApplicationController 的空类，因此它自动获得所有默认的控制器行为。让我们把它变得更有趣。我们需要添加一些代码，让我们的控制器处理传入的请求。这些代码需要做什么？目前它什么都不用做——我们只需要一个空的动作方法。那么，下一个问题是，这个方法应该叫什么？为了回答这个问题，我们需要看看 Rails 处理请求的方式。

##### Rails 与请求 URL

与任何其他 Web 应用程序一样，Rails 应用程序在用户看来与一个 URL 相关联。当你在浏览器中访问该 URL 时，你是在与应用程序代码通信，它会为你生成响应。

然而，实际情况要比这复杂一些。假设你的应用程序可以通过 URL http://pragprog.com/ 访问。托管你应用程序的 Web 服务器对路径相当智能。它知道发送到该 URL 的传入请求必定是在与应用程序通信。传入 URL 中超过此处的任何内容都不会改变这一点——同一个应用程序仍会被调用。任何额外的路径信息都会传递给应用程序，应用程序可将其用于自身的内部目的。

Rails 使用路径来确定要使用的控制器名称以及要在该控制器上调用的动作名称。⁵ 图 4.2 展示了这一点。路径的第一部分是控制器名称，路径的第二部分是动作名称。这显示在下一页的图 4.3 中。

![](img/a160fc3a330a0b3b2a764d41d614e688_47_0.png)

图 4.2：URL 被映射到控制器和动作。

##### 我们的第一个动作

让我们为 Say 控制器添加一个名为 hello 的动作。从前面的讨论中我们知道，添加 hello 动作意味着在 SayController 类中创建一个名为 hello 的方法。但它应该做什么呢？目前，它不需要做任何事情。请记住，控制器的工作是设置好相关事务，以便视图知道要显示什么。在我们的第一个应用程序中，没有什么需要设置的，因此空动作就可以了。使用你喜欢的编辑器修改 `app/controllers` 目录中的 `say_controller.rb` 文件，添加如下所示的 `hello` 方法，然后保存文件：

```
Download work/demo1/app/controllers/say_controller.rb
class SayController < ApplicationController
  def hello
  end
end
```

> 5. Rails 在解析传入 URL 时相当灵活。在本章中，我们描述默认机制。我们将在第 426 页的 21.2 节 “路由请求” 中展示如何覆盖此机制。

http://pragprog.com/say/hello

创建 SayController 的一个实例，并调用动作方法 hello

```
class UserController
```

```
class SayController
```

```
class ProductController
```

```
class LoginController
  def login
    # code . . .
  end
end
```

```
class SayController
  def hello
    # code for hello action
  end
end
```

图 4.3：Rails 路由到控制器和动作。

现在让我们尝试调用它。在浏览器窗口中导航到 URL http://localhost:3000/say/hello。（注意，在开发环境中，路径前面没有任何应用程序字符串——我们直接路由到控制器。）你会看到类似下面的内容：⁶

![](img/a160fc3a330a0b3b2a764d41d614e688_48_0.png)

这可能令人烦恼，但这个错误完全合理（除了奇怪的路径）。我们创建了控制器类和动作方法，但还没有告诉 Rails 要显示什么。而这正是视图发挥作用的地方。还记得我们运行脚本创建新控制器的时候吗？该命令添加了

> 6. 如果你反而看到类似 “No route matches "/say/hello"” 的消息，请尝试停止并重新启动服务器，因为你所做的一些事情导致 Rails 在控制器创建之前缓存了配置信息。




将三个文件和一个新目录添加到我们的应用程序中。该目录将包含控制器视图的模板文件。在我们的例子中，我们创建了一个名为 say 的控制器，因此视图将位于目录 app/views/say 中。

为了完成我们的“Hello, World!” 应用程序，让我们创建一个模板。默认情况下，Rails 会在与正在处理的动作同名的文件中查找模板。在我们的例子中，这意味着我们需要在目录 app/views/say 中创建一个名为 hello.html.erb⁷ 的文件。（为什么是 .html.erb？我们一分钟后会解释。）现在，让我们只在其中放入一些基本的 HTML：

```
Download work/demo1/app/views/say/hello.html.erb
<html>
  <head>
    <title>Hello, Rails!</title>
  </head>
  <body>
    <h1>Hello from Rails!</h1>
  </body>
</html>
```

保存文件 hello.html.erb，然后刷新浏览器窗口。你应该会看到它显示我们的友好问候。注意，我们不需要重新启动应用程序即可看到更新。在开发期间，Rails 会在你保存文件时自动将更改集成到正在运行的应用程序中：

![](img/a160fc3a330a0b3b2a764d41d614e688_49_0.png)

到目前为止，我们已在 Rails 应用程序树中添加了两个文件。我们向控制器添加了一个动作，并创建了一个模板来在浏览器中显示页面。这些文件位于 Rails 层次结构中的标准位置：控制器放在 app/controllers 中，视图放在 app/views 的子目录中。这在下一页的图 4.4 中显示。

#### 使其动态化

到目前为止，我们的 Rails 应用程序相当无聊——它只是显示一个静态页面。为了使其更具动态性，让我们在每次显示页面时显示当前时间。

为此，我们需要对视图中的模板文件进行更改——它现在需要以字符串的形式包含时间。这提出了两个问题。首先，我们如何向模板添加动态内容？其次，我们从哪里获取时间？

7. 在 Rails 的早期版本中，该文件将被称为 hello.rhtml。

![](img/a160fc3a330a0b3b2a764d41d614e688_50_0.png)

图 4.4：控制器和视图的标准位置

##### 动态内容

在 Rails 中创建动态模板有两种方法。⁸ 其中一种使用名为 Builder 的技术，我们将在第 23.1 节 Builder Templates，第 510 页讨论。第二种方法，我们在这里使用，是在模板本身中嵌入 Ruby 代码。这就是我们将模板文件命名为 hello.html.erb 的原因；.html.erb 后缀告诉 Rails 使用一个名为 ERb 的系统来扩展文件中的内容。

ERb 是一个过滤器，它接收一个 .erb 文件并输出转换后的版本。输出文件在 Rails 中通常是 HTML，但可以是任何内容。普通内容会原样通过而不被更改。然而，位于 <%= 和 %> 之间的内容会被解释为 Ruby 代码并执行。该执行的結果会被转换为字符串，并以该值替换文件中的 <%=...%> 序列。例如，将 hello.html.erb 改为包含以下内容：

```
Download erb/ex1.html.erb
<ul>
  <li>Addition: <%= 1+2 %> </li>
  <li>Concatenation: <%= "cow" + "boy" %> </li>
  <li>Time in one hour: <%= 1.hour.from_now %> </li>
</ul>
```

8. 实际上有三种方法，但第三种 RJS 仅用于为已显示的页面添加 Ajax 魔法。我们将在第 600 页讨论 RJS。

当你刷新浏览器时，模板将生成以下 HTML：

```
<ul>
<li>Addition: 3 </li>
<li>Concatenation: cowboy </li>
<li>Time in one hour: Fri May 23 14:30:32 -0400 2008 </li>
</ul>
```

在浏览器窗口中，你会看到类似以下内容：

- Addition: 3
- Concatenation: cowboy
- Time in one hour: Fri May 23 14:30:32 -0400 2008

此外，.html.erb 文件中位于 <% 和 %> 之间（没有等号）的內容会被解释为执行的 Ruby 代码，但不会替换回输出中。有趣的是，这种处理可以与非 Ruby 代码混合使用。例如，我们可以制作一个节日版的 hello.html.erb：

```
<% 3.times do %>
Ho!<br />
<% end %>
Merry Christmas!
```

这将生成以下 HTML：

Download erb/ex2.html.erb

```
Ho!<br />

Ho!<br />

Ho!<br />

Merry Christmas!
```

注意文件中的文本在 Ruby 循环的每次迭代中都会被发送到输出流一次。

但这里还有一件奇怪的事情。所有空白行是从哪里来的？它们来自输入文件。如果你想想看，原文件在第一行和第三行的 %> 之后都包含一个换行符（或字符）。因此，<% 3.times do %> 被从文件中剥离，但换行符保留下来。每次循环时，此换行符都会添加到输出文件中，并附带 Ho! 行的完整文本。这就解释了输出中每个 Ho! 行之前的空白行。同样，<% end %> 之后的换行符也解释了最后一个 Ho! 行与 Merry Christmas! 行之间的空白行。

通常这无关紧要，因为 HTML 对空白并不太在意。然而，如果你使用此模板机制来创建电子邮件或 <pre> 块中的 HTML，你会希望删除这些空白行。方法是

将 ERb 序列的结尾从 %> 改为 -%>。该减号告诉 Rails 从输出中删除其后的任何换行符。如果我们在 3.times 行上添加一个减号，像这样：

```
Download erb/ex2a.html.erb

<% 3.times do -%>
Ho!<br />
<% end %>
Merry Christmas!
```

我们得到以下结果：⁹

```
Ho!<br />
Ho!<br />
Ho!<br />

Merry Christmas!
```

在包含 end 的行上添加一个减号，像这样：

```
Download erb/ex2b.html.erb

<% 3.times do -%>
Ho!<br />
<% end -%>
Merry Christmas!
```

以消除 Merry Christmas! 之前的空白行：

```
Ho!<br />
Ho!<br />
Ho!<br />
Merry Christmas!
```

通常，是否抑制这些换行符是品味问题，而非必要问题。然而，你会在野外的 Rails 代码中看到这种使用减号的方式，因此最好知道它做了什么。

在下面的示例中，循环设置了一个变量，该变量在每次循环执行时都会被插值到文本中：

```
Download erb/ex3.html.erb

<% 3.downto(1) do |count| -%>
<%= count %>...<br />
<% end -%>
Lift off!
```

> 9. 如果你仍在输出中看到空白行，请检查行末是否没有多余的空白字符。为此生效，-%> 字符必须是该行的最后一个字符。

当我们刷新浏览器窗口时，我们会看到时间以 Ruby 的标准格式显示：

![](img/a160fc3a330a0b3b2a764d41d614e688_55_0.png)

注意，如果你在浏览器中点击刷新，每次显示页面时时间都会更新。看起来我们确实在生成动态内容。

为什么我们要费心在控制器中设置要显示的时间，然后在视图中使用它？好问题。在此应用程序中，我们本可以直接在模板中嵌入对 Time.now 的调用，但通过将其放在控制器中，我们获得了某些好处。例如，我们未来可能希望扩展应用程序以支持多个国家的用户。在这种情况下，我们希望本地化时间的显示，选择适合用户区域设置的格式以及适合其时区的時間。这将是一定量的应用程序级代码，并且可能不适合嵌入在视图级别。通过在控制器中设置要显示的时间，我们使应用程序更具灵活性——我们可以更改控制器中显示格式和时区，而无需更新使用该时间对象的任何视图。时间是数据，应由控制器提供给视图。我们在引入模型后会看到更多这种情况。

##### 到目前为止的故事

让我们简要回顾一下我们当前应用程序的工作方式：

1. 用户导航到我们的应用程序。在我们的例子中，我们使用类似 http://localhost:3000/say/hello 的本地 URL 来执行此操作。
2. Rails 分析 URL。say 部分被视为控制器的名称，因此 Rails 创建了 Ruby 类 SayController 的一个新实例（它在 app/controllers/say_controller.rb 中找到）。
3. URL 路径的下一部分，hello，标识一个动作。Rails 在控制器中调用同名的方法。此动作方法创建一个保存当前时间的新 Time 对象，并将其存放在 @time 实例变量中。
4. Rails 查找要显示结果的模板。它在 app/views 目录中搜索与控制器同名的子目录（say），并在该子目录中搜索以动作命名的文件（hello.html.erb）。





让我们把这个动作命名为 goodbye。我们的控制器现在看起来如下：

Download work/demo3/app/controllers/say_controller.rb

```ruby
class SayController < ApplicationController
  def hello
    @time = Time.now
  end

  def goodbye
  end
end
```

接下来我们需要在目录 `app/views/say` 中创建一个新的模板。这次它叫做 `goodbye.html.erb`，因为默认情况下模板会以其关联的动作命名。

Download work/demo3/app/views/say/goodbye.html.erb

```html
<html>
  <head>
    <title>See You Later!</title>
  </head>
  <body>
    <h1>Goodbye!</h1>
    <p>
      It was nice having you here.
    </p>
  </body>
</html>
```

再次启动我们可靠的浏览器，但这次使用 URL http://localhost:3000/say/goodbye 指向我们的新视图。你应该会看到类似这样的内容：

![](img/a160fc3a330a0b3b2a764d41d614e688_57_0.png)

现在我们需要链接这两个屏幕。我们将在 hello 屏幕上放置一个链接，带我们到 goodbye 屏幕，反之亦然。在真正的应用程序中，我们可能希望将这些做成适当的按钮，但现在我们只使用超链接。

我们已经知道 Rails 使用约定来将 URL 解析为目标控制器和该控制器中的一个动作。因此，一个简单的方法是为我们的链接采用这种 URL 约定。

文件 `hello.html.erb` 将包含以下内容：

```html
<html>
  ...
  <p>
    Say <a href="/say/goodbye">Goodbye</a>!
  </p>
  ...
```

而文件 `goodbye.html.erb` 将指向另一边：

```html
<html>
  ...
  <p>
    Say <a href="/say/hello">Hello</a>!
  </p>
  ...
```

这种方法当然会起作用，但有点脆弱。如果我们将应用程序移动到 Web 服务器上的不同位置，URL 将不再有效。它还将 Rails URL 格式的假设编码到我们的代码中；未来版本的 Rails 可能会改变这一点。

幸运的是，这些不是我们必须承担的风险。Rails 带有许多可以在视图模板中使用的辅助方法。这里，我们将使用辅助方法 `link_to`，它会创建一个指向某个动作的超链接。¹⁰ 使用 `link_to`，`hello.html.erb` 变为如下：

Download work/demo4/app/views/say/hello.html.erb

```html
<html>
  <head>
    <title>Hello, Rails!</title>
  </head>
  <body>
    <h1>Hello from Rails!</h1>
    <p>
      It is now <%= @time %>.
    </p>
    <p>
      Time to say
      <%= link_to "Goodbye!", :action => "goodbye" %>
    </p>
  </body>
</html>
```

在 ERb `<%=...%>` 序列中有一个 `link_to` 调用。这会创建一个链接到将调用 goodbye 动作的 URL。对 `link_to` 的调用中的第一个参数是要在超链接中显示的文本，而下一个参数告诉 Rails 生成指向 goodbye 动作的链接。因为我们没有指定控制器，所以将使用当前控制器。

> 10. link_to 方法可以做更多的事情，但让我们现在慢慢来....

#### 4.4 我们刚刚做了什么

在本章中，我们构建了一个玩具应用程序。做这件事向我们展示了以下内容：

- 如何创建一个新的 Rails 应用程序以及如何在该应用程序中创建一个新的控制器
- Rails 如何将传入的请求映射到你代码上的调用
- 如何在控制器中创建动态内容并通过视图模板显示它
- 如何链接页面

这是一个很好的基础。现在让我们开始构建真正的应用程序。

##### 玩耍时间

这里有一些你可以自己尝试的内容：

- 为 say 应用程序编写一个页面，说明你在 ERb 中可以做的循环。
- 尝试在 ERb `<%= %>` 序列末尾添加和删除减号（换句话说，将 `%>` 更改为 `-%>`，反之亦然）。使用浏览器的 查看 → 源 选项查看差异。
- 对以下 Ruby 方法的调用返回当前目录中的所有文件列表：

  `@files = Dir.glob('*')`

  在控制器动作中使用它来设置实例变量，然后编写相应的模板，在浏览器上以列表形式显示文件名。

  提示：在 ERb 示例中，我们看到了如何迭代 n 次。你可以使用类似这样的东西迭代集合：

  ```erb
  <% for file in @files %>
  file name is: <%= file %>
  <% end %>
  ```

  你可能想使用 `<ul>` 来表示列表。

（你可以在 http://pragprog.wikidot.com/rails-play-time 找到提示。）

##### 清理

也许你一直在跟着做并编写本章的代码。如果是这样，很可能应用程序仍在你的计算机上运行。当我们在十页左右开始编写下一个应用程序时，我们第一次运行它时会遇到冲突，因为它也将尝试使用计算机的端口 3000 与浏览器通信。现在是停止当前应用程序的好时机，通过在你用来启动它的窗口中按 Ctrl-C 来停止它。

## 第二部分

## 构建应用程序

### 第 5 章

### Depot 应用程序

我们可以在一天中随意拼凑简单的测试应用程序，但这不会帮助我们支付账单。所以，让我们深入点更有分量的东西。让我们创建一个名为 Depot 的基于 Web 的购物车应用程序。

世界还需要另一个购物车应用程序吗？不，但这并没有阻止数百名开发人员编写一个。为什么我们要与众不同？

更严肃地说，我们的购物车将说明 Rails 开发的许多特性。我们将看到如何创建简单的维护页面，链接数据库表，处理会话并创建表单。在接下来的八章中，我们还将涉及单元测试、安全性和页面布局等外围主题。

#### 5.1 增量开发

我们将逐步开发这个应用程序。我们不会在开始编码之前尝试指定一切。相反，我们将制定足够的规范让我们开始，然后立即创建一些功能。我们将尝试想法，收集反馈，然后继续进行另一个迷你设计和开发的循环。

这种编码风格并不总是适用。它需要与应用程序用户密切合作，因为我们希望在进行过程中收集反馈。我们可能会犯错误，或者客户可能会发现他们要求的是一个东西，但实际上想要的是另一个。无论原因是什么——我们越早发现我们犯了错误，修复该错误的成本就越低。总的来说，在这种开发风格下，我们在进行过程中会有很多变化。

因此，我们需要使用一套不会因为我们改变主意而惩罚我们的工具集。如果我们决定需要在数据库表中添加一个新列或更改页面之间的导航，我们需要能够在那里进行更改，而无需大量的编码或配置麻烦。正如你将看到的，Ruby on Rails 在处理变化方面表现出色——它是理想的敏捷编程环境。

无论如何，继续进行应用程序。

#### 5.2 Depot 做什么

让我们开始为 Depot 应用程序草拟一个大纲规范。我们将查看高级用例并勾勒出通过网页的流程。我们还将尝试弄清楚应用程序需要什么数据（承认我们的初始猜测很可能错误）。

##### 用例

用例只是一个关于某个实体如何使用系统的陈述。顾问发明了这种短语来标记我们一直都知道的事情——这是商业生活的扭曲，华丽的词总是比朴素的词更贵，即使朴素的词更有价值。

Depot 的用例很简单（有些人会说悲惨地简单）。我们从确定两个不同的角色或参与者开始：买家和卖家。

买家使用 Depot 浏览我们要出售的产品，选择一些购买，并提供创建订单所需的信息。

卖家使用 Depot 维护要出售的产品列表，确定正在等待发货的订单，并将订单标记为已发货。（卖家还使用 Depot 来赚取大量金钱并退休到热带岛屿，但这是另一本书的主题。）

就目前而言，这就是我们需要的所有细节。我们可以详细说明维护产品意味着什么以及什么构成准备发货的订单，但为什么要费心？如果有不明显细节，我们很快就会在向客户展示我们工作的连续迭代时发现它们。

说到获取反馈，让我们不要忘记现在就获取一些——让我们通过询问我们的用户来确保我们的初始（承认很粗略）用例是正确的。假设用例通过了检验，让我们弄清楚应用程序将如何从其各种用户的角度工作。

##### 页面流程

我们总是喜欢对应用程序中的主要页面有一个想法，并大致了解用户如何在它们之间导航。这个开发阶段的这些页面流程可能不完整，但它们仍然帮助我们专注于需要做什么并了解动作的顺序。




有些人喜欢用 Photoshop、Word 或（天哪）HTML 来模拟 Web 应用的页面流程。我们则喜欢用铅笔和纸张。这样更快，而且客户也能参与其中，拿起铅笔直接在纸上涂改。

![](img/a160fc3a330a0b3b2a764d41d614e688_64_0.png)

图 5.1：买家页面流程

买家流程的第一版草图如图 5.1 所示。它相当传统。买家看到一个目录页面，一次选择一个产品。每选择一个产品，该产品就会被添加到购物车中，并且每次选择后都会显示购物车。买家可以继续使用目录页面购物，也可以结账并购买购物车中的物品。在结账过程中，我们收集联系方式和付款详细信息，然后显示收据页面。我们还不知道如何处理付款，因此这些细节在流程中相当模糊。

卖家流程如图 5.2（下一页）所示，也相当简单。登录后，卖家看到一个菜单，可以让她创建或查看产品，或者发货现有订单。一旦查看产品，卖家可以选择编辑产品信息或彻底删除该产品。

![](img/a160fc3a330a0b3b2a764d41d614e688_65_0.png)

图 5.2：卖家页面流程

发货选项非常简单。它逐页显示每个尚未发货的订单，每页一个订单。卖家可以选择跳到下一个订单，或者根据页面上的信息适当发货。

发货功能显然在现实世界中不会长久存在，但发货也是那些现实往往比想象中更奇特的领域之一。如果一开始就过度规定，我们很可能会出错。目前就让它保持原样吧，我们有信心随着用户对我们应用的使用经验增加而进行更改。

##### 数据

最后，我们需要考虑将要处理的数据。

请注意，我们这里没有使用诸如 schema 或 classes 之类的词汇。我们也没有谈论数据库、表、键等东西。我们只是在谈论数据。在开发的这个阶段，我们甚至不知道是否会使用数据库——有时一个平面文件就能轻松胜过数据库表。

基于用例和流程，我们很可能会处理图 5.3（下一页）中所示的数据。同样，使用铅笔和纸张似乎比某些花哨的工具容易得多，但请使用任何对你有用的方法。

![](img/a160fc3a330a0b3b2a764d41d614e688_66_0.png)

图 5.3：对应用数据的初步猜测

在绘制数据图时引发了一些问题。当用户购买物品时，我们需要某个地方来保存他们购买的产品列表，因此我们添加了购物车。但除了作为临时保存此产品列表的地方外，购物车似乎有点像幽灵——我们找不到任何有意义的存储内容。为了反映这种不确定性，我们在图中的购物车框内加了一个问号。我们假设这种不确定性将在实现 Depot 时得到解决。

提出高级别数据也引发了一个问题：订单中应该包含哪些信息？同样，我们选择暂时保持相当开放——当我们开始向客户展示早期迭代时，我们将进一步细化。

最后，你可能已经注意到我们在订单项数据中复制了产品的价格。这里我们稍微违反了“一开始保持简单”的规则，但这是基于经验的越界行为。如果产品价格发生变化，该价格变化不应反映在当前未完成订单的订单项价格中，因此每个订单项需要反映下订单时产品的价格。

同样，在这一点上，我们会与客户再次确认我们是否仍在正确的轨道上。（在我们绘制这三张图时，客户很可能就坐在我们旁边。）

##### 一般恢复建议

本书中的所有内容都经过测试。如果你严格按照此场景操作，在 Linux、Mac OS X 或 Windows 上使用 SQLite3 和已发布的 Rails 2.2.2 版本，那么一切应该按描述的那样工作。然而，偏离此路径的情况可能会发生。即使是最好的人也会打错字，而且旁支探索不仅可能，而且受到积极鼓励。请注意，这可能会将你引向奇怪的地方。不要害怕：针对常见问题的具体恢复措施出现在这些问题经常发生的特定章节中。这里还包括一些额外的一般性建议。

你只需要在书中注明需要这样做的少数几个地方重启服务器。但在某些情况下，特别是使用较早版本的 Rails 时，重启服务器可能是必要的。

一些值得了解的“神奇”命令，稍后会详细说明，包括 `rake db:sessions:clear` 和 `rake db:migrate:redo`。

如果你的服务器不接受表单上的某些输入，请在浏览器中刷新表单并重新提交。

#### 5.3 开始编码

因此，在与客户坐下来进行一些初步分析之后，我们准备开始使用计算机进行开发了！我们将从最初的三个图表开始工作，但我们很有可能会很快丢弃它们——随着我们收集反馈，它们将变得过时。有趣的是，这正是我们没有在它们身上花太多时间的原因——如果你没有花很长时间创建某样东西，就更容易丢弃它。

在接下来的章节中，我们将基于当前的理解开始开发应用程序。然而，在我们翻过那一页之前，我们只需再回答一个问题：我们首先应该做什么？

我们喜欢与客户合作，以便共同确定优先级。在这种情况下，我们会向她指出，在系统中定义一些基本产品之前，很难开发其他任何东西，因此我们建议花几个小时让产品维护功能的初始版本运行起来。当然，她会同意的。

### 第 6 章：任务 A：产品维护

在本章中，我们将看到

- 创建新应用程序，
- 配置数据库，
- 创建模型和控制器，
- 运行数据库迁移，
- 执行验证和错误报告，以及
- 使用视图和助手。

我们的第一个开发任务是创建 Web 界面，使我们能够维护产品信息——创建新产品、编辑现有产品、删除不需要的产品等等。我们将以小迭代的方式开发此应用程序，其中“小”意味着“以分钟为单位”。让我们开始吧。

#### 6.1 迭代 A1：让某些东西运行起来

也许令人惊讶的是，我们几乎可以立即让这个迭代的第一版工作起来。我们将从创建一个新的 Rails 应用程序开始。这就是我们将进行所有工作的地方。接下来，我们将创建一个数据库来保存我们的信息（实际上，我们将创建三个数据库）。一旦基础工作就绪，我们将执行以下操作：

- 配置我们的 Rails 应用程序以指向我们的数据库。
- 创建用于保存产品信息的表。
- 让 Rails 为我们生成产品维护应用程序的初始版本。

##### 创建 Rails 应用程序

回到第 44 页，我们看到了如何创建新的 Rails 应用程序。转到命令提示符，输入 `rails` 加上我们项目的名称。在这种情况下，我们的项目名为 depot，因此输入：

```
work> rails depot
```

我们看到大量输出滚动而过。当它完成后，我们发现创建了一个新目录 depot。那将是我们开展工作的地点。

```
work> cd depot
depot> ls -p
README          config/         lib/            script/         vendor/
Rakefile        db/             log/            test/
app/            doc/            public/         tmp/
```

将连接信息嵌入代码中的方法也不灵活。你可能会在编写代码时使用开发数据库。接下来你可能需要使用测试数据库运行相同的代码。最终，你会希望将其部署到生产环境中。每次切换目标数据库时，都必须编辑连接调用。有一条编程规则说，只有在将应用程序切换到生产环境时，你才会输错密码。

聪明的开发人员会将连接信息保留在代码之外。有时你可能希望使用某种存储库来存储所有信息。Java 开发人员经常使用 JNDI 来查找连接参数，但这对我们将要编写的普通 Web 应用程序来说有点沉重，因此 Rails 简单地使用平面文件。你可以在 `config/database.yml` 中找到它：

```
# ... some comments ...

development:
  adapter: sqlite3
  database: db/development.sqlite3
  pool: 5
  timeout: 5000
```

database.yml 包含有关数据库连接的信息。它包含三个部分，分别对应开发、测试和生产数据库。如果你决定叛逆并使用不同的配置，那么此文件中将需要不同的内容。你可能甚至需要直接编辑此文件。

但在此之前，让我们重新开始。删除 Rails 为你生成的所有文件，并生成一套新的。毕竟，你还没有在这些文件上投入太多。只需输入：

```
depot> cd ..
work> rm -rf depot
work> rails --database=mysql depot
work> cd depot
```

新的 database.yml 文件将类似于以下内容：

```
development:
  adapter: mysql
  encoding: utf8
  database: depot_development
  username: root
  password:
  host: localhost
```

2. 名称中的 .yml 部分表示 YAML，或“YAML ain't a markup language”（YAML 不是一种标记语言）。这是一种在平面文件中存储结构化信息的简单方式（而且它不是 XML）。自 2003 年以来发布的 Ruby 都内置了 YAML 支持。
3. 命令 `rails --help` 列出了可用的数据库选项。Windows 用户将希望使用 `rd /S /Q depot` 命令而不是 `rm -rf depot`。





可能在你的默认 `database.yml` 文件中会出现或不会出现的还有一些额外参数。

- `socket:` 告诉 MySQL 数据库适配器在何处找到用于与 MySQL 服务器通信的 socket。如果该值不正确，Rails 可能无法找到 MySQL socket。如果你在连接数据库时遇到问题，可以尝试注释掉这一行（在前面加上 `#`）。或者，你也可以通过运行命令 `mysql_config --socket` 来找到 socket 的正确路径。
- `timeout:` 告诉 SQLite 3 数据库适配器在需要获取独占锁时，你愿意等待多长时间，以毫秒为单位。
- `pool:` 告诉 Rails 你的应用程序可以同时拥有多少个与数据库服务器的连接。

记住，如果你只是刚开始并且对使用 Rails 默认设置感到满意，就不必担心所有这些配置细节。

##### 测试你的配置

如果你选择让 Rails 根据你的数据库配置创建数据库，现在就是执行的时候了。Rails 提供了一个 Rake 任务，可以为你处理这件事：

```
depots> rake db:create RAILS_ENV='development'
```

在我们继续之前，我们最好先测试一下目前的配置——我们可以检查 Rails 是否能够连接到我们的数据库，并且它是否具有创建表所需的访问权限。从应用程序的顶层目录，在命令行中输入以下神奇的咒语。（它是神奇的，因为你现在并不真的需要知道它在做什么。你以后会弄清楚的。）

```
depots> rake db:migrate
```

会发生两种情况之一。 要么回显一行（例如说 `(in /Users/dave/work/depot)`），要么出现某种错误。错误意味着 Rails 目前无法使用你的数据库。如果你看到错误，不要惊慌！这很可能是一个简单的配置问题。可以尝试以下操作：

- 检查你在 `database.yml` 的 `development:` 部分中为数据库指定的名称。它应与你创建的数据库名称相同（使用 `mysqladmin` 或其他数据库管理工具）。
- 检查 `database.yml` 中的用户名和密码是否与第 70 页上创建的一致。
- 检查你的数据库服务器是否正在运行。

首先，我们将启动一个本地基于 WEBrick 的 Web 服务器，由 Rails 提供：

```
depots> ruby script/server
=> Booting WEBrick...
=> Rails application started on http://0.0.0.0:3000
=> Ctrl-C to shutdown server; call with --help for options
[2008-03-27 11:54:55] INFO  WEBrick 1.3.1
[2008-03-27 11:54:55] INFO  ruby 1.8.6 (2007-09-24) [i486-linux]
[2008-03-27 11:54:55] INFO  WEBrick::HTTPServer#start: pid=6200 port=3000
```

正如我们在第 4 章《即时满足》中的演示应用程序中所做的那样，此命令在我们的本地主机端口 3000 上启动了一个 Web 服务器。⁹让我们连接到它。记住，我们提供给浏览器的 URL 包含端口号（3000）和控制器名称的小写形式（`products`）。

![](img/a160fc3a330a0b3b2a764d41d614e688_77_0.png)

这很无聊。它显示的是一个空的产品列表。让我们添加一些。点击 New product 链接，一个表单应该会出现。继续填写它：

![](img/a160fc3a330a0b3b2a764d41d614e688_77_1.png)

9. 你在尝试运行 WEBrick 时可能会收到 `Address already in use` 的错误。这只意味着你的机器上已经有一个 Rails WEBrick 服务器正在运行。如果你一直在按照书中的示例进行操作，那很可能就是第 4 章的“Hello, World!”应用程序。找到其控制台，并使用 Ctrl-C 终止服务器。

点击 Create 按钮，你应该会看到新产品已成功创建。如果现在点击 Back 链接，你应该会在列表中看到新产品：

![](img/a160fc3a330a0b3b2a764d41d614e688_78_0.png)

也许这不是最漂亮的界面，但它能工作，我们可以把它展示给客户以供批准。她可以玩玩其他链接（显示详情、编辑现有产品等等……）。我们向她解释说这只是第一步——我们知道它很粗糙，但我们希望尽早获得她的反馈。（而且三条命令在任何人的书中都算很早了。）

#### 6.3 迭代 A2：添加一个缺失的列

于是，我们向客户展示了我们生成的脚手架代码，解释说它仍然很粗糙。她很高兴能这么快看到一些可运行的东西。一旦她玩了一会儿，她注意到缺少了一些东西——我们的产品没有价格。

这意味着我们需要在数据库表中添加一列。一些开发者（和 DBA）会启动一个实用程序并发出等效于以下命令的命令：

```sql
alter table products add column price decimal(8,2);
```

但我们对迁移很熟悉。使用迁移来添加新列将为我们提供一个受版本控制的模式历史记录，以及一个简单的方法来重新创建它。

我们将首先创建迁移。之前我们使用的是在创建 product 模型时自动生成的迁移。这次，我们必须显式创建它。我们将为其取一个描述性的名称——这将在一年后我们回到应用程序时帮助我们记住每个迁移的作用。我们的约定是，在迁移创建表时使用动词 create，在向现有表添加列时使用 add。

```
depots> ruby script/generate migration add_price_to_product price:decimal
 exists   db/migrate
 create   db/migrate/20080601000002_add_price_to_product.rb
```

注意生成的文件具有基于 UTC 的时间戳前缀（在本例中为 20080601000002）。UTC 是协调世界时，前身为格林威治标准时间（GMT）。时间戳的格式为 YYYYMMDDhhmmss。Rails 使用此时间戳来跟踪哪些迁移已添加到模式中以及哪些尚未添加（并且还告诉它迁移应应用的顺序）。

打开迁移源文件，并编辑 up 方法，插入代码以在 products 表中 price 列的定义中添加 `:precision`、`:scale` 和 `:default` 参数¹⁰，如以下代码所示。down 方法使用 `remove_column` 删除该列。

```
Download depot_a/db/migrate/20080601000002_add_price_to_product.rb
class AddPriceToProduct < ActiveRecord::Migration
  def self.up
    add_column :products, :price, :decimal,
      :precision => 8, :scale => 2, :default => 0
  end

  def self.down
    remove_column :products, :price
  end
end
```

`:precision` 参数告诉数据库为 price 列存储八位有效数字，而 `:scale` 选项表示其中两位数字将在小数点后。 我们可以存储从 -999,999.99 到 +999,999.99 的价格。¹¹

此代码还展示了迁移的另一个优点——我们可以访问底层数据库的功能来执行诸如为列设置默认值等任务。不要太担心这里使用的语法；我们稍后会深入讨论。

现在我们可以再次运行迁移：

```
depots> rake db:migrate
(in /Users/rubys/work/depot)
== 20080601000002 AddPriceToProduct: migrating ====================
-- add_column(:products, :price, :decimal, {:scale=>2, :default=>0, :precision=>8})
-> 0.0061s
== 20080601000002 AddPriceToProduct: migrated (0.0062s) ===============
```

Rails 知道数据库目前处于版本 20080601000001，因此只应用我们新创建的 20080601000002 迁移。

10. 请务必记住在前一行末尾添加逗号。

11. 在撰写本文时，SQLite 3 的最新版本（即 3.5.9 版）将解析并存储此模式信息，但除此之外会忽略它，给你的是 16 位精度和可变小数位数。如果你认为这很重要，你可能需要选择不同的数据库用于部署。





##### 价格、美元和美分

当我们定义模式时，我们决定将产品价格存储在十进制列中，而不是浮点数。是有原因的。浮点数会受到舍入误差的影响：把足够多的产品放入购物车，你可能会看到总价为 234.99 而不是 235.00。十进制数在数据库和 Ruby 中都以缩放整数存储，因此它们具有精确的表示。

但我们还没有完成。 这只处理了模型。 控制流没有改变，因此控制器不需要更改。 剩下的就是视图。 虽然这意味着我们必须编辑四个文件，但更改非常直接。 请注意，show.html.erb 文件中的更改略有不同。 目前不要太担心细节；我们稍后会重新审视用户界面。

```
Download depot_a/app/views/products/index.html.erb
<h1>Listing products</h1>

<table>
  <tr>
    <th>Title</th>
    <th>Description</th>
    <th>Image url</th>
    <th>Price</th>
  </tr>

<% for product in @products %>
  <tr>
    <td><%=h product.title %></td>
    <td><%=h product.description %></td>
    <td><%=h product.image_url %></td>
    <td><%=h product.price %></td>
    <td><%= link_to 'Show', product %></td>
    <td><%= link_to 'Edit', edit_product_path(product) %></td>
    <td><%= link_to 'Destroy', product, :confirm => 'Are you sure?', :method => :delete %></td>
  </tr>
<% end %>
</table>

<br />

<%= link_to 'New product', new_product_path %>
```

```
Download depot_ca/app/views/products/new.html.erb

<h1>New product</h1>

<% form_for(@product) do |f| %>
  <%= f.error_messages %>

  <p>
    <%= f.label :title %><br />
    <%= f.text_field :title %>
  </p>
  <p>
    <%= f.label :description %><br />
    <%= f.text_area :description, :rows => 6 %>
  </p>
  <p>
    <%= f.label :image_url %><br />
    <%= f.text_field :image_url %>
  </p>
  <p>
    <%= f.label :price %><br />
    <%= f.text_field :price %>
  </p>

  <p>
    <%= f.submit "Create" %>
  </p>
<% end %>

<%= link_to 'Back', products_path %>
```

```
Download depot_ca/app/views/products/edit.html.erb

<h1>Editing product</h1>

<% form_for(@product) do |f| %>
  <%= f.error_messages %>

  <p>
    <%= f.label :title %><br />
    <%= f.text_field :title %>
  </p>
  <p>
    <%= f.label :description %><br />
    <%= f.text_area :description %>
  </p>
  <p>
    <%= f.label :image_url %><br />
    <%= f.text_field :image_url %>
  </p>
  <p>
    <%= f.label :price %><br />
    <%= f.text_field :price %>
  </p>
```

```
<p>
  <%= f.submit "Update" %>
</p>
<% end %>

<%= link_to 'Show', @product %> |
<%= link_to 'Back', products_path %>

Download depot_a/app/views/products/show.html.erb

<p>
  <b>Title:</b>
  <%=h @product.title %>
</p>

<p>
  <b>Description:</b>
  <%=h @product.description %>
</p>

<p>
  <b>Image url:</b>
  <%=h @product.image_url %>
</p>

<p>
  <b>Price:</b>
  <%=h @product.price %>
</p>

<%= link_to 'Edit', edit_product_path(@product) %> |
<%= link_to 'Back', products_path %>
```

这里是精彩的部分。 转到你的浏览器，它已经在与应用程序通信。 点击刷新，你现在应该能在这四个页面中看到价格列。

我们说过 Product 模型会去 products 表中查找它应该拥有哪些属性。 在开发模式下，Rails 每次浏览器发送请求时都会重新加载模型，因此模型始终反映当前数据库模式。 而我们已更新视图，以便它们可以使用此模型信息来更新显示的屏幕。

在技术层面上这里并没有真正的魔法，但这种能力对开发过程有很大的影响。 你多久会实现客户要求的东西，只是在你最终向他们展示工作应用程序时才被告知“哦，这不是我想要的”？ 大多数人发现，当他们可以实际操作时，更容易理解想法。 Rails 将文字快速转化为工作应用程序的速度意味着你离让客户操作结果从未如此遥远。 这些短反馈周期意味着你和客户都能更早地了解真实需求，并且你浪费在重构应用程序上的时间要少得多。

![](img/a160fc3a330a0b3b2a764d41d614e688_86_0.png)

# 图 6.2：价格验证失败。

我们将其设为受保护方法，因为它不应该在模型上下文之外调用。 当我们进一步处理产品时，请在向此模型添加方法时小心——如果你在 protected 声明之后添加它们，它们在类外部将不可见。 新操作必须放在 protected 行之前。

protected → 第 672 页

```
validate :price_must_be_at_least_a_cent

protected
def price_must_be_at_least_a_cent
  errors.add(:price, 'should be at least 0.01') if price.nil? || price < 0.01
end
```

down 方法清空表。 迁移的创建方式与其他迁移一样：

```
depot> ruby script/generate migration add_test_data
exists  db/migrate
create  db/migrate/20080601000003_add_test_data.rb
```

然后我们添加代码来填充 products 表。 这使用了 Product 模型的 create 方法。 以下是从该文件摘录的内容。 （而不是手工输入迁移，你可能想从网上提供的示例代码中复制该文件。¹⁵） 将其复制到应用程序的 db/migrate 目录中，并删除你刚刚生成的那个。 如果你下载的文件时间戳早于你已迁移的其他文件，请不要担心，因为 Rails 知道哪些迁移已完成，哪些尚未完成。

顺便说一下，复制图像¹⁶ 和文件 depot.css¹⁷ 到相应的位置（应用程序中的 public/images 和 public/stylesheets）。 警告：此迁移在加载新数据之前会从 products 表中删除现有数据。 如果你刚刚花了几个小时将自己的数据输入应用程序，你可能不想运行它！

```
Download depot_c/db/migrate/20080601000003_add_test_data.rb
class AddTestData < ActiveRecord::Migration
  def self.up
    Product.delete_all
    Product.create(:title => 'Pragmatic Version Control',
      :description =>
      %{
        <p>
          This book is a recipe-based approach to using Subversion that will
          get you up and running quickly---and correctly. All projects need
          version control: it's a foundational piece of any project's
          infrastructure. Yet half of all project teams in the U.S. don't use
          any version control at all. Many others don't use it well, and end
          up experiencing time-consuming problems.
        </p>},
      :image_url => '/images/svn.jpg',
      :price => 28.50)
    # ...
  end

  def self.down
    Product.delete_all
  end
end
```

（请注意，此代码使用 %{...}。 这是双引号字符串文字的替代语法，方便用于长字符串。 还要注意，因为

15. http://media.pragprog.com/titles/rails3/code/depot_c/db/migrate/20080601000003_add_test_data.rb
16. http://media.pragprog.com/titles/rails3/code/depot_c/public/images
17. http://media.pragprog.com/titles/rails3/code/depot_c/public/stylesheets/depot.css

它使用 Rails 的 create 方法，如果由于验证错误而无法插入记录，它将静默失败。）

运行迁移将使用测试数据填充你的 products 表：

```
depot>  rake db:migrate
```

现在让我们整理产品列表。 这里有两部分。 最终我们将编写一些使用 CSS 样式化展示的 HTML。 但为此工作，我们需要告诉浏览器获取样式表。

我们需要一个放置 CSS 样式定义的位置。 所有脚手架生成的应用程序都使用 public/stylesheets 目录中的 stylesheet scaffold.css。 而不是修改此文件，我们创建了一个新的应用程序样式表 depot.css，并将其放在同一目录中。 该样式表的完整列表从第 721 页开始。

最后，我们需要将这些样式表链接到我们的 HTML 页面。 如果你查看我们到目前为止创建的 .html.erb 文件，你不会找到任何对样式表的引用。 你甚至找不到 HTML <head> 部分，其中通常会放置此类引用。 相反，Rails 保留了一个单独的文件，用于为所有产品页面创建标准页面环境。 该文件名为 products.html.erb，是一个 Rails 布局，位于 layouts 目录中：

Download depot_b/app/views/layouts/products.html.erb

```
Line 1 <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">

<html xmlns="http://www.w3.org/1999/xhtml" xml:lang="en" lang="en">
5 <head>
  <meta http-equiv="content-type" content="text/html;charset=UTF-8" />
  <title>Products: <%= controller.action_name %></title>
  <%= stylesheet_link_tag 'scaffold' %>
</head>
10 <body>

  <p style="color: green"><%= flash[:notice] %></p>

  <%= yield %>
15
</body>
</html>
```

第八行加载样式表。 它使用 stylesheet_link_tag 创建一个 HTML <link> 标签，该标签加载标准 scaffold 样式表。 我们只需在此处添加我们的 depot.css 文件（去掉 .css 扩展名）。 不要担心文件的其余部分；我们稍后会查看。

Download depot_c/app/views/layouts/products.html.erb

```
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
```


##### `:method => :delete` 是怎么回事？

你可能已经注意到，由脚手架生成的 *destroy* 链接包含了 `:method => :delete` 参数。该参数是在 Rails 1.2 中增加的，它决定了在 ProductsController 类中调用哪个方法，同时也会影响使用的 HTTP 方法。

浏览器使用 HTTP 与服务器通信。HTTP 定义了一组浏览器可以使用的动词，并规定了每种动词的使用时机。例如，普通超链接使用 HTTP GET 请求。HTTP 定义 GET 请求用于获取数据；它不应产生任何副作用。因此，Rails 团队修改了脚手架代码生成器，强制链接发出 HTTP DELETE 请求\*。这些 DELETE 请求允许产生副作用，因此更适合用于删除资源。

\* 在某些情况下，根据浏览器是否能够发出 DELETE 方法，Rails 会用 POST 方法代替 DELETE。无论采用哪种方式，请求都不会被缓存或由网络爬虫触发。

即使这个简单的模板也使用了 Rails 的许多内置特性：

-   列表中的行具有交替的背景颜色。这是通过将每一行的 CSS 类设置为 `list-line-even` 或 `list-line-odd` 来实现的。Rails 的辅助方法 `cycle` 自动在连续的行之间切换这两种样式名称。
-   使用 `truncate` 辅助方法仅显示描述的前八十个字符。但在调用 `truncate` 之前，我们调用了 `gsub` 来移除描述中的 HTML 标签。¹⁸
-   我们还使用了 `h` 方法来确保产品标题和描述中任何剩余的 HTML 都被转义。
-   看一下 `link_to 'Destroy'` 这一行。请注意它带有参数 `:confirm => "Are you sure?"` 。如果单击此链接，Rails 会安排浏览器弹出对话框，在链接跳转并删除产品之前请求确认。（另外，请参阅本页侧边栏，了解该操作的更多信息。）

我们向数据库加载了一些测试数据，重写了显示产品列表的 `index.html.erb` 文件，添加了 `depot.css` 样式表，并通过编辑布局文件 `products.html.erb` 将该样式表链接到页面中。

18. 如果你看到类似 `undefined method 'for' for {length=>80}.Hash` 的消息，那么你可能没有运行 Rails 2.2.2 或更高版本。参见第 3 章“安装 Rails”（第 31 页）了解升级信息，或者简单地从该调用中删除 `length =>`（保留 80）。

在本章中，我们将看到

-   编写我们自己的视图，
-   使用布局装饰页面，
-   集成 CSS，
-   使用辅助方法，以及
-   将页面链接到操作。

### 第 7 章

### 任务 B：目录显示

总而言之，到目前为止这一天过得很顺利。我们从客户那里收集了初始需求，记录了基本流程，初步确定了所需的数据，并为 Depot 应用程序的产品组装了维护页面。我们甚至设法在上午结束时享用了一顿不错的午餐。

精神饱满之后，我们继续第二个任务。我们与客户讨论了优先级，她说她希望开始从买家的角度看看应用程序的外观。我们的下一个任务是创建一个简单的目录显示。

从我们的角度来看，这也非常合理。一旦我们将产品安全地存入数据库，显示它们应该相当简单。这也为我们后续开发购物车部分代码提供了基础。

我们还应该能够借鉴刚才在产品维护任务中所做的工作——目录显示实际上只是一个美化过的产品列表。那么，让我们开始吧。

#### 7.1 迭代 B1：创建目录列表

我们已经创建了 products 控制器，供卖家管理 Depot 应用程序。现在，是时候创建第二个控制器，用于与付费客户交互了。我们叫它 Store。

```
depot> ruby script/generate controller store index
exists   app/controllers/
exists   app/helpers/
create   app/views/store
exists   test/functional/
create   app/controllers/store_controller.rb
create   test/functional/store_controller_test.rb
create   app/helpers/store_helper.rb
create   app/views/store/index.html.erb
```

![](img/a160fc3a330a0b3b2a764d41d614e688_97_0.png)

图 7.1：我们的第一个（丑陋的）目录页面

一般来说，尽量养成在模板中输入 `<%=h ... %>` 的习惯，只有当你确信可以安全地移除 `h` 时才将其移除。

我们还使用了 `image_tag` 辅助方法。这个方法会生成一个 HTML `<img>` 标签，并将其参数作为图像源。

点击刷新后，显示画面如图 7.1 所示。页面相当丑陋，因为我们还没有包含 CSS 样式表。正当我们思考这个问题时，客户恰好路过，她指出她也希望面向公众的页面看起来有像样的标题和侧边栏。

在现实世界中，此时我们可能会想请设计人员来——我们已经见过太多程序员设计的网站，不忍心再给世界添一个。但 Pragmatic Web Designer 正在某个海滩寻找灵感，要到今年晚些时候才能回来，所以让我们暂时先放一个占位符。是时候进行一次迭代了。

#### 7.2 迭代 B2：添加页面布局

典型网站中的页面往往共享相似的布局——设计人员会创建一个标准模板，用于放置内容。我们的任务是将这种页面装饰添加到每个商店页面中。

幸运的是，在 Rails 中我们可以定义布局。布局是一个模板，我们可以将额外内容流入其中。在我们的案例中，我们可以为所有商店页面定义一个单独的布局，并将目录页面插入该布局中。稍后我们可以对购物车和结账页面做同样的事情。因为只有一个布局，我们可以通过编辑一个文件来改变网站这部分区域的整体外观和感觉。这让我们对暂时放置占位符感到安心；当设计师最终从岛上回来后，我们可以进行更新。

在 Rails 中，有多种指定和使用布局的方法。现在我们将选择最简单的。如果我们在 `app/views/layouts` 目录中创建一个与控制器同名模板文件，那么该控制器渲染的所有视图将默认使用该布局。所以，现在让我们创建一个。我们的控制器叫 store，因此我们将布局命名为 `store.html.erb`：

下载 depot_e/app/views/layouts/store.html.erb

```
Line 1 <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html>
<head>
<title>Pragprog Books Online Store</title>
<%= stylesheet_link_tag "depot", :media => "all" %>
</head>
<body id="store">
<div id="banner">
<%= image_tag("logo.png") %>
<%= @page_title || "Pragmatic Bookshelf" %>
</div>
<div id="columns">
<div id="side">
<a href="http://www....">Home</a><br />
<a href="http://www..../faq">Questions</a><br />
<a href="http://www..../news">News</a><br />
<a href="http://www..../contact">Contact</a><br />
</div>
<div id="main">
<%= yield :layout %>
</div>
</div>
</body>
</html>
```

除了常见的 HTML 元素之外，这个布局还有三个 Rails 特定的项目。第 6 行使用 Rails 辅助方法生成一个指向我们 `depot.css` 样式表的 `<link>` 标签。在第 11 行，我们将页面标题设置为实例变量 `@page_title` 的值。然而，真正的魔法发生第 21 行。当我们调用 `yield` 并传递名称 `:layout` 时，Rails 会自动替换页面特定的内容——即由该请求调用的视图生成的内容。在我们的案例中，这将是由 `index.html.erb` 生成的目录页面。³

为了使其正常工作，我们需要在 `depot.css` 样式表中添加以下内容：

```
Download depot_e/public/stylesheets/depot.css

/* Styles for main page */

#banner {
  background: #9c9;
  padding-top: 10px;
  padding-bottom: 10px;
  border-bottom: 2px solid;
  font: small-caps 40px/40px "Times New Roman", serif;
  color: #282;
  text-align: center;
}

#banner img {
  float: left;
}

#columns {
  background: #141;
}

#main {
  margin-left: 13em;
  padding-top: 4ex;
  padding-left: 2em;
  background: white;
}

#side {
  float: left;
  padding-top: 1em;
  padding-left: 1em;
  padding-bottom: 1em;
  width: 12em;
  background: #141;
}

#side a {
  color: #bfb;
  font-size: small;
}
```

3. Rails 还会将变量 `@content_for_layout` 设置为渲染操作的结果，因此你也可以将此值替换到布局中以代替 `yield`。这是原来的做法（而且我们个人认为它更可读）。使用 `yield` 被认为更酷。





![](img/a160fc3a330a0b3b2a764d41d614e688_103_0.png)

## Figure 7.3: 现在有一个加入购物车按钮。

- 修改应用程序，使点击图书的图像也会调用尚未编写的 add_to_cart 动作。提示：link_to 的第一个参数会放在生成的 <a> 标签中，而 Rails 辅助方法 image_tag 会构造一个 HTML <img> 标签。将对其的调用作为 link_to 调用的第一个参数包含在内。确保在对 link_to 的调用中，在你的 html_options 中包含 :method => :post。
- number_to_currency 辅助方法的完整描述如下：

```
number_to_currency(number, options = {})
```

将数字格式化为货币字符串。options 哈希可用于自定义输出格式。数字可以使用 :precision 键包含精度级别；默认值为 2。货币类型可以使用 :unit 键设置（默认 "$"）。单位分隔符可以使用 :separator 键设置（默认 "."）。分隔符可以使用 :delimiter 键设置（默认 ","）。

```
number_to_currency(1234567890.50)          -> $1,234,567,890.50
number_to_currency(1234567890.506)         -> $1,234,567,890.51
number_to_currency(1234567890.50, :unit => "&pound;",
                    :separator => ",", :delimiter => "")
                    -> &pound;1234567890,50
```

尝试设置各种选项，并观察对你的目录列表的影响。

（你会在 http://pragprog.wikidot.com/rails-play-time. 上找到提示。）

实现此会话跟踪的底层机制各不相同。有时应用程序会在每个页面的表单数据中编码会话信息。有时编码后的会话标识符会添加到每个 URL 的末尾（所谓的 URL 重写选项）。有时应用程序使用 cookie。Rails 使用基于 cookie 的方法。

cookie 只是一块由 Web 应用程序传递给 Web 浏览器的命名数据。浏览器会记住它。此后，当浏览器向应用程序发送请求时，cookie 数据会随之发送。应用程序使用 cookie 中的信息将请求与服务器上存储的会话信息匹配起来。这是对一个混乱问题的丑陋解决方案。幸运的是，作为 Rails 程序员，你不必担心所有这些低级细节。事实上，唯一需要深入了解这些细节的原因是为了解释为什么 Rails 应用程序的用户必须在浏览器中启用 cookie。

与其让开发人员担心协议和 cookie，Rails 提供了一个简单的抽象。在控制器内部，Rails 维护一个特殊的类似哈希的集合，称为 session。你在处理请求期间存储在此哈希中的任何键/值对，都将在同一浏览器的后续请求中可用。

在 Depot 应用程序中，我们希望使用会话功能来存储每个买家购物车中的信息。但我们在这里必须稍微小心一点——这个问题比看起来要深。存在弹性和可扩展性的问题。

一种选择是将会话信息存储在服务器上的文件中。如果你运行单个 Rails 服务器，这没有问题。但想象一下，你的商店应用程序变得如此流行，以至于单台服务器机器的容量用尽，你需要运行多台机器。来自特定用户的第一个请求可能被路由到一台后端机器，但第二个请求可能转到另一台。存储在第一台服务器上的会话数据在第二台服务器上不可用；用户会在请求之间看到购物车中的商品出现和消失，从而感到非常困惑。

因此，最好确保会话信息存储在应用程序外部的某个地方，以便在需要时可以在多个应用程序进程之间共享。而且如果此外部存储是持久的，我们甚至可以重启服务器而不会丢失任何会话信息。我们在第 22.2 节 Rails Sessions，第 477 页中讨论了设置会话信息的所有内容，我们会看到有许多不同的会话存储选项。现在，让我们安排我们的应用程序将会话数据存储在数据库中的一张表中。

#### 将会话放入数据库

Rails 使将会话数据存储在数据库中变得很容易。我们需要运行几个 Rake 任务来创建具有正确布局的数据库表。

首先，我们将创建一个包含会话表定义的迁移。有预定义的 Rake 任务可以创建我们需要的迁移：

```
depot> rake db:sessions:create
exists  db/migrate
create  db/migrate/20080601000004_create_sessions.rb
```

然后，我们将应用迁移以将表添加到我们的模式中：

```
depot> rake db:migrate
```

如果现在查看你的数据库，你会发现一个名为 sessions 的新表。

接下来，我们必须告诉 Rails 对我们的应用程序会话使用数据库存储（默认是存储在 cookie 中）。这是一个配置选项，因此不出所料，你会在 config 目录中的一个文件中找到它的指定。打开文件 environment.rb，你会看到一堆配置选项，都被注释掉了。向下扫描，找到看起来像这样的选项：¹

```
# Use the database for sessions instead of the cookie-based default,
# which shouldn't be used to store highly confidential information
# (create the session table with 'rake db:sessions:create')
# config.action_controller.session_store = :active_record_store
```

请注意，最后一条语句被注释掉了。删除该行开头的 # 字符以激活数据库会话存储：

```
# Use the database for sessions instead of the cookie-based default,
# which shouldn't be used to store highly confidential information
# (create the session table with 'rake db:sessions:create')
config.action_controller.session_store = :active_record_store
```

#### 会话与浏览器

正如我们所讨论的，Rails 会话的默认实现是使用 cookie 在用户浏览器上存储会话 id。当来自该浏览器的请求进来时，Rails 提取会话 id 并使用它从（在我们的例子中）数据库中检索会话数据。但这里有一个重要的细微差别：cookie 是由服务器主机名和 cookie 名称共同存储在浏览器上的。如果你在一台服务器上运行两个不同的应用程序，你可能希望它们使用不同的 cookie 名称来存储其会话键。如果不这样做，它们会相互干扰。

幸运的是，Rails 处理了这个问题。当你使用 rails 命令创建一个新应用程序时，它会为存储会话 id 的 cookie 建立一个名称。此名称包含你的应用程序的名称。

1. 在 Rails 2.3 中，你需要在 config/initializers/session_store.rb 中查找 ActionController::Base.session_store 的设置。

事实证明，在 Ruby 中有一种更地道的方式来做同样的事情：

```
private

  def find_cart
    session[:cart] ||= Cart.new
  end
```

此方法相当棘手。它使用 Ruby 的条件赋值运算符，||= 。如果 session 哈希具有对应于键 :cart 的值，则立即返回该值。否则，将创建一个新的 Cart 对象并分配给 session。此新 Cart 然后被返回。

请注意，我们将 find_cart 方法设为 private。这可以防止 Rails 将其作为控制器上的操作公开。当我们进一步处理购物车时，请小心向此控制器添加方法——如果你在 private 声明之后添加它们，它们在类外部将不可见。新的操作必须放在 private 行之前。

#### 8.2 迭代 C1：创建购物车

我们查看会话是因为我们需要一个地方来保存我们的购物车。我们已经解决了会话问题，所以让我们继续实现购物车。现在，让我们保持简单。它保存数据并包含一些业务逻辑，因此我们知道它在逻辑上是一个模型。但是，我们需要购物车数据库表吗？不一定。购物车与买家的会话绑定，只要该会话数据在所有服务器上可用（当我们最终在多服务器环境中部署时），这可能就足够了。所以现在，我们假设购物车是一个常规类，看看会发生什么。我们将使用编辑器在 app/models 目录中创建文件 cart.rb。³ 实现很简单。购物车基本上是项目数组的包装器。当添加产品（使用 add_product 方法）时，它会被附加到项目列表中：

```
class Cart
  attr_reader :items

  def initialize
    @items = []
  end

  def add_product(product)
    @items << product
  end
end
```

3. 请注意，我们不使用 Rails 模型生成器来创建此文件。生成器仅用于创建基于数据库的模型。





回到 http://localhost:3000/store 主目录页面，将另一种商品添加到购物车。你会看到购物车中原来有两个条目，再加上这个新商品。看来我们的会话机制已经生效了。该让我们的客户看看了，于是我们把她叫过来，自豪地展示我们漂亮的新购物车。令我们有些沮丧的是，她发出了那种“啧啧”的声音——顾客在准备告诉你“你显然没搞明白”之前通常会这样。

她解释说，真正的购物车不会为同一商品显示两行。相反，它们只显示该商品一行，并带有一个数量 2。看来我们又要进行下一轮迭代了。

#### 8.3 迭代 C2：打造更聪明的购物车

看来我们得想办法把数量与购物车中的每个商品关联起来。让我们创建一个新的模型类 `CartItem`，其中包含对商品和数量的引用：

```
Download depot_g/app/models/cart_item.rb
class CartItem
  attr_reader :product, :quantity

  def initialize(product)
    @product = product
    @quantity = 1
  end

  def increment_quantity
    @quantity += 1
  end

  def title
    @product.title
  end

  def price
    @product.price * @quantity
  end
end
```

现在，我们将在 Cart 的 `add_product` 方法中使用这个类。这段代码会检查我们的商品列表中是否已经包含要添加的商品；如果包含，就增加数量；如果不包含，就添加一个新的 `CartItem`：

```
Download depot_g/app/models/cart.rb
def add_product(product)
  current_item = @items.find {|item| item.product == product}
  if current_item
    current_item.increment_quantity
  else
```

当 Rails 从会话中取出购物车时，它得到的是一个装满商品对象的购物车，而不是购物车条目。这就是我们的问题所在。

确认这个问题最简单的方法是删除旧的会话，清除原始购物车实现的所有痕迹。因为我们使用基于数据库的会话，所以可以用一个方便的 Rake 任务来清空会话表：

```
depot> rake db:sessions:clear
```

现在如果你点击“刷新”，你会看到一个不同的错误：`ActionController::InvalidAuthenticityToken`。考虑到你刚刚清除了所有会话，这并不太令人惊讶。要彻底解决这个问题，你需要点击“后退”按钮，直到看到目录页，然后在该页面上点击“刷新”（以便开始一个新的会话），只有这样才能验证应用程序运行的是新的购物车和新的 `add_to_cart` 视图。

##### 故事的教训

我们的问题是由会话存储了旧版本的购物车对象引起的，它与我们新的源文件不兼容。我们通过清除旧会话数据来解决这个问题。因为我们在会话数据中存储了完整的对象，所以每当我们更改应用程序的源代码时，都可能与这些数据不兼容，从而导致运行时错误。这不仅仅是开发阶段的问题。

假设我们使用旧版本的购物车发布了 Depot 应用程序的第一版，有成千上万的客户在忙着购物。然后我们决定发布新的、改进后的购物车模型。代码进入生产环境后，突然所有正在疯狂购物的客户发现，他们在向购物车添加商品时遇到了错误。我们唯一的解决办法是删除会话数据，而这会让客户的购物车丢失。

这告诉我们，将会话数据中的应用程序级对象存储起来，通常是一个非常糟糕的主意。对应用程序的任何更改都可能要求我们在下次更新生产环境时丢失现有会话。

相反，推荐的做法是只在会话中存储简单数据：字符串、数字等。将应用程序对象保存在数据库中，然后通过主键从会话数据中引用它们。如果我们要将 Depot 应用程序部署到生产环境，明智的做法是让 `Cart` 类成为一个 Active Record 对象，并将购物车数据存储在数据库中。5 然后会话将存储购物车对象的 id。当请求到来时，我们从会话中提取这个 id，然后从数据库加载购物车。6 虽然这不会自动解决更新应用程序时的所有问题，但它给了你一个处理迁移问题的机会。

5. 但我们不会在这个演示应用中这样做，因为我们想说明这些问题。
6. 事实上，我们可以将这种功能抽象成一个叫做过滤器的东西，并让它自动发生。我们将在第 488 页开始介绍过滤器。

![](img/a160fc3a330a0b3b2a764d41d614e688_114_0.png)

总之，我们现在有了一个购物车，它为其中包含的每个商品都维护一个数量，并且我们有一个显示该数量的视图。我们可以在图 8.1 中看到它的样子。

我们很高兴有了一个像样的成果，于是把客户叫过来，向她展示我们一上午的工作成果。她很满意——她看到这个网站开始有了雏形。然而，她也很不安，因为她刚刚在行业媒体上读到一篇文章，说电子商务网站每天都在遭受攻击和破坏。她读到其中一种攻击方式是向 Web 应用程序发送带有恶意参数的请求，希望发现 bug 和安全漏洞。她注意到，将商品添加到购物车的链接看起来像 `store/add_to_cart/1`，其中 1 是我们的内部商品 id。她心存恶意，手动在浏览器中输入这个请求，给了一个 `wibble` 的商品 id。当我们的应用程序显示下一页的图 8.2 中的页面时，她并不满意。这暴露了太多关于我们应用程序的信息。而且看起来也相当不专业。因此，看来我们的下一轮迭代将致力于让应用程序更具韧性。

#### 8.4 迭代 C3：处理错误

看一下图 8.2 中显示的页面，很明显，我们的应用程序在 store 控制器的第 16 行抛出了一个异常。⁷ 也就是这一行：

```
product = Product.find(params[:id])
```

7. 你的行号可能不同。

消息。例如，当我们的 `add_to_cart` 操作检测到传入无效的商品 id 时，它可以将该错误消息存储在 flash 区域中，并重定向到 `index` 操作以重新显示目录。`index` 操作的视图可以提取错误并将其显示在目录页面的顶部。flash 信息可以通过 `flash` 访问器方法在视图中访问。

为什么我们不能直接把错误存储在任何普通的实例变量中？请记住，在应用程序向浏览器发送重定向之后，浏览器会向我们的应用程序发送一个新的请求。当我们收到该请求时，应用程序已经继续运行了——之前请求中的所有实例变量早已消失。flash 数据存储在会话中，以便在请求之间可用。

掌握了这些关于 flash 数据的背景知识后，我们现在可以修改 `add_to_cart` 方法，让它拦截无效的商品 id 并报告问题：

```
Download depot_h/app/controllers/store_controller.rb

def add_to_cart
  product = Product.find(params[:id])
  @cart = find_cart
  @cart.add_product(product)
rescue ActiveRecord::RecordNotFound
  logger.error("Attempt to access invalid product #{params[:id]}")
  flash[:notice] = "Invalid product"
  redirect_to :action => 'index'
end
```

`rescue` 子句拦截了由 `Product.find` 抛出的异常。在处理器中，我们做了以下事情：

- 使用 Rails 日志记录器来记录错误。每个控制器都有一个 `logger` 属性。这里我们用它来在错误日志级别记录一条消息。

- 创建一个带有解释的 flash 通知。与会话一样，你可以像访问哈希一样访问 flash。这里我们使用键 `:notice` 来存储消息。

- 使用 `redirect_to` 方法重定向到目录显示。该方法接受广泛的参数（类似于我们在模板中遇到的 `link_to` 方法）。在这种情况下，它指示浏览器立即请求将调用当前控制器 `index` 操作的 URL。为什么要重定向，而不是直接在这里显示目录？如果我们重定向，用户的浏览器最终会显示一个类似 `http://.../store/index` 的 URL，而不是 `http://.../store/add_to_cart/wibble`。这样我们就更少暴露应用程序的内部结构。同时，我们也避免用户通过点击“重新加载”按钮再次触发错误。





有了这些代码，我们可以重新运行客户那个有问题的查询。这一次，当我们输入以下 URL 时：

```
http://localhost:3000/store/add_to_cart/wibble
```

我们不会在浏览器中看到一堆错误。相反，目录页面会正常显示。如果我们查看日志文件（日志目录中的 development.log）的末尾，就会看到我们的消息。⁹

```
Parameters: {"action"=>"add_to_cart", "id"=>"wibble", "controller"=>"store"}
Product Load (0.000246) SELECT * FROM "products" WHERE ("products"."id" = 0)
Attempt to access invalid product wibble
Redirected to http://localhost:3000/store/index
Completed in 0.00522 (191 reqs/sec) . . .

Processing StoreController#index ...
. . .
Rendering within layouts/store
Rendering store/index
```

所以，日志记录生效了。但 flash 消息并没有出现在用户的浏览器中。那是因为我们没有显示它。我们需要在布局中添加一些代码，让它显示存在的 flash 消息。下面的 html.erb 代码检查 notice 级别的 flash 消息，并在必要时创建一个包含该消息的新 `<div>`：

```
<% if flash[:notice] %>
  <div id="notice"><%= flash[:notice] %></div>
<% end -%>
```

那么，我们该把这段代码放在哪里呢？我们可以把它放在目录显示模板（即 index.html.erb 中的代码）的顶部。毕竟，我们现在正希望它出现在那里。但更理想的是，所有页面都有一种标准化的错误显示方式。

9. 在 Unix 机器上，我们可能会使用 tail 或 less 等命令来查看这个文件。在 Windows 上，你可以使用自己最喜欢的编辑器。通常，最好保持一个窗口打开，以便查看追加到该文件的新行。在 Unix 中，你可以使用 `tail -f`。你可以从 http://gnuwin32.sourceforge.net/packages/coreutils.htm 下载 Windows 版的 tail 命令，或者从 http://tailforwin32.sourceforge.net/ 获取基于 GUI 的工具。最后，有些 OS X 用户使用 Console.app 来跟踪日志文件。只需在命令行中输入 `open name.log` 即可。

我们已经在使用 Rails 布局来让所有商店页面保持统一的外观，所以让我们把处理 flash 的代码添加到该布局中。这样，如果我们的客户突然觉得错误信息放在侧边栏更好，我们只需修改一处，所有商店页面都会同步更新。

因此，我们新的商店布局代码现在如下所示：

```
Download depot_h/app/views/layouts/store.html.erb
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html>
<head>
  <title>Pragprog Books Online Store</title>
  <%= stylesheet_link_tag "depot", :media => "all" %>
</head>
<body id="store">
  <div id="banner">
    <%= image_tag("logo.png") %>
    <%= @page_title || "Pragmatic Bookshelf" %>
  </div>
  <div id="columns">
    <div id="side">
      <a href="http://www....">Home</a><br />
      <a href="http://www..../faq">Questions</a><br />
      <a href="http://www..../news">News</a><br />
      <a href="http://www..../contact">Contact</a><br />
    </div>
    <div id="main">
      <% if flash[:notice] -%>
        <div id="notice"><%= flash[:notice] %></div>
      <% end -%>
      <%= yield :layout %>
    </div>
  </div>
</body>
</html>
```

我们还需要为 notice 框添加一条新的 CSS 样式规则：

```
Download depot_h/public/stylesheets/depot.css
#notice {
  border: 2px solid red;
  padding: 1em;
  margin-bottom: 2em;
  background-color: #f0f0f0;
  font: bold smaller sans-serif;
}
```

这一次，当我们手动输入无效的产品代码时，会在目录页面顶部看到错误报告。

![](img/a160fc3a330a0b3b2a764d41d614e688_119_0.png)

感觉一个迭代即将结束，我们把客户叫过来，向她展示错误现在已得到妥善处理。她很高兴，继续试用这个应用。她注意到新购物车显示有一个小问题——没有清空购物车中商品的办法。这个小改动将成为我们的下一个迭代。我们应该在回家之前完成它。

#### 8.5 迭代 C4：完成购物车

到目前为止，我们已经知道，要实现“清空购物车”功能，必须在购物车中添加一个链接，并在商店控制器中实现 empty_cart 方法。我们先从模板开始。我们不用超链接，而是用 button_to 方法在页面上放一个按钮：

```
Download depot_h/app/views/store/add_to_cart.html.erb
<h2>Your Pragmatic Cart</h2>
<ul>
  <% for item in @cart.items %>
    <li><%= item.quantity %> &times; <%=h item.title %></li>
  <% end %>
</ul>

<%= button_to 'Empty cart', :action => 'empty_cart' %>
```

在控制器中，我们将实现 empty_cart 方法。它会从会话中移除购物车，并在重定向到 index 页面之前，将一条消息写入 flash：

```
Download depot_h/app/controllers/store_controller.rb
def empty_cart
  session[:cart] = nil
  flash[:notice] = "Your cart is currently empty"
  redirect_to :action => 'index'
end
```

现在，当我们查看购物车并点击 Empty Cart 按钮时，会被带回目录页面，并看到一条友好的小消息：

![](img/a160fc3a330a0b3b2a764d41d614e688_119_1.png)

不过，在我们急着自我表扬之前，先回头看看我们的代码。我们刚刚引入了一些重复。

在商店控制器中，我们现在有两处代码都在向 flash 写入消息并重定向到 index 页面。听起来我们应该把这些公共代码提取到一个方法中，所以让我们实现 redirect_to_index，并修改 add_to_cart 和 empty_cart 方法来使用它：

```
Download depot_i/app/controllers/store_controller.rb

def add_to_cart
  product = Product.find(params[:id])
  @cart = find_cart
  @cart.add_product(product)
rescue ActiveRecord::RecordNotFound
  logger.error("Attempt to access invalid product #{params[:id]}")
  redirect_to_index("Invalid product")
end

def empty_cart
  session[:cart] = nil
  redirect_to_index("Your cart is currently empty")
end

private

def redirect_to_index(msg)
  flash[:notice] = msg
  redirect_to :action => 'index'
end
```

最后，我们终于可以来整理购物车显示了。与其为每个商品使用 `<li>` 元素，不如用表格。同样，我们将依靠 CSS 来完成样式设计：

```
Download depot_i/app/views/store/add_to_cart.html.erb

<div class="cart-title">Your Cart</div>
<table>
  <% for item in @cart.items %>
    <tr>
      <td><%= item.quantity %>&times;</td>
      <td><%=h item.title %></td>
      <td class="item-price"><%= number_to_currency(item.price) %></td>
    </tr>
  <% end %>

  <tr class="total-line">
    <td colspan="2">Total</td>
    <td class="total-cell"><%= number_to_currency(@cart.total_price) %></td>
  </tr>
</table>

<%= button_to "Empty cart", :action => :empty_cart %>
```

为了让这能正常工作，我们需要在 Cart 模型中添加一个方法，返回所有商品的总价。我们可以使用 Rails 简洁的 sum 方法来实现，对集合中每个商品的价格求和：

```
def total_price
  @items.sum { |item| item.price }
end
```

然后，我们需要在 depot.css 样式表中添加一小段样式：

```
/* Styles for the cart in the main page */

.cart-title {
  font: 120% bold;
}

.item-price, .total-line {
  text-align: right;
}

.total-line .total-cell {
  font-weight: bold;
  border-top: 1px solid #595;
}
```

最终效果是一个更好看的购物车：

![](img/a160fc3a330a0b3b2a764d41d614e688_121_0.png)

#### 我们刚才做了什么

这是忙碌而充实的一天。我们为商店添加了购物车，并且在这个过程中初步接触了一些很棒的 Rails 特性：

- 使用会话（session）来存储状态
- 创建并集成非数据库模型
- 使用 flash 在动作之间传递错误和响应
- 使用 logger 记录事件
- 从控制器中消除重复

我们也制造了不少错误，也知道了如何解决它们。

但是，就在我们认为这个功能已经完成的时候，客户踱步过来，手里拿着一本 *《信息技术与高尔夫周刊》*。显然，里面有一篇关于新型浏览器界面的文章，这种界面的内容可以实时更新。“Ajax。”她自豪地说。嗯……我们明天再看看这个吧。

#### 动手练习

这里有一些你可以自己尝试的内容：

- 在会话中添加一个新变量，记录用户访问商店控制器 index 动作的次数。第一次访问时，计数不会在会话中。你可以用这样的代码来测试：

  ```
  if session[:counter].nil?
  ...
  ```

  如果会话变量不存在，你需要初始化它，然后才能递增它。

- 将这个计数传给模板，并显示在目录页面顶部。提示：pluralize 辅助方法（见第 517 页）在构造显示消息时可能很有用。

- 每当用户向购物车添加商品时，将计数器重置为零。

- 修改模板，仅当计数器大于 5 时才显示它。

（你可以在 http://pragprog.wikidot.com/rails-play-time 找到提示。）





partial once for each item in the collection. Let’s rewrite our cart view to use this feature:

```
```erb
<div class="cart-title">Your Cart</div>
<table>
  <%= render(:partial => "cart_item", :collection => @cart.items) %>

  <tr class="total-line">
    <td colspan="2">Total</td>
    <td class="total-cell"><%= number_to_currency(@cart.total_price) %></td>
  </tr>

</table>

<%= button_to "Empty cart", :action => :empty_cart %>
```
```

That’s a lot simpler. The render method takes the name of the partial and the collection object as parameters. The partial template itself is simply another template file (by default in the same directory as the template that invokes it). However, to keep the names of partials distinct from regular templates, Rails automatically prepends an underscore to the partial name when looking for the file. That means our partial will be stored in the file _cart_item.html.erb in the app/views/store directory.

```
```erb
<tr>
  <td><%= cart_item.quantity %>&times;</td>
  <td><%=h cart_item.title %></td>
  <td class="item-price"><%= number_to_currency(cart_item.price) %></td>
</tr>
```
```

There’s something subtle going on here. Inside the partial template, we refer to the current cart item using the variable cart_item. That’s because the render method in the main template arranges to set a variable with the same name as the partial template to the current item each time around the loop. The partial is called cart_item, so inside the partial we expect to have a variable called cart_item.

So, now we’ve tidied up the cart display, but that hasn’t moved it into the sidebar. To do that, let’s revisit our layout. If we had a partial template that could display the cart, we could simply embed a call like this within the sidebar:

```
```ruby
render(:partial => "cart")
```
```

But how would the partial know where to find the cart object? One way would be for it to make an assumption. In the layout, we have access to the @cart instance variable that was set by the controller. It turns out that this is also available inside partials called from the layout. However, this is a bit like calling a method and passing it some value in a global variable. It works, but it’s

ugly coding, and it increases coupling (which in turn makes your programs brittle and hard to maintain).

Remember using render with the collection option inside the add_to_cart template? It set the variable cart_item inside the partial. It turns out we can do the same when we invoke a partial directly. The :object parameter to render takes an object that is assigned to a local variable with the same name as the partial. So, in the layout we could call this:

```
<%= render(:partial => "cart", :object => @cart) %>
```

and in the _cart.html.erb template, we can refer to the cart via the variable cart.

Let’s do that wiring now. First, we’ll create the _cart.html.erb template. This is basically our add_to_cart template but using cart instead of @cart. (Note that it’s OK for a partial to invoke other partials.)

```
Download depot_j/app/views/store/_cart.html.erb
<div class="cart-title">Your Cart</div>
<table>
  <%= render(:partial => "cart_item", :collection => cart.items) %>
  <tr class="total-line">
    <td colspan="2">Total</td>
    <td class="total-cell"><%= number_to_currency(cart.total_price) %></td>
  </tr>
</table>

<%= button_to "Empty cart", :action => :empty_cart %>
```

Now we’ll change the store layout to include this new partial in the sidebar:

```
Download depot_j/app/views/layouts/store.html.erb
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html>
<head>
  <title>Pragprog Books Online Store</title>
  <%= stylesheet_link_tag "depot", :media => "all" %>
</head>
<body id="store">
  <div id="banner">
    <%= image_tag("logo.png") %>
    <%= @page_title || "Pragmatic Bookshelf" %>
  </div>
  <div id="columns">
    <div id="side">
      <div id="cart">
        <%= render(:partial => "cart", :object => @cart) %>
      </div>
```

You tell form_remote_tag how to invoke your server application using the :url parameter. This takes a hash of values that are the same as the trailing parameters we passed to button_to. The code inside the Ruby block (between the do and end keywords) is the body of the form. In this case, we have a simple submit button. From the user's perspective, this page looks identical to the previous one.

While we're dealing with the views, we also need to arrange for our application to send the JavaScript libraries used by Rails to the user's browser. We'll talk more about this in Chapter 24, The Web, v2.0, on page 563, but for now let's just add a call to javascript_include_tag to the <head> section of the store layout:

```
Download depot_l/app/views/layouts/store.html.erb
<html>
<head>
<title>Pragprog Books Online Store</title>
<%= stylesheet_link_tag "depot", :media => "all" %>
<%= javascript_include_tag :defaults %>
</head>
```

So far, we've arranged for the browser to send an Ajax request to our application. The next step is to have the application return a response. The plan is to create the updated HTML fragment that represents the cart and to have the browser stick that HTML into the DOM¹ as a replacement for the cart that's already there. The first change is to stop the add_to_cart action redirecting to the index display. (We know, we just added that only a few pages back. Now we're taking it out again. We're agile, right?) What we are going to replace it with is a call to respond_to telling it that we want to respond with a format of .js.²

```
Download depot_l/app/controllers/store_controller.rb
def add_to_cart
  product = Product.find(params[:id])
  @cart = find_cart
  @cart.add_product(product)
  respond_to do |format|
    format.js
  end
rescue ActiveRecord::RecordNotFound
  logger.error("Attempt to access invalid product #{params[:id]}")
  redirect_to_index("Invalid product")
end
```

1. The Document Object Model. This is the browser's internal representation of the structure and content of the document being displayed. By manipulating the DOM, we cause the display to change in front of the user's eyes.

2. This syntax may seem surprising at first, but it is simply a method call that is passing a block as an argument. Blocks are described in Section A.9, Blocks and Iterators, on page 675. We will cover the respond_to method in greater detail in Section 12.1, Responding Appropriately, on page 185.

Because of this change, when add_to_cart finishes handling the Ajax request, Rails will look for an add_to_cart template to render. We deleted the old .html.erb template back on page 129, so it looks like we’ll need to add something back in. Let’s do something a little bit different.

Rails supports RJS templates—the JS stands for JavaScript. A .js.rjs template is a way of getting JavaScript on the browser to do what you want, all by writing server-side Ruby code. Let’s write our first: add_to_cart.js.rjs. It goes in the app/views/store directory, just like any other template:

```
depot1/app/views/store/add_to_cart.js.rjs
page.replace_html("cart", :partial => "cart", :object => @cart)
```

Let’s analyze that template. The page variable is an instance of something called a JavaScript generator—a Rails class that knows how to create JavaScript on the server and have it executed by the browser. Here, we tell it to replace the content of the element on the current page with the id cart with…something. The remaining parameters to replace_html look familiar. They should—they’re the same ones we used to render the partial in the store layout. This simple RJS template renders the HTML that represents the cart. It then tells the browser to replace the content of the <div> whose id="cart" with that HTML.

Does it work? It’s hard to show in a book, but it sure does. Make sure you reload the index page in order to get the form_remote_tag and the JavaScript libraries loaded into your browser. Then, click one of the Add to Cart buttons. You should see the cart in the sidebar update. And you shouldn’t see your browser show any indication of reloading the page. You’ve just created an Ajax application.

#### Troubleshooting

Although Rails makes Ajax incredibly simple, it can’t make it foolproof. And, because you’re dealing with the loose integration of a number of technologies, it can be hard to work out why your Ajax doesn’t work. That’s one of the reasons you should always add Ajax functionality one step at a time.

Here are a few hints if your Depot application didn’t show any Ajax magic:

- Did you delete the old add_to_cart.html.erb file?
- Did you remember to include the JavaScript libraries in the store layout (using javascript_include_tag)?
- Does your browser have any special incantation to force it to reload everything on a page? Sometimes browsers hold local cached versions of page assets, and this can mess up testing. Now would be a good time to do a full reload.





![](img/a160fc3a330a0b3b2a764d41d614e688_133_0.png)

**图 9.2：应用“黄色淡出技术”的购物车**展示了原始购物车。用户点击“Add to Cart”按钮后，计数更新为 2，同时该行高亮闪烁。随后，在短时间内，它逐渐淡出为背景色。

让我们在购物车中添加这种高亮效果。每当购物车中的商品被更新（无论是添加还是修改数量）时，就闪烁其背景色。这样，即使整个页面没有刷新，用户也能更清楚地看到发生了变化。

我们遇到的第一个问题是如何识别购物车中最近更新的商品。现在，每个商品只是一个`<tr>`元素。我们需要找到一种方法来标记最近更改的那个。工作从 Cart 模型开始。让`add_product`方法返回被添加到购物车或更新数量的`CartItem`对象：

下载 depot_m/app/models/cart.rb

```ruby
def add_product(product)
  current_item = @items.find {|item| item.product == product}
  if current_item
    current_item.increment_quantity
  else
    current_item = CartItem.new(product)
    @items << current_item
  end
  current_item
end
```

## 标题

Rails 生成器自动为我们的每个控制器（products 和 store）创建了一个辅助方法文件。Rails 命令本身（最初创建应用程序的命令）创建了`application_helper.rb`文件。如果你愿意，可以将方法组织到控制器特定的辅助文件中，但实际上所有辅助方法都可供所有视图使用。目前，我们只需要在 store 视图中使用它，所以让我们先把它放到那里。

让我们来看一下`helpers`目录中的`store_helper.rb`文件：

```ruby
module StoreHelper
end
```

让我们编写一个名为`hidden_div_if`的辅助方法。它接受一个条件、一组可选属性和一个块。它将块生成的输出包裹在一个`<div>`标签中，如果条件为真，则添加`display: none`样式。我们会在 store 布局中这样使用它：

下载 depot_n/app/views/layouts/store.html.erb

```erb
<% hidden_div_if(@cart.items.empty?, :id => "cart") do %>
  <%= render(:partial => "cart", :object => @cart) %>
<% end %>
```

我们将辅助方法添加到`app/helpers`目录中的`store_helper.rb`文件中，使其仅限于 store 控制器使用：

下载 depot_n/app/helpers/store_helper.rb

```ruby
module StoreHelper
  def hidden_div_if(condition, attributes = {}, &block)
    if condition
      attributes["style"] = "display: none"
    end
    content_tag("div", attributes, &block)
  end
end
```

这段代码使用了 Rails 标准辅助方法`content_tag`，它可以将块生成的输出包裹在标签中。通过使用`&block`记号，我们让 Ruby 将传递给`hidden_div_if`的块传给`content_tag`。

最后，我们不再在 flash 中设置之前用于在用户清空购物车时显示的消息。现在不再需要它了，因为当目录索引页面重绘时，购物车会从侧边栏中明显消失。但还有另一个原因要删除它。既然我们使用 Ajax 将商品添加到购物车，在用户购物时，主页面不会在请求之间重绘。这意味着我们将继续显示一条说购物车为空的 flash 消息，即使我们在侧边栏中显示购物车。

下载 depot_n/app/controllers/store_controller.rb

```ruby
def empty_cart
  session[:cart] = nil
  redirect_to_index
end
```

虽然这看起来有很多步骤，但事实上并非如此。我们要让购物车隐藏和显示，只是让 CSS 的 display 样式根据购物车中的商品数量来决定，并使用 RJS 模板在购物车从空变为有一个商品时调用`blind_down`效果。

每个人都为看到我们漂亮的新界面而兴奋。事实上，因为我们的电脑位于办公室网络上，所以同事们将浏览器指向我们的测试应用程序，亲自试用。随后传来许多低声惊叹，大家惊叹于购物车出现然后更新的方式。每个人都喜欢它。所有人，除了 Bruce。Bruce 不信任浏览器中运行的 JavaScript，并将其关闭。而禁用 JavaScript 后，我们所有花哨的 Ajax 都停止工作了。当 Bruce 向购物车添加商品时，他看到了一些奇怪的东西：

```
$("cart").update("<h1>Your Cart</h1>\n\n<ul>\n  \n <li id=\"current_item\">\n\n 3 &times; Pragmatic Project Automation\n</li>\n</ul>\n  \n<form method=\"post\" action=\"/store/empty_cart\" class=\"button-to...
```

显然这样不行。我们需要让我们的应用程序在用户禁用浏览器中的 JavaScript 时也能工作。这将是我们下一次迭代。

#### 9.5 迭代 D5：在 JavaScript 被禁用时降级

还记得吗？在第 128 页，我们曾安排购物车出现在侧边栏中。这是在应用程序中添加一行 Ajax 代码之前做的。如果当浏览器禁用 JavaScript 时我们能够回退到这种行为，那么应用程序就既能供 Bruce 使用，也能供其他同事使用。这基本上意味着，如果到达`add_to_cart`的传入请求不是来自 JavaScript，我们就希望像原始应用程序那样重定向到索引页面。当索引页显示时，更新的购物车会出现在侧边栏中。

如果用户点击`form_remote_tag`中的按钮，会出现两种情况之一。如果 JavaScript 被禁用，则使用常规 HTTP POST 请求调用应用程序中的目标操作——就像普通 HTML 表单一样。然而，如果启用了 JavaScript，它会覆盖这种常规 POST，而是使用一个 JavaScript 对象与服务器建立反向通道。这个对象是`XMLHttpRequest`类的一个实例。由于这个名字很长，大多数人（以及 Rails）将其缩写为`xhr`。

因此，在服务器端，我们可以通过检查传入请求是否由`xhr`对象生成来判断我们是否在与支持 JavaScript 的浏览器通信。而 Rails 的 request 对象，在控制器和视图中都可用，使得测试这个条件变得容易。它提供了一个`xhr?`方法。因此，使我们的应用程序在 JavaScript 是否启用的情况下都能工作，只需要在`add_to_cart`操作中加入两行代码：

下载 depot_o/app/controllers/store_controller.rb

```ruby
def add_to_cart
  product = Product.find(params[:id])
  @cart = find_cart
  @current_item = @cart.add_product(product)
  respond_to do |format|
    format.js if request.xhr?
    format.html {redirect_to_index}
  end
rescue ActiveRecord::RecordNotFound
  logger.error("Attempt to access invalid product #{params[:id]}")
  redirect_to_index("Invalid product")
end
```

#### 9.6 我们做了什么

在这一迭代中，我们为购物车添加了 Ajax 支持：

- 我们将购物车移到了侧边栏。然后安排了`add_to_cart`操作重新显示目录页面。
- 我们使用`form_remote_tag`通过 Ajax 调用`add_to_cart`操作。
- 然后我们使用一个 RJS 模板，仅用购物车的 HTML 更新页面。
- 为了帮助用户看到购物车的变化，我们添加了高亮效果，同样使用 RJS 模板。
- 我们编写了一个辅助方法，在购物车为空时隐藏它，并使用 RJS 模板在添加商品时显示它。
- 最后，我们通过回退到我们开始 Ajax 之旅之前实现的行为，使我们的应用程序在用户浏览器禁用 JavaScript 时也能工作。

需要记住的关键点是 Ajax 开发的增量风格。从一个常规应用程序开始，然后逐个添加 Ajax 功能。Ajax 可能很难调试：通过将其缓慢地添加到应用程序中，如果应用程序停止工作，你更容易追踪发生了什么变化。而且，正如我们所见，从一个常规应用程序开始，可以在同一代码库中更容易地支持 Ajax 和非 Ajax 行为。




最后，我们给你几个提示。首先，如果你打算进行大量 Ajax 开发，你可能需要熟悉浏览器的 JavaScript 调试工具及其 DOM 检查器。*实用 Ajax：Web 2.0 入门*[GGA06] 的第 8 章包含许多有用的技巧。其次，Firefox 的 NoScript 插件让检查启用/禁用 JavaScript 变成一键轻松的事。还有人发现开发时使用两个不同的浏览器很有用——一个启用 JavaScript，另一个禁用。然后，当添加新功能时，用两个浏览器进行测试将确保你的应用在 JavaScript 启用与否的情况下都能正常工作。

#### 练习时间

以下是一些可以自己尝试的内容：

-   在 7.4 节“*练习时间*”（第 103 页）中，有一项活动是让点击图片将商品加入购物车。将其改为使用 form_remote_tag 和 image_submit_tag。
-   目前，当用户清空购物车时，整个目录会重绘，购物车随即被隐藏。你能修改应用，改用 Script.aculo.us 的 blind_up 效果吗？
-   如果浏览器禁用了 JavaScript，你做的修改还能正常工作吗？
-   为新的购物车条目尝试其他视觉效果。例如，你能将它们初始状态设为隐藏，然后让它们逐渐显现吗？这样做会不会让 Ajax 代码与初始页面显示之间共享购物车条目 partical 变得困难？
-   在购物车中每件商品旁边添加一个链接。点击该链接时，应调用一个动作来减少商品数量，当数量减为零时将其从购物车中删除。先在不使用 Ajax 的情况下让它正常工作，然后再加入 Ajax 的精彩之处。

（你可以在 http://pragprog.wikidot.com/rails-play-time 找到提示。）

在本章中，我们将看到

-   使用外键关联表，
-   使用 belongs_to 和 has_many，
-   创建基于模型的表单（form_for），以及
-   将表单、模型和视图关联起来。

### 第 10 章

### 任务 E：结账！

让我们盘点一下。到目前为止，我们已经构建了一个基本的产品管理后台，实现了一个商品目录，还有一个看起来相当漂亮的购物车。那么，现在我们需要让买家真正购买购物车里的内容。让我们实现结账功能。

我们不会在这里过度复杂化。目前，我们只需采集客户的联系信息和支付选项。利用这些信息，我们将在数据库中创建订单。在此过程中，我们会进一步了解模型、验证和表单处理。

#### 10.1 迭代 E1：捕获订单

订单是一组订单项（line items），以及购买交易的相关详细信息。我们已经有了订单项的某种雏形。购物车中包含购物车条目，但我们目前还没有对应的数据库表。我们也没有保存订单信息的表。不过，根据第 67 页的图表，加上与客户的简短交流，我们现在可以生成 Rails 模型，并填充迁移以创建相应的数据表。

首先，我们创建两个模型：

```
depot> ruby script/generate scaffold order name:string address:text \
email:string pay_type:string
...
depot> ruby script/generate scaffold line_item product_id:integer \
order_id:integer quantity:integer total_price:decimal
...
```

然后我们编辑生成器创建的两个迁移文件。

首先，在创建 orders 表时，对 pay_type 的大小设置一个限制：

```
class CreateOrders < ActiveRecord::Migration
  def self.up
    create_table :orders do |t|
      t.string :name
      t.text :address
      t.string :email
      t.string :pay_type, :limit => 10

      t.timestamps
    end
  end

  def self.down
    drop_table :orders
  end
end
```

然后，调整 line_items 的迁移：

```
class CreateLineItems < ActiveRecord::Migration
  def self.up
    create_table :line_items do |t|
      t.integer :product_id, :null => false, :options =>
        "CONSTRAINT fk_line_item_products REFERENCES products(id)"
      t.integer :order_id, :null => false, :options =>
        "CONSTRAINT fk_line_item_orders REFERENCES orders(id)"
      t.integer :quantity, :null => false
      t.decimal :total_price, :null => false, :precision => 8, :scale => 2

      t.timestamps
    end
  end

  def self.down
    drop_table :line_items
  end
end
```

注意，这个表有两个外键。line_items 表中的每一行都与一个订单和一个产品关联。不幸的是，这带来多个问题。

首先，Rails 迁移没有提供独立于数据库的方式来指定这些外键约束，因此我们不得不求助于添加原生的 DDL 子句（这里使用的是 SQLite 3 的）作为选项。其次，在撰写本文时，SQLite 3.4.0 会解析这些约束，但不会强制实施外键约束。最后，这些自定义约束不会

##### 乔问道……

##### 信用卡处理在哪里？

在这一点上，我们的教程应用将与现实略有偏差。在现实世界中，我们可能希望应用处理结账的商业部分。我们甚至可能希望集成信用卡处理（可能使用 Payment 模块* 或 Tobias Lütke 的 ActiveMerchant 库†）。然而，与后端支付处理系统集成需要大量文书工作和绕很多弯。这会分散我们对 Rails 的注意力，因此我们决定先跳过这个细节。

* http://rubyforge.org/projects/payment
† http://www.activemerchant.org/

被存储在 db/schema.rb 文件中，因此也不会被复制到测试数据库中。¹

现在我们已经创建了两个迁移，可以应用它们了：

```
depot> rake db:migrate
== 20080601000005 CreateOrders: migrating ====================================
-- create_table(:orders)
   -> 0.0066s
== 20080601000005 CreateOrders: migrated (0.0096s) ===========================
== 20080601000006 CreateLineItems: migrating ==================================
-- create_table(:line_items)
   -> 0.0072s
== 20080601000006 CreateLineItems: migrated (0.0500s) ========================
```

由于数据库的 schema_migrations 表中没有这两个新迁移的记录，db:migrate 任务将两者都应用到了数据库。当然，我们也可以在单独创建迁移后逐一运行迁移任务。

##### 模型之间的关系

数据库现在已经知道 line_items、orders 和 products 之间的关系。然而，Rails 应用并不知道。我们需要添加一些

1. 许多 Rails 开发者并不费心指定数据库级的约束（如外键），而是依赖应用代码来确保一切正确拼接。这可能正是 Rails 迁移不允许你指定约束的原因。然而，涉及数据库完整性时，很多人（包括 Dave 和 Sam）认为一盎司的额外检查可以省去大量深夜生产系统调试的麻烦。如果你对此感兴趣，可以在第 308 页找到更多信息。

##### 创建订单捕获表单

现在我们有了表和模型，就可以开始结账流程了。首先，我们需要在购物车中添加一个“结账”按钮。我们将其链接到 store 控制器中的 checkout 动作：

```
Download depot_p/app/views/store/cart.html.erb
<div class="cart-title">Your Cart</div>
<table>
  <%= render(:partial => "cart_item", :collection => cart.items) %>

  <tr class="total-line">
    <td colspan="2">Total</td>
    <td class="total-cell"><%= number_to_currency(cart.total_price) %></td>
  </tr>

</table>

►
<%= button_to "Checkout", :action => 'checkout' %>
<%= button_to "Empty cart", :action => :empty_cart %>
```

我们希望 checkout 动作向用户呈现一个表单，提示他们输入 orders 表中的信息：姓名、地址、电子邮件地址和支付类型。这意味着我们将在某个时候显示一个包含表单的 Rails 模板。该表单上的输入字段需要链接到 Rails 模型对象中的相应属性，因此我们需要在 checkout 动作中创建一个空的模型对象，让这些字段有东西可操作。²（我们还必须找到当前的购物车，因为它会显示在布局中。在每个动作开始时查找购物车开始变得繁琐；我们稍后会看到如何消除这种重复。）

```
Download depot_p/app/controllers/store_controller.rb
def checkout
  @cart = find_cart
  if @cart.items.empty?
    redirect_to_index("Your cart is empty")
  else
    @order = Order.new
  end
end
```

注意我们如何检查购物车中是否有物品。这可以防止人们直接导航到结账选项并创建空订单。

现在来看模板本身。为了捕获用户信息，我们将使用表单。与所有 HTML 表单一样，诀窍在于将初始值填充到

> 2. 再说一次，如果你在跟着操作，请记住动作（actions）必须放在控制器中的 private 关键字之前。




controller:
def edit
@order = Order.find(...)
end

model object:
@order.name → "Dave"

```
<% form_for :order, :url => { :action => :save_order } do |form| %>
<p>
<label for="order_name">Name:</label>
<%= form.text_field :name, :size => 40 %>
</p>
<% end %>
```

Name: Dave

Figure 10.1: Names in form_for map to objects and attributes.

form fields and then extracting those values back out into our application when the user hits the submit button.

In the controller, we set up the @order instance variable to reference a new Order model object. We do this because the view populates the form from the data in this object. As it stands, that's not particularly interesting. Because it's a new model object, all the fields will be empty. However, consider the general case. Maybe we want to edit an existing order. Or maybe the user has tried to enter an order but their data has failed validation. In these cases, we want any existing data in the model shown to the user when the form is displayed. Passing in the empty model object at this stage makes all these cases consistent—the view can always assume it has a model object available.

Then, when the user hits the submit button, we'd like the new data from the form to be extracted into a model object back in the controller.

Fortunately, Rails makes this relatively painless. It provides us with a bunch of form helper methods. These helpers interact with the controller and with the models to implement an integrated solution for form handling. Before we start on our final form, let's look at a simple example:

```
Line 1  <% form_for :order, :url => { :action => :save_order } do |form| %>
2       <p>
3         <label for="order_name">Name:</label>
4         <%= form.text_field :name, :size => 40 %>
5       </p>
6  <% end %>
```

There are two interesting things in this code. First, the form_for helper on line 1 sets up a standard HTML form. But it does more. The first parameter, :order, tells the method that it’s dealing with an object in an instance variable named @order. The helper uses this information when naming fields and when arranging for the field values to be passed back to the controller.

The :url parameter tells the helper what to do when the user hits the submit button. In this case, we’ll generate an HTTP POST request that’ll end up getting handled by the save_order action in the controller.

You’ll see that form_for sets up a Ruby block environment (this block ends on line 6). Within this block, you can put normal template stuff (such as the <p> tag). But you can also use the block’s parameter (form in this case) to reference a form context. We use this context on line 4 to add a text field to the form. Because the text field is constructed in the context of the form_for, it is automatically associated with the data in the @order object.

All these relationships can be confusing. It’s important to remember that Rails needs to know both the *names* and the *values* to use for the fields associated with a model. The combination of form_for and the various field-level helpers (such as text_field) give it this information. We can see this process in Figure 10.1, on the preceding page.

Now we can create the template for the form that captures a customer’s details for checkout. It’s invoked from the checkout action in the store controller, so the template will be called checkout.html.erb in the directory app/views/store.

Rails has form helpers for all the different HTML-level form elements. In the code that follows, we use text_field and text_area helpers to capture the customer’s name, e-mail, and address:

```
```erb
<div class="depot-form">

  <%#= error_messages_for 'order' %>

  <% form_for :order, :url => { :action => :save_order } do |form| %>
    <fieldset>
      <legend>Please Enter Your Details</legend>

      <div>
        <% form.label :name, "Name:" %>
        <% form.text_field :name, :size => 40 %>
      </div>

      <div>
        <% form.label :address, "Address:" %>
        <% form.text_area :address, :rows => 3, :cols => 40 %>
      </div>
```
```

```
<div>
  <%= form.label :email, "E-Mail:" %>
  <%= form.text_field :email, :size => 40 %>
</div>

<div>
  <%= form.label :pay_type, "Pay with:" %>
  <%= form.select :pay_type,
                  Order::PAYMENT_TYPES,
                  :prompt => "Select a payment method" %>
</div>

<%= submit_tag "Place Order", :class => "submit" %>
</fieldset>
<% end %>
</div>
```

The only tricky thing in there is the code associated with the selection list. We've assumed that the list of available payment options is an attribute of the Order model—it will be an array of arrays in the model file. The first element of each subarray is the string to be displayed as the option in the selection, and the second value gets submitted in the request and ultimately is what is stored in the database.³ We'd better define the option array in the model order.rb before we forget:

```
Download depot_p/app/models/order.rb
class Order < ActiveRecord::Base
  PAYMENT_TYPES = [
    # Displayed          stored in db
    [ "Check",          "check" ],
    [ "Credit card",    "cc" ],
    [ "Purchase order", "po" ]
  ]

  # ...
```

In the template, we pass this array of payment type options to the select helper. We also pass the :prompt parameter, which adds a dummy selection containing the prompt text.

> 3. If we anticipate that other non-Rails applications will update the orders table, we might want to move the list of payment types into a separate lookup table and make the payment type column a foreign key referencing that new table. Rails provides good support for generating selection lists in this context too. You simply pass the select helper the result of doing a find(:all) on your lookup table.

##### Add a little CSS magic:

Download depot_p/public/stylesheets/depot.css

```
/* Styles for order form */

.depot-form fieldset {
  background: #efe;
}

.depot-form legend {
  color: #dfd;
  background: #141;
  font-family: sans-serif;
  padding: 0.2em 1em;
}

.depot-form label {
  width: 5em;
  float: left;
  text-align: right;
  padding-top: 0.2em;
  margin-right: 0.1em;
  display: block;
}

.depot-form select, .depot-form textarea, .depot-form input {
  margin-left: 0.5em;
}

.depot-form .submit {
  margin-left: 4em;
}

.depot-form div {
  margin: 0.5em 0;
}
```

We're ready to play with our form. Add some stuff to your cart, and then click the Checkout button. You should see something like Figure 10.2, on the next page.

Looking good! But, if you click the Place Order button, you'll be greeted with the following:

```
Unknown action
No action responded to save_order
```

Before we move on to that new action, though, let's finish off the checkout action by adding some validation. We'll change the Order model to verify that the customer enters data for all the fields (including the payment type drop-down list).

![](img/a160fc3a330a0b3b2a764d41d614e688_150_0.png)

Figure 10.2: Our checkout screen

We also validate that the payment type is one of the accepted values.[^4][^5]

```
```ruby
class Order < ActiveRecord::Base
  PAYMENT_TYPES = [
    # Displayed          stored in db
    [ "Check",           "check" ],
    [ "Credit card",     "cc" ],
    [ "Purchase order",  "po" ]
  ]

  validates_presence_of :name, :address, :email, :pay_type
  validates_inclusion_of :pay_type, :in =>
    PAYMENT_TYPES.map {|disp, value| value}

  # ...
```
```

Note that we already call the error_messages_for helper at the top of the page.

> [^4]: To get the list of valid payment types, we take our array of arrays and use the Ruby map method to extract just the values.
> 
> [^5]: Some folks might be wondering why we bother to validate the payment type, given that its value comes from a drop-down list that contains only valid values. We do it because an application can't assume that it's being fed values from the forms it creates. Nothing is stopping a malicious user from submitting form data directly to the application, bypassing our form. If the user set an unknown payment type, they might conceivably get our products for free.





这会报告验证失败（但只有在我们再写完一段代码后才会生效）。

##### 捕获订单详情

让我们在控制器中实现 `save_order` 动作。该方法需要完成以下工作：

- 1. 从表单捕获值，填充一个新的 Order 模型对象。
- 2. 将购物车中的订单项添加到该订单中。
- 3. 验证并保存订单。如果失败，显示相应的消息，并让用户纠正任何问题。
- 4. 订单成功保存后，重新显示目录页面，并显示一条确认订单已提交的消息。

该方法的最终代码大致如下：

```
Download depot_p/app/controllers/store_controller.rb

Line 1 def save_order
- @cart = find_cart
- @order = Order.new(params[:order])
- @order.add_line_items_from_cart(@cart)
5 if @order.save
- session[:cart] = nil
- redirect_to_index("Thank you for your order")
- else
- render :action => 'checkout'
10 end
end
```

在第 3 行，我们创建了一个新的 Order 对象，并用表单数据初始化它。这里我们想要与订单对象相关的所有表单数据，所以从参数中选取 `:order` 哈希（这是我们在 `form_for` 中作为第一个参数传入的名称）。下一行会把已经存储在购物车中的条目添加到该订单中——我们稍后会编写实际的方法。

接下来，在第 5 行，我们告诉订单对象将自身（及其子项，即订单项）保存到数据库。在此过程中，订单对象会执行验证（但我们稍后再讨论）。如果保存成功，我们要做两件事：首先，从 `session` 中删除购物车，为该客户的下一笔订单做好准备；然后，使用 `redirect_to_index` 方法重新显示目录页面，并显示一条令人愉快的消息。相反，如果保存失败，我们重新显示结算表单。

##### 乔问道……

###### 你难道不会创建重复订单吗？

乔看到我们的控制器在两个动作 `checkout` 和 `save_order` 中都创建了 Order 模型对象，他担心为什么这不会导致数据库中出现重复订单。

答案很简单：`checkout` 动作在内存中创建一个 Order 对象，只是为了让模板代码有可操作的对象。响应发送到浏览器后，这个特定对象就会被丢弃，最终被 Ruby 的垃圾回收器回收。它从未接近过数据库。

`save_order` 动作也会创建一个 Order 对象，并用表单字段填充它。这个对象确实会被保存到数据库中。

因此，模型对象扮演两个角色：它们在数据库之间映射数据，但它们也只是保存业务数据的普通对象。只有当你告诉它们时（通常通过调用 `save`），它们才会影响数据库。

在 `save_order` 动作中，我们假定订单对象包含 `add_line_items_from_cart` 方法，所以现在来实现这个方法：

```
Download: depot_p/app/models/order.rb

def add_line_items_from_cart(cart)
  cart.items.each do |item|
    li = LineItem.from_cart_item(item)
    line_items << li
  end
end
```

注意，我们不需要对外键字段做任何特殊处理，比如在订单项行中设置 `order_id` 列来引用新建的订单行。Rails 使用我们添加到 Order 和 LineItem 模型中的 `has_many` 和 `belongs_to` 声明替我们完成了这种关联。在第 4 行，将每个新的订单项追加到 `line_items` 集合中，就把键管理的责任交给了 Rails。

Order 模型中的这个方法反过来依赖于 line item 模型中的一个简单辅助方法，该方法根据购物车条目构造一个新的订单项：

```
Download: depot_p/app/models/line_item.rb

class LineItem < ActiveRecord::Base
  belongs_to :order
  belongs_to :product
```

![](img/a160fc3a330a0b3b2a764d41d614e688_154_0.png)

图 10.3：满堂红！每个字段都未通过验证。

##### 最后一个 Ajax 改动

接受订单后，我们会重定向到首页，显示令人愉快的 flash 消息“感谢您的订单”。如果用户继续购物，且浏览器启用了 JavaScript，我们会在侧边栏中填充购物车，而不会重绘主页面。这意味着 flash 消息会继续显示。我们希望，在用户向购物车添加第一个条目后，它就会消失（就像浏览器禁用 JavaScript 时那样）。幸运的是，修复很简单：在向购物车添加内容时，只需隐藏包含 flash 消息的 `<div>`。不过，事情往往没有那么简单。

最初尝试隐藏 flash 时，可能会在 `add_to_cart.js.rjs` 中添加下面这一行：

```
page[:notice].hide
# rest as before...
```

然而，这并不起作用。如果我们第一次进入商店，flash 中没有任何内容，所以 `id` 为 `notice` 的 `<div>` 不会显示。如果没有 `id` 为 `notice` 的 `<div>`，RJS 模板生成的、试图隐藏该 `<div>` 的 JavaScript 就会崩溃，模板的其余部分永远不会执行。结果，你在侧边栏中永远看不到购物车更新。

解决办法有点小技巧。我们只想在 `notice` `<div>` 存在时执行 `.hide`，但 RJS 不能让我们生成用于检测 `<div>` 的 JavaScript。不过，它确实允许我们遍历页面上与某个 CSS 选择器模式匹配的元素。所以，让我们遍历所有 `id` 为 `notice` 的 `<div>` 标签。循环要么找到一个（我们可以隐藏它），要么一个也没有，这时 `hide` 就不会被调用。

```
Download depot_p/app/views/store/add_to_cart.js.rjs
page.select("div#notice").each { |div| div.hide }

page.replace_html("cart", :partial => "cart", :object => @cart)

page[:cart].visual_effect :blind_down if @cart.total_items == 1

page[:current_item].visual_effect :highlight,
  :startcolor => "#88ff88",
  :endcolor => "#114411"
```

客户很满意。我们已经实现了产品维护、基本目录和购物车，现在又有了一个简单的订购系统。显然，我们还需要编写某种订单履行应用程序，但这可以等到新的迭代再做。（而那个迭代我们在本书中会跳过；它对 Rails 没有太多新内容可讲。）

#### 我们刚刚做了什么

在相当短的时间内，我们完成了以下工作：

- - 我们添加了 `orders` 和 `line_items` 表（以及相应的模型），并将它们关联了起来。
- - 我们创建了一个表单来捕获订单详情，并将其与订单模型关联。
- - 我们添加了验证，并使用辅助方法向用户显示错误。

#### 动手练习

这里有一些你可以自己尝试的内容：

- - 追踪 `save_order`、`add_line_items_from_cart` 和 `from_cart_item` 方法的执行流程。控制器、订单模型和订单项模型之间是否看起来充分解耦？（一种判断方法是查看潜在变化——如果你更改了某些内容，比如给购物车条目添加一个新字段，这个变化是否会在代码中引起连锁反应？）你能找到进一步降低耦合的方法吗？
- - 当结算页面已经显示时，如果点击侧边栏中的“结账”按钮，会发生什么？你能找到在这种情况下禁用该按钮的方法吗？（提示：在控制器中设置的变量在布局、局部模板以及直接渲染的模板中都可用。）
- - 目前可用的支付类型列表是作为 Order 类中的一个常量存储的。你能把这个列表移到数据库表中吗？你仍然能让该字段的验证生效吗？

（你可以在 http://pragprog.wiki dot.com/rails-play-time 找到提示。）

## Pragmatic 书架

## 您的购物车

1x Pragmatic Project Automation $29.95
总计 $29.95

结账

清空购物车

- - 首页
- - 问题
- - 新闻
- - 联系

## 请输入您的详细信息

姓名：Dave Thomas
地址：123 Main St
电子邮件：customer@pragprog.com
支付方式：支票
提交订单

## Pragmatic 书架

- - 首页
- - 问题
- - 新闻
- - 联系

感谢您的订单

## 您的 Pragmatic 目录

## Pragmatic Project Automation

《Pragmatic Project Automation》向您展示如何通过自动化提高项目流程的一致性和可重复性，以降低风险和错误。

简而言之，我们将让名为计算机的这个工具为您处理那些单调（但重要）的项目事务。

图 10.4：我们的首次结账





在本章中，我们将看到

- 向模型添加虚拟属性，
- 使用更多验证，
- 编写没有底层模型的表单，
- 实现单动作表单处理，
- 向会话添加身份验证，
- 使用 script/console，
- 使用数据库事务，以及
- 编写 Active Record 钩子。

### 第 11 章

### 任务 F：管理

我们有一个满意的客户——在很短的时间内，我们共同搭建了一个她可以开始向用户展示的基础购物车。还有一个改动她希望看到。现在，任何人都可以访问管理功能。她希望我们添加一个基本用户管理系统，要求你登录后才能进入网站的管理部分。

我们很乐意这样做，因为这给了我们一个机会来查看虚拟属性和过滤器，并且让我们可以稍微整理一下应用程序。

与客户交谈后，似乎我们不需要为应用程序设计一个特别复杂的安保系统。我们只需要根据用户名和密码识别一些人。一旦被识别，这些人就可以使用所有管理功能。

#### 11.1 迭代 F1：添加用户

让我们先创建一个模型和数据库表来保存管理员的用户名和密码。与其以明文存储密码，我们将它们通过 SHA1 摘要处理，生成一个 160 位的哈希值。我们通过对用户提供的密码进行摘要并将该哈希值与数据库中的值进行比较来检查用户的密码。该系统通过加盐变得更加安全，加盐会通过将密码与伪随机字符串组合来改变创建哈希时使用的种子。¹

```
depot> ruby script/generate scaffold \
  user name:string hashed_password:string salt:string
```

由于修改了 config/routes.rb，而该文件出于性能原因会被缓存，你需要重启服务器。

> 1. 关于如何执行此操作的其它配方，请参阅 Chad Fowler 的 Rails Recipes [Fow06] 中的 Authentication 和 Role-Based Authentication 部分。

完成后，让我们看看生成的迁移：

```
Download depot_p/db/migrate/20080601000007_create_users.rb
class CreateUsers < ActiveRecord::Migration
  def self.up
    create_table :users do |t|
      t.string :name
      t.string :hashed_password
      t.string :salt

      t.timestamps
    end
  end

  def self.down
    drop_table :users
  end
end
```

现在像往常一样运行迁移：

```
depot> rake db:migrate
```

现在我们必须完善用户模型。这看起来相当复杂，因为它必须从应用程序的角度与密码的明文版本协同工作，同时在数据库中维护盐值和哈希密码。让我们分段查看模型。首先，这里是验证：

```
Download depot_p/app/models/user.rb
class User < ActiveRecord::Base

  validates_presence_of  :name
  validates_uniqueness_of :name

  attr_accessor :password_confirmation
  validates_confirmation_of :password

  validate :password_non_blank

private

  def password_non_blank
    errors.add(:password, "Missing password") if hashed_password.blank?
  end
end
```

对于这样一个简单的模型来说，这已经是相当多的验证了。我们检查名称是否存在且唯一（即数据库中不能有两个用户具有相同的名称）。然后是神秘的 validates_confirmation_of 声明。

你知道那些表单会提示你输入密码，然后要求你在另一个字段中重新输入，以便验证你输入的内容是否与你认为的一致吗？好吧，Rails 可以自动验证这两个密码是否匹配。我们稍后会看到它是如何工作的。现在，我们只需要知道我们需要两个密码字段，一个用于实际密码，另一个用于其确认。

最后，我们检查密码是否已设置。但我们并没有检查 password 属性本身。为什么？因为它实际上并不存在——至少不在数据库中。与其如此，我们检查其代理，即哈希密码是否存在。但要理解这一点，我们必须看看我们如何处理密码存储。

首先让我们看看如何创建哈希密码。诀窍是创建一个唯一的盐值，将其与明文密码组合成一个字符串，然后对结果运行 SHA1 摘要，返回一个 40 个字符的十六进制字符串。我们将其写成私有类方法。（我们还需要记得在文件中 require digest/sha1 库。参见第 163 页开始的列表以查看其位置。）

```
Download depot_p/app/models/user.rb
def self.encrypted_password(password, salt)
  string_to_hash = password + "wibble" + salt
  Digest::SHA1.hexdigest(string_to_hash)
end
```

我们通过将随机数与用户对象的 object id 拼接来创建盐字符串。盐值具体是什么并不重要，只要它不可预测即可（例如，使用时间作为盐，其熵就低于随机字符串）。我们将这个新盐存储到模型对象的 salt 属性中。同样，这是一个私有方法，因此将其放在源代码中 private 关键字之后：

```
Download depot_p/app/models/user.rb
def create_new_salt
  self.salt = self.object_id.to_s + rand.to_s
end
```

这段代码中有一个我们以前没有见过的细微差别。请注意，我们写了 self.salt =.... 这强制赋值使用 salt= 访问器方法——我们说的是“在当前对象中调用方法 salt”。如果没有 self.，Ruby 会认为我们正在为局部变量赋值，我们的代码将没有任何效果。²

2. 尽管直接使用实例变量也能达到正确的结果，但它也会将你绑定到可能并不总是相同的表示形式。属性 salt/salt= 是对底层模型属性的“官方”接口，因此最好使用它们而不是实例变量。另一种看待方式是，由于属性构成了类的公共接口的一部分，那么类也应该吃自己的狗粮并使用该接口。如果你内部使用 @xx 而外部使用 .xx，未来出现某种不匹配的可能性就很大了。

现在我们需要编写一些代码，以便每当将新的明文密码存储到用户对象中时，我们会自动创建一个哈希版本（它将被存储到数据库中）。我们将通过使明文密码成为模型的 *虚拟属性* 来实现这一点——它对我们的应用程序看起来像一个属性，但不会持久化到数据库中。

如果不是为了创建哈希版本的需要，我们可以简单地使用 Ruby 的 attr_accessor 声明来实现：

```
attr_accessor :password
```

在幕后，attr_accessor 生成两个访问器方法：一个名为 password 的读取器和一个名为 password= 的写入器。写入器方法名以等号结尾意味着它可以被赋值。因此，与其使用标准的访问器，我们将简单地实现我们自己的公共方法，并让写入器同时创建新的盐并设置哈希密码：

```
def password
  @password
end

def password=(pwd)
  @password = pwd
  return if pwd.blank?
  create_new_salt
  self.hashed_password = User.encrypted_password(self.password, self.salt)
end
```

还有一个最后的改动。让我们编写一个公共类方法，如果调用者提供正确的名称和密码，则返回一个用户对象。由于传入的密码是明文，我们必须使用名称作为键读取用户记录，然后使用该记录中的盐值再次构造哈希密码。然后，如果哈希密码匹配，我们返回用户对象。我们可以使用此方法来验证用户。

```
def self.authenticate(name, password)
  user = self.find_by_name(name)
  if user
    expected_password = encrypted_password(password, user.salt)
    if user.hashed_password != expected_password
      user = nil
    end
  end
  user
end
```

这段代码使用了巧妙的 Active Record 技巧。你会看到该方法的第一行调用了 find_by_name。但我们并没有定义这样名称的方法。





然而，Active Record 注意到对未定义方法的调用，并发现它以字符串 find_by 开头并以列名结尾。它随后为我们动态构造一个查找方法，并将其添加到我们的类中。我们从第 341 页开始讨论这些动态查找器。

用户模型包含相当多的代码，但它展示了模型可以承载相当多的业务逻辑。让我们在继续进入控制器之前先回顾整个模型：

```
Download depot_p/app/models/user.rb
require 'digest/sha1'

class User < ActiveRecord::Base

  validates_presence_of    :name
  validates_uniqueness_of  :name

  attr_accessor :password_confirmation
  validates_confirmation_of :password

  validate :password_non_blank

  def self.authenticate(name, password)
    user = self.find_by_name(name)
    if user
      expected_password = encrypted_password(password, user.salt)
      if user.hashed_password != expected_password
        user = nil
      end
    end
    user
  end

  # 'password' is a virtual attribute
  def password
    @password
  end

  def password=(pwd)
    @password = pwd
    return if pwd.blank?
    create_new_salt
    self.hashed_password = User.encrypted_password(self.password, self.salt)
  end

private

  def password_non_blank
    errors.add(:password, "Missing password") if hashed_password.blank?
  end

def create_new_salt
  self.salt = self.object_id.to_s + rand.to_s
end

def self.encrypted_password(password, salt)
  string_to_hash = password + "wibble" + salt
  Digest::SHA1.hexdigest(string_to_hash)
end
end
```

##### 管理我们的用户

除了我们设置的模型和表之外，我们已经为管理模型生成了一些脚手架。然而，这个脚手架需要一些调整（主要是精简）才能使用。

让我们从控制器开始。它定义了标准方法：index、show、new、edit、update 和 delete。但对于用户来说，实际上并没有太多可展示的内容，除了名称和难以理解的密码哈希。因此，让我们在创建操作或更新操作后避免重定向到显示用户。相反，让我们重定向到索引并将用户名添加到 flash 通知中。

在我们这里的同时，让我们也按名称对索引中返回的用户进行排序：

Download depot_p/app/controllers/users_controller.rb

```
class UsersController < ApplicationController
  # GET /users
  # GET /users.xml
  def index
    @users = User.find(:all, :order => :name)

    respond_to do |format|
      format.html # index.html.erb
      format.xml  { render :xml => @users }
    end
  end

  # GET /users/1
  # GET /users/1.xml
  def show
    @user = User.find(params[:id])

    respond_to do |format|
      format.html # show.html.erb
      format.xml  { render :xml => @user }
    end
  end

  # GET /users/new
  # GET /users/new.xml
  def new
    @user = User.new

    respond_to do |format|
      format.html # new.html.erb
      format.xml  { render :xml => @user }
    end
  end

  # GET /users/1/edit
  def edit
    @user = User.find(params[:id])
  end

  # POST /users
  # POST /users.xml
  def create
    @user = User.new(params[:user])

    respond_to do |format|
      if @user.save
        flash[:notice] = "User #{@user.name} was successfully created."
        format.html { redirect_to(:action => 'index') }
        format.xml  { render :xml => @user, :status => :created,
                      :location => @user }
      else
        format.html { render :action => "new" }
        format.xml  { render :xml => @user.errors,
                      :status => :unprocessable_entity }
      end
    end
  end

  # PUT /users/1
  # PUT /users/1.xml
  def update
    @user = User.find(params[:id])

    respond_to do |format|
      if @user.update_attributes(params[:user])
        flash[:notice] = "User #{@user.name} was successfully updated."
        format.html { redirect_to(:action => 'index') }
        format.xml  { head :ok }
      else
        format.html { render :action => "edit" }
        format.xml  { render :xml => @user.errors,
                      :status => :unprocessable_entity }
      end
    end
  end

  # DELETE /users/1
  # DELETE /users/1.xml
  def destroy
    @user = User.find(params[:id])
    @user.destroy

    respond_to do |format|
      format.html { redirect_to(users_url) }
      format.xml  { head :ok }
    end
  end
end
```

接下来，列出用户的视图包含太多信息。具体来说，它包含哈希密码和盐。我们将简单地删除这两个字段的 th 和 td 行，留下更简单的视图：

Download depot_p/app/views/users/index.html.erb

```
<h1>Listing users</h1>

<table>
  <tr>
    <th>Name</th>
  </tr>

<% for user in @users %>
  <tr>
    <td><%=h user.name %></td>
    <td><%= link_to 'Show', user %></td>
    <td><%= link_to 'Edit', edit_user_path(user) %></td>
    <td><%= link_to 'Destroy', user, :confirm => 'Are you sure?', :method => :delete %></td>
  </tr>
<% end %>
</table>

<br />

<%= link_to 'New user', new_user_path %>
```

最后，我们需要更新用于创建新用户的表单。首先，我们用密码和密码确认字段替换哈希密码和盐文本字段。然后我们添加 legend 和 fieldset 标签。最后我们用一个 <div> 标签包装输出，该标签的类我们在样式表中之前定义过。

Download depot_p/app/views/users/new.html.erb

```
<div class="depot-form">

<% form_for(@user) do |f| %>
  <%= f.error_messages %>

  <fieldset>
    <legend>Enter User Details</legend>

    <div>
      <%= f.label :name %>:
      <%= f.text_field :name, :size => 40 %>
    </div>

<div>
  <%= f.label :user_password, 'Password' %>:
  <%= f.password_field :password, :size => 40 %>
</div>

<div>
  <%= f.label :user_password_confirmation, 'Confirm' %>:
  <%= f.password_field :password_confirmation, :size => 40 %>
</div>

<div>
  <%= f.submit "Add User", :class => "submit" %>
</div>

</fieldset>
<%= end %>

</div>
```

就这样。我们现在可以向数据库添加用户。但在尝试之前，让我们链接我们的样式表。同样，我们通过修改用户视图的布局来做到这一点：

Download depot_p/app/views/layouts/users.html.erb

```
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">

<html xmlns="http://www.w3.org/1999/xhtml" xml:lang="en" lang="en">
<head>
  <meta http-equiv="content-type" content="text/html;charset=UTF-8" />
  <title>Users: <%= controller.action_name %></title>
  <%= stylesheet_link_tag 'scaffold', 'depot' %>
</head>
```

让我们试试。导航到 http://localhost:3000/users/new，你应该会看到这个令人惊叹的页面设计示例：

![](img/a160fc3a330a0b3b2a764d41d614e688_166_0.png)

点击 Add User 后，索引会重新显示，并带有愉快的 flash 通知。

如果我们查看数据库，你会看到我们已经存储了用户详细信息。 当然，你的行中的值会不同，因为盐值本质上是随机的。

```
depot> sqlite3 -line db/development.sqlite3 "select * from users"
    id = 1
    name = dave
    hashed_password = a12b1dbb97d3843ee27626b2bb96447941887ded
    salt = 203333500.653238054564258
    created_at = 2008-05-19 21:40:19
    updated_at = 2008-05-19 21:40:19
```

#### 11.2 迭代 F2：登录

为商店管理员添加登录支持意味着什么？

- 我们需要提供一个表单，让他们输入用户名和密码。
- 一旦他们登录，我们需要在他们的会话期间（或直到他们注销）以某种方式记录这一事实。
- 我们需要限制对应用程序管理部分的访问，只允许已登录的人管理商店。

我们需要一个控制器来支持登录操作，并且它需要在 session 中记录一些内容以表明管理员已登录。让我们先定义一个 admin 控制器，其中包含三个操作，login、logout 和 index（它只是欢迎管理员）：

```
depot> ruby script/generate controller admin login logout index
exists  app/controllers/
exists  app/helpers/
create  app/views/admin
exists  test/functional/
create  app/controllers/admin_controller.rb
create  test/functional/admin_controller_test.rb
create  app/helpers/admin_helper.rb
create  app/views/admin/login.html.erb
create  app/views/admin/logout.html.erb
create  app/views/admin/index.html.erb
```

登录操作需要在 session 中记录一些内容以表明管理员已登录。让我们让它使用键 :user_id 存储其 User 对象的 id。登录代码如下所示：

```
Download depot_p/app/controllers/admin_controller.rb
def login
  if request.post?
    user = User.authenticate(params[:name], params[:password])
    if user
      session[:user_id] = user.id
```





```
redirect_to(:action => "index")
else
  flash.now[:notice] = "Invalid user/password combination"
end
end
end
```

在此方法中，我们将检测我们是被调用来显示初始（空）表单还是被调用来保存已完成表单中的数据。我们将通过查看传入请求的 HTTP 方法来做到这一点。如果它来自一个 &lt;a href="..."&gt; 链接，我们会将其视为 GET 请求。如果它包含表单数据（当用户点击提交按钮时就会如此），我们会看到一个 POST。（因此，这种风格有时被称为 postback 处理。）

使用 postback 处理，就没有必要发出重定向，也就没有必要在请求之间使 flash 可用。flash.now 使通知可用于模板，而无需将其存储在 session 中。

我们也在做另一件新的事情，即使用一个不直接与模型对象关联的表单。要了解它是如何工作的，让我们来看一下 login action 的模板：

```erb
Download depot_p/app/views/admin/login.html.erb

<div class="depot-form">
  <% form_tag do %>
    <fieldset>
      <legend>Please Log In</legend>

      <div>
        <label for="name">Name:</label>
        <%= text_field_tag :name, params[:name] %>
      </div>

      <div>
        <label for="password">Password:</label>
        <%= password_field_tag :password, params[:password] %>
      </div>

      <div>
        <%= submit_tag "Login" %>
      </div>
    </fieldset>
  <% end %>
</div>
```

此表单与我们之前看到的不同。不同于使用 form_for，它使用 form_tag，后者只是构建一个普通的 HTML &lt;form&gt;。在该表单内部，它使用 text_field_tag 和 password_field_tag，这两个助手创建 HTML &lt;input&gt; 标签。每个助手接受两个参数。第一个是赋予字段的名称，第二个是用于填充字段的值。这种表单样式允许我们将 params 结构中的值直接与表单字段关联——不需要模型对象。在我们的例子中，我们选择直接在表单中使用 params 对象。另一种选择是让控制器设置实例变量。

图 11.1：参数在控制器、模板和浏览器之间的流动。

图 11.1 说明了这种表单样式的流程。请注意，表单字段的值如何使用 params hash 在控制器和视图之间通信：视图从 params[:name] 获取要在字段中显示的值，并且当用户提交表单时，新的字段值以相同的方式提供给控制器。

如果用户成功登录，我们将用户记录的 id 存储在 session 数据中。我们将使用 session 中该值的存在作为标志来指示管理员已登录。

最后，是时候添加索引页面了，这是管理员登录后看到的第一个屏幕。让我们让它有用——我们将让它显示商店中订单的总数。在目录 app/views/admin 中创建文件 index.html.erb 中的模板。（此模板使用 pluralize 助手，在本例中根据其第一个参数的基数生成字符串 order 或 orders。）

```erb
Download depot_p/app/views/admin/index.html.erb

<h1>Welcome</h1>

It's <%= Time.now %>
We have <%= pluralize(@total_orders, "order") %> .
```

index action 设置计数：

```ruby
Download depot_p/app/controllers/admin_controller.rb

def index
  @total_orders = Order.count
end
```

现在我们可以体验作为管理员登录的乐趣：

![](img/a160fc3a330a0b3b2a764d41d614e688_170_0.png)

我们向客户展示了我们所在的位置，但她指出我们仍然没有控制对管理页面的访问（这毕竟是本次练习的目的）。

#### 11.3 Iteration F3: Limiting Access

我们希望阻止没有管理员登录的人访问我们网站的管理页面。事实证明，使用 Rails *filter* 设施很容易实现。

Rails 过滤器允许你在 action 方法被调用之前、之后或两者之后拦截对它们的调用，添加你自己的处理。在我们的例子中，我们将使用 *before filter* 来拦截对 admin 控制器中所有 action 的调用。拦截器可以检查 session[:user_id]。如果设置并且如果它对应于数据库中的用户，应用程序就知道管理员已登录，并且调用可以继续。如果未设置，拦截器可以发出重定向，在本例中重定向到我们的登录页面。

我们应该把这个方法放在哪里？它可以直接放在 admin 控制器中，但出于不久后会显现的原因，让我们把它放在 ApplicationController 中，即我们所有控制器的父类。它在目录 app/controllers 中的文件 application.rb³ 中。还要注意，我们需要限制对该方法的访问，因为 application.rb 中的方法作为实例方法出现在我们所有的控制器中。这里的任何公共方法都作为 action 对最终用户公开。

```ruby
Download depot_p/app/controllers/application.rb
# Filters added to this controller apply to all controllers in the application.
# Likewise, all the methods added will be available for all controllers.

class ApplicationController < ActionController::Base
  before_filter :authorize, :except => :login
  helper :all # include all helpers, all the time

  # See ActionController::RequestForgeryProtection for details
  # Uncomment the :secret if you're not using the cookie session store
  protect_from_forgery :secret => '8fc080370e56e929a2d5afca5540a0f7'

  # See ActionController::Base for details
  # Uncomment this to filter the contents of submitted sensitive data parameters
  # from your application log (in this case, all fields with names like "password").
  # filter_parameter_logging :password

  protected
    def authorize
      unless User.find_by_id(session[:user_id])
        flash[:notice] = "Please log in"
        redirect_to :controller => 'admin', :action => 'login'
      end
    end
end
```

此授权方法可以通过添加一行代码在我们管理控制器的任何 action 之前被调用。请注意，我们对所有控制器中的所有方法都这样做，除了名为 login 的方法，应该只有一个，即 Admin 控制器中的方法。

请注意，这走得太远了。我们刚刚将对商店本身的访问限制为管理员。这不好。

我们可以回去更改设置，以便仅标记需要授权的方法。这种方法称为黑名单，容易出现遗漏错误。更好的方法是“白名单”或列出不需要授权的方法或控制器，就像我们对 login 方法所做的那样。我们只需在 StoreController 类中为 authorize 方法提供一个覆盖即可：

```ruby
Download depot_q/app/controllers/store_controller.rb

class StoreController < ApplicationController
  #...
  protected

  def authorize
  end
end
```

##### A Friendlier Login System

按现在的代码，如果管理员在登录前尝试访问受限页面，他们将被带到登录页面。当他们登录后，标准状态页面将被显示——他们的原始请求将被遗忘。如果你愿意，可以更改应用程序，以便他们在登录后被转发到他们最初请求的页面。

首先，在 authorize 方法中，如果需要登录用户，请在 session 中记住传入请求的 URI：

```ruby
def authorize
  unless User.find_by_id(session[:user_id])
    session[:original_uri] = request.request_uri
    flash[:notice] = "Please log in"
    redirect_to(:controller => "admin", :action => "login")
  end
end
```

一旦我们登录某人，我们就可以检查 session 中是否存储了 URI，如果有则重定向到它。我们还需要在使用后清除该存储的 URI。

```ruby
def login
  session[:user_id] = nil
  if request.post?
    user = User.authenticate(params[:name], params[:password])
    if user
      session[:user_id] = user.id
      uri = session[:original_uri]
      session[:original_uri] = nil
      redirect_to(uri || { :action => "index" })
    else
      flash.now[:notice] = "Invalid user/password combination"
    end
  end
end
```





如果你跟着操作，请删除你的会话信息（因为在其中我们已经登录了）：

```
depot> rake db:sessions:clear
```

导航到 http://localhost:3000/products/。过滤方法在前往产品列表的路上拦截了我们，并改为向我们显示登录屏幕。

我们向客户展示，并得到了一个大大的微笑和一个请求：我们能否添加一个侧边栏，并在其中放置指向用户和产品管理功能的链接？而且顺便说一下，我们能否添加列出和删除管理员用户的功能？当然可以！

#### 11.4 迭代 F4：添加侧边栏，更多的管理功能

让我们从侧边栏开始。我们从 store 控制器那里得知，我们需要使用一个布局。为什么要重复自己呢？如果我们能让过滤器成为应用范围的，我们也应该能对布局做同样的事情。事实证明我们确实可以。我们再次编辑 app/controllers/application.rb，这次添加了对 layout 的调用：

```
Download depot_q/app/controllers/application.rb
class ApplicationController < ActionController::Base
  layout "store"
  #...
```

现在如果我们访问 http://localhost:3000/admin，我们会看到一个错误，视图试图显示购物车。我们需要做的是防止隐藏的 cart <div> 在根本没有购物车的功能中出现。同时，我们可以在布局的侧边栏中添加指向各种管理功能的链接，并在 session 中存在 :user_id 时才显示它们：

```
Download depot_q/app/views/layouts/store.html.erb
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html>
<head>
<title>Pragprog Books Online Store</title>
<%= stylesheet_link_tag "depot", :media => "all" %>
<%= javascript_include_tag :defaults %>
</head>
<body id="store">
<div id="banner">
<%= image_tag("logo.png") %>
<%= @page_title || "Pragmatic Bookshelf" %>
</div>
<div id="columns">
<div id="side">
<% if @cart %>
```
```
<% hidden_div_if(@cart.items.empty?, :id => "cart") do %>
  <%= render(:partial => "cart", :object => @cart) %>
<% end %>
<% end %>

<a href="http://www....">Home</a><br />
<a href="http://www..../faq">Questions</a><br />
<a href="http://www..../news">News</a><br />
<a href="http://www..../contact">Contact</a><br />

<% if session[:user_id] %>
<br />
<%= link_to 'Orders', :controller => 'orders' %><br />
<%= link_to 'Products', :controller => 'products' %><br />
<%= link_to 'Users', :controller => 'users' %><br />
<br />
<%= link_to 'Logout', :controller => 'admin', :action => 'logout' %>
<% end %>
</div>
<div id="main">
  <% if flash[:notice] -%>
<div id="notice"><%= flash[:notice] %></div>
  <% end -%>

  <%= yield :layout %>
</div>
</div>
</body>
</html>
```

现在如果我们返回到 http://localhost:3000/admin，我们会看到熟悉的 Pragmatic Bookshelf 横幅和侧边栏。但如果我们访问 http://localhost:3000/users，我们就看不到。事实证明我们还需要做一件事：我们需要阻止生成的脚手架覆盖应用默认布局。这很容易。我们只需删除生成的布局即可：

```
rm app/views/layouts/products.html.erb
rm app/views/layouts/users.html.erb
rm app/views/layouts/orders.html.erb
```

##### 最后一个管理员离开时...

现在一切都开始成形了。我们可以登录，通过侧边栏上的链接查看用户列表。

让我们试试看。我们打开看起来像图 11.2 的用户列表屏幕，然后点击 dave 旁边的 destroy 链接来删除该用户。果然，我们的用户被移除了。但令我们惊讶的是，随后我们被呈现了登录屏幕。我们刚刚从系统中删除了唯一的管理员用户。当下一个请求进来时，身份验证失败，因此应用程序拒绝让我们进入。我们必须再次登录

> 4. Windows 用户应使用 erase 命令代替。

![](img/a160fc3a330a0b3b2a764d41d614e688_175_0.png)

图 11.2：列出我们的用户

在使用任何管理功能之前。但现在我们有一个尴尬的问题：数据库中没有管理员用户，所以我们无法登录。

幸运的是，我们可以从命令行快速向数据库添加一个用户。如果你调用命令 script/console，Rails 会调用 Ruby 的 irb 实用程序，但它是在你的 Rails 应用程序的上下文中进行的。这意味着你可以通过输入 Ruby 语句并查看它们返回的值来与应用程序的代码进行交互。我们可以利用这一点直接调用我们的用户模型，让它为我们向数据库中添加一个用户：

```
depot> ruby script/console
Loading development environment.
>> User.create(:name => 'dave', :password => 'secret',
    :password_confirmation => 'secret')
=> #<User:0x2933060 @attributes={...} ...>
>> User.count
=> 1
```

>> 序列是提示符。在第一个之后，我们调用 User 类来创建一个新用户，在第二个之后，我们再次调用它以显示我们确实在数据库中有单个用户。在我们输入的每个命令之后，script/console 会显示代码返回的值（在第一种情况下，它是模型对象，在第二种情况下，它是计数）。

恐慌结束。我们现在可以重新登录到应用程序。但我们如何才能阻止这种情况再次发生呢？有几种方法。例如，我们可以编写代码来防止你删除自己的用户。这并不完全有效——理论上，A 可能在 B 删除 A 的同时删除 B。相反，让我们尝试另一种方法。我们将在数据库事务中删除用户。如果在删除用户后数据库中没有剩余用户，我们将

回滚事务，恢复我们刚刚删除的用户。

为此，我们将使用一个 Active Record 钩子方法。我们已经见过其中一个：validate 钩子由 Active Record 调用以验证对象的状态。事实证明 Active Record 定义了二十多个钩子方法，每个方法都在对象生命周期的特定点被调用。我们将使用 after_destroy 钩子，它在 SQL 删除执行后被调用。如果存在名为此的方法并且它是公开可见的，它会方便地在与删除相同的事务中被调用，因此如果它引发异常，事务将被回滚。钩子方法如下所示：

```
Download depot_q/app/models/user.rb
def after_destroy
  if User.count.zero?
    raise "Can't delete last user"
  end
end
```

这里的关键概念是使用异常来指示删除用户时的错误。此异常有两个目的。首先，因为它是在事务内部引发的，所以它会导致自动回滚。通过在用户表为空后删除时引发异常，我们撤销删除并恢复最后一个用户。

其次，异常将错误信号传回控制器，我们在其中使用 begin/end 块来处理它并在 flash 中向用户报告错误。如果你只想中止事务但不以其他方式发出异常，请引发 ActiveRecord::Rollback 异常，因为这是 ActiveRecord::Base.transaction 不会传递的唯一异常。

```
Download depot_q/app/controllers/users_controller.rb
def destroy
  @user = User.find(params[:id])
  begin
    flash[:notice] = "User #{@user.name} deleted"
    @user.destroy
  rescue Exception => e
    flash[:notice] = e.message
  end

  respond_to do |format|
    format.html { redirect_to(users_url) }
    format.xml  { head :ok }
  end
end
```

事实上，这段代码仍然存在潜在的时序问题——如果两个管理员的时机恰好合适，他们仍可能各自删除最后两个用户。修复这个问题需要比我们在这里所能容纳的更多的数据库技巧。

##### 注销

我们的管理布局在侧边栏菜单中有一个注销选项。admin 控制器中对其的实现非常简单：

```
Download depot_q/app/controllers/admin_controller.rb

def logout
  session[:user_id] = nil
  flash[:notice] = "Logged out"
  redirect_to(:action => "login")
end
```

我们最后一次把客户叫过来，她玩弄着商店应用程序。她尝试了我们新的管理功能并检查了买家体验。她尝试输入错误的数据。应用程序表现得非常出色。她微笑了，我们几乎完成了。

我们已经完成了功能的添加，但在离开之前，我们最后再浏览一下代码。我们注意到 store 控制器中有一点丑陋的重复。除了 empty_cart 之外的每个 action 都必须在 session 数据中查找用户的购物车。以下行：

```
@cart = find_cart
```

在控制器中到处出现。现在我们知道了过滤器，我们可以修复这个问题。我们将更改 find_cart 方法，使其直接将结果存储到 @cart 实例变量中：

```
Download depot_q/app/controllers/store_controller.rb

def find_cart
  @cart = (session[:cart] || Cart.new)
end
```

我们将然后使用一个 before 过滤器在除了 empty_cart 之外的每个 action 上调用此方法：

```
Download depot_q/app/controllers/store_controller.rb

before_filter :find_cart, :except => :empty_cart
```

这让我们可以在 action 方法中删除对 @cart 的其余赋值。最终的列表从第 694 页开始显示。

#### 我们刚刚做了什么

到本迭代结束时，我们已完成以下工作：

- 我们创建了一个用户模型和数据库表，并验证了属性。它使用加盐哈希将密码存储在数据库中。我们创建了一个代表明文密码的虚拟属性，并对其进行了编码，以便在明文版本更新时创建哈希版本。





- 我们手动创建了一个控制器来处理登录和注销，并实现了一个单动作的登录方法，该方法根据使用 HTTP GET 还是 POST 调用而采用不同的路径。我们使用了 `form_for` 辅助方法来渲染表单。
- 我们创建了一个登录动作。该动作使用了不同风格的表单——一个没有对应模型的表单。我们看到了参数如何在视图和控制器之间传递。
- 我们在 `app/controllers` 目录下的 `application.rb` 文件中的 `ApplicationController` 类中创建了一个应用范围的控制器辅助方法。
- 我们使用 before 过滤器来调用 `authorize` 方法，从而控制对管理功能的访问。
- 我们看到了如何使用 `script/console` 直接与模型交互（在我们删除了最后一个用户后帮助我们摆脱困境）。
- 我们将布局统一为单一的应用范围布局。
- 我们看到了事务如何帮助防止删除最后一个用户。
- 我们使用了另一个过滤器来为控制器动作设置一个共同的环境。

#### Playtime

这里有一些你可以自己尝试的内容：

- 修改用户更新函数，使其接受确认密码而不是哈希密码和盐。
- 将上一章中的结账代码改编为使用单个动作，而不是两个。
- 当系统在新机器上首次安装时，数据库中没有定义管理员，因此没有管理员可以登录。但是，如果没有管理员可以登录，那么就没人能创建管理员用户。更改代码，以便如果数据库中未定义管理员，则任何用户名都可用于登录（让你可以快速创建真正的管理员）。⁵
- 尝试使用 `script/console`。尝试创建产品、订单和订单项。注意保存模型对象时的返回值——当验证失败时，你会看到返回 `false`。通过检查错误来找出原因：

  ```
  >> prd = Product.new
  => #<Product id: nil, title: nil, description: nil, image_url: nil, created_at: nil, updated_at: nil, price: #<BigDecimal:246aa1c,'0.0',4(8)>>
  >> prd.save
  => false
  >> prd.errors.full_messages
  => ["Image url must be a URL for a GIF, JPG, or PNG image",
      "Image url can't be blank", "Price should be at least 0.01",
      "Title can't be blank", "Description can't be blank"]
  ```

5. 稍后，在第 17.4 节《数据迁移》，第 304 页，我们将讨论作为迁移的一部分填充数据库表的方法。

(你可以在 http://pragprog.wikidot.com/rails-play-time 找到提示。)

在本章中，我们将看到

- 使用“has_many :through”连接表，
- 创建 REST 接口，
- 使用 builder 模板生成 XML，
- 使用模型对象的 `to_xml` 生成 XML，
- 使用模型对象的 `atom_helper` 生成 Atom，
- 使用模型对象的 `to_json` 生成 JSON，
- 处理不同内容类型的请求，
- 创建应用程序文档，以及
- 获取我们应用程序的统计信息。

### Chapter 12

### Task G: One Last Wafer-Thin Change

在我们完成最初几次迭代后的几天里，我们为购物系统添加了履行功能并将其推出。它取得了巨大的成功，在随后的几个月中，Depot 应用程序成为业务的核心——事实上，营销人员也对它产生了兴趣。他们希望向购买了特定书籍的人发送群发邮件，告知他们有新书可用。他们已经有了垃圾^H^H^H^H邮件¹系统；它只需要包含客户姓名和电子邮件地址的 XML 订阅源。

#### 12.1 Generating the XML Feed

让我们为我们的应用程序设置一个 REST 风格的接口。REST 代表 REpresentational State Transfer，这基本上意味着避免共享状态并专注于交换资源的表示。在 HTTP 的上下文中，它建议你使用一组统一的方法（GET、POST、DELETE 等）来在应用程序之间发送请求。在我们的例子中，我们将让营销系统向我们发送一个 HTTP GET 请求，要求提供购买了特定产品的客户的详细信息。我们的应用程序将使用 XML 文档进行响应。² 我们与营销部门的 IT 人员交谈，他们同意一个简单的请求 URL 格式：

```
http://mystore.com/info/who_bought/<product id>
```

因此，我们需要解决两个问题。我们需要能够找到购买了特定产品的客户，并且我们需要从该列表生成 XML 订阅源。让我们先从生成列表开始。

> 1. 很久以前，Ctrl-H 用于表示退格。有关更多详细信息，请参阅 http://en.wikipedia.org/wiki/Backspace。
> 2. 我们本可以使用 Web 服务来实现此传输——Rails 有一个插件可添加作为 SOAP 和 XML-RPC 客户端和服务器的支持。然而，在这种情况下，这似乎有点过头了。

##### Creating a REST Interface

考虑到这可能不是营销人员提出的最后一个请求，我们创建一个新的控制器来处理信息请求：

```
depot> ruby script/generate controller info who_bought
exists  app/controllers/
exists  app/helpers/
create  app/views/info
exists  test/functional/
create  app/controllers/info_controller.rb
create  test/functional/info_controller_test.rb
create  app/helpers/info_helper.rb
create  app/views/info/who_bought.html.erb
```

我们将向 info 控制器添加 who_bought 动作。它只是根据产品 id 加载订单列表：

```
Download depot_q/app/controllers/info_controller.rb

class InfoController < ApplicationController
  def who_bought
    @product = Product.find(params[:id])
    @orders  = @product.orders
    respond_to do |format|
      format.xml { render :layout => false }
    end
  end
end

protected

  def authorize
  end
end
```

现在我们需要实现返回 XML 给调用者的模板。我们可以使用我们一直用来渲染网页的 ERb 模板来做到这一点，但有几种更好的方法。第一种使用 builder 模板，旨在使创建 XML 文档变得容易。让我们看看我们在 `app/views/info` 目录中创建的模板 `who_bought.xml.builder`：

```
Download depot_q/app/views/info/who_bought.xml.builder

xml.order_list(:for_product => @product.title) do
  for o in @orders
    xml.order do
      xml.name(o.name)
      xml.email(o.email)
    end
  end
end
```

![](img/a160fc3a330a0b3b2a764d41d614e688_183_0.png)

Figure 12.2: XML returned by the who_bought action

信不信由你，这只是 Ruby 代码。它使用 Jim Weirich 的 Builder 库，该库在执行程序时作为副作用生成一个格式良好的 XML 文档。

在 builder 模板中，变量 xml 表示正在构建的 XML 对象。当我们在该对象上调用方法时（例如我们在模板第一行对 `order_list` 的调用），builder 会发出相应的 XML 标签。如果将哈希传递给其中一个方法，则它用于构造 XML 标签的属性。如果我们传递一个字符串，则它用作标签的值。

如果要嵌套标签，请向外部 builder 方法调用传递一个块。块内创建的 XML 元素将嵌套在外部元素内。我们在示例中使用它将 `<order>` 标签列表嵌入到 `<order_list>` 中，然后将 `<name>` 标签和 `<email>` 标签嵌入到每个 `<order>` 中。

我们可以使用浏览器或从命令行测试此方法。如果将 URL 输入浏览器，XML 将被返回。显示方式取决于浏览器：在 Mac 上，Safari 会渲染文本并忽略标签，而 Firefox 会显示 XML 的漂亮高亮表示（如下图 12.2 所示）。在所有浏览器中，View → Source 选项应显示从我们的应用程序发送的确切内容。

我们也可以使用 `curl` 或 `wget` 等工具从命令行查询你的应用程序。

```
depot> curl http://localhost:3000/info/who_bought/3
<order_list for_product="Pragmatic Version Control">
  <order>
    <name>Dave Thomas</name>
    <email>customer@pragprog.com</email>
  </order>
  <order>
    <name>F &amp; W Flintstone</name>
    <email>rock_crusher@bedrock.com</email>
  </order>
</order_list>
```

事实上，这引出了一个有趣的问题：我们能否安排我们的动作，使从浏览器访问它时看到一个漂亮格式化的列表，而 REST 请求则返回 XML？

##### Responding Appropriately

请求通过 HTTP 进入 Rails 应用程序。HTTP 消息由一些头部和（可选）一些数据（例如表单的 POST 数据）组成。其中一个头部是 Accept，客户端使用它来告诉服务器可能返回的内容类型。例如，浏览器可能会发送包含以下头部的 HTTP 请求：

```
Accept:  text/html, text/plain, application/xml
```

理论上，服务器应仅返回与这三种类型之一匹配的内容。

我们可以使用它来编写根据 Accept 头部进行条件处理的动作。例如，我们可以编写一个 who_bought 动作，使用 Accept 头部。如果客户端只接受 XML，则我们可以返回 XML 格式的 REST 响应。如果客户端接受 HTML，则我们可以改为渲染 HTML 页面。

在 Rails 中，我们使用 `respond_to` 方法根据 Accept 头部执行条件处理。首先，让我们为 HTML 视图编写一个简单的模板：

```
Download depot_r/app/views/info/who_bought.html.erb
<h3>People Who Bought <%= @product.title %></h3>
<ul>
  <% for order in @orders -%>
    <li>
      <%= mail_to order.email, order.name %>
    </li>
  <% end -%>
</ul>
```



现在我们将使用 respond_to 根据传入请求的 Accept 头来向量到正确的模板：

```
Download depot_r/app/controllers/info_controller.rb
def who_bought
  @product = Product.find(params[:id])
  @orders  = @product.orders
  respond_to do |format|
    format.html
    format.xml { render :layout => false }
  end
end
```

在 respond_to 块内部，我们列出我们接受的内容类型。你可以把它想成有点像 case 语句，但它有一个很大的不同：它忽略我们列出选项的顺序，而是使用传入请求的顺序（因为客户端有权说它偏好的格式是什么）。

这里我们为每种内容类型使用默认操作。对于 html，该操作是调用 render。对于 xml，操作是渲染 builder 模板。净效果是客户端可以从同一个 action 中选择接收 HTML 或 XML。

不幸的是，这很难用浏览器来尝试。相反，让我们使用命令行客户端。这里我们使用 curl（但工具如 wget 同样适用）。curl 的 -H 选项让我们可以指定请求头。让我们先请求 XML：

```
depot> curl -H "Accept: application/xml" \
        http://localhost:3000/info/who_bought/3
<order_list for_product="Pragmatic Version Control">
  <order>
    <name>Dave Thomas</name>
    <email>customer@pragprog.com</email>
  </order>
  <order>
    <name>F &amp; W Flintstone</name>
    <email>crusher@bedrock.com</email>
  </order>
</order_list>
```

然后是 HTML：

```
depot> curl -H "Accept: text/html" \
        http://localhost:3000/info/who_bought/3
<h3>People Who Bought Pragmatic Project Automation</h3>
<ul>
  <li>
    <a href="mailto:customer@pragprog.com">Dave Thomas</a>
  </li>
  <li>
    <a href="mailto:crusher@bedrock.com">F & W Flintstone</a>
  </li>
</ul>
```

##### 另一种请求 XML 的方式

虽然使用 Accept 头是指定你想要接收的内容类型的“官方” HTTP 方式，但并非总能从客户端设置此头。Rails 提供了另一种选择：我们可以将首选格式作为 URL 的一部分设置。如果我们希望对 who_bought 请求的响应以 HTML 返回，我们可以请求 /info/who_bought/1.html。如果我们想要 XML，我们可以使用 /info/who_bought/1.xml。而且这可以扩展到任何内容类型（只要我们在 respond_to 块中编写适当的处理器）。如果你需要使用默认不支持的 MIME 类型，你可以在 environment.rb 中按如下方式注册自己的处理器：

```
Mime::Type.register "image/jpg", :jpg
```

此行为已由 Rails 提供的默认路由配置启用。我们将在第 457 页解释为什么这样工作——现在，只需相信它。在 config 目录中打开 routes.rb，并查找以下行：

```
map.connect ':controller/:action/:id.:format'
```

此默认路由说 URL 可能以文件扩展名结尾（.html、.xml 等）。如果是这样，该扩展名将被存储在变量 format 中。而 Rails 使用该变量来伪造请求的内容类型。

尝试请求 URL http://localhost:3000/info/who_bought/3.xml。根据你的浏览器，你可能会看到格式良好的 XML 显示，也可能会看到空白页。如果看到后者，请使用浏览器的 查看 → 源 代码 功能来查看响应。

##### 自动生成 XML

在之前的示例中，我们通过使用 builder 模板手工生成 XML 响应。这给了我们控制返回元素顺序的能力。但如果该顺序不重要，我们可以让 Rails 为我们生成模型对象的 XML，只需调用模型的 to_xml 方法即可。在下面的代码中，我们重写了 XML 请求的默认行为以使用它：

```
def who_bought
  @product = Product.find(params[:id])
  @orders  = @product.orders
  respond_to do |format|
    format.html
    format.xml { render :layout => false ,
                :xml => @product.to_xml(:include => :orders) }
  end
end
```

render 的 :xml 选项告诉它将响应内容类型设置为 application/xml。然后 to_xml 调用的结果被发送回客户端。

在这种情况下，我们转储 @product 变量以及引用该产品的任何订单：

```
depots> curl --silent http://localhost:3000/info/who_bought/3.xml
<?xml version="1.0" encoding="UTF-8"?>
<product>
  <created-at type="datetime">2008-09-09T01:56:58Z</created-at>
  <description>&lt;p&gt;
    This book is a recipe-based approach to using Subversion that will
    get you up and running quickly---and correctly. All projects need
    version control: it's a foundational piece of any project's
    infrastructure. Yet half of all project teams in the U.S. don't use
    any version control at all. Many others don't use it well, and end
    up experiencing time-consuming problems.
  &lt;/p&gt;</description>
  <id type="integer">3</id>
  <image-url>/images/svn.jpg</image-url>
  <price type="decimal">28.5</price>
  <title>Pragmatic Version Control</title>
  <updated-at type="datetime">2008-09-09T01:56:58Z</updated-at>
  <orders type="array">
    <order>
      <address>123 Main St</address>
      <created-at type="datetime">2008-09-09T01:58:07Z</created-at>
      <email>customer@pragprog.com</email>
      <id type="integer">1</id>
      <name>Dave Thomas</name>
      <pay-type>check</pay-type>
      <updated-at type="datetime">2008-09-09T01:58:07Z</updated-at>
    </order>
  </orders>
</product>
```

请注意，默认情况下 to_xml 会转储所有内容。你可以告诉它排除某些属性，但这很快就会变得混乱。如果你必须生成符合特定 schema 或 DTD 的 XML，你最好坚持使用 builder 模板。

##### Atom Feed

如果想要创建自定义客户端，自定义 XML 是可以的。但使用标准 Feed 格式，如 Atom，意味着你可以立即利用各种现有的客户端。因为 Rails 已经知道 id、日期和链接，所以它可以让你不必担心这些烦人的细节，而专注于生成可读性强的摘要：

```
def who_bought
  @product = Product.find(params[:id])
  @orders  = @product.orders
  respond_to do |format|
    format.html
    format.atom { render :layout => false }
  end
end
```

然后我们提供一个模板，该模板不仅利用 Builder 提供的通用 XML 功能，还利用 atom_feed 助手提供的对 Atom Feed 格式的了解：

```
Download depot_r/app/views/info/who_bought.atom.builder
atom_feed do |feed|
  feed.title "Who bought #{@product.title}"
  feed.updated @orders.first.created_at

  for order in @orders
    feed.entry(order) do |entry|
      entry.title "Order #{order.id}"
      entry.summary :type => 'xhtml' do |xhtml|
        xhtml.p "Shipped to #{order.address}"

        xhtml.table do
          xhtml.tr do
            xhtml.th 'Product'
            xhtml.th 'Quantity'
            xhtml.th 'Total Price'
          end
          for item in order.line_items
            xhtml.tr do
              xhtml.td item.product.title
              xhtml.td item.quantity
              xhtml.td number_to_currency item.total_price
            end
          end
          xhtml.tr do
            xhtml.th 'total', :colspan => 2
            xhtml.th number_to_currency \
              order.line_items.map(&:total_price).sum
          end
        end

        xhtml.p "Paid by #{order.pay_type}"
      end
      entry.author do |author|
        entry.name order.name
        entry.email order.email
      end
    end
  end
end
```

我们可以自己试试：

```
depot> curl --silent http://localhost:3000/info/who_bought/3.atom
<?xml version="1.0" encoding="UTF-8"?>
<feed xml:lang="en-US" xmlns="http://www.w3.org/2005/Atom">
  <id>tag:localhost,2005:/info/who_bought/3</id>
  <link type="text/html" href="http://localhost:3000" rel="alternate"/>
  <link type="application/atom+xml"
    href="http://localhost:3000/info/who_bought/3.atom" rel="self"/>



```
<title>Who bought Pragmatic Version Control</title>
<updated>2008-09-09T20:19:23Z</updated>
<entry>
  <id>tag:localhost,2005:Order/1</id>
  <published>2008-09-09T20:19:23Z</published>
  <updated>2008-09-09T20:19:23Z</updated>
  <link type="text/html" href="http://localhost:3000/orders/1" rel="alternate"/>
  <title>Order 1</title>
  <summary type="xhtml">
    <div xmlns="http://www.w3.org/1999/xhtml">
      <p>1 line item</p>
      <p>Shipped to 123 Main St</p>
      <p>Paid by check</p>
    </div>
  </summary>
  <author>
    <name>Dave Thomas</name>
    <email>customer@pragprog.com</email>
  </author>
</entry>
</feed>
```

看起来不错。现在我们可以用自己的阅读器订阅它了。

##### JSON 也一样！

对于那些更喜欢花括号的人来说，Rails 同样可以轻松地自动生成 JavaScript Object Notation（JSON）：

```
def who_bought
  @product = Product.find(params[:id])
  @orders = @product.orders
  respond_to do |format|
    format.html
    format.json { render :layout => false ,
                  :json => @product.to_json(:include => :orders) }
  end
end
```

```
depot> curl -H "Accept: application/json" \
         http://localhost:3000/info/who_bought/3
{"product": {"price": 28.5, "created_at": "2008-09-09T02:22:29Z",
"title": "Pragmatic Version Control", "image_url": "/images/svn.jpg",
"updated_at": "2008-09-09T02:22:29Z", "id": 3, "orders": [{"name":
"Dave Thomas", "address": "123 Main St", "created_at":
"2008-09-09T02:23:39Z", "updated_at": "2008-09-09T02:23:39Z",
"pay_type": "check", "id": 1, "email": "customer@pragprog.com"}],
"description": "<p>\n      This book is a recipe-based approach to
using Subversion that will \n          get you up and running
quickly---and correctly. All projects need\n          version control:
it's a foundational piece of any project's \n          infrastructure.
Yet half of all project teams in the U.S. don't use\n          any
version control at all. Many others don't use it well, and end \nup experiencing time-consuming problems.\n      </p>"}}
```

在本章中，我们将看到

- 模板的本地化，以及
- I18n 的数据库设计注意事项。

### 第 13 章

### 任务 I：国际化

现在，我们已经有了一个基本的购物车在运行，客户开始询问除英语以外的其他语言，她说公司正在大力推进新兴市场的扩张。除非我们能用客户理解的语言展示内容，否则客户就会白白错过赚钱的机会。我们不能让这种情况发生。

第一个问题是，我们谁都不是专业翻译。客户向我们保证，这部分工作不需要我们操心，因为会外包出去。我们只需要关心如何启用翻译。此外，我们还暂时不用担心管理页面，因为所有管理员都讲英语。我们需要关注的是商店界面。

这让我们松了一口气，于是凭着一点高中西班牙语的记忆，我们开始动手。

#### 13.1 迭代 I1：启用翻译

我们先创建一个新的配置文件，其中封装了我们关于哪些区域设置可用、它们存放在何处以及什么作为默认值的信息。

```
Download depot_s/config/initializers/i18n.rb

I18n.default_locale = 'en'

LOCALES_DIRECTORY = "#{RAILS_ROOT}/config/locales/"

LANGUAGES = {
  'English' => 'en',
  "Espa\xc3\xb1ol" => 'es'
}
```

现在让我们来看看这段代码。

我们使用 I18n 模块做的第一件事是设置默认区域设置。Rails 在 2.2 版本中引入了 I18n 模块。这个名字有点滑稽，但总比每次都输入 internationalization 要好得多。毕竟 Internationalization 以 i 开头，以 n 结尾，中间有 18 个字母。

接下来，我们设置一个常量，该常量包含区域设置所在目录的名称。我们利用已有的 RAILS_ROOT 常量来确保这个目录名与代码保持一致。

最后一个常量是一个从显示名称到区域名称的哈希。不幸的是，我们现在只有美式键盘，而 español 中有一个字符无法直接通过键盘输入。不同的操作系统有不同的处理方式，通常最简单的做法是从网站上直接复制粘贴正确的文本。如果你这样做，只要确保你的编辑器配置为 UTF-8 即可。同时，我们选择使用两个字节的十六进制值来表示西班牙语中“带波浪线的 n”字符。

为了让 Rails 识别这个配置更改，需要重启服务器。

现在我们需要使用这个列表。我们注意到布局右上角有一些未使用的区域，于是在 image_tag 之前添加了一个表单：

```
Download depot_s/app/views/layouts/store.html.erb

<% form_tag '', :method => 'GET', :class => 'locale' do %>
  <%= select_tag 'locale', options_for_select(LANGUAGES, I18n.locale),
    :onchange => 'this.form.submit()' %>
  <%= submit_tag 'submit' %>
  <%= javascript_tag "$$('.locale input').each(Element.hide)" %>
<% end %>
```

form_tag 指定了一个空白 URI，因此提交此表单时，浏览器会重新请求当前页面。很巧妙，对吧？我们使用 GET 方法，因为没有状态需要传递。class 属性让我们可以将表单与某些 CSS 关联起来。

select_tag 用于定义该表单的一个输入字段，即 locale。它是一个基于配置文件中设置的 LANGUAGES 哈希的选项列表，默认值为当前区域设置（这也通过 I18n 模块提供）。我们还设置了一个 onchange 事件处理程序，只要值发生变化就会提交表单。这只有在启用 JavaScript 时才有效，但很方便。

然后，我们添加一个 submit_tag，用于 JavaScript 不可用的情况；还添加了一小段 JavaScript，它会隐藏 locale 表单中的每个 input 标签，尽管我们知道只有一个。

因此，我们在所有控制器的公共基类 ApplicationController 中创建了一个 before_filter：

```
Download depot_s/app/controllers/application.rb
class ApplicationController < ActionController::Base
  layout "store"
  before_filter :authorize, :except => :login
  before_filter :set_locale
  #...
protected
  def set_locale
    session[:locale] = params[:locale] if params[:locale]
    I18n.locale = session[:locale] || I18n.default_locale

    locale_path = "#{LOCALES_DIRECTORY}/#{I18n.locale}.yml"

    unless I18n.load_path.include? locale_path
      I18n.load_path << locale_path
      I18n.backend.send(:init_translations)
    end

  rescue Exception => err
    logger.error err
    flash.now[:notice] = "#{I18n.locale} translation not available"

    I18n.load_path -= [locale_path]
    I18n.locale = session[:locale] = I18n.default_locale
  end
end
```

这段代码会从 params 中获取 locale 值（如果 params 中存在该值，理应存在，但小心无大错），并设置到 session 中；然后从 session 中设置 I18n.locale，同样非常谨慎；最后，如果 locale 文件不在加载路径中，则将其添加并加载。

我们格外小心地将任何错误完整记录到日志中供管理员查看，并在失败时向用户报告一条通用消息，这样他们就不会困惑为什么自己的更改没有生效，同时从加载路径和 I18n.locale 中恢复有问题的区域设置。

现在，当我们更改值时，值仍会跳回英文，但至少我们可以在屏幕上看到一条消息，说明翻译不可用，并在日志中看到一条消息，表明文件未找到。也许看起来没什么进展，但这已经是进步了。

![](img/a160fc3a330a0b3b2a764d41d614e688_196_0.png)

但在创建这些文件之前，我们需要有内容放进这些文件。我们先从布局开始，因为它相当显眼。我们把任何需要翻译的文本替换为对 I18n.translate 的调用（它被方便地别名为 I18n.t，甚至更简单地写作 t），并为每个可翻译字符串提供一个我们自己选择的、以点分隔的唯一名称：

```
Download depot_s/app/views/layouts/store.html.erb
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html>
<head>
<title>Pragprog Books Online Store</title>
<%= stylesheet_link_tag "depot", :media => "all" %>
<%= javascript_include_tag :defaults %>
</head>
<body id="store">
<div id="banner">
<%= form_tag '', :method => 'GET', :class => 'locale' do %>
<%= select_tag 'locale', options_for_select(LANGUAGES, I18n.locale),
:onchange => 'this.form.submit()' %>
<%= submit_tag 'submit' %>
<%= javascript_tag "$$('.locale input').each(Element.hide)" %>
<% end %>
<%= image_tag("logo.png") %>
<%= @page_title || I18n.t('layout.title') %>
</div>
<div id="columns">
<div id="side">
<% if @cart %>
```




```
<% hidden_div_if(@cart.items.empty?, :id => "cart") do %>
  <%= render(:partial => "cart", :object => @cart) %>
<% end %>
<% end %>
<a href="http://www...."> <%= I18n.t 'layout.side.home' %> </a><br />
<a href="http://www..../faq"> <%= I18n.t 'layout.side.questions' %> </a><br />
<a href="http://www..../news"> <%= I18n.t 'layout.side.news' %> </a><br />
<a href="http://www..../contact"> <%= I18n.t 'layout.side.contact' %> </a><br />
<% if session[:user_id] %>
  <br />
  <%= link_to 'Orders', :controller => 'orders' %><br />
  <%= link_to 'Products', :controller => 'products' %><br />
  <%= link_to 'Users', :controller => 'users' %><br />
  <br />
  <%= link_to 'Logout', :controller => 'admin', :action => 'logout' %>
<% end %>
</div>
<div id="main">
  <% if flash[:notice] -%>
  <div id="notice"><%= flash[:notice] %></div>
  <% end -%>

  <%= yield :layout %>
</div>
</div>
</body>
</html>
```

下面是相应的 locale 文件，首先是英文版：

下载 depot_s/config/locales/en.yml

```
en:
  layout:
    title: "Pragmatic Bookshelf"
    side:
      home: "Home"
      questions: "Questions"
      news: "News"
      contact: "Contact"
```

接下来是西班牙文版：

下载 depot_s/config/locales/es.yml

```
es:
  layout:
    title: "Publicaciones de Pragmatic"
    side:
      home: "Inicio"
      questions: "Preguntas"
      news: "Noticias"
      contact: "Contacto"
```

格式是 YAML，与配置数据库时使用的格式相同。YAML 只是由缩进的名称和值组成，此处的缩进与我们创建的名称结构相匹配：

![](img/a160fc3a330a0b3b2a764d41d614e688_198_0.png)

接下来要更新的是产品索引模板：

下载 depot_s/app/views/store/index.html.erb

```
<h1><%= I18n.t 'main.title' %></h1>

<% for product in @products %>
  <div class="entry">
    <%= image_tag(product.image_url) %>
    <h3><%=h product.title %></h3>
    <%= product.description %>
    <div class="price-line">
      <span class="price"><%= number_to_currency(product.price) %></span>
      <% form_remote_tag :url => {:action => 'add_to_cart', :id => product} do %>
        <%= submit_tag I18n.t('main.button.add') %>
      <% end %>
    </div>
  </div>
<% end %>
```

下面是 locales 文件相应的更新：

```
Download depot_s/config/locales/en.yml

en:
  main:
    title: "Your Pragmatic Catalog"
    button:
      add: "Add to Cart"
```

```
Download depot_s/config/locales/es.yml

es:
  main:
    title: "Su Cat&aacute;logo de Pragmatic"
    button:
      add: "A&ntilde;adir al Carrito"
```

请注意，由于我们没有在 ERb 模板中使用 Rails 的 h 辅助函数，因此可以自由使用 HTML 实体名称来表示键盘上不存在的字符：

![](img/a160fc3a330a0b3b2a764d41d614e688_199_0.png)

感觉信心十足，我们接着来看购物车局部模板：

```
Download depot_s/app/views/store/_cart.html.erb

<div class="cart-title"><%= I18n.t 'layout.cart.title' %></div>
<table>
  <%= render(:partial => "cart_item", :collection => cart.items) %>
```

```
<tr class="total-line">
    <td colspan="2">Total</td>
    <td class="total-cell"><%= number_to_currency(cart.total_price) %></td>
</tr>

</table>
```

```
<%= button_to I18n.t('layout.cart.button.checkout'), :action => 'checkout' %>
<%= button_to I18n.t('layout.cart.button.empty'), :action => :empty_cart %>
```

下载 depot_s/config/locales/en.yml

```
en:
  cart:
    title: "Your Cart"
    button:
      empty: "Empty cart"
      checkout: "Checkout"
```

下载 depot_s/config/locales/es.yml

```
es:
  layout:
    cart:
      title: "Carrito de la Compra"
      button:
        empty: "Vaciar Carrito"
        checkout: "Comprar"
```

![](img/a160fc3a330a0b3b2a764d41d614e688_200_0.png)

此时，我们遇到了第一个问题。货币金额在 es 中显示为 49.9，而不是 $49.90。这是因为不同 locale 之间不只是语言不同，货币也不同。数字的惯用显示方式同样有所差异。

于是，我们首先与客户确认，并核实目前暂时不用担心汇率（呼！），因为这部分将由信用卡公司和/或电汇公司处理，但在西班牙语中显示结果时，我们需要在数值后面加上“USD”或“$US”字符串。

另一个差异是数字本身的显示方式。小数部分用逗号分隔，千位分隔符则用点号表示。

货币问题远比乍看起来复杂，需要做很多决定。幸运的是，Rails 知道在翻译文件中查找这些信息；我们只需提供即可：

```
Download depot_s/config/locales/es.yml

es:
  number:
    currency:
      format:
        unit: "$US"
        precision: 2
        separator: ","
        delimiter: "."
        format: "%n&nbps;%u"
```

```
Download depot_s/config/locales/en.yml

en:
  number:
    currency:
      format:
        unit: "$"
        precision: 2
        separator: "."
        delimiter: ","
        format: "%u%n"
```

我们已经为 number.currency.format 指定了单位（unit）、精度（precision）、小数点分隔符（separator）和千位分隔符（delimiter）。这些含义不言自明。format 则稍微复杂一些：%n 是数字本身的占位符；&nbsp; 是一个不换行空格字符，可防止该值被拆分成多行；%u 是货币单位的占位符。

![](img/a160fc3a330a0b3b2a764d41d614e688_202_0.png)

现在感觉已经接近尾声了。接下来是结账表单：

下载 depot_s/app/views/store/checkout.html.erb

```
<div class="depot-form">

  <%= error_messages_for 'order' %>

  <% form_for :order, :url => { :action => :save_order } do |form| %>
    <fieldset>
      <legend><%= I18n.t 'checkout.legend' %></legend>

      <div>
        <%= form.label :name, I18n.t('checkout.name') + ":" %>
        <%= form.text_field :name, :size => 40 %>
      </div>

      <div>
        <%= form.label :address, I18n.t('checkout.address') + ":" %>
        <%= form.text_area :address, :rows => 3, :cols => 40 %>
      </div>

      <div>
        <%= form.label :email, I18n.t('checkout.email') + ":" %>
        <%= form.text_field :email, :size => 40 %>
      </div>

      <div>
        <%= form.label :pay_type, I18n.t('checkout.pay_type') + ":" %>
        <%= form.select :pay_type,
            Order::PAYMENT_TYPES,
            :prompt => I18n.t('checkout.pay_prompt')
        %>
      </div>
```

```
<%= submit_tag I18n.t('checkout.submit'), :class => "submit" %>
</fieldset>
<% end %>
</div>
```

下面是 locales 文件：

下载 depot_s/config/locales/en.yml

en:

```
checkout:
  legend: "Please Enter your Details"
  name: "Name"
  address: "Address"
  email: "E-mail"
  pay_type: "Pay with"
  pay_prompt: "Select a payment method"
  submit: "Place Order"
```

下载 depot_s/config/locales/es.yml

es:

```
checkout:
  legend: "Por favor, introduzca sus datos"
  name: "Nombre"
  address: "Direcci&oacute;n"
  email: "E-mail"
  pay_type: "Pagar con"
  pay_prompt: "Seleccione un m\xC3\xA9todo de pago"
  submit: "Realizar Pedido"
```

请注意，在支付提示中我们不能使用 HTML 实体，因此必须改用十六进制。同样，专业翻译人员不会遇到这个问题，因为他们会使用适合当前任务的键盘。

![](img/a160fc3a330a0b3b2a764d41d614e688_203_0.png)

这些内容同样要写入 YAML 文件：

下载 depot_s/config/locales/es.yml

```
es:
  activerecord:
    models:
      order: "pedido"
    attributes:
      order:
        address: "Direcci&oacute;n"
        name: "Nombre"
        email: "E-mail"
        pay_type: "Forma de pago"
```

![](img/a160fc3a330a0b3b2a764d41d614e688_205_0.png)

现在我们提交订单，会收到一条“感谢您的订单”消息。

我们需要更新 flash 消息：

下载 depot_s/app/controllers/store_controller.rb

```
def save_order
  @order = Order.new(params[:order])
  @order.add_line_items_from_cart(@cart)
  if @order.save
    session[:cart] = nil
    redirect_to_index(I18n.t('flash.thanks'))
  else
    render :action => 'checkout'
  end
end
```

下载 depot_s/config/locales/en.yml

```
en:
  flash:
    thanks: "Thank you for your order"
```





一个单独的产品会 `has_many :summaries`，而一个单独的摘要会 `belongs_to :product`。

为了封装这一知识，产品模型可以为这两个字段提供虚拟访问器，根据当前语言环境选择并缓存正确的标题和描述。这种关注点分离将使实现能够随着新需求的出现而演进。

准备就绪后，我们挽起袖子。但在开始之前，客户路过。我们兴奋地告诉她我们即将做的事情，她起初礼貌地倾听，但在我们说完后，她告诉我们我们全都错了。

本例中销售的产品是书籍。与锤子和图钉不同，不仅仅是标签使用特定语言。一本英文书的每一页都是英文。将书翻译成法语或韩语会得到一本不同的书——一本页数不同、ISBN 号码不同，甚至价格可能也不同的书。

于是，我们思考了一秒钟，然后眼睛一亮，因为这要简单得多。我们所需要做的就是在现有的产品表中添加一个语言环境列（我们已经知道如何添加列），并更改 `find_products_for_sale` 方法，使其只返回与客户语言环境匹配的项目。

```
find(:all, :order => "title", :conditions => {:locale => I18n.locale})
```

#### 我们刚刚做了什么

到本迭代结束时，我们已完成以下工作：

- 我们为应用程序设置了默认语言环境。
- 我们提供了一个输入选择字段，使用户能够选择其他语言环境。
- 我们修改了布局和视图，以便调用 I18n 模块来翻译界面文本部分。
- 我们为这些文本字段创建了翻译文件。
- 我们对货币金额的显示进行了本地化。
- 我们还对 ActiveRecord 错误以及模型和属性名称进行了本地化。

#### 练习时间

这里有一些你可以自己尝试的内容：

- 将语言环境添加到 products 列，并调整索引视图以仅选择与语言环境匹配的产品。调整 products 视图，以便可以查看、输入和更改此新列。在每个语言环境中输入几件产品，并测试 resulting 应用程序。
- 确定美元与欧元之间的当前汇率，并在选择 `es_es` 时将货币显示本地化为欧元。

（你会在 http://pragprog.wikidot.com/rails-play-time. 上找到提示。）

本章由 Mike Clark（http://clarkware.com）撰写。Mike 是一名独立顾问、作者和培训师。最重要的是，他是一名程序员。他帮助团队使用敏捷实践更快地构建更好的软件。凭借在 J2EE 和测试驱动开发方面的丰富背景，他目前正将自己的经验应用于 Rails 项目。

### 第 14 章

### 任务 T：测试

在短时间内，我们开发了一个体面的基于 Web 的购物车应用程序。一路上，我们通过编写少量代码，然后在 Web 浏览器中按按钮（客户在我们身边）来查看应用程序是否按预期运行，从而获得了快速反馈。这种测试策略在开发 Rails 应用程序的前大约一小时内有效，但此后不久，你积累了足够多的功能，手动测试就不再可扩展。每次你必须按所有按钮时，你的手指都会感到疲倦，你的思维也会变得麻木，因此你很少甚至从不进行测试。

然后有一天，你做了一个小的更改，它破坏了一些功能，但你直到客户打电话给你说她不再满意时才意识到。如果这还不够糟糕，弄清楚到底出了什么问题需要你花费数小时。你在这里做了一个无辜的更改，但它在那里破坏了东西。到你解开谜团时，客户已经找到了新的最佳程序员。

不必如此。摆脱这种疯狂有一个实用的替代方案：编写测试！

在本章中，我们将为我们所熟知和喜爱的应用程序——Depot 应用程序编写自动化测试。¹ 理想情况下，我们会增量地编写这些测试，以便在途中获得小小的信心提升。因此，我们称之为任务 T，因为我们应该始终进行测试。你将在第 713 页开始找到本章的代码列表。

> 1. 我们将测试的是原版的 Depot。如果您已进行修改（也许是通过尝试各章末尾的练习时间练习），您可能需要进行调整。

#### 14.1 测试内置于其中

在构建 Depot 时我们所做的快速松散编码，很容易让人认为 Rails 将测试视为事后想法。事实远非如此。Rails 框架的真正乐趣之一是它从每个项目的开始就内置了测试支持。事实上，从你使用 rails 命令创建新应用程序的那一刻起，Rails 就开始为你生成测试基础设施。

我们还没有为 Depot 应用程序编写过一行测试代码，但如果你查看该项目的顶级目录，你会注意到一个名为 test 的子目录。在此目录中，你会看到四个目录和一个 helper 文件：

```
depot> ls -p test
fixtures/      functional/      integration/      test_helper.rb   unit/
```

因此，我们的第一个决定——在哪里放置测试——已经为我们做出了。rails 命令创建了完整的测试目录结构。

按照惯例，Rails 将测试模型的东西称为单元测试，将测试控制器中单个操作的东西称为功能测试，将测试一个或多个控制器流程的东西称为集成测试。让我们在 unit 和 functional 子目录中窥探一下，看看里面已经有什么：

```
depot> ls test/unit
line_item_test.rb   order_test.rb      product_test.rb    user_test.rb
```

```
depot> ls test/functional
admin_controller_test.rb          products_controller_test.rb
info_controller_test.rb           store_controller_test.rb
line_items_controller_test.rb     users_controller_test.rb
orders_controller_test.rb
```

看吧！Rails 已经创建了文件来保存我们之前使用 generate 脚本创建的模型单元测试和控制器功能测试。这是一个好的开始，但 Rails 只能帮助我们到此为止。它把我们引向正确的道路，让我们专注于编写好的测试。我们将从数据所在的地方开始，然后逐渐向上，接近用户所在的地方。

#### 14.2 模型的单元测试

我们很久以前在第 69 页为 Depot 应用程序创建的第一个模型是 Product。让我们看看当我们生成该模型时，Rails 在文件 `test/unit/product_test.rb` 中生成了什么样的测试内容：

```
Download depot_r/test/unit/product_test.rb

require 'test_helper'

class ProductTest < ActiveSupport::TestCase
  # Replace this with your real tests.
  test "the truth" do
    assert true
  end
end
```

好的，我们的第二个决定——如何编写测试——也已经为我们做出了。生成的 ProductTest 是 ActiveSupport::TestCase 的子类。ActiveSupport::TestCase 是 Test::Unit::TestCase 类的子类这一事实告诉我们，Rails 生成的测试基于随 Ruby 预安装的 Test::Unit 框架。这是个好消息，因为如果我们已经用 Test::Unit 测试测试过我们的 Ruby 程序（为什么不呢？），那么我们就可以利用这些知识来测试 Rails 应用程序。如果你对 Test::Unit 不熟悉，不用担心。我们会慢慢来。

在这个测试用例中，Rails 生成了一个名为 the truth 的单个测试。其中的 assert 行是一个实际的测试。尽管如此，它并不是一个很好的测试——它所做的只是测试 true 是否为 true。显然，这是一个占位符，但它很重要，因为它让我们看到所有测试基础设施都已到位。因此，让我们尝试运行这个测试类：

```
depot> ruby -I test test/unit/product_test.rb
Loaded suite test/unit/product_test
Started
EE
Finished in 0.559942 seconds.

1) Error:
test_truth(ProductTest):
ActiveRecord::StatementInvalid: SQLite3::SQLException: no such table:
users: DELETE FROM "users" WHERE 1=1
... a whole bunch of tracing...
1 tests, 0 assertions, 0 failures, 2 errors
```

猜猜不是真理。测试不仅仅是失败了；它爆炸了！值得庆幸的是，它留下了一个线索——它找不到名为 users 的表。² 哼。

> 2. 如果你使用的是 SQLite 3 以外的数据库，消息可能表明类似 Unknown database。 如果是这样，你将需要创建数据库。只需使用 `rake db:create RAILS_ENV=test` 或随数据库提供的管理工具即可。

##### 仅用于测试的数据库

还记得第 70 页我们谈到 Depot 应用程序的开发数据库时吗？如果你查看 config 目录中的 database.yml 文件，你会注意到 Rails 实际上为三个单独的数据库创建了配置：

- `db/development.sqlite3` 将是我们的开发数据库。我们所有的编程工作都将在此进行。
- `db/test.sqlite3` 是一个测试数据库。
- `db/production.sqlite3` 是生产数据库。我们在上线时应用程序将使用它。





protected
  def price_must_be_at_least_a_cent
    errors.add(:price, 'should be at least 0.01') if price.nil? ||
      price < 0.01
  end
```

我们如何知道这个验证是否生效？让我们来测试一下。首先，如果我们创建一个没有任何属性设定的产品，我们期望它无效，并且每个字段都关联一个错误。我们可以使用模型的 valid? 方法来查看它是否通过验证，也可以使用错误列表的 invalid? 方法来查看某个特定属性是否关联了错误。

现在我们知道了要测试什么，我们需要知道如何告诉测试框架我们的代码是否通过或失败。我们使用断言来做到这一点。断言只是一个方法调用，告诉框架我们期望为真。最简单的断言是方法 assert，它期望其参数为真。如果是这样，就不会发生特殊情况。但是，如果 assert 的参数为 false，断言就会失败。框架会输出一条消息并停止执行包含失败的测试方法。在我们的例子中，我们期望一个空的 Product 模型无法通过验证，所以我们可以通过断言它无效来表达这一期望。

```
assert !product.valid?
```

让我们写出完整的测试：

```
Download depot_r/test/unit/product_test.rb
test "invalid with empty attributes" do
  product = Product.new
  assert !product.valid?
  assert product.errors.invalid?(:title)
  assert product.errors.invalid?(:description)
  assert product.errors.invalid?(:price)
  assert product.errors.invalid?(:image_url)
end
```

当我们运行测试用例时，我们现在会看到两个测试被执行（原始的真值测试和我们的新测试）：

```
depot> ruby -I test test/unit/product_test.rb
Loaded suite test/unit/product_test
Started
..
Finished in 0.092314 seconds.
2 tests, 6 assertions, 0 failures, 0 errors
```

果然，验证生效了，我们所有的断言都通过了。

很明显，在这一点上我们可以深入挖掘并单独测试各个验证。让我们看看其中三个可能的测试。

首先，我们将检查价格验证是否按预期工作：

```
Download depot_r/test/unit/product_test.rb
test "positive price" do
  product = Product.new(:title       => "My Book Title",
                        :description => "yyy",
                        :image_url   => "zzz.jpg")

  product.price = -1
  assert !product.valid?
  assert_equal "should be at least 0.01", product.errors.on(:price)

  product.price = 0
  assert !product.valid?
  assert_equal "should be at least 0.01", product.errors.on(:price)

  product.price = 1
  assert product.valid?
end
```

在这段代码中，我们创建一个新产品，然后尝试将其价格分别设为 -1、0 和 +1，每次都验证产品。如果我们的模型工作正常，前两个应该是无效的，我们验证与 price 属性关联的错误消息是我们期望的。最后一个价格是可以接受的，所以我们断言模型现在是有效的。（有些人会把这三个测试放到三个独立的测试方法中——这完全合理。）

接下来，我们将测试我们是否验证了图片 URL 以 .gif、.jpg 或 .png 之一结尾：

```
Download depot_r/test/unit/product_test.rb
test "image url" do
  ok = %w{ fred.gif fred.jpg fred.png FRED.JPG FRED.Jpg http://a.b.c/x/y/z/fred.gif }
  bad = %w{ fred.doc fred.gif/more fred.gif.more }

  ok.each do |name|
    product = Product.new(:title       => "My Book Title",
                          :description => "yyy",
                          :price       => 1,
                          :image_url   => name)
    assert product.valid?, product.errors.full_messages
  end

  bad.each do |name|
    product = Product.new(:title => "My Book Title",
                          :description => "yyy",
                          :price => 1,
                          :image_url => name)
    assert !product.valid?, "saving #{name}"
  end
end
```

在这里我们稍微混合了一下。与其写出九个独立的测试，我们使用了两个循环，一个来检查我们期望通过验证的用例，第二个来尝试我们期望失败的用例。你会注意到我们在 assert 方法调用中还添加了一个额外参数。所有测试断言都接受一个可选的尾随参数，其中包含一个字符串。如果断言失败，该字符串会连同错误消息一起输出，这对于诊断出了什么问题非常有用。

最后，我们的模型包含一个验证，用于检查数据库中所有产品标题都是唯一的。为了测试这一点，我们需要将产品数据存储在数据库中。

一种方法是让测试创建一个产品并保存它，然后再创建一个具有相同标题的另一个产品并尝试保存它。这显然是可行的。但有一种更符合惯例的方法——我们可以使用 Rails fixtures。

##### Test Fixtures

在测试的世界里，fixture 是你可以运行测试的环境。例如，如果你正在测试一块电路板，你可能会把它安装在一个测试夹具中，该夹具为其提供运行被测功能所需的电源和输入。

在 Rails 的世界里，测试 fixture 只是一个模型（或模型）在测试下初始内容的规范。如果，例如，我们希望确保在每次单元测试开始时我们的 products 表都以已知数据开始，我们可以在 fixture 中指定这些内容，Rails 会处理其余部分。

你将 fixture 数据指定在 test/fixtures 目录中的文件中。这些文件包含以逗号分隔值（CSV）或 YAML 格式的测试数据。对于我们的测试，我们将使用 YAML，这是首选格式。每个 YAML fixture 文件包含单个模型的数据。fixture 文件的名称很重要；文件的基名必须与数据库表的名称匹配。因为我们需要一些 Product 模型的数据，该模型存储在 products 表中，我们将把它添加到名为 products.yml 的文件中。Rails 在我们第一次创建模型时已经创建了这个 fixture 文件：

```
# Read about fixtures at http://ar.rubyonrails.org/classes/Fixtures.html

one:
  title: MyString
  description: MyText
  image_url: MyString

two:
  title: MyString
  description: MyText
  image_url: MyString
```

fixture 文件包含我们希望插入数据库的每一行的条目。每行都有一个名称。在 Rails 生成的 fixture 的情况下，行被命名为 *one* 和 *two*。就数据库而言，这个名称没有意义——它不会插入到行数据中。相反，正如我们稍后将看到的，该名称为我们在测试代码中引用测试数据提供了一种方便的方式。

在每个条目内部，你会看到一个缩进⁴的属性名/值对列表。在进行更改时要小心，因为你需要确保每个条目中列名的名称与数据库列名正确匹配；与数据库列名不匹配可能会导致难以追踪的异常。

让我们用一些可以用来测试我们的产品模型的东西替换 fixture 文件中的虚拟数据。我们先从一本书开始。（注意，你不必在测试 fixture 中包含 id 列。）

```yaml
ruby_book*:
  title:       Programming Ruby
  description: Dummy description
  price:       1234
  image_url:   ruby.png
```

现在我们有了 fixture 文件，我们希望 Rails 在我们运行单元测试时将测试数据加载到 products 表中。事实上，Rails 已经在这样做了（约定优于配置万岁！），但你可以通过在 ProductTest 中指定以下行来控制要加载哪些 fixtures：

```ruby
fixtures :products
```

fixtures 指令在测试用例中的每个测试方法运行之前，将给定模型名称对应的 fixture 数据加载到对应的数据库表中。fixture 文件的名称决定了要加载的表，因此使用 :products 将导致使用 products.yml fixture 文件。

让我们换一种说法。 在 ProductTest 类的情况下，添加 fixtures 指令意味着在每个测试方法运行之前，products 表将被清空，然后用 Ruby 书的单行填充。每个测试方法在测试数据库中都得到一个全新初始化的表。

##### Using Fixture Data

现在我们知道了如何将 fixture 数据放入数据库，我们需要找到在测试中使用它的方法。

4. 就像在你的 config/database.yml 中一样，你必须在每条数据行的开头使用空格而不是制表符，并且同一行的所有行必须具有相同的缩进。




##### 大卫说...

###### 选择好的夹具名称

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

##### 测试购物车

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

##### 单元测试支持

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

#### 14.3 控制器的功能测试

控制器掌控全局。它们接收传入的 Web 请求（通常是用户输入），与模型交互以收集应用程序状态，然后通过让适当的视图向用户显示内容来作出响应。因此，在测试控制器时，我们要确保给定的请求能得到适当的响应。我们仍然需要模型，但单元测试已经覆盖了它们。

Rails 将测试单个控制器的测试称为功能测试。Depot 应用有四个控制器，每个控制器都有许多动作。这里有很多东西可以测试，但我们会挑一些重点来讲解。让我们从用户开始的地方开始——登录。

##### 管理员

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



响应对象，等等。在我们的应用完成处理一个请求后，Rails 会取出响应对象中的信息，并用它向客户端发送响应。

请求和响应对象对于我们功能测试的运行至关重要——使用它们意味着我们不必启动真实的 Web 服务器就可以运行控制器测试。也就是说，功能测试不一定需要 Web 服务器、网络或客户端。

##### 索引页：仅供管理员

好的，现在让我们编写第一个控制器测试——一个简单地“访问”索引页面的测试：

```
Download depot_r/test/functional/admin_controller_test.rb

test "index" do
  get :index
  assert_response :success
end
```

`get` 方法是由测试辅助器加载的一个便捷方法，它模拟向 `AdminController` 的 `index` 动作发起一个 Web 请求（可以看作 HTTP GET），并捕获响应。然后，`assert_response` 方法会检查响应是否成功。

好，让我们看看运行这个测试时会发生什么。我们将使用 `-n` 选项来指定要运行的特定测试方法的名称：

```
depot> ruby -I test test/functional/admin_controller_test.rb -n test_index
Loaded suite test/functional/admin_controller_test
Started
F
Finished in 0.239281 seconds.

1) Failure:
test_index(AdminControllerTest)
[test/functional/admin_controller_test.rb:20:in `test_index'
/Library/Ruby/Gems/1.8/ ... /setup_and_teardown.rb:33:in `__send__'
/Library/Ruby/Gems/1.8/ ... /setup_and_teardown.rb:33:in `run']:
Expected response to be a <:success>, but was <302>
```

这看起来很简单，那么发生了什么？响应码 302 表示请求被重定向了，所以它不算成功。但为什么会重定向？因为这就是我们设计 `ApplicationController` 的方式。它使用一个前置过滤器来拦截那些未以管理员身份登录的用户不能访问的动作调用。在这个例子中，前置过滤器确保在 `index` 动作运行之前先执行 `authorize` 方法。

```
class ApplicationController < ActionController::Base
  layout "store"
  before_filter :authorize, :except => :login
  #...

  protected
    def authorize
      unless User.find_by_id(session[:user_id])
        flash[:notice] = "Please log in"
        redirect_to :controller => 'admin', :action => 'login'
      end
    end
end
```

由于我们还没有登录，会话中不存在有效用户，因此请求会被重定向到登录动作。根据 `authorize` 的逻辑，结果页面应该包含一条 *flash* 通知，告诉我们需要登录。好的，让我们重写功能测试来捕获这一流程：

```
test "index without user" do
  get :index
  assert_redirected_to :action => "login"
  assert_equal "Please log in", flash[:notice]
end
```

这一次，当我们请求 index 动作时，预期会被重定向到登录动作，并看到视图生成的 flash 通知：

```
depot> ruby -I test test/functional/admin_controller_test.rb
Loaded suite test/functional/admin_controller_test
Started
.
Finished in 0.0604571 seconds.
1 tests, 2 assertions, 0 failures, 0 errors
```

确实，我们得到了预期结果。⁶ 现在我们知道，在用户登录之前，仅管理员的动作是不可访问的（*前置过滤器*正在起作用）。让我们在拥有有效用户的情况下尝试查看索引页面。

回顾一下，应用会将当前登录用户的 id 存储到会话中，以 `:user_id` 键作为索引。因此，要模拟一个已登录用户，我们只需在发起 index 请求前将一个用户 id 设置到会话中即可。现在唯一的问题是如何确定该使用哪个用户 id。

> ⁶. 取决于你的 Rails 版本，控制台日志可能会显示通过了三个断言。那是因为旧版 Rails 中的 `assert_redirected_to` 方法内部使用了两个底层断言。

我们不能随便塞一个随机数进去，因为应用控制器的 `authorize` 方法会根据它的值从数据库获取对应的用户行。看来我们需要向 users 表中填充一些有效数据。这正好给了我们一个了解动态夹具的机会。

##### 动态夹具

我们将创建一个 `users.yml` 测试夹具，向 `users` 表添加一行数据。我们将这个用户命名为 `dave`。

```
dave:
  name: dave
  salt: NaCl
  hashed_password: ???
```

一切都很顺利，直到 `hashed_password` 这一行。我们应该用什么作为值？在真实表中，这个值是使用 User 类中的 `encrypted_password` 方法计算出来的。该方法接收一个明文密码和一个盐值，并创建一个 SHA1 哈希值。

一种办法是启动 `script/console` 并手动调用该方法。然后我们可以复制该方法返回的值，粘贴到夹具文件中。这样可行，但有点晦涩，而且如果我们更改密码生成机制，测试可能会失败。如果能在数据加载到数据库时，使用应用程序的代码生成哈希密码，岂不是很好？那么，请看下面的内容：

```
<% SALT = "NaCl" unless defined?(SALT) %>
```

```
dave:
  name: dave
  salt: <%= SALT %>
  hashed_password: <%= User.encrypted_password('secret', SALT) %>
```

`hashed_password` 这一行的语法应该看起来很眼熟：`<%=...%>` 指令与我们在模板中替换值所用的指令相同。事实证明，Rails 在测试夹具中也支持这些替换。这就是为什么我们称它们为动态夹具。

现在我们可以再次测试 `index` 动作了。我们必须记得在 admin 控制器测试类中添加 `fixtures` 指令：

```
fixtures :users
```

然后我们编写测试方法：

```
test "index with user" do
  get :index, {}, { :user_id => users(:dave).id }
  assert_response :success
  assert_template "index"
end
```

这里的关键概念是 `get` 方法的调用。注意，我们在动作名称后面添加了几个新参数。参数 2 是一个空哈希——表示要传递给动作的参数。参数 3 是一个用于填充会话数据的哈希。这里我们使用了自己的用户夹具，将会话条目 `:user_id` 设置为测试用户的 id。然后我们的测试断言响应成功（而非重定向），并且动作渲染了 `index` 模板。（我们稍后会更深入地讨论所有这些断言。）

##### 登录

现在测试数据库中已经有了一个用户，让我们看看能否以该用户身份登录。如果使用浏览器，我们会导航到登录表单，输入用户名和密码，然后将这些字段提交给 admin 控制器的 `login` 动作。我们预期会被重定向到 index 列表页，并且会话中妥善地存放着测试用户的 id。下面是在功能测试中实现这一过程的代码：

```
Download depot_r/test/functional/admin_controller_test.rb

test "login" do
  dave = users(:dave)
  post :login, :name => dave.name, :password => 'secret'
  assert_redirected_to :action => "index"
  assert_equal dave.id, session[:user_id]
end
```

这里我们使用了 `post` 方法来模拟提交表单数据，并将 `name` 和 `password` 表单字段的值作为参数传递。

如果我们尝试使用无效密码登录，会发生什么？

```
Download depot_r/test/functional/admin_controller_test.rb

test "bad password" do
  dave = users(:dave)
  post :login, :name => dave.name, :password => 'wrong'
  assert_template "login"
end
```

不出所料，测试用户没有被重定向到 index 列表页，而是再次看到了登录表单。

##### 功能测试的便捷功能

以上是对如何为控制器编写功能测试的一次简短浏览。在此期间，我们使用了 Rails 自带的许多辅助方法和断言，它们能让你的测试工作更轻松。在我们继续深入之前，现在来仔细看看 Rails 专为测试控制器提供的一些便捷功能。

###### assert_dom_not_equal(expected_html, actual_html, message)

比较两个包含 HTML 的字符串，如果它们由同一个文档对象模型表示/不由同一个文档对象模型表示，则断言成功。由于该断言会比较两个字符串的完整（规范化）版本，因此面对应用变更时它很脆弱。请考虑改用 `assert_select`。

```
expected = "<html><body><h1>User Unknown</h1></body></html>"
assert_dom_equal(expected, @response.body)
```

###### assert_response(type, message)

断言响应是一个数字 HTTP 状态码，或是以下符号之一。其中一些符号涵盖一段响应码范围（例如，`:redirect` 表示状态码 300–399）。

- :accepted – 202
- :bad_gateway – 502
- :bad_request – 400
- :conflict – 409
- :continue – 100
- :created – 201
- :error – 500–599
- :expectation_failed – 417
- :failed_dependency – 424
- :forbidden – 403
- :found – 302
- :gateway_timeout – 504
- :gone – 410
- :http_version_not_supported – 505
- :im_used – 226
- :insufficient_storage – 507
- :internal_server_error – 500
- :length_required – 411
- :locked – 423
- :method_not_allowed – 405
- :missing – 404
- :moved_permanently – 301
- :multi_status – 207
- :multiple_choices – 300
- :no_content – 204
- :non_authoritative_information – 203
- :not_acceptable – 406





- :not_extended – 510
- :not_found – 404
- :not_implemented – 501
- :not_modified – 304
- :ok – 200
- :partial_content – 206
- :payment_required – 402
- :precondition_failed – 412
- :processing – 102
- :proxy_authentication_required – 407
- :redirect – 300-399
- :request_entity_too_large – 413
- :request_timeout – 408
- :request_uri_too_long – 414
- :requested_range_not_satisfiable – 416
- :reset_content – 205
- :see_other – 303
- :service_unavailable – 503
- :success – 200
- :switching_protocols – 101
- :temporary_redirect – 307
- :unauthorized – 401
- :unprocessable_entity – 422
- :unsupported_media_type – 415
- :upgrade_required – 426
- :use_proxy – 305

Examples:

```
assert_response :success
assert_response :not_implemented
assert_response 200
```

###### assert_redirected_to(options, message)

断言传入的重定向选项与最后一次操作中调用的重定向相匹配。你也可以传入一个简单的字符串，它将与重定向生成的 URL 进行比较。

Examples:

```
assert_redirected_to :controller => 'login'
assert_redirected_to :controller => 'login', :action => 'index'
assert_redirected_to "http://my.host/index.html"
```

###### assert_template(expected, message)

断言请求使用指定的模板文件进行渲染。

Examples:

```
assert_template 'store/index'
```

###### assert_select(...)

参见第 14.3 节，Testing Response Content，第 234 页。

###### assert_tag(...)

断言响应正文中存在一个满足所有给定条件的标签/节点/元素。条件参数必须是以下任意键的哈希表（所有键都是可选的）：

- :tag: 节点类型必须与对应值匹配
- :attributes: 一个哈希表。节点的属性必须与哈希表中的对应值匹配。
- :parent: 一个哈希表。节点的父节点必须与对应的哈希表匹配。
- :child: 一个哈希表。节点的直接子节点中至少有一个必须满足哈希表描述的标准。
- :ancestor: 一个哈希表。节点的祖先中至少有一个必须满足哈希表描述的标准。
- :descendant: 一个哈希表。节点的后代中至少有一个必须满足哈希表描述的标准。
- :sibling: 一个哈希表。节点的兄弟节点中至少有一个必须满足哈希表描述的标准。
- :after: 一个哈希表。节点必须位于满足哈希表描述标准的任何兄弟节点之后，并且至少有一个兄弟节点匹配。
- :before: 一个哈希表。节点必须位于满足哈希表描述标准的任何兄弟节点之前，并且至少有一个兄弟节点匹配。
- :children: 一个哈希表，用于统计节点的子节点。接受以下键：
  - :count: 必须是数字或范围，必须等于（或包含）匹配的子节点数
  - :less_than: 匹配的子节点数必须小于该数字
  - :greater_than: 匹配的子节点数必须大于该数字
  - :only: 另一个哈希表，由用于匹配子节点的键组成，并且只有匹配的子节点才会被计数
- :content: 节点的文本内容必须与给定值匹配。这不会匹配标签体内的 HTML 标签——仅匹配文本。

###### assert_no_tag(...)

与 assert_tag 相同，但断言不存在匹配的标签。

Rails 提供了一些额外的断言来测试控制器路由组件。我们在第 21.4 节，Testing Routing，第 458 页讨论这些断言。

##### Variables

请求执行后，功能测试可以使用以下变量中的值进行断言：

**assigns(key=nil)**

最后一次操作中分配的实例变量。

```
assert_not_nil assigns["items"]
```

assigns 哈希表必须使用字符串作为索引引用。例如，assigns[:items] 将无法工作，因为键是符号。要使用符号作为键，请改用方法调用而不是索引引用：

```
assert_not_nil assigns(:items)
```

我们可以用以下方式测试控制器操作找到了三个订单：

```
assert_equal 3, assigns(:orders).size
```

**session**

会话中的对象哈希表。

```
assert_equal 2, session[:cart].items.size
```

**flash**

当前在会话中的 flash 对象哈希表。

```
assert_equal "Danger!", flash[:notice]
```

**cookies**

发送给用户的 cookie 哈希表。

```
assert_equal "Fred", cookies[:name]
```

**redirect_to_url**

上一个操作重定向到的完整 URL。

```
assert_equal "http://test.host/login", redirect_to_url
```

##### Functional Testing Helpers

Rails 在功能测试中提供了以下辅助方法：

###### find_tag(conditions)

在响应中找到一个标签，使用与 assert_tag 相同的条件。

```
get :index
tag = find_tag :tag => "form",
                :attributes => { :action => "/store/add_to_cart/993" }
assert_equal "post", tag.attributes["method"]
```

这最好使用 assert_select 编写。

###### find_all_tag(conditions)

返回满足给定条件的标签数组。

###### follow_redirect

如果前一个操作生成了重定向，此方法通过发出 get 请求来跟随它。功能测试只能跟随重定向到其自己的控制器。

```
post :add_to_cart, :id => 123
assert_redirected_to :action => :index
follow_redirect
assert_response :success
```

###### fixture_file_upload(path, mime_type)

创建通常由浏览器 <input type="file"> 字段上传的 MIME 编码内容。将其用于在 post 请求中设置相应的表单参数。

```
post :report_bug,
  :screenshot => fixture_file_upload("screen.png", "image/png")
```

###### with_routing

暂时用新的 RouteSet 实例替换 ActionController::Routing::Routes。使用它来测试不同的路由配置。

```
with_routing do |set|
  set.draw do |map|
    map.connect ':controller/:action/:id'
    assert_equal(
      ['/content/10/show', {}],
      map.generate(:controller => 'content', :id => 10, :action => 'show')
    )
  end
end
```

##### Testing Response Content

Rails 1.2 引入了一个新的断言 assert_select，它允许你深入到应用程序返回的响应的结构和内容中。它通常比 assert_tag 更具功能性且更易于使用。例如，功能测试可以用以下断言验证响应包含包含文本 Pragprog Books Online Store 的 title 元素：

```
assert_select "title", "Pragprog Books Online Store"
```

对于更进取的人来说，以下测试响应包含一个 id 为 cart 的 <div>。在该 <div> 内，必须有一个包含三行的表格。class 为 total-line 的行的最后一个 <td> 必须具有内容 $57.70。

```
assert_select "div#cart" do
  assert_select "table" do
    assert_select "tr", :count => 3
    assert_select "tr.total-line td:last-of-type", "$57.70"
  end
end
```

Rails 还提供了 css_select 辅助方法，可用于表达更复杂的表达式：

```
# 确保每行有三列
assert_equal css_select('tr').size * 3, css_select('td').size
```

这显然功能强大。让我们花点时间来研究它。

assert_select 建立在 Assaf Arkin 的 HTML::Selector 库之上。该库允许你使用大量借鉴自层叠样式表选择器的语法来导航格式良好的 HTML 文档。在选择器的基础上，Rails 增加了对 resulting 节点集执行一组测试的能力。让我们先从选择器语法开始。

###### Selectors

选择器语法很复杂——可能比正则表达式更复杂。然而，它与 CSS 选择器语法的相似性意味着，如果以下简要总结过于简略，你应该能在网上找到许多示例。在下面的描述中，我们将借用 W3C 用于描述选择器的术语。⁷

###### Simple Selectors

简单选择器由可选的类型选择器组成，后跟任意数量的类选择器、id 选择器、属性选择器或伪类。

类型选择器只是文档中标签的名称。例如，以下类型选择器匹配文档中所有的 <p> 标签：

```
p
```

（值得强调“所有”这个词——选择器操作文档节点的集合。）

如果省略类型选择器，则选择文档中的所有节点。

类型选择器可以用类选择器、id 选择器、属性选择器或伪类限定。每个限定符都会减少所选节点的集合。

> 7. http://www.w3.org/TR/REC-CSS2/selector.html




###### 类选择器和 id 选择器非常简单：

```
p#some-id      # selects the paragraph with id="some-id"

p.some-class   # selects paragraph(s) with class="some-class"
```

属性选择器出现在方括号中。语法如下：

```
p[name]          # paragraphs with an attribute name
p[name=value]     # paragraphs with an attribute name=value
p[name^=string]   # ... name=value, value starts with 'string'
p[name$=string]   # ... name=value, value ends with 'string'
p[name*=string]   # ... name=value, value must contain 'string'
p[name~=string]   # ... name=value, value must contain 'string'
                  # as a space-separated word
p[name|=string]   # ... name=value, value starts 'string'
                  # followed by a space
```

让我们看一些示例：

```
p[class=warning]      # all paragraphs with class="warning"

tr[id=total]          # the table row with id="total"

table[cellpadding]    # all table tags with a cellpadding attribute

div[class*=error]     # all div tags with a class attribute
                      # containing the text error

p[secret][class=shh]  # all p tags with both a secret attribute
                      # and a class="shh" attribute

[class=error]         # all tags with class="error"
```

类选择器和 id 选择器是 `class=` 和 `id=` 的快捷方式：

```
p#some-id      # same as p[id=some-id]
p.some-class   # same as p[class=some-class]
```

###### 链式选择器

你可以组合多个简单选择器来创建链式选择器。这些选择器允许你描述元素之间的关系。在接下来的描述中，`sel_1`、`sel_2` 等代表简单选择器。

`sel_1 sel_2`
选择所有以 `sel_1` 为祖先的 `sel_2` 元素。（选择器之间用一个或多个空格分隔。）

`sel_1 > sel_2`
选择所有以 `sel_1` 为父元素的 `sel_2` 元素。因此：

```
table  td      # will match all td tags inside table tags
table > td      # won't match in well-formed HTML,
                # as td tags have tr tags as parents
```

###### sel_1 + sel_2

选择所有紧随 `sel_1` 之后的 `sel_2` 元素。注意，“紧随”意味着这两个选择器描述的是同级节点，而不是父子节点。

```
td.price + td.total    # select all td nodes with class="total"
                       # that follow a <td class="price">
```

###### sel_1 ~ sel_2

选择所有在 `sel_1` 之后的 `sel_2` 元素。

```
div#title ~ p    # all the p tags that follow a
                  # <div id="title">
```

###### sel_1, sel_2

选择所有被 `sel_1` 或 `sel_2` 选中的元素。

```
p.warn, p.error    # all paragraphs with a class of
                    # warn or error
```

###### 伪类

伪类通常允许你根据元素的位置来选择元素（尽管也有一些例外）。它们都以冒号作为前缀。

###### :root

只选择根元素。这在测试 XML 响应时有时很有用。

```
order:root         # only returns a selection if the
                    # root of the response is <order>
```

###### sel:empty

仅当 `sel` 既没有子节点也没有文本内容时才会选择。

```
div#error:empty    # selects the node <div id="error">
                    # only if it is empty
```

###### sel_1 sel_2:only-child

选择作为 `sel_1` 节点唯一子节点的所有节点。

```
div :only-child    # select the child nodes of divs that
                    # have only one child
```

###### sel_1 sel_2:nth-child(n)

选择所有作为 `sel_1` 节点第 n 个子节点的 `sel_2` 节点，其中 n 从 1 开始计数。将此与稍后描述的 nth-of-type 进行对比。

```
table tr:nth-child(2)    # the second row of every table
```

```
div p:nth-child(2)       # the second element of each div
# if that element is a <p>
```

###### sel_1 sel_2:nth-last-child(n)

选择所有作为 `sel_1` 节点倒数第 n 个子节点的 `sel_2` 节点。

```
table tr:nth-last-child(2)  # the second to last row in every table
```

###### sel_1 sel_2:only-of-type

选择所有作为 `sel_1` 节点唯一子节点的 `sel_2` 节点。（也就是说，`sel_1` 节点可能有多个子节点，但只有一个是 `sel_2` 类型。）

```
div p:only-of-type  # all the paragraphs in divs that
# contain just one paragraph
```

###### sel_1 sel_2:first-of-type

选择父节点为 `sel_1` 节点的第一个 `sel_2` 类型节点。

```
div.warn p:first-of-type  # the first paragraph in <div class="warn">
```

###### sel_1 sel_2:last-of-type

选择父节点为 `sel_1` 节点的最后一个 `sel_2` 类型节点。

```
div.warn p:last-of-type  # the last paragraph in <div class="warn">
```

###### sel_1 sel_2:nth-of-type(n)

选择所有作为 `sel_1` 节点第 n 个子节点的 `sel_2` 节点，但只计算类型与 `sel_2` 匹配的节点。

```
div p:nth-of-type(2)  # the second paragraph of each div
```

###### sel_1 sel_2:nth-last-of-type(n)

选择所有作为 `sel_1` 节点倒数第 n 个子节点的 `sel_2` 节点，从末尾开始计数，但只计算类型与 `sel_2` 匹配的节点。

```
div p:nth-last-of-type(2)  # the second to last paragraph of each div
```

nth-xxx 选择器的数值参数可以是以下形式：

###### d（一个数字）

计数 d 个节点。

###### an+d（来自分组的节点）

将子节点分成每组 a 个，然后从每组中选择第 d 个节点。

```
div#story p:nth-child(3n+1)    # every third paragraph of
# the div with id="story"
```

###### -an+d（来自分组的节点）

将子节点分成每组 a 个，然后选择最多 d 组中的第一个节点。（是的，这是一个奇怪的语法。）

```
div#story p:nth-child(-n+2)    # The first two paragraphs
```

odd（奇数编号的节点）
even（偶数编号的节点）
交替选择子节点。

```
div#story p:nth-child(odd)    # paragraphs 1, 3, 5, ...
div#story p:nth-child(even)    # paragraphs 2, 4, 6, ...
```

最后，你可以反转任何选择器的含义。

`:not(sel)`
选择所有未被 `sel` 选中的节点。

```
div :not(p)        # all the non-paragraph nodes of all divs
```

现在我们知道了如何选择响应中的节点，让我们看看如何编写断言来测试响应的内容。

##### 面向响应的断言

`assert_select` 断言可以用于功能测试和集成测试中。它最简单的形式是接受一个选择器。如果响应中至少有一个节点匹配，断言通过；如果没有节点匹配，则断言失败。

```
assert_select "title"        # does our response contain a <title> tag
```

```
# and a <div class="cart"> with a
# child <div id="cart-title">
assert_select "div.cart > div#cart-title"
```

除了简单地测试所选节点是否存在之外，你还可以将它们的內容与字符串或正则表达式进行比较。仅当所有选中的节点都等于该字符串或与正则表达式匹配时，断言才会通过：

```
assert_select "title", "Pragprog Online Book Store"
assert_select "title", /Online/
```

如果你传入一个数字或 Ruby 范围，则当节点数量等于该数字或在该范围内时，断言通过：

```
assert_select "title", 1                # must be just one title element
assert_select "div#main div.entry", 1..10   # one to 10 entries on a page
```

将 `false` 作为第二个参数等同于传递零：如果没有选中任何节点，则断言成功。

你也可以在选择器后面传递一个哈希，从而测试多个条件。

例如，要测试恰好有一个 title 节点且该节点匹配正则表达式 `/pragprog/`，你可以使用：

```
assert_select "title", :count => 1, :text => /pragprog/
```

该哈希可以包含以下键：

| 键 | 描述 |
|---|---|
| `:text => S \| R` | 一个字符串或正则表达式，必须与节点的内容匹配。 |
| `:count => n` | 必须恰好选择 *n* 个节点。 |
| `:minimum => n` | 必须至少选择 *n* 个节点。 |
| `:maximum => n` | 最多必须选择 *n* 个节点。 |

##### 嵌套选择器断言

一旦 `assert_select` 选择了一组节点并通过了与该组节点相关的任何测试，你可能想要在该节点集内执行额外的测试。例如，我们在本节开头使用一个测试来检查页面是否包含一个 id 为 cart 的 `<div>`。这个 `<div>` 应该包含一个表格，该表格本身应恰好包含三行。在 class 为 total-line 的行中，最后一个 `<td>` 应包含内容 $57.70。

我们可以使用一系列断言来表达：

```
assert_select "div#cart"
assert_select "div#cart table tr", 3
assert_select "div#cart table tr.total-line td:last-of-type", "$57.70"
```

通过在块中嵌套选择，我们可以简化这些断言：

```
assert_select "div#cart" do
  assert_select "table" do
    assert_select "tr", :count => 3
    assert_select "tr.total-line td:last-of-type", "$57.70"
  end
end
```

##### 其他断言

除了 `assert_select`，Rails 还提供了类似的基于选择器的断言，用于验证 RJS 更新和插入操作的 HTML 内容（`assert_select_rjs`）、XML 响应中的编码 HTML（`assert_selected_encoded`）以及电子邮件的 HTML 正文（`assert_select_email`）。详情请参阅 Rails 文档。

#### 14.4 应用程序的集成测试

下一级测试是演练我们应用程序中的流程。在许多方面，这就像测试客户在我们开始编写应用程序时给我们的一个用户故事。例如，我们可能被告知



让我们从用户故事的第一句话开始攻击：用户进入商店索引页面。

```
Download depot_r/test/integration/user_stories_test.rb
get "/store/index"
assert_response :success
assert_template "index"
```

这几乎看起来像一个功能测试。主要区别在于 get 方法。在功能测试中我们只检查一个控制器，所以在调用 get 时只指定一个 action。在集成测试中，我们可以在应用程序中到处游走，所以我们需要传入要调用的控制器和 action 的完整（相对）URL。

故事中的下一句话是 他们选择一个产品，将其添加到购物车。我们知道我们的应用程序使用 Ajax 请求将商品添加到购物车，所以我们将使用 xml_http_request 方法来调用 action。当它返回时，我们将检查购物车现在是否包含所请求的商品：

```
Download depot_r/test/integration/user_stories_test.rb
xml_http_request :put, "/store/add_to_cart", :id => ruby_book.id
assert_response :success

cart = session[:cart]
assert_equal 1, cart.items.size
assert_equal ruby_book, cart.items[0].product
```

在一个惊人的剧情转折中，用户故事继续， 他们然后结账.... 在我们的测试中这很容易：

```
Download depot_r/test/integration/user_stories_test.rb
post "/store/checkout"
assert_response :success
assert_template "checkout"
```

此时，用户必须在结账表单上填写他们的详细信息。一旦他们填写并提交数据，我们的应用程序就会创建订单并重定向到索引页面。让我们从 HTTP 层面开始，通过向 save_order action 发布表单数据并验证我们已被重定向到索引。我们还将检查购物车现在是否为空。测试辅助方法 post_via_redirect 生成 post 请求然后跟随任何返回的重定向，直到返回非重定向响应。

```
Download depot_r/test/integration/user_stories_test.rb
post_via_redirect "/store/save_order",
    :order => { :name    => "Dave Thomas",
                :address => "123 The Street",
                :email   => "dave@pragprog.com",
                :pay_type => "check" }
```

```
assert_response :success
assert_template "index"
assert_equal 0, session[:cart].items.size
```

最后，我们将进入数据库并确保我们创建了一个订单和对应的订单项，并且它们包含的详细信息是正确的。因为我们在测试开始时清空了 orders 表，所以我们只需验证它现在只包含我们的新订单：

Download depot_r/test/integration/user_stories_test.rb

```
orders = Order.find(:all)
assert_equal 1, orders.size
order = orders[0]

assert_equal "Dave Thomas", order.name
assert_equal "123 The Street", order.address
assert_equal "dave@pragprog.com", order.email
assert_equal "check", order.pay_type

assert_equal 1, order.line_items.size
line_item = order.line_items[0]
assert_equal ruby_book, line_item.product
```

就这样。这是集成测试的完整源代码：

Download depot_r/test/integration/user_stories_test.rb

```
require 'test_helper'

class UserStoriesTest < ActionController::IntegrationTest
  fixtures :products

  # A user goes to the index page. They select a product, adding it to their
  # cart, and check out, filling in their details on the checkout form. When
  # they submit, an order is created containing their information, along with a
  # single line item corresponding to the product they added to their cart.

  test "buying a product" do
    LineItem.delete_all
    Order.delete_all
    ruby_book = products(:ruby_book)

    get "/store/index"
    assert_response :success
    assert_template "index"

    xml_http_request :put, "/store/add_to_cart", :id => ruby_book.id
    assert_response :success

    cart = session[:cart]
    assert_equal 1, cart.items.size
    assert_equal ruby_book, cart.items[0].product
```

```
post "/store/checkout"
assert_response :success
assert_template "checkout"

post_via_redirect "/store/save_order",
    :order => { :name    => "Dave Thomas",
                :address => "123 The Street",
                :email   => "dave@pragprog.com",
                :pay_type => "check" }

assert_response :success
assert_template "index"
assert_equal 0, session[:cart].items.size

orders = Order.find(:all)
assert_equal 1, orders.size
order = orders[0]

assert_equal "Dave Thomas",    order.name
assert_equal "123 The Street", order.address
assert_equal "dave@pragprog.com", order.email
assert_equal "check",          order.pay_type

assert_equal 1, order.line_items.size
line_item = order.line_items[0]
assert_equal ruby_book, line_item.product
end
end
```

##### 更高级的测试

（本节包含可以安全跳过的进阶材料。）

集成测试设施非常不错：我们不知道有其他框架提供如此高级别的内置测试。但我们可以把它提升得更高。想象一下，能够给你的 QA 人员一个用于应用程序测试的迷你语言（有时称为领域特定语言）。他们可以用这样的语言编写我们之前的测试：

Download depot_r/test/integration/dsl_user_stories_test.rb

```
def test_buying_a_product
  dave = regular_user
  dave.get "/store/index"
  dave.is_viewing "index"
  dave.buys_a @ruby_book
  dave.has_a_cart_containing @ruby_book
  dave.checks_out DAVES_DETAILS
  dave.is_viewing "index"
  check_for_order DAVES_DETAILS, @ruby_book
end
```

此代码使用在测试类内部定义的哈希 DAVES_DETAILS：

```
DAVES_DETAILS = {
  :name => "Dave Thomas",
  :address => "123 The Street",
  :email => "dave@pragprog.com",
  :pay_type => "check"
}
```

它可能不是很棒的文学作品，但仍然相当易读。那么，我们如何为他们提供这种功能呢？事实证明，使用 Ruby 的一个很棒的设施——单例方法——相当容易。

如果 obj 是一个包含任何 Ruby 对象的变量，我们可以使用以下语法定义仅适用于该对象的方法：

```
def obj.method_name
  # ...
end
```

一旦我们这样做了，我们就可以像调用任何其他方法一样在 obj 上调用 method_name：

```
obj.method_name
```

这就是我们实现测试语言的方式。我们将使用 open_session 方法创建一个新的测试会话，并在该会话上定义所有辅助方法。在我们的示例中，这是在 regular_user 方法中完成的：

```
def regular_user
  open_session do |user|
    def user.is_viewing(page)
      assert_response :success
      assert_template page
    end

    def user.buys_a(product)
      xml_http_request :put, "/store/add_to_cart", :id => product.id
      assert_response :success
    end

    def user.has_a_cart_containing(*products)
      cart = session[:cart]
      assert_equal products.size, cart.items.size
      for item in cart.items
        assert products.include?(item.product)
      end
    end

    def user.checks_out(details)
      post "/store/checkout"
```

```
assert_response :success
assert_template "checkout"

post_via_redirect "/store/save_order",
    :order => { :name    => details[:name],
                :address => details[:address],
                :email   => details[:email],
                :pay_type => details[:pay_type]
              }

assert_response :success
assert_template "index"
assert_equal 0, session[:cart].items.size
end
end
end
```

regular_user 方法返回此增强的会话对象，然后我们的其余脚本就可以使用它来运行测试。

一旦我们定义了这个迷你语言，编写更多测试就很容易了。例如，这里有一个测试，验证两个用户同时购买商品时没有相互影响。（我们缩进了与 Mike 会话相关的行，以便更容易看到流程。）

Download depot_r/test/integration/dsl/user_stories_test.rb

```
def test_two_people_buying
  dave = regular_user
    mike = regular_user
  dave.buys_a @ruby_book
    mike.buys_a @rails_book
  dave.has_a_cart_containing @ruby_book
  dave.checks_out DAVES_DETAILS
    mike.has_a_cart_containing @rails_book
  check_for_order DAVES_DETAILS, @ruby_book
    mike.checks_out MIKES_DETAILS
  check_for_order MIKES_DETAILS, @rails_book
end
```

我们从第 717 页开始展示迷你语言版本的测试类的完整列表。

##### 集成测试支持

集成测试与功能测试表面上非常相似，事实上我们在单元和功能测试中使用的所有断言在集成测试中都有效。然而需要谨慎，因为许多辅助方法在细节上有所不同。

集成测试围绕会话的概念展开。会话代表一个在浏览器中与我们的应用程序交互的用户。虽然在概念上与控制器中的 session 变量相似，但这里的 session 词含义不同。




当你开始运行集成测试时，你会获得一个默认会话（如果你确实需要，可以在实例变量 `integration_session` 中访问它）。所有集成测试方法（如 `get`）实际上都是这个会话上的方法：测试框架会替你代理这些调用。不过，你也可以创建显式会话（使用 `open_session` 方法），并直接在这些会话上调用这些方法。这让你可以同时模拟多个用户（或者让你创建具有不同特征的会话，在测试中按顺序使用）。我们在第 245 页的测试中看到了多会话的示例。

在集成测试中向集成测试属性赋值时，务必使用显式接收者：

```
self.accept = "text/plain"      # works
open_session do |sess|
  sess.accept = "text/plain"   # works
end
accept = "text/plain"          # doesn't work--local variable
```

集成测试会话具有以下属性。在下面的列表中，`sess` 代表一个会话对象。

- `accept`
  - 要发送的 Accept 头。
  - `sess.accept = "text/xml,text/html"`
- `controller`
  - 对上次请求所使用的控制器实例的引用。
- `cookies`
  - Cookie 的哈希。设置该哈希中的条目即可在请求中发送 Cookie；读取哈希中的值可以查看响应中设置了哪些 Cookie。
- `headers`
  - 上次响应返回的头信息，以哈希形式呈现。
- `host`
  - 将此值设置为与下一个请求关联的主机名。当你编写的应用行为取决于服务器的主机名时，该设置很有用。
  - `sess.host = "fred.blog_per_user.com"`
- `path`
  - 上次请求的 URI。

当你部署应用后，发现运行变慢时，性能测试可以帮助隔离问题。而且，一旦隔离出问题，让测试保留在原处有助于防止问题再次出现。

与数据库相关的性能问题就是这类问题的常见例子。一个应用可能正常运行数月，然后有人向数据库添加了一个索引。虽然该索引有助于解决某个特定问题，但它也会带来一个意想不到的副作用：显著拖慢应用的另一个部分。

在过去（没错，那不过是短短几年前），我们曾建议创建单元测试来监控性能问题。其思路是，当性能开始超过某个预设限制时，这些测试会给你一个早期预警：你在测试期间就能发现，而不是在部署之后。事实上，我们仍然建议这样做，稍后我们会提到。然而，这种孤立的性能测试并非全貌，在本节末尾，我们还会对其他类型的性能测试提出建议。

让我们从一个略带人为的场景开始。我们需要知道商店控制器能否在三秒内处理创建 100 个订单。我们希望针对一个包含 1000 个产品的数据库进行测试（因为我们怀疑产品数量可能很重要）。我们该如何为此编写测试？

为了创建所有这些产品，我们使用一个动态 fixture：

```
Download depot_r/test/fixtures/performance/products.yml

<% 1.upto(1000) do |i| %>
product_<%= i %>:
  id: <%= i %>
  title: Product Number <%= i %>
  description: My description
  image_url: product.gif
  price: 1234
<% end %>
```

请注意，我们将这个 fixture 文件放在了 fixtures 目录的 performance 子目录中。fixture 文件的名称必须与数据库表名匹配，因此我们不能在同一目录下为 products 表放置多个 fixture。我们希望将常规 fixtures 目录保留给常规单元测试使用的测试数据，所以只需在子目录中放置另一个 products.yml 文件。

注意，在测试中，我们从 1 循环到 1000。一开始很容易想使用 `1000.times do |i|...`，但这行不通。`times` 方法会生成从 0 到 999 的数字，如果我们把 0 作为 id 值传给 SQLite 3，它会忽略该值并使用自动生成的键值。这可能会导致键冲突。

浮点数秒数）。在我们的例子中，该代码块使用我们创建的 1000 个产品中的 100 个产品（按逆序，只是为了增加一点变化）来创建 100 个订单。

你会发现代码还有一个棘手的特性：

```
Download depot_r/test/performance/order_speed_test.rb
@controller.logger.silence do
end
```

默认情况下，Rails 会将其处理这 100 个订单所做的工作全部记录到日志文件（test.log）中。事实证明，这是相当大的开销，因此我们将记录操作放在一个日志被静默的代码块中，以屏蔽日志记录。在我的 G5 上，这能使执行该代码块所需的时间减少约 30%。稍后我们会看到，在实际生产代码中，还有更好的方式来屏蔽日志记录。

让我们运行性能测试：

```
depot> ruby -I test test/performance/order_speed_test.rb
Started
.
Finished in 1.849848 seconds.
1 tests, 102 assertions, 0 failures, 0 errors
```

它在测试环境中运行正常。然而，性能问题通常会在生产环境中暴露出来，而那里正是我们希望能够监控应用的地方。幸运的是，在那个环境中我们也有一些选择。

#### 性能分析与基准测试

让我们运行性能分析器来深入探究：

```
depot> ruby script/performance/profiler 'User.encrypted_password("secret", "salt")'
Loading Rails...
Using the standard Ruby profiler.
% cumulative self total
time seconds seconds calls ms/call ms/call name
78.65 58.63 58.63 1 58630.00 74530.00 Integer#times
21.33 74.53 15.90 1000000 0.02 0.02 Math.sin
1.25 75.46 0.93 1 930.00 930.00 Profiler__.start_profile
0.01 75.47 0.01 12 0.83 0.83 Symbol#to_sym
... 
0.00 75.48 0.00 1 0.00 0.00 Hash#update
```

这很奇怪——该方法似乎将大部分时间花在了 `times` 和 `sin` 方法上。让我们看看源代码：

```
def self.encrypted_password(password, salt)
  1000000.times { Math.sin(1) }
  string_to_hash = password + salt
  Digest::SHA1.hexdigest(string_to_hash)
end
```

哎呀！那个循环是我在手动测试时为了放慢速度而添加的，部署应用前我一定忘记删除它了。看来我一个星期不能用红色订书机了。

到目前为止所描述的方法都是无侵入性的，因为它们不涉及修改应用。这只剩下生产环境中真正棘手的问题。Rails 对此也有解决方案：ActionController 有一个名为 `benchmark` 的方法，它可以度量并记录单个代码块的执行时长。默认情况下，`benchmark` 会屏蔽代码块内的日志记录，除非将 `use_silence` 设置为 `false`。此外，仅当记录器的当前级别与 `log_level` 匹配时，`benchmark` 才会记录基准测试。这使得在生产环境中加入 `benchmark` 语句变得容易，而且这些语句的开销很低，因为只有当日志级别足够低时才会执行 `benchmark`。

ActionView::Helpers::BenchmarkHelper 为我们提供了类似的 `benchmark` 辅助方法，可在视图中使用。

无论如何，请记住日志文件。它们是宝贵的时间信息金矿。

#### 14.6 使用模拟对象

在某个时候，我们需要向 Depot 应用添加代码，从我们亲爱的客户那里实际收款。所以，想象一下我们已经填好了所有必要的文书，将信用卡号变成银行账户中的真金白银。然后我们在文件中创建了一个 PaymentGateway 类。





method. 这意味着我们不必为 PaymentGateway  stub 出所有的方法，只需 stub 我们想要在测试运行时重新定义的方法即可。在本例中，新的 collect 方法仅返回一个假响应。

有了这个文件，StoreController 将使用 stub 的 PaymentGateway 类。这是由于 Rails 安排搜索路径优先包含 mock 路径——文件 test/mocks/test/payment_gateway.rb 会被加载，而不是 lib/payment_gateway.rb。

就这么简单。通过使用 stubs，我们可以简化测试并集中精力测试最重要的内容。而 Rails 让这一切变得毫不费力。

##### Stubs vs. Mocks

你可能已经注意到，前一节对这些假类和方法使用 *stub* 术语，但 Rails 却将它们放在 test/mocks 的子目录中。Rails 在这里对术语的使用有些随意。它所称的 mocks 实际上只是 stubs：被伪造的代码片段，可以消除对某些资源的需求。

然而，如果你真的想要 mock 对象——即测试它们被如何使用，并在使用不当的情况下引发错误的对象，请查看 Flex Mock，⁹ Jim Weirich 的 Ruby mock 对象库，或 James Mead 的 Mocha，¹⁰。

#### What We Just Did

我们为 Depot 应用编写了一些测试，但并未测试所有内容。不过，有了我们现在所知的知识，我们本可以测试所有内容。的确，Rails 提供了出色的支持来帮助你编写良好的测试。尽早且频繁地测试——你会在 bug 有机会潜逃之前将其抓住，你的设计会得到改进，你的 Rails 应用也会因此感谢你。

## Part III

## Working with the Rails Framework

### Chapter 15

### Rails in Depth

在完成了我们的 Depot 项目后，现在似乎是深入了解 Rails 的好时机。在本书的剩余部分，我们将按主题逐一讲解 Rails（基本上就是按模块逐一讲解）。

本章为后续内容奠定基础。它讲述了理解其余内容所需的高层知识：目录结构、配置、环境、支持类以及调试提示。但首先，我们必须问一个重要问题....

#### 15.1 So, Where's Rails?

Rails 的一个有趣之处在于它是如何组件化的。从开发者的角度来看，你花费所有时间处理 Active Record 和 Action View 等高层模块。确实有一个名为 Rails 的组件，但它位于其他组件之下，默默地协调它们的行为并使它们无缝协同工作。没有 Rails 组件，几乎不会发生什么事。但与此同时，只有很小一部分底层基础设施与开发者日常工作相关。我们将在本章剩余部分介绍相关部分。

#### 15.2 Directory Structure

Rails 假设了某种运行时的目录布局。如果我们运行命令 rails my_app，就会得到下一页图 15.1 所示的顶层目录。让我们看看每个目录包含什么内容（尽管不一定按顺序）。config 和 db 目录需要更详细的讨论，因此每个目录都有自己的章节。

顶层目录还包含一个 Rakefile。你可以用它来运行测试、创建文档、提取当前 schema 的结构等。

my_app/
README  安装和使用信息。
Rakefile  构建脚本。
app/  模型、视图和控制器文件放在这里。
config/  配置和数据库连接参数。
db/  Schema 和迁移信息。
doc/  自动生成的文档。
lib/  共享代码。
log/  应用产生的日志文件。
public/  可通过 Web 访问的目录。你的应用由此运行。
script/  实用脚本。
test/  单元、功能和集成测试、fixtures 和 mocks。
tmp/  运行时临时文件。
vendor/  导入的代码。

Figure 15.1: Result of rails my_app command

在提示符下输入 rake --tasks 可查看完整列表。输入 rake --describe task 可查看特定任务的更完整描述。

##### app/ and test/

我们的大部分工作都在 app 和 test 目录中进行。应用的主要代码位于 app 目录下，如下一页图 15.2 所示。我们将在本书后面更详细地介绍 Active Record、Action Controller 和 Action View 时，再谈论 app 目录的结构，而我们已经在第 14 章 Task T: Testing，第 210 页回顾了 test。

##### doc/

doc 目录用于应用文档。它使用 RDoc 生成。如果你运行 rake doc:app，你将在目录 doc/app 中得到 HTML 文档。你可以通过编辑文件 doc/README_FOR_APP 为此文档创建一个特殊的首页。我们商店应用的顶层文档如图 12.3，第 192 页所示。

![](img/a160fc3a330a0b3b2a764d41d614e688_258_0.png)

Figure 15.2: The app directory

##### lib/

lib 目录存放不适合 neatly 放入模型、视图或控制器的应用代码。例如，你可能编写了一个库来创建 PDF 收据，供商店客户下载。¹ 这些收据直接从控制器发送到浏览器（使用 send_data 方法）。创建这些 PDF 收据的代码自然会放在 lib 目录中。

lib 目录也是放置在模型、视图或控制器之间共享的代码的好地方。也许你需要一个库来验证信用卡号码的校验和，执行某些财务计算，或计算复活节日期。任何不是直接模型、视图或控制器的东西都应放入 lib。

> 1. ...which we did in the new Pragmatic Programmer store.

不要觉得必须把一堆文件直接塞进 lib 目录本身。大多数有经验的 Rails 开发者会创建子目录来在 lib 下对相关功能进行分组。例如，在 Pragmatic Programmer 商店中，生成收据、用于运输的报关文件以及其他 PDF 格式文档的代码都放在目录 lib/pdf_stuff 中。

一旦你在 lib 目录中有了文件，你就可以在应用的其他部分使用它们。如果文件包含类或模块，并且文件名使用类或模块名称的小写形式，那么 Rails 会自动加载该文件。例如，我们可能在目录 lib/pdf_stuff 中的文件 receipt.rb 中有一个 PDF 收据写入器。只要我们的类名为 PdfStuff::Receipt，Rails 就能自动找到并加载它。

对于那些无法满足自动加载条件的库，你可以使用 Ruby 的 require 机制。如果文件在 lib 目录中，你可以直接按名称 require 它。例如，如果我们的复活节计算库在文件 lib/easter.rb 中，我们可以在任何模型、视图或控制器中使用以下方式包含它：

```
require "easter"
```

如果库位于 lib 的子目录中，请记住在 require 语句中包含该目录的名称。例如，要包含一个用于航空邮件的运费计算，我们可能会添加以下行：

```
require "shipping/airmail"
```

##### Rake Tasks

你还会在 lib 下找到一个空的 tasks 目录。你可以在这里编写自己的 Rake 任务，从而为项目添加自动化。这不是一本关于 Rake 的书，所以我们在这里不会深入探讨，但这里有一个简单示例。Rails 提供了一个 Rake 任务来告诉你已执行的最新迁移。

但可能有助于看到 *所有* 已执行的迁移列表。我们将编写一个 Rake 任务来打印 schema_migration 表中列出的版本。这些任务是 Ruby 代码，但需要放在扩展名为 .rake 的文件中。我们将它命名为 db_schema_migrations.rake：

```
namespace :db do
  desc "Prints the migrated versions"
  task :schema_migrations => :environment do
    puts ActiveRecord::Base.connection.select_values(
      'select version from schema_migrations order by version'
    )
  end
end
```




###### generate

一个代码生成器。开箱即用，它会创建控制器、邮件处理器、模型、脚手架和 Web 服务。你也可以从 Rails 网站下载额外的生成器模块。² 运行 `generate` 不带参数可查看特定生成器的使用信息，例如：`ruby script/generate migration`。

###### plugin

帮助你安装和管理插件——扩展 Rails 功能的功能块。

###### runner

在 Web 上下文之外执行应用程序中的方法。你可以用它从 cron 作业中调用缓存过期方法或处理传入的电子邮件。

###### server

使用 Mongrel（如果你的机器上可用）或 WEBrick 在自包含的 Web 服务器中运行你的 Rails 应用程序。我们在开发 Depot 应用程序期间一直在使用它。

`script` 目录包含两个子目录，每个子目录都包含更专业的脚本。目录 `script/process` 包含三个脚本，可帮助控制已部署的 Rails 应用程序。我们将在部署章节中讨论这些。目录 `script/performance` 包含三个脚本，可帮助你了解应用程序的性能特征。

###### benchmarker

为应用程序中的一个或多个方法生成性能数据。

###### profiler

创建应用程序中一段代码的运行时分析摘要。

###### request

创建应用程序处理的 URI 请求的运行时分析摘要。

###### tmp/

Rails 将临时文件保存在 `tmp` 目录中也就不足为奇了。你会在这里找到缓存内容、会话和套接字的子目录。

2. http://wiki.rubyonrails.org/rails/pages/AvailableGenerators

##### 将应用程序绑定到 Gem 版本

在 `config` 目录中 `environment.rb` 的最顶部，你通常会找到类似这样的行：

```
RAILS_GEM_VERSION = "2.2.2"
```

如果此行存在，Rails 在应用程序加载时会查询系统上安装的 gem 并安排加载正确的版本（本例中为 2.2.2）。

尽管这种方法很简单，但它有一个主要缺点：如果部署到未包含指定 Rails 版本的机器上，你的应用程序将无法运行。为了更稳健的部署，最好将 Rails 冻结到你的 `vendor` 目录中。这会将 Rails 框架复制到你的应用程序中。其他 Ruby 库仍会全局访问。

如果你想恢复使用系统范围的 Rails 版本，可以删除 `vendor/rails` 目录或运行以下命令：

```
depot> rake rails:unfreeze
```

这些 Rake 任务会接受 Rails 的一个版本（当前版本或特定标签）并将其冻结到你的 `vendor` 目录中。这比让项目随着核心团队每天的更改而动态更新风险更小，但作为交换，如果你需要获取最后时刻的功能，就需要解冻并重新冻结。

##### 使用 Edge Rails

除了将 Rails 的当前 gem 版本冻结到应用程序中，你还可以将应用程序链接到 Rails 自己的开发存储库中的最新快照（Rails 核心开发者提交代码的地方）。这称为 Edge Rails。

为此，我们再次使用 Rake 任务：

```
depot> rake rails:freeze:edge
```

#### 15.3 Rails 配置

Rails 运行时配置由 `config` 目录中的文件控制。这些文件与运行时环境的概念协同工作。

- `app/controllers` 目录及其子目录。
- `app/models` 目录以及其所有以下划线或小写字母开头的子目录。
- `vendor` 目录和每个插件子目录中的 `lib`。
- 目录 `app`、`app/helpers`、`app/services`、`config` 和 `lib`。

每个目录仅在存在时才会被添加到加载路径中。

此外，Rails 会检查应用程序中是否存在 `vendor/rails` 目录。如果存在，它会安排从那里加载自身，而不是从共享库代码加载。

##### 配置参数

你通过在 Rails 模块中设置各种选项来配置 Rails。通常你会在 `environment.rb` 的末尾（如果你希望设置适用于所有环境）或 `environments` 目录中的环境特定文件中进行这些设置。

我们在第 680 页的附录 B 中提供了所有这些配置参数的列表。

#### 15.4 命名约定

Rails 新手有时会对它自动处理命名的方式感到困惑。他们惊讶于他们调用模型类为 `Person`，Rails 却 somehow 知道去查找名为 `people` 的数据库表。本节旨在记录这种隐式命名的工作方式。

这里的规则是 Rails 使用的默认约定。你可以使用 Rails 类中的适当声明覆盖所有这些约定。

##### 混合大小写、下划线和复数

我们经常使用短语来命名变量和类。在 Ruby 中，约定是变量名全部为小写，单词之间用下划线分隔。类和模块的命名方式不同：没有下划线，每个词的首字母都大写（包括第一个）。（我们称之为混合大小写，原因显而易见。）这些约定导致了诸如 `order_status` 这样的变量名和诸如 `LineItem` 这样的类名。

Rails 采用此约定并以两种方式扩展它。首先，它假设数据库表名像变量名一样使用小写字母，单词之间用下划线分隔。Rails 还假设表名始终是复数。这导致了诸如 `orders` 和 `third_parties` 这样的表名。

在另一个维度上，Rails 假设文件以小写和下划线命名。

Rails 利用对命名约定的了解自动转换名称。例如，你的应用程序可能包含处理行项目的模型类。你会使用 Ruby 命名约定定义该类，称其为 `LineItem`。从此名称，Rails 会自动推断出以下内容：

- 对应的数据库表将称为 `line_items`。这是类名，转换为小写，单词之间用下划线并复数化。
- Rails 也会知道在 `app/models` 目录中名为 `line_item.rb` 的文件中查找类定义。

Rails 控制器有额外的命名约定。如果我们的应用程序有一个商店控制器，则会发生以下情况：

- Rails 假设类名为 `StoreController`，并且它位于 `app/controllers` 目录中名为 `store_controller.rb` 的文件中。
- 它还假设有一个名为 `StoreHelper` 的辅助模块，位于 `app/helpers` 目录中的文件 `store_helper.rb` 中。
- 它将在 `app/views/store` 目录中查找此控制器的视图模板。
- 它默认会将这些视图的输出包装在 `app/views/layouts` 目录中文件 `store.html.erb` 或 `store.xml.erb` 中包含的布局模板中。

所有这些约定都显示在下一页的图 15.3 中。

还有一个额外的变化。在正常的 Ruby 代码中，你必须使用 `require` 关键字在引用类和模块之前包含 Ruby 源文件。因为 Rails 知道文件名和类名之间的关系，所以在 Rails 应用程序中通常不需要 `require`。相反，你第一次引用一个未知类或模块时，Rails 会使用命名约定将类名转换为文件名，并在幕后尝试加载该文件。净效果是你通常可以引用（例如）模型类的名称，该模型将被自动加载到你的应用程序中。

##### 将控制器分组到模块中

到目前为止，我们所有的控制器都位于 `app/controllers` 目录中。有时将此安排添加更多结构会很方便。例如，我们的商店最终可能有许多执行相关但不相交的管理员功能的控制器。为了不污染顶级命名空间，我们可能会选择将它们分组到单个 `admin` 命名空间中。





##### 模型命名

| 方面 | 值 |
| --- | --- |
| 表 | line_items |
| 文件 | app/models/line_item.rb |
| 类 | LineItem |

##### 控制器命名

| 方面 | 值 |
| --- | --- |
| URL | http://../store/list |
| 文件 | app/controllers/store_controller.rb |
| 类 | StoreController |
| 方法 | list |
| 布局 | app/views/layouts/store.html.erb |

##### 视图命名

| 方面 | 值 |
| --- | --- |
| URL | http://../store/list |
| 文件 | app/views/store/list.html.erb (or .builder or .rjs) |
| 辅助模块 | module StoreHelper |
| 文件 | app/helpers/store_helper.rb |

图 15.3：命名约定摘要

Rails 使用简单的命名约定来实现这一点。如果传入的请求具有名为（例如）`admin/book` 的控制器，Rails 将在目录 `app/controllers/admin` 中查找名为 `book_controller` 的控制器。也就是说，控制器名称的最后一部分始终解析为名为 `name_controller.rb` 的文件，而任何前导路径信息都将用于在 `app/controllers` 目录开始的子目录中导航。

假设我们的程序有两个这样的控制器组（例如，`admin/xxx` 和 `content/xxx`），并且这两个组都定义了 book 控制器。那么在 `app/controllers` 的 `admin` 和 `content` 子目录中都会有一个名为 `book_controller.rb` 的文件。这两个控制器文件都将定义一个名为 `BookController` 的类。如果 Rails 不采取进一步措施，这两个类就会冲突。

为了解决这个问题，Rails 假定 `app/controllers` 目录的子目录中的控制器位于以子目录命名的 Ruby 模块中。因此，`admin` 子目录中的 book 控制器将这样声明：

```
class Admin::BookController < ActionController::Base
  # ...
end
```

### David 说。 . .

###### 为什么表要用复数？

因为在对话中听起来不错。真的。“从 products 中选择一个 Product。” 以及 “Order has_many :line_items。”

其意图是通过创建一个可供双方共享的领域语言来弥合编程和对话之间的差距。拥有这样的语言意味着减少了原本会混淆产品描述与客户讨论的心理翻译，而实际上它被实现为商品主体。这些沟通差距必然会导致错误。

如果遵循标准约定，Rails 会免费为您提供大部分配置。开发人员因此会因做正确的事情而获得奖励，所以这与其说是放弃“你的方式”，不如说是免费获得生产力。

content 子目录中的 book 控制器将位于 Content 模块中：

```
class Content::BookController < ActionController::Base
  # ...
end
```

因此，这两个控制器在应用程序内部保持分离。

这些控制器的模板出现在 `app/views` 的子目录中。因此，对应于此请求的视图模板：

```
http://my.app/admin/book/edit/1234
```

将位于此文件：

```
app/views/admin/book/edit.html.erb
```

你会很高兴知道控制器生成器理解模块中控制器的概念，并允许你使用以下这样的命令创建它们：

```
myapp> ruby script/generate controller Admin::Book action1 action2 ...
```

这种控制器命名模式在我们开始生成 URL 以链接操作时会有影响。我们将在第 440 页开始讨论这个问题。

#### 15.5 Rails 中的日志记录

Rails 已将日志记录内置到框架中。或者，更准确地说，Rails 向 Rails 应用程序中的所有代码公开了一个 Logger 对象。

Logger 是一个简单的日志框架，随最近版本的 Ruby 一起提供。（你可以通过在命令提示符下输入 `ri Logger` 或查阅 Programming Ruby [TFH05] 中的标准库文档获取更多信息。）就我们的目的而言，知道我们可以以 warning、info、error 和 fatal 级别生成日志消息就足够了。然后我们可以决定（可能在环境文件中）将哪些级别的日志写入日志文件。

```
logger.warn("I don't think that's a good idea")
logger.info("Dave's trying to do something bad")
logger.error("Now he's gone and broken it")
logger.fatal("I give up")
```

在 Rails 应用程序中，这些消息会写入 log 目录中的文件。使用的文件取决于应用程序运行的环境。开发应用程序将记录到 `log/development.log`，测试中的应用程序记录到 `test.log`，生产应用程序记录到 `production.log`。

#### 15.6 调试提示

错误会发生。即使在 Rails 应用程序中也是如此。本节提供了一些追踪它们的提示。

首先，也是最重要的，编写测试！Rails 使编写单元测试和功能测试变得容易（如我们在第 14 章，任务 T：测试，第 210 页所见）。使用它们，你会发现你的错误率大幅下降。你还将降低一个月前编写的代码突然出现错误的风险。测试是廉价的保险。

测试告诉你某事是否有效，并帮助你隔离有问题的代码。有时，原因并不立即显现。

如果问题出在模型中，你可能可以通过在 Web 应用程序之外运行有问题的类来追踪它。`script/console` 脚本允许你在 irb 会话中启动 Rails 应用程序的一部分，让你尝试方法。以下是我们使用控制台更新产品价格的会话：

```
depot> ruby script/console
Loading development environment.
irb(main):001:0> pr = Product.find(:first)
=> #<Product:0x248acd0 @attributes={"image_url"=>"/images/sk..."
irb(main):002:0> pr.price
=> 29.95
irb(main):003:0> pr.price = 34.95
=> 34.95
irb(main):004:0> pr.save
=> true
```

日志记录和跟踪是理解复杂应用程序动态的绝佳方式。你会在开发日志文件中找到大量信息。当发生意外情况时，这可能是你首先应该查看的地方。检查 Web 服务器日志是否存在异常也很有价值。如果你使用 WEBrick 进行开发，这将在你发出 `script/server` 命令的控制台上滚动显示。

你可以使用上一节描述的 Logger 对象向日志添加自己的消息。有时日志文件太忙，难以找到你添加的消息。在这种情况下，如果你使用 WEBrick，写入 STDERR 将导致你的消息出现在 WEBrick 控制台上，与正常的 WEBrick 跟踪混合在一起。

如果页面显示的信息不正确，你可能想转储从控制器传入的对象。`debug` 辅助方法对此很有用。它很好地格式化对象，并确保其内容是有效的 HTML。

```
<h3>Your Order</h3>

<%= debug(@order) %>

<div id="ordersummary">
  ...
</div>
```

最后，对于那些似乎怎么也修不好的问题，你可以祭出大招，让 irb 指向你的正在运行的应用程序。这通常仅适用于开发环境中的应用程序。

要使用断点，请按以下步骤操作：

1. 在你希望应用程序首次停止的代码点插入对方法 `debugger` 的调用。
2. 在一个方便的控制台上，使用 `-u` 或 `--debugger` 参数启动服务器，如下所示。³

   ```
   depot> ruby script/server -u
   => Booting WEBrick...
   => Debugger enabled
   => Rails application started on http://0.0.0.0:3000
   ```

3. 使用浏览器，触发你的应用程序以使其命中 `debugger` 方法。当它这样做时，运行 `script/server` 的控制台

³ 你需要安装 ruby-debug 才能以调试模式运行服务器。使用 gems，请使用 `gem install ruby-debug`。

### 第 16 章：Active Support

Active Support 是一组由所有 Rails 组件共享的库。其中大部分内容 intended for Rails 的内部使用。然而，Active Support 还以有趣且有用的方式扩展了 Ruby 的一些内置类。在本节中，我们将快速列出这些扩展中最受欢迎的。

我们还将简要介绍 Ruby 和 Rails 如何处理 Unicode 字符串，从而能够创建正确处理国际文本的网站。

#### 16.1 一般可用的扩展

正如我们在第 563 页查看 Ajax 时会看到的，有时将 Ruby 对象转换为中性形式以允许它们发送到远程程序（通常是用户浏览器中运行的 JavaScript）是有用的。Rails 为 Ruby 对象扩展了两种方法，`to_json` 和 `to_yaml`。这些方法将对象转换为 JavaScript Object Notation（JSON）和 YAML（Rails 配置和 fixture 文件中使用的相同记法）：

```
require 'rubygems'
require 'activesupport'

# 为演示目的，创建一个具有两个属性的 Ruby 结构
Rating = Struct.new(:name, :ratings)
rating = Rating.new("Rails", [ 10, 10, 9.5, 10 ])

# 并以两种方式序列化该结构的对象...
puts rating.to_json      #=> ["Rails", [10, 10, 9.5, 10]]
puts rating.to_yaml      #=> --- !ruby/struct:Rating
                          name: Rails
                          ratings:
                          - 10
                          - 10
                          - 9.5
                          - 10
```



# 大卫说……

# 为什么扩展基类不会导致世界末日

第一次看到 5.months + 30.minutes 时所产生的敬畏感，通常很快就会被一种恐慌状态所取代。如果任何人都能随意改变整数的工作方式，这难道不会导致一个完全无法维护、如地狱般的意大利面条式代码泥潭吗？是的，如果每个人都一直这么干，确实会。但他们没有，所以也不会。

不要将 Active Support 想象成一组对 Ruby 语言的随意扩展，仿佛谁都可以往字符串类里塞入自己的私房特性。把它想象成一种所有 Rails 程序员都通用的 Ruby 方言。因为 Active Support 是 Rails 的必需组成部分，你始终可以放心，在任何一个 Rails 应用中，5.months 都能正常工作。这就消解了“一千个人有一千种 Ruby 方言”的问题。

在语言扩展方面，Active Support 让我们两者兼得。它属于情境化的标准化。

此外，所有 Active Record 对象和所有哈希都支持 to_xml 方法。我们在第 187 页的 12.1 节“自动生成 XML”中已经见过。

为了更容易判断对象是否为空，Rails 为所有 Ruby 对象扩展了 blank? 方法。它对于 nil 和 false 始终返回 true，对于数字和 true 始终返回 false。对于其他所有对象，当该对象为空时返回 true。（只包含空格的字符串被视为空字符串。）

```
puts [ ].blank?        #=> true
puts { 1 => 2 }.blank? #=> false
puts " cat ".blank?   #=> false
puts "".blank?        #=> true
puts " ".blank?       #=> true
puts nil.blank?        #=> true
```

#### 16.2 枚举与数组

由于 Web 应用要花大量时间处理集合，Rails 为 Ruby 的 Enumerable 混入模块增添了一些魔法。

group_by 方法将集合划分为若干组值。做法是：对集合中的每个元素调用一次块，并将块返回的结果作为分组键。最终得到一个哈希，其中每个键都关联着来自原集合的一个元素数组。

```
[1,2,3,4,5,6,7].in_groups_of(3, "X") {|slice| puts slice.inspect}
    #=> [1, 2, 3]
        [4, 5, 6]
        [7, "X", "X"]
```

尽管 Ruby 一直为数组提供 first 和 last 方法，Rails 还增加了 second、third、fourth、fifth 以及 forty_two。此外，还提供了一些有助于从数组中切取片段的方法。from 返回从给定索引开始的数组尾部；to 返回从开头到给定索引（含）的数组头部。rand 从数组中返回一个随机元素。最后，split 与 String 上的同名方法类似，可以根据分隔值或可选块的结果来拆分数组。

#### 16.3 哈希

哈希也没有被冷落；它们同样获得了一大堆有用的方法。按照 Ruby 的惯例，以感叹号（!）结尾的方法具有破坏性；换言之，它们会作为副作用更新调用对象。

reverse_merge 和 reverse_merge! 的行为与 Ruby 的 merge 类似，区别在于调用哈希中的键优先于传入参数哈希中的键。这对于用默认值初始化选项哈希特别有用。

deep_merge 和 deep_merge! 返回一个新哈希，将两个哈希递归合并。

diff 返回一个新哈希，表示两个哈希之间的差异。

except 和 except! 返回一个不包含给定键的新哈希。

slice 和 slice! 返回一个只包含给定键的新哈希。

stringify_keys 和 stringify_keys! 将所有键转换为字符串。

symbolize_keys 和 symbolize_keys! 将所有键转换为符号。

#### 16.4 字符串扩展

Ruby 1.8 的新手常常会惊讶地发现，像 string[2] 这样对字符串进行索引返回的是整数，而不是单字符字符串。这个问题在 Ruby 1.9 中已修复，但就目前而言，大多数人仍然在使用 Ruby 1.8。

Rails 以多种方式缓和了这一过渡。首先，它为字符串添加了一些辅助方法，从而带来更自然的行为：

```
string = "Now is the time"
puts string.at(2)      #=> "w"
puts string.from(8)    #=> "he time"
puts string.to(8)      #=> "Now is th"
```

有些单词是不可数的（比如我们程序中的 bug）。你可以通过 uncountable 方法告诉词形变化器：

```
ActiveSupport::Inflector.inflections do |inflect|
  inflect.uncountable("air", "information", "water")
end
>> "water".pluralize      #=> "water"
>> "water".singularize   #=> "water"
```

#### 16.5 对数字的扩展

你可以对浮点数进行舍入：

```
puts (1.337).round_with_precision(2) #=> 1.34
```

整数获得了 even? 和 odd? 两个实例方法。你也可以使用 ordinalize 获取整数的序数形式：

```
puts 3.ordinalize    #=> "3rd"
puts 321.ordinalize  #=> "321st"
```

所有数值对象都获得了一组缩放方法。单数和复数形式都受支持。

```
puts 20.bytes       #=> 20
puts 20.kilobytes   #=> 20480
puts 20.megabytes   #=> 20971520
puts 20.gigabytes   #=> 21474836480
puts 20.terabytes   #=> 219900232555520
puts 20.petabytes   #=> 225179998136852480
puts 1.exabyte      #=> 1152921504606846976
```

还有一些基于时间的缩放方法。这些方法将接收者转换为相应的秒数。months 和 years 方法并不精确——假设一个月为 30 天，一年为 365 天。不过，Time 类已经扩展出一些方法，可以为你提供准确的相对日期（参见紧随其后的小节中的描述）。同样，单数和复数形式都受支持：

```
puts 20.seconds     #=> 20
puts 20.minutes     #=> 1200
puts 20.hours       #=> 72000
puts 20.days        #=> 1728000
puts 20.weeks       #=> 12096000
puts 20.fortnights  #=> 24192000
puts 20.months      #=> 51840000
puts 20.years       #=> 630720000
```

你还可以使用 ago 和 from_now 方法（或它们各自的别名 until 和 since）来计算相对于某个时间（默认为 Time.now）的时间。

```
puts Time.now                 #=> Thu May 18 23:29:14 CDT 2006
puts 20.minutes.ago           #=> Thu May 18 23:09:14 CDT 2006
puts 20.hours.from_now        #=> Fri May 19 19:29:14 CDT 2006
puts 20.weeks.from_now        #=> Thu Oct 05 23:29:14 CDT 2006
puts 20.months.ago            #=> Sat Sep 25 23:29:16 CDT 2004
puts 20.minutes.until("2006-12-25 12:00:00".to_time)
                             #=> Mon Dec 25 11:40:00 UTC 2006
puts 20.minutes.since("2006-12-25 12:00:00".to_time)
                             #=> Mon Dec 25 12:20:00 UTC 2006
```

怎么样，很酷吧？而且还有更酷的……

#### 16.6 时间与日期扩展

Time 类获得了许多有用的方法，帮助你计算相对时间和日期，并格式化时间字符串。其中许多方法都有别名；详情请参阅 API 文档。

```
now = Time.now
puts now                         #=> Thu May 18 23:36:10 CDT 2006
puts now.to_date                 #=> 2006-05-18
puts now.to_s                    #=> Thu May 18 23:36:10 CDT 2006
puts now.to_s(:short)            #=> 18 May 23:36

puts now.to_s(:long)             #=> May 18, 2006 23:36
puts now.to_s(:db)               #=> 2006-05-18 23:36:10
puts now.to_s(:rfc822)           #=> Thu, 18 May 2006 23:36:10 -0500
puts now.ago(3600)               #=> Thu May 18 22:36:10 CDT 2006
puts now.at_beginning_of_day     #=> Thu May 18 00:00:00 CDT 2006

puts now.at_beginning_of_month  #=> Mon May 01 00:00:00 CDT 2006
puts now.at_beginning_of_week   #=> Mon May 15 00:00:00 CDT 2006
puts now.at_beginning_of_quarter#=> Sat Apr 01 00:00:00 CST 2006
puts now.at_beginning_of_year   #=> Sun Jan 01 00:00:00 CST 2006
puts now.at_midnight             #=> Thu May 18 00:00:00 CDT 2006

puts now.change(:hour => 13)     #=> Thu May 18 13:00:00 CDT 2006
puts now.last_month              #=> Tue Apr 18 23:36:10 CDT 2006
puts now.last_year               #=> Wed May 18 23:36:10 CDT 2005
puts now.midnight                #=> Thu May 18 00:00:00 CDT 2006
puts now.monday                  #=> Mon May 15 00:00:00 CDT 2006

puts now.months_ago(2)           #=> Sat Mar 18 23:36:10 CDT 2006
puts now.months_since(2)         #=> Tue Jul 18 23:36:10 CDT 2006
puts now.next_week               #=> Mon May 22 00:00:00 CDT 2006
puts now.next_year               #=> Fri May 18 23:36:10 CDT 2007
puts now.seconds_since_midnight  #=> 84970.423472

puts now.since(7200)             #=> Fri May 19 01:36:10 CDT 2006
puts now.tomorrow                #=> Fri May 19 23:36:10 CDT 2006
puts now.years_ago(2)            #=> Tue May 18 23:36:10 CDT 2004
puts now.years_since(2)          #=> Sun May 18 23:36:10 CDT 2008
puts now.yesterday               #=> Wed May 17 23:36:10 CDT 2006
```


puts now.advance(:days => 30)      #=> Sat Jun 17 23:36:10 CDT 2006
puts Time.days_in_month(2)         #=> 28
puts Time.days_in_month(2, 2000)   #=> 29
puts now.xmlschema                 #=> "2006-05-18T23:36:10-06:00"

Rails 2.1 引入了时区支持。你可以在 config/environment.rb 中设置默认时区：

config.time_zone = 'UTC'

在动作（action）中，你可以覆盖时区并将任何时间转换为指定时区：

Time.zone = 'Eastern Time (US & Canada)'
puts Time.now.in_time_zone

Active Support 还包含一个 TimeZone 类。TimeZone 对象封装了时区的名称和偏移量。该类包含世界时区列表。详见 Active Support RDoc。

Rails 2.2 引入了三个查询给定时间的方法：past?、today? 和 future? 分别查询给定时间是否早于当前时间、是否在今天日期，或者是否在将来。

Date 对象也获得了一些有用的方法：

date = Date.today
puts date.tomorrow                 #=> "Fri, 19 May 2006"
puts date.yesterday                #=> "Wed, 17 May 2006"
puts date.current                  #=> "Thu, 18 May 2006"

当设置了 config.time_zone 时，current 返回 Time.zone.today；否则，它只返回 Date.today：

puts date.to_s                     #=> "2006-05-18"
puts date.xmlschema                #=> "2006-05-18T00:00:00-06:00"
puts date.to_time                  #=> Thu May 18 00:00:00 CDT 2006
puts date.to_s(:short)             #=> "18 May"
puts date.to_s(:long)              #=> "May 18, 2006"
puts date.to_s(:db)                #=> "2006-05-18"

最后一个将日期转换为你的应用程序当前使用的默认数据库可接受的字符串。你可能已经注意到 Time 类也有类似的扩展，用于以数据库特定的格式格式化 datetime 字段。

你可以为日期和时间格式化添加自己的扩展。例如，你的应用程序可能需要显示序数日期（一年中的第几天）。Ruby 的 Date 和 Time 库都支持 strftime 方法来格式化日期，所以你可以使用类似这样的代码：

>> d = Date.today
=> #<Date: 4907769/2,0,2299161>
>> d.to_s
=> "2006-05-29"
>> d.strftime("%y-%j")
=> "06-149"

不过，你可能希望通过扩展日期的 to_s 方法封装这种格式化。在你的 environment.rb 文件中，添加类似下面的一行：

ActiveSupport::CoreExtensions::Date::Conversions::DATE_FORMATS.merge!(
  :ordinal => "%Y-%j"
)

现在你可以这么说：

any_date.to_s(:ordinal)    #=> "2006-149"

你也可以扩展 Time 类的字符串格式化：

ActiveSupport::CoreExtensions::Time::Conversions::DATE_FORMATS.merge!(
  :chatty => "It's %I:%M%p on %A, %B %d, %Y"
)
Time.now.to_s(:chatty)    #=> "It's 12:49PM on Monday, May 29, 2006"

String 类还添加了两个有用的与时间相关的方法。to_time 和 to_date 方法分别返回 Time 和 Date 对象：

puts "2006-12-25 12:34:56".to_time    #=> Mon Dec 25 12:34:56 UTC 2006
puts "2006-12-25 12:34:56".to_date    #=> 2006-12-25

#### 16.7 Ruby 符号的扩展

（自 Ruby 1.8.7 起，此功能已成为语言的一部分，但使用该语言先前版本的 Rails 用户也可以使用此功能。）

我们经常使用迭代器，而块所做的只是对其参数调用一个方法。我们在之前的 group_by 和 index_by 示例中就是这样做过的：

groups = posts.group_by { |post| post.author_id }

Rails 为此提供了一种简写记法。我们可以将这段代码写成这样：

groups = posts.group_by(&:author_id)

类似地，下面的代码：

us_states = State.find(:all)
state_lookup = us_states.index_by { |state| state.short_name }

也可以写成这样：

us_states = State.find(:all)
state_lookup = us_states.index_by(&:short_name)

#### 16.8 with_options

许多 Rails 方法将选项哈希作为最后一个参数。有时你会发现自己在连续调用几个这样的方法，其中每个

我们将使用单个动作来保持控制器简单：

class PeopleController < ApplicationController

  def index
    @person = Person.new(params[:person])
    @person.save! if request.post?
    @people = Person.find(:all)
  end
end

数据库是支持 Unicode 的。现在我们需要确保浏览器端也支持。

自 Rails 1.2 起，默认的 content-type 头如下所示：

Content-Type: text/html; charset=UTF-8

不过，为了确保起见，我们还会在页面头部添加一个 <meta> 标签来强制执行这一点。这也意味着如果用户将页面保存到本地文件，之后也能正确显示。这是我们的布局文件：

<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml" xml:lang="en" lang="en">
<head>
<meta http-equiv="content-type" content="text/html; charset=UTF-8"/>
<title>My Name List</title>
</head>
<body>
<%= yield :layout %>
</body>
</html>

在我们的 index 视图中，我们将显示数据库中的完整名称列表，并提供一个简单的表单让人们输入新名称。在列表中，我们将显示名称及其以字节和字符计的大小，并且为了展示一下，我们还将它反转。

<table border="1">
<tr>
<th>Name</th><th>bytes</th><th>chars</th><th>reversed</th>
</tr>
<% for person in @people %>
<tr>
<td><%=h person.name %></td>
<td><%= person.name.length %></td>
<td><%= person.name.chars.length %></td>
<td><%=h person.name.chars.reverse %></td>
</tr>
<% end %>
</table>

<% form_for :person do |form| %>
  New name: <%= form.text_field :name %>
  <%= submit_tag "Add" %>
<% end %>

当我们在浏览器中指向我们的 people 控制器时，会看到一个空表。让我们从在名称字段中输入“Dave”开始：

![](img/a160fc3a330a0b3b2a764d41d614e688_288_0.png)

当我们点击 Add 按钮时，我们看到字符串“Dave”既有 4 个字节也有 4 个字符——正常的 ASCII 字符在 UTF-8 中占用 1 个字节：

![](img/a160fc3a330a0b3b2a764d41d614e688_288_1.png)

在输入 Günter 后点击 Add，我们会看到不同情况：

![](img/a160fc3a330a0b3b2a764d41d614e688_288_2.png)

因为 ü 字符在 UTF-8 中需要 2 个字节来表示，所以我们看到该字符串的字节长度为 7，字符长度为 6。注意反转后的形式显示正确。

最后，我们将添加一些日语文本：

![](img/a160fc3a330a0b3b2a764d41d614e688_288_3.png)

现在字节长度和字符长度之间的差距更大了。然而，字符串仍然能按字符逐个正确反转。

### 第 17 章：迁移

Rails 鼓励敏捷、迭代的开发风格。我们不期望第一次就把所有事情都做对。相反，我们编写测试并与客户互动，在开发过程中不断深化我们的理解。

为了使其奏效，我们需要一套支持性的实践。我们编写测试来帮助设计接口，并在改动时充当安全网；我们使用版本控制来存储应用程序的源文件，使我们能够撤销错误并监控每天的变更。

但应用程序还有另一个会变化的领域，一个我们无法直接使用版本控制管理的领域。Rails 应用程序中的数据库模式会随着开发的推进而不断演变：我们这里加一张表，那里重命名一列，诸如此类。数据库与应用代码同步变化。

从历史上看，这一直是个问题。开发人员（或数据库管理员）按需进行模式更改。然而，如果应用程序代码回滚到之前的版本，就很难撤销数据库模式的更改以使数据库与之前的应用版本保持一致——数据库本身没有版本信息。

多年来，开发人员想出了处理这个问题的办法。一种方案是将定义模式的 Data Definition Language（DDL）语句以源码形式放在版本控制之下。每当你更改模式时，就编辑该文件以反映这些更改。然后删除开发数据库，并通过应用 DDL 从头重新创建模式。如果你需要回滚一周，从版本控制系统检出的应用代码和 DDL 是同步的。当你从 DDL 重新创建模式时，你的数据库就会回到过去的某个时间点。

只不过……因为每次应用 DDL 时都会删除数据库，你会丢失开发数据库中的任何数据。难道不是更方便



to be able to apply only those changes that are necessary to move a database from version *x* to version *y*? This is exactly what Rails migrations let you do.

Let’s start by looking at migrations at an abstract level. Imagine we have a table of order data. One day, our customer comes in and asks us to add the customer’s e-mail address to the data we capture in an order. This involves a change to the application code and the database schema. To handle this, we create a database migration that says “add an e-mail column to the orders table.” This migration sits in a separate file, which we place under version control alongside all our other application files. We then apply this migration to our database, and the column gets added to the existing orders table.

Exactly how does a migration get applied to the database? It turns out that every generated migration has a Coordinated Universal Time (UTC) timestamp associated with it. These numbers contain the four-digit year, followed by two digits each for the month, day, hour, minute, and second, all based on the mean solar time at the Royal Observatory in Greenwich, London.¹ Because migrations tend to be created relatively infrequently and the accuracy is recorded down to the second, the chances of any two people getting the same timestamp is vanishingly small. And the benefit of having timestamps that can be deterministically ordered far outweighs the minuscule risk of this occurring.

Rails remembers the version number of *each* migration applied to the database. Then, when you ask it to update the schema by applying new migrations, it compares the version numbers in the database schema_migrations table with the version numbers of the available migrations. If it finds migrations with version numbers that are not in the schema_migrations table, it applies them one at a time and in order.

But how do we revert a schema to a previous version? We do it by making each migration reversible. Each migration actually contains two sets of instructions. One set tells Rails what changes to make to the database when applying the migration, and the other set tells Rails how to undo those changes. In our orders table example, the *up* part of the migration adds the e-mail column to the table, and the *down* part removes that column. Now, to revert a schema, we simply tell Rails the version number that we would like the database schema to be at. If the current schema_migrations table has a row with a higher version numbers than this target number, Rails takes the migration with the

> ¹ Rails versions prior to 2.1 used a much simpler sequence number and stored the version number of the latest one applied in a single row in a table named schema_info. Because such sequence numbers will undoubtedly be much lower than any UTC timestamp, these older migrations will automatically be treated as if they were generated before Rails 2.1 was installed. If you would prefer to use numeric prefixes, you can turn timestamped migrations off by setting config.active_record.timestamped_migrations to false.

highest version number and applies its undo action. This removes the migration’s change from the schema and from the schema_migrations table. It repeats this process until the database reaches the desired version.

#### 17.1 Creating and Running Migrations

A migration is simply a Ruby source file in your application’s db/migrate directory. Each migration file’s name starts with a number of digits (typically fourteen) and an underscore. Those digits are the key to migrations, because they define the sequence in which the migrations are applied—they are the individual migration’s version number.

Here’s what the db/migrate directory of our Depot application looks like:

```
depot> ls db/migrate
20080601000001_create_products.rb
20080601000002_add_price_to_product.rb
20080601000003_add_test_data.rb
20080601000004_create_sessions.rb
20080601000005_create_orders.rb
20080601000006_create_line_items.rb
```

Although you could create these migration files by hand, it’s easier (and less error prone) to use a generator. As we saw when we created the Depot application, there are actually two generators that create migration files:

- The *model* generator creates a migration to in turn create the table associated with the model (unless you specify the `--skip-migration` option). As the example that follows shows, creating a model called discount also creates a migration called `dddddddddddddd_create_discounts.rb`:
  
  ```text
  depot> ruby script/generate model discount
         exists  app/models/
         exists  test/unit/
         exists  test/fixtures/
         create  app/models/discount.rb
         create  test/unit/discount_test.rb
         create  test/fixtures/discounts.yml
         exists  db/migrate
         create  db/migrate/20080601000014_create_discounts.rb
  ```

- You can also generate a migration on its own:
  
  ```text
  depot> ruby script/generate migration add_price_column
         exists  db/migrate
         create  db/migrate/20080601000015_add_price_column.rb
  ```

Later, starting in *Anatomy of a Migration*, we’ll see what goes in the migration files. But for now, let’s jump ahead a little in the workflow and see how to run migrations.

You can also redo one or more migrations:

```
depot> rake db:migrate:redo STEP=3
```

By default, redo will roll back one migration and rerun it. To roll back multiple migrations, pass the STEP= parameter.

#### 17.2 Anatomy of a Migration

Migrations are subclasses of the Rails class ActiveRecord::Migration. The class you create should contain at least the two class methods up and down:

```
class SomeMeaningfulName < ActiveRecord::Migration
  def self.up
    # ...
  end

  def self.down
    # ...
  end
end
```

The name of the class, after all uppercase letters are downcased and preceded by an underscore, must match the portion of the filename after the version number. For example, the previous class could be found in a file named 20080601000017_some_meaningful_name.rb. No two migrations can contain classes with the same name.

The up method is responsible for applying the schema changes for this migration, while the down method undoes those changes. Let's make this more concrete. Here's a migration that adds an e_mail column to the orders table:

```
class AddEmailToOrders < ActiveRecord::Migration
  def self.up
    add_column :orders, :e_mail, :string
  end

  def self.down
    remove_column :orders, :e_mail
  end
end
```

See how the down method undoes the effect of the up method?

##### Column Types

The third parameter to add_column specifies the type of the database column. In the previous example, we specified that the e_mail column has a type of :string. But just what does this mean? Databases typically don't have column types of :string.

|  | db2 | mysql | openbase | oracle |
|:---:|:---:|:---:|:---:|:---:|
| :binary | blob(32768) | blob | object | blob |
| :boolean | decimal(1) | tinyint(1) | boolean | number(1) |
| :date | date | date | date | date |
| :datetime | timestamp | datetime | datetime | date |
| :decimal | decimal | decimal | decimal | decimal |
| :float | float | float | float | number |
| :integer | int | int(11) | integer | number(38) |
| :string | varchar(255) | varchar(255) | char(4096) | varchar2(255) |
| :text | clob(32768) | text | text | clob |
| :time | time | time | time | date |
| :timestamp | timestamp | datetime | timestamp | date |

|  | postgresql | sqlite | sqlserver | sybase |
|:---:|:---:|:---:|:---:|:---:|
| :binary | bytea | blob | image | image |
| :boolean | boolean | boolean | bit | bit |
| :date | date | date | datetime | datetime |
| :datetime | timestamp | datetime | datetime | datetime |
| :decimal | decimal | decimal | decimal | decimal |
| :float | float | float | float(8) | float(8) |
| :integer | integer | integer | int | int |
| :string | (note 1) | varchar(255) | varchar(255) | varchar(255) |
| :text | text | text | text | text |
| :time | time | datetime | datetime | time |
| :timestamp | timestamp | datetime | datetime | timestamp |

Note 1: character varying(256)

Figure 17.1: Migration and database column types





但如果我们的应用程序已经把像 'new' 这样的数据存储在该列中，down 方法就会丢失它——“new”无法转换为整数。如果这是可以接受的，那么迁移本身是可以接受的。但是，如果我们想要创建一个单向迁移——即无法逆转的迁移——我们就需要阻止 down 迁移被应用。在这种情况下，Rails 提供了一个特殊的异常供我们抛出：

```
class ChangeOrderTypeToString < ActiveRecord::Migration
  def self.up
    change_column :orders, :order_type, :string, :null => false
  end

  def self.down
    raise ActiveRecord::IrreversibleMigration
  end
end
```

#### 17.3 管理表

到目前为止，我们一直在使用迁移来操作现有表中的列。现在让我们来看一下创建和删除表：

```
class CreateOrderHistories < ActiveRecord::Migration
  def self.up
    create_table :order_histories do |t|
      t.integer :order_id, :null => false
      t.text :notes

      t.timestamps
    end
  end

  def self.down
    drop_table :order_histories
  end
end
```

create_table 接受一个表名（记住，表名是复数形式）和一个块。（它还接受一些稍后会讨论的可选参数。）该块会传入一个表定义对象，我们用它来定义表中的列。

对各种表定义方法的调用应该看起来很熟悉——它们与之前使用的 add_column 方法类似，只是这些方法不以表名作为第一个参数，方法名本身就是所需的数据类型。这减少了重复。

请注意，我们没有为新表定义 id 列。除非另有说明，否则 Rails 迁移会自动为它们创建的所有表添加一个名为 id 的主键。有关更深入的讨论，请参阅第 303 页的第 17.3 节，主要键。

即使应用程序不再有 OrderHistory 类，以下版本的第四次迁移也能正常工作：

```
class CreateOrderHistories < ActiveRecord::Migration
  class Order < ActiveRecord::Base; end
  class OrderHistory < ActiveRecord::Base; end

  def self.up
    create_table :order_histories do |t|
      t.integer :order_id, :null => false
      t.text :notes

      t.timestamps
    end

    order = Order.find :first
    OrderHistory.create(:order => order_id, :notes => "test")
  end

  def self.down
    drop_table :order_histories
  end
end
```

只要我们的模型类不包含在迁移中会用到的任何额外功能，这就可以工作——我们在这里创建的只是最基本的版本。

如果重命名表对你来说是个问题，我们建议按照第 313 页的第 17.8 节，管理迁移中所述合并你的迁移。

##### 定义索引

迁移可以（并且可能应该）为表定义索引。例如，我们可能会注意到，一旦数据库中的订单数量变大，基于客户姓名进行搜索所需的时间比我们希望的要长。是时候使用恰如其名的方法 add_index 来添加索引了：

```
class AddCustomerNameIndexToOrders < ActiveRecord::Migration
  def self.up
    add_index :orders, :name
  end

  def self.down
    remove_index :orders, :name
  end
end
```

如果我们给 add_index 提供可选参数 :unique => true，就会创建一个唯一索引，强制索引列中的值唯一。

##### David 说. . .

##### 在现实世界中避免仅数据迁移

数据-only 迁移在此示例中使用是为了避免对如何真正进行适当的种子数据进行冗长讨论，但让我仍然给你一点这方面的讨论。核心观点是，迁移并不是真正用于携带种子数据的。它们在本质上过于临时，无法可靠地做到这一点。迁移的作用是将你从一个版本的模式带到下一个版本，而不是从头创建全新的模式——我们有 db/schema.rb 文件用于此目的。

因此，一旦你真正开始使用一个真实的应用程序，人们在设置应用程序时就不会运行你的早期迁移。他们将从 db/schema.rb 中存储的版本开始，并忽略所有之前的迁移。这意味着由迁移创建的任何数据都不会进入数据库，因此你不能依赖它。

有许多替代方法可以拥有更永久的种子数据。最简单的方法可能就是在 db/ 中创建一个新的 seed.rb 文件，其中包含那些 Product.create 调用以进行设置。该文件可以在 rake db:schema:load 创建初始模式后调用。

在这种情况下，你可能想要调查在此表上创建一个或多个索引以加快书籍和作者之间的导航。

#### 17.4 数据迁移

迁移只是 Ruby 代码；它们可以做我们想要的任何事情。而且，由于它们也是 Rails 代码，因此它们可以完全访问我们在应用程序中已编写的代码。特别是，迁移可以访问我们的模型类。这使得创建操作开发数据库中数据的迁移变得很容易。

让我们看两个在迁移中操作数据的有用场景：加载开发数据以及在应用程序版本之间迁移数据。

##### 使用迁移加载数据

我们的大多数应用程序在有意义地使用它们之前，甚至在开发期间，都需要在数据库中加载相当多的背景信息。如果我们正在编写一个在线商店，我们就需要产品数据。我们可能还需要有关运费、用户配置文件数据等的信息。在过去，开发人员习惯于将这些数据硬编码到他们的数据库中，通常通过手工输入 SQL insert 语句来完成。这很难管理且通常不可重复。这也使得项目进行到一半才加入的开发人员难以快速上手。

迁移使这变得容易得多。在我们几乎所有的 Rails 项目中，我们都会发现自己创建 *仅数据* 迁移——迁移会将数据加载到现有模式中而不是更改模式本身。

请注意，我们在这里谈论的是创建在开发人员使用应用程序时方便的数据，以及创建“固定”数据，例如查找表。你仍然希望创建包含特定于测试的数据的 fixtures。

以下是来自新 Pragmatic Bookshelf 商店的 Rails 应用程序的一个仅数据迁移：

```
class TestDiscounts < ActiveRecord::Migration
  def self.up
    down

    rails_book_sku = Sku.find_by_sku("RAILS-B-00")
    ruby_book_sku  = Sku.find_by_sku("RUBY-B-00")
    auto_book_sku  = Sku.find_by_sku("AUTO-B-00")

    discount = Discount.create(:name => "Rails + Ruby Paper",
                               :action => "DEDUCT_AMOUNT",
                               :amount => "15.00")
    discount.skus = [rails_book_sku, ruby_book_sku]
    discount.save!

    discount = Discount.create(:name => "Automation Sale",
                               :action => "DEDUCT_PERCENT",
                               :amount => "5.00")
    discount.skus = [auto_book_sku]
    discount.save!
  end

  def self.down
    Discount.delete_all
  end
end
```

##### 从 Fixtures 加载数据

Fixtures 通常包含在运行测试时使用的数据。然而，通过一点额外的管道，我们也可以在迁移期间使用它们来加载数据。

为了说明过程，让我们假设我们的数据库有一个新的 users 表。

让我们在 db/migrate 下创建一个子目录来存放我们将加载到开发数据库中的数据。让我们将该目录命名为 dev_data：

```
depots> mkdir db/migrate/dev_data
```

在该目录中，我们将创建一个 YAML 文件，其中包含我们想要加载到 users 表中的数据。我们将该文件命名为 users.yml：

```
dave:
  name: Dave Thomas
  status: admin

mike:
  name: Mike Clark
  status: admin

fred:
  name: Fred Smith
  status: audit
```

现在我们将生成一个迁移来将数据从此 fixture 加载到我们的开发数据库中：

```
depots> ruby script/generate migration load_users_data
exists  db/migrate
create  db/migrate/20080601000020_load_users_data.rb
```

最后，我们将在迁移中编写加载 fixture 数据的代码。这有点神奇，因为它依赖于 Rails fixture 代码的一个后门接口。

```
require 'active_record/fixtures'

class LoadUserData < ActiveRecord::Migration
  def self.up
    directory = File.join(File.dirname(__FILE__), 'dev_data')
    Fixtures.create_fixtures(directory, "users")
  end

  def self.down
    User.delete_all
  end
end
```





创建 `create_fixtures` 的第一个参数是包含 fixture 数据的目录的路径。我们将其设为相对于迁移文件的路径，因为我们将数据存储在 migrations 的子目录中。

请注意：在迁移中加载的唯一数据应该是你也希望在生产环境中看到的数据，例如查找表、预定义用户等。不要通过这种方式将测试数据加载到你的应用程序中。如果你发现自己想这样做，请考虑改为创建 Rake 任务（见第 15.2 节 Rake Tasks，第 260 页）。

##### 使用迁移迁移数据

有时模式更改也涉及迁移数据。例如，在项目开始时，你可能有一个使用 float 存储价格的模式。然而，如果你后来遇到舍入问题，你可能希望改为将价格存储为整数分。

如果你一直在使用迁移将数据加载到数据库中，那么这不是问题。只需更改迁移文件，使其不再将 12.34 加载到 price 列中，而是加载 1234。但如果这不可行，你可能希望在迁移内部执行转换。

一种方法是先将现有列值乘以 100，然后再更改列类型：

```ruby
class ChangePriceToInteger < ActiveRecord::Migration
  def self.up
    Product.update_all("price = price * 100")
    change_column :products, :price, :integer
  end

  def self.down
    change_column :products, :price, :float
    Product.update_all("price = price / 100.0")
  end
end
```

注意 down 迁移如何通过在列改回后才进行除法来撤销更改。

#### 17.5 高级迁移

大多数 Rails 开发者使用迁移的基本功能来创建和维护其数据库模式。然而，每隔一段时间，将迁移推进一步会很有用。本节涵盖一些更高级的迁移用法。

这次，让它成为一个普通的实例方法，而不是类方法：

```ruby
module MigrationHelpers

  def foreign_key(from_table, from_column, to_table)
    constraint_name = "fk_#{from_table}_#{to_table}"

    execute %{
      CREATE TRIGGER #{constraint_name}_insert
      BEFORE INSERT ON #{from_table}
      FOR EACH ROW BEGIN
        SELECT
          RAISE(ABORT, "constraint violation: #{constraint_name}")
        WHERE
          (SELECT id FROM #{to_table} WHERE id = NEW.#{from_column}) IS NULL;
      END;
    }

    execute %{
      CREATE TRIGGER #{constraint_name}_update
      BEFORE UPDATE ON #{from_table}
      FOR EACH ROW BEGIN
        SELECT
          RAISE(ABORT, "constraint violation: #{constraint_name}")
        WHERE
          (SELECT id FROM #{to_table} WHERE id = NEW.#{from_column}) IS NULL;
      END;
    }

    execute %{
      CREATE TRIGGER #{constraint_name}_delete
      BEFORE DELETE ON #{to_table}
      FOR EACH ROW BEGIN
        SELECT
          RAISE(ABORT, "constraint violation: #{constraint_name}")
        WHERE
          (SELECT id FROM #{from_table} WHERE #{from_column} = OLD.id) IS NOT NULL;
      END;
    }
  end
end
```

我们现在可以通过在迁移文件顶部添加以下行，将其添加到任何迁移中：

```ruby
require "migration_helpers"

class CreateLineItems < ActiveRecord::Migration
  extend MigrationHelpers
```

require 行将模块定义带入迁移的代码中，而 extend 行将 MigrationHelpers 模块中的方法作为类方法添加到迁移中。我们可以使用此技术开发和共享任意数量的迁移助手。

我们可以尝试回滚迁移，但这不会成功。因为原始迁移失败，数据库中的模式版本没有更新，所以 Rails 不会尝试回滚它。

此时，你可以胡乱手动更改模式信息并删除表。但这可能不值得。我们在这种情况下的建议是简单地删除整个数据库，重新创建它，并应用迁移使其恢复最新。你不会失去任何东西，并且你会知道你拥有一个一致的模式。

所有这些讨论表明，迁移对生产数据库的使用是危险的。你应该运行它们吗？我们真的不能说。如果你组织中有数据库管理员，那就是他们的决定。如果你自己决定，你必须权衡风险。但是，如果你决定继续，你真的必须先备份数据库。然后，你可以通过前往生产服务器上具有数据库角色的机器上的应用程序目录并执行以下命令来应用迁移：

```shell
depot> RAILS_ENV=production rake db:migrate
```

这就是本书开头法律声明生效的时候之一。如果这删除了你的数据，我们概不负责。

#### 17.7 迁移之外进行模式操作

本章迄今为止描述的所有迁移方法也作为 Active Record 连接对象的方法可用，因此可以在 Rails 应用程序的模型、视图和控制器内访问。

例如，你可能发现如果 orders 表在 city 列上有索引，某个长时间运行的报告运行速度会快很多。然而，在应用程序日常运行期间并不需要该索引，并且测试表明维护它会明显减慢应用程序速度。

让我们编写一个创建索引、运行代码块，然后删除索引的方法。这可以是模型中的私有方法，也可以实现在库中。

```ruby
def run_with_index(column)
  connection.add_index(:orders, column)
  begin
    yield
  ensure
    connection.remove_index(:orders, column)
  end
end
```

模型中的统计收集方法可以按如下方式使用它：

```ruby
def get_city_statistics
  run_with_index(:city) do
    # .. calculate stats
  end
end
```

#### 17.8 管理迁移

迁移有一个缺点。随着时间的推移，你的模式定义将被分散在多个单独的迁移文件中，许多文件可能影响模式中每个表的定义。当这种情况发生时，很难确切地看到每个表包含什么。以下是一些让生活更轻松的建议。

一个答案是查看文件 db/schema.rb。迁移运行后，此文件将以 Ruby 形式包含整个数据库定义。

或者，一些团队不使用单独的迁移来捕获模式的所有版本。相反，他们为每个表保留一个迁移文件，以及其他迁移文件用于将开发数据加载到这些表中。当他们需要更改模式时（例如向表添加列），他们编辑该表的现有迁移文件。然后他们删除并重新创建数据库并重新应用所有迁移。遵循这种方法，他们始终可以通过查看该表的迁移文件来看到每个表的总定义。

为了使这在实践中可行，每个团队成员都需要留意在从项目存储库更新其本地源代码时修改了哪些文件。当迁移文件更改时，这表明数据库模式需要重新创建。

尽管这种方案似乎违背了迁移的精神，但在实践中效果很好。

另一种方法是按照本章前面描述的方式使用迁移——为每次对模式的更改创建一个新的迁移。为了跟踪模式的演变，你可以使用 annotate_models 插件。运行后，此插件会查看当前模式并在该表的模型文件顶部添加每个表的描述。

使用以下命令安装 annotate_models 插件（已拆分为两行以适应页面）：

```shell
depot> ruby script/plugin install \
        http://repo.pragprog.com/svn/Public/plugins/annotate_models/
```

安装后，你可以随时使用以下命令运行它：

```shell
depot> rake annotate_models
```




完成上述操作后，每个模型源文件都会有一个注释块，记录相应数据库表中的列。例如，在我们的 Depot 应用中，文件 line_item.rb 的开头将如下所示：

```
```ruby
# == Schema Information
# Schema version: 20080601000007
#
# Table name: line_items
#
# id           :integer        not null, primary key
# product_id   :integer        not null
# order_id     :integer        not null
# quantity     :integer        not null
# total_price  :decimal(8, 2)  not null
# created_at   :datetime
# updated_at   :datetime

class LineItem < ActiveRecord::Base
  # ...
```
```

如果之后修改了模式（schema），只需重新运行 Rake 任务，注释块就会更新以反映数据库的当前状态。

### 第18章

### Active Record 第一部分：
基础

Active Record 是 Rails 提供的对象关系映射（ORM）层。在本章中，我们将介绍基础知识——连接数据库、映射表以及操作数据。我们将在下一章中探讨使用 Active Record 管理表关系，并在再下一章中深入探讨 Active Record 对象的生命周期（包括验证和过滤器）。

Active Record 严格遵循标准的 ORM 模型：表映射到类，行映射到对象，列映射到对象属性。它在配置方式上不同于大多数其他 ORM 库。通过使用一组合理的默认值，Active Record 最大限度地减少了开发人员执行的配置量。为了说明这一点，下面是一个独立程序，它使用 Active Record 包装 SQLite 3 数据库中的订单表。在找到具有特定 id 的订单后，它会修改购买者姓名并将结果保存回数据库，更新原始行。¹

```
require "rubygems"
require "activerecord"

ActiveRecord::Base.establish_connection(:adapter => "sqlite3",
  :database => "db/development.sqlite3")

class Order < ActiveRecord::Base
end

order = Order.find(1)
order.name = "Dave Thomas"
order.save
```

1. 本章中的示例连接到我们在编写本书时使用的机器上的各种 SQLite 3 数据库。你需要调整连接参数才能使它们适用于你的数据库。我们将在第 322 页的 18.4 节“连接数据库”中讨论连接数据库。

##### 大卫说...

###### 我们的属性在哪里？

将数据库管理员（DBA）视为与程序员不同的角色的观念，导致一些开发者在代码和模式之间划出严格的界限。Active Record 模糊了这种区分，而最明显的体现莫过于模型中缺少显式的属性定义。

但请放心。实践表明，无论是查看数据库模式、单独的 XML 映射文件，还是模型中的内联属性，差别都不大。这种复合视图与模型-视图-控制器模式中已有的分离类似——只是规模更小。

一旦把表模式视为模型定义一部分的不适感消失，你就会开始意识到保持 DRY 的好处。当你需要向模型添加属性时，只需创建一个新的迁移并重新加载应用程序。

从模式演化中移除“构建”步骤，使其与其余代码一样敏捷。从一个小的模式开始，并根据需要进行扩展和更改，会变得容易得多。

在 Depot 应用中，我们的 orders 表由以下迁移定义：

Download depot_r/db/migrate/20080601000005_create_orders.rb

def self.up
  create_table :orders do |t|
    t.string :name
    t.text :address
    t.string :email
    t.string :pay_type, :limit => 10

    t.timestamps
  end
end

我们已经编写了一个 Order 模型类作为 Depot 应用的一部分。让我们使用便捷的 script/console 命令来试用它。首先，我们请求一个列名列表：

```
depot> ruby script/console
Loading development environment (Rails 2.2.2)
>> Order.column_names
=> ["id", "name", "address", "email", "pay_type", "created_at", "updated_at"]
```

要在条件中将列作为布尔值查询，我们必须在列名后面附加一个问号：

```
# INSTEAD, DO THIS
user = Users.find_by_name("Dave")
if user.superuser?
  grant_privileges
end
```

这种形式的属性访问器会查看列的值。仅当它是数字 0；字符串 "0"、"f"、"false" 或 ""（空字符串）之一；nil；或常量 false 时，它才被解释为 false。否则，它被解释为 true。

如果你使用遗留模式，或者数据库使用英语以外的语言，上一段中关于“真”的定义可能不成立。在这种情况下，你可以覆盖谓词方法的内置定义。例如，在荷兰语中，字段可能包含 J 或 N（表示 Ja 或 Nee）。在这种情况下，你可以这样写：

```
class User < ActiveRecord::Base
  def superuser?
    self.superuser == 'J'
  end
  # . . .
end
```

#### 18.3 主键和 ids

如果你一直在查看 Depot 应用的底层数据库表，你会注意到每张表都有一个名为 id 的整数主键列。默认情况下，当我们使用 create_table 方法时，Rails 迁移会添加这个列。这是 Active Record 的一个约定。

“等等！”你喊道。“我的 orders 表的主键不应该是订单号或其他有意义的列吗？为什么要使用像 id 这样的人工主键？”

原因主要是实际考虑——外部数据的格式可能随时间变化。例如，你可能认为书籍的 ISBN 可以作为书籍表的主键。毕竟，ISBN 是唯一的。但在这本书的第一版和当前版本之间的短短几年里，美国出版业经历了一次重大变革，为所有 ISBN 增加了额外的数字。

如果我们使用 ISBN 作为书籍表的主键，就必须更新每一行以反映这一变化。但随后我们还会遇到另一个问题。数据库中的其他表会通过主键引用书籍表中的行。我们不能更改书籍表中的键，除非我们首先遍历并更新所有这些引用。这将涉及删除

```
book = LegacyBook.find("0-12345-6789")
puts book.title     # => "My Great American Novel"
p book.attributes   # => {"isbn"=>"0-12345-6789",
                    "title"=>"My Great American Novel"}
```

更让人困惑的是，模型对象的属性使用列名 isbn 和 title——id 并不出现。当你需要设置主键时，请使用 id。在其他所有时候，请使用实际的列名。

##### 复合主键

使用多列来标识每一行的表被称为具有复合主键。Rails 不支持这样的表，无论是在使用迁移创建它们时，还是在尝试使用 Active Record 时。

不过，一切并未结束。如果我们需要复合主键来让 Rails 适应遗留模式，我们可以去 Google 搜索一些插件。有人正在开发这些插件。[^5]

#### 18.4 连接数据库

Active Record 抽象了*数据库连接*的概念，使应用程序无需处理与特定数据库相关的细节。相反，Active Record 应用程序使用通用调用，将细节委托给一组特定于数据库的适配器。（当代码开始进行基于 SQL 的查询时，这种抽象会稍微失效，稍后我们会看到。）

指定连接的一种方法是使用 establish_connection 类方法。[^6] 例如，以下调用创建到名为 railsdb.sqlite3 的 SQLite 3 数据库的连接。它将成为所有模型类使用的默认连接。

```
ActiveRecord::Base.establish_connection(
  :adapter => "sqlite3",
  :database => "/db/railsdb.sqlite3"
)
```

##### 适配器特定信息

Active Record 支持 DB2、Firebird、Frontbase、MySQL、Openbase、Oracle、Postgres、SQLite、SQL Server 和 Sybase 数据库（这个列表还会增长）。每个适配器接受一组略有不同的连接参数，我们将在下面（非常无聊的）章节中列出。与 Rails 一贯的情况一样，事情变化很快。我们建议你访问 Rails wiki，网址是 http://wiki.rubyonrails.org/rails ，查看关于数据库适配器的最新信息。

- 5. 比如 Nic Williams 的网站：http://compositekeys.rubyforge.org/
- 6. 在完整的 Rails 应用中，还有另一种指定连接的方式。我们在第 266 页描述它。





然而，这个库性能不佳，因此我们建议安装 MySQL 的低级 C 绑定。

```
depot> gem install mysql
```

`:socket` 参数似乎会引起很多问题。这反映了 MySQL 中一些糟糕的实现决策。当你构建 MySQL 时，会将其硬编码为客户端用于与服务器通信的 socket 文件的位置。如果你曾在不同时期使用不同的包管理系统安装 MySQL，你可能会发现该 socket 被配置在不同的位置。如果你在一组配置下构建 Ruby 库，然后重新安装 MySQL，这些库可能就不再工作，因为 socket 可能已移动。`:socket` 参数允许你覆盖 Ruby 库中内置的位置，并指向 socket 文件的当前位置。

你可以通过命令行使用以下命令确定 socket 文件的位置：

```
depot> mysql_config --socket
```

连接参数：

```
:adapter => "mysql",
:database => "railsdb",
:username => "optional",  # defaults to 'root'
:password => "optional",
:socket   => "path to socket",
:port     => optional
:encoding => "utf8", "latin1", ...
```

## 使用以下参数通过安全 SSL 连接连接到 MySQL
## 服务器。要使用无客户端证书的 SSL，请将 :sslca 设置为 "/dev/null"

```
:sslkey    => "path to key file",
:sslcert   => "path to certificate file"
:sslca     => "path to certificate authority file"
:sslcapath => "directory containing trusted SSL CA certificates",
:ssl cipher => "list of allowable ciphers"
```

##### Openbase Adapter

需要：Ruby/OpenBase，来自 http://ruby-openbase.rubyforge.org/。

连接参数：

```
:adapter => "openbase",
:database => "railsdb",
:username => "optional",
:password => "optional",
:host     => "optional"
```

```
:dsn      => "required for odbc"
:username  => "optional",
:password  => "optional",
:autocommit => true,
```

##### Sybase Adapter

需要：sybase-ctlib 库。¹⁰

连接参数：

```
:adapter   => "sybase",
:database  => "railsdb",
:host     => "host",
:username  => "optional",
:password  => "optional",
:numconvert => true
```

如果 `:numconvert` 参数为 true（默认值），适配器将不会引用看起来像有效整数的值。

##### Connections and Models

连接与模型类相关联。每个类继承其父类的连接。由于 `ActiveRecord::Base` 是所有 Active Record 类的基类，为其设置连接就会为所有定义的 Active Record 类设置默认连接。但是，你可以在需要时覆盖此设置。

在下面的示例中，我们应用程序的大多数表都在名为 online 的 MySQL 数据库中。出于历史原因（还有其他原因吗？），customers 表位于 backend 数据库中。由于 `establish_connection` 是一个类方法，我们可以直接在 `class Customer` 的定义内调用它：

```
ActiveRecord::Base.establish_connection(
  :adapter  => "mysql",
  :host     => "dbserver.com",
  :database => "online",
  :username => "groucho",
  :password => "swordfish")
```

```
class LineItem < ActiveRecord::Base
  # ...
end
```

```
class Order < ActiveRecord::Base
  # ...
end
```

```
class Product < ActiveRecord::Base
  # ...
end
```

```
class Customer < ActiveRecord::Base
  establish_connection(
    :adapter => "mysql",
    :host => "dbserver.com",
    :database => "backend",
    :username => "chicho",
    :password => "piano")
  # ...
end
```

当我们在本书记述 Depot 应用程序时，我们没有使用 `establish_connection` 方法。相反，我们在 `config/database.yml` 文件中指定了连接参数。对于大多数 Rails 应用程序来说，这是首选的工作方式。它不仅能将所有连接信息移出代码，而且还能更好地与 Rails 的测试和部署方案配合使用。之前为特定连接适配器列出的所有参数也可以在 YAML 文件中使用。有关详细信息，请参阅第 15.3 节“配置数据库连接”，第 266 页。

最后，你可以结合这两种方法。如果向 `establish_connection` 传递一个符号，Rails 会在 `database.yml` 中查找同名部分，并基于其中找到的参数建立连接。这样，你就可以将所有连接细节移出代码。

#### 18.5 Create, Read, Update, Delete (CRUD)

Active Record 使实现四种基本数据库操作变得容易：创建、读取、更新和删除。

在本节中，我们将使用 MySQL 数据库中的 orders 表。以下示例假设我们为该表有一个基本的 Active Record 模型：

```
class Order < ActiveRecord::Base
end
```

##### Creating New Rows

在对象关系范式中，表表示为类，表中的行对应于该类的对象。似乎合理的是，我们通过创建适当类的新对象来创建表中的行。我们可以通过调用 `Order.new` 来创建表示 orders 表中行的新对象。然后我们可以填充属性的值（对应于数据库中的列）。最后，我们调用对象的 `save` 方法将订单存储回数据库。没有此调用，订单将只存在于本地内存中。

```
Download e1/ar/new_examples.rb
an_order = Order.new
an_order.name      = "Dave Thomas"
an_order.email     = "dave@pragprog.com"
an_order.address   = "123 Main St"
an_order.pay_type  = "check"
an_order.save
```

Active Record 构造函数接受一个可选块。如果存在，该块将以新创建的订单作为参数调用。这在你想要创建并保存订单而无需创建新的局部变量时可能很有用。

```
Download e1/ar/new_examples.rb
Order.new do |o|
  o.name    = "Dave Thomas"
  # ...
  o.save
end
```

最后，Active Record 构造函数接受一个属性值的哈希作为可选参数。此哈希中的每个条目都对应要设置的属性的名称和值。正如我们稍后在书中所看到的，这在将 HTML 表单中的值存储到数据库行时很有用。

```
Download e1/ar/new_examples.rb
an_order = Order.new(
  :name     => "Dave Thomas",
  :email    => "dave@pragprog.com",
  :address  => "123 Main St",
  :pay_type => "check")
an_order.save
```

请注意，在所有这些示例中，我们都没有设置新行的 id 属性。由于我们使用了 Active Record 的默认整数列作为主键的默认值，Active Record 会在保存行时自动创建一个唯一值并设置 id 属性。我们随后可以通过查询该属性找到此值。

```
Download e1/ar/new_examples.rb
an_order = Order.new
an_order.name = "Dave Thomas"
# ...
an_order.save
puts "The ID of this order is #{an_order.id}"
```

`new` 构造函数在内存中创建一个新的 Order 对象；我们必须在某个时候记住将其保存到数据库中。Active Record 有一个便捷方法 `create`，它既实例化模型对象又将其存储到数据库中。

##### David Says. . .
To Raise, or Not to Raise?

当你使用基于主键的查找器时，你正在寻找特定的记录。你期望它存在。对 `Person.find(5)` 的调用基于我们对 people 表的了解。我们想要 id 为 5 的行。如果此调用不成功——如果 id 为 5 的记录已被销毁——我们就处于异常情况。这要求引发异常，因此 Rails 引发 `RecordNotFound`。

另一方面，使用条件进行搜索的查找器是在寻找匹配项。因此，`Person.find(:first, :conditions=>"name='Dave'")` 等同于告诉数据库（作为黑盒）“给我第一个名字为 Dave 的 person 行。”这表现出一种截然不同的检索方法；我们事先并不确定是否会得到结果。结果集可能为空是完全可能的。因此，对于查找单行的查找器返回 nil，以及对于查找多行的查找器返回空数组，是自然的、非异常的响应。

通常，你需要基于主键值以外的条件读取行。Active Record 提供了执行这些查询的一系列选项。我们将从查看低级的 `find` 方法开始，然后再转向更高级别的动态查找器。

到目前为止，我们只是触及了 `find` 的表面，使用它根据作为参数传递的 id 返回一行或多行。然而，`find` 有点分裂的人格。如果你将 `:first` 或 `:all` 中的一个符号作为第一个参数传递，谦逊的旧 `find` 就会变成强大的搜索机器。

`:first` 变体的 `find` 返回与一组条件匹配的第一行，而 `:all` 形式返回匹配行的数组。这两种形式都接受一组关键字参数来控制它们的行为。但在查看这些之前，我们需要花一页或两页时间解释 Active Record 如何处理 SQL。

##### SQL and Active Record

为了说明 Active Record 如何与 SQL 配合工作，让我们看一下 `find(:all, :conditions =>...)` 方法调用的 `:conditions` 参数。此 `:conditions` 参数决定 `find` 返回哪些行；它对应于 SQL `where` 子句。例如，要返回 Dave 的所有订单且付款类型为 "po"，我们可以使用以下方法：

```
pos = Order.find(:all,
    :conditions => "name = 'Dave' and pay_type = 'po'")
```





The result will be an array of all the matching rows, each neatly wrapped in an Order object. If no orders match the criteria, the array will be empty.

That's fine if our condition is predefined, but how do we handle the situation where the name of the customer is set externally (perhaps coming from a web form)? One way is to substitute the value of that variable into the condition string:

```
# get the name from the form
name = params[:name]
# DON'T DO THIS!!
pos = Order.find(:all,
  :conditions => "name = '#{name}' and pay_type = 'po'")
```

As the comment suggests, this really isn't a good idea. Why? It leaves the database wide open to something called a SQL injection attack, which we describe in more detail in Chapter 27, Securing Your Rails Application, on page 637. For now, take it as a given that substituting a string from an external source into a SQL statement is effectively the same as publishing your entire database to the whole online world.

Instead, the safe way to generate dynamic SQL is to let Active Record handle it. Wherever we can pass in a string containing SQL, we can also pass in an array or a hash. Doing this allows Active Record to create properly escaped SQL, which is immune from SQL injection attacks. Let's see how this works.

If we pass an array when Active Record is expecting SQL, it treats the first element of that array as a template for the SQL to generate. Within this SQL, we can embed placeholders, which will be replaced at runtime by the values in the rest of the array.

One way of specifying placeholders is to insert one or more question marks in the SQL. The first question mark is replaced by the second element of the array, the next question mark by the third, and so on. For example, we could rewrite the previous query as this:

```
name = params[:name]
pos = Order.find(:all,
  :conditions => ["name = ? and pay_type = 'po'", name])
```

We can also use named placeholders. Each placeholder is of the form :name, and the corresponding values are supplied as a hash, where the keys correspond to the names in the query:

```
name     = params[:name]
pay_type = params[:pay_type]
pos = Order.find(:all,
  :conditions => ["name = :name and pay_type = :pay_type",
                  {:pay_type => pay_type, :name => name}])
```

We'll place and illustrate them using find(:all, ...). We'll call find with a first parameter of :first or :all the finder method.

With no extra parameters, the finder effectively executes a select * from... statement. The :all form returns all rows from the table, and :first returns one. The order is not guaranteed (so Order.find(:first) will not necessarily return the first order created by your application).

##### :conditions

As we saw in the previous section, the :conditions parameter lets us specify the condition passed to the SQL where clause used by the find method. This condition can be a string containing SQL, an array containing SQL and substitution values, or a hash. (From now on we won't mention this explicitly—whenever we talk about a SQL parameter, assume the method can accept an array, a string, or a hash.)

```
daves_orders = Order.find(:all, :conditions => "name = 'Dave'")

name = params[:name]
other_orders = Order.find(:all, :conditions => ["name = ?", name])

yet_more = Order.find(:all,
    :conditions => ["name = :name and pay_type = :pay_type", params[:order]])
still_more = Order.find(:all, :conditions => params[:order])
```

##### :order

SQL doesn't guarantee that rows will be returned in any particular order unless we explicitly add an order by clause to the query. The :order parameter lets us specify the criteria we'd normally add after the order by keywords. For example, the following query would return all of Dave's orders, sorted first by payment type and then by shipping date (the latter in descending order):

```
orders = Order.find(:all,
    :conditions => "name = 'Dave'",
    :order      => "pay_type, shipped_at DESC")
```

##### :limit

We can limit the number of rows returned by find(:all, ...) with the :limit parameter. If we use the limit parameter, we'll probably also want to specify the sort order to ensure consistent results. For example, the following returns the first ten matching orders:

```
orders = Order.find(:all,
    :conditions => "name = 'Dave'",
    :order      => "pay_type, shipped_at DESC",
    :limit      => 10)
```

##### :offset

The :offset parameter goes hand in hand with the :limit parameter. It allows us to specify the offset of the first row in the result set that will be returned by find.

```
# The view wants to display orders grouped into pages,
# where each page shows page_size orders at a time.
# This method returns the orders on page page_num (starting
# at zero).
def Order.find_on_page(page_num, page_size)
  find(:all,
    :order => "id",
    :limit => page_size,
    :offset => page_num*page_size)
end
```

We can use :offset in conjunction with :limit to step through the results of a query n rows at a time.

##### :joins

The :joins parameter to the finder method lets us specify a list of additional tables to be joined to the default table. This parameter is inserted into the SQL immediately after the name of the model's table and before any conditions specified by the :conditions parameter. The join syntax is database-specific. The following code returns a list of all line items for the book called Programming Ruby:

```
LineItem.find(:all,
  :conditions => "pr.title = 'Programming Ruby'",
  :joins      => "as li inner join products as pr on li.product_id = pr.id")
```

In addition to being able to specify :joins as a string, we can pass a symbol, an array, or a hash, and Rails will build the SQL query for us. For details, see the documentation for ActiveRecord::Associations::ClassMethods under Table Aliasing.

As we'll see in Chapter 19, Active Record: Relationships Between Tables, on page 357, we probably won't use the :joins parameter of find very much—Active Record handles most of the common intertable joins for us.

##### :select

By default, find fetches all the columns from the underlying database table—it issues a select * from... to the database. Override this with the :select option, which takes a string that will appear in place of the * in the select statement.

This option allows us to limit the values returned in cases where we need only a subset of the data in a table. For example, our table of podcasts might contain information on the title, speaker, and date and might also contain a

##### :lock

The :lock option takes either a string or the constant true. If we pass it a string, it should be a SQL fragment in our database's syntax that specifies a kind of lock. With MySQL, for example, a share mode lock gives us the latest data in a row and guarantees that no one else can alter that row while we hold the lock. We could write code that debits an account only if there are sufficient funds using something like the following:

```
Account.transaction do
  ac = Account.find(id, :lock => "LOCK IN SHARE MODE")
  ac.balance -= amount if ac.balance > amount
  ac.save
end
```

If we give :lock a value of true, the database's default exclusive lock is obtained (normally this will be "for update"). We can often eliminate the need for this kind of locking using transactions (discussed starting on page 418) and optimistic locking (which starts on page 422).

There's one additional parameter, :include, that kicks in only if we have associations defined. We'll talk about it starting on page 394.

##### Finding Just One Row

The find(:all, ...) method returns an array of model objects. If instead we want just one object returned, we can use find(:first, ...). This takes the same parameters as the :all form, but the :limit parameter is forced to the value 1, so only one row will be returned.

Download el/ar/find_examples.rb

```
# return an arbitrary order
order = Order.find(:first)

# return an order for Dave
order = Order.find(:first, :conditions => "name = 'Dave Thomas'")

# return the latest order for Dave
order = Order.find(:first,
                    :conditions => "name = 'Dave Thomas'",
                    :order       => "id DESC")
```

If the criteria given to find(:first, ...) result in multiple rows being selected from the table, the first of these is returned. If no rows are selected, nil is returned.

##### Writing Our Own SQL

The find method constructs the full SQL query string for us. The method find_by_sql lets our application take full control. It accepts a single parameter containing a SQL select statement (or an array containing SQL and placeholder values, as for find) and returns a (potentially empty) array of model objects.





所有聚合函数都接受一个选项哈希，与可以传递给 find 的哈希非常相似。（count 函数是个例外——我们会单独讨论它。）

:conditions
将函数限制为匹配的行。条件可以以与 find 方法相同的格式指定。

:joins
指定要连接的附加表。

:limit
将结果集限制为给定数量的行。这仅在分组结果时才有用（我们稍后会讨论）。

:order
对结果集进行排序（仅在与 :group 一起使用时有用）。

:having
指定 SQL HAVING ... 子句。

:select
指定要在聚合中使用的列（但这可以简单地作为聚合函数的第一个参数指定）。

:distinct （仅限 count）
仅统计列中的不同值。

这些选项可以组合使用：

```
Order.minimum :amount
Order.minimum :amount, :conditions => "amount > 20"
```

这些函数对值进行聚合。默认情况下，它们返回单个结果，例如，返回满足某些条件的订单的最小订单金额。但是，如果你包含 :group 子句，函数将改为产生一系列结果，为分组表达式具有相同值的每组记录产生一个结果。例如，以下代码计算每个州的最大销售额：

```
result = Order.maximum :amount, :group => "state"
puts result  #=> [["TX", 12345], ["NC", 3456], ...]
```

此代码返回一个有序哈希。你可以使用分组元素（在我们的示例中为 "TX"、"NC"...）对其进行索引。你也可以使用 each 按顺序遍历条目。每个条目的值是聚合函数的值。

使用分组时，:order 和 :limit 参数才真正发挥作用。

作用域也可以组合。查找最近一周通过支票支付的订单同样简单：

```
orders = Orders.checks.last_n_days(7)
```

除了使应用程序代码更易于编写和阅读之外，命名作用域还可以使代码更高效。例如，前面的语句被实现为单个 SQL 查询。

可以使用 scope 命名作用域创建匿名作用域：

```
in_house = Orders.scoped(:conditions => 'email LIKE "%@pragprog.com"')
```

当然，匿名作用域也可以组合：

```
in_house.checks.last_n_days(7)
```

作用域不限于条件；我们可以在 find 调用中做的几乎所有事情都可以在作用域中做：:limit、:order、:join 等等。只需注意 Rails 不知道如何处理多个 order 或 limit 子句，因此请确保在每个调用链中仅使用一次。

Rails 甚至提供了一个名为 all 的作用域，其功能等同于 find(:all)。

##### 重新加载数据

在一个数据库可能被多个进程（或多个应用程序）访问的应用程序中，始终存在获取的模型对象可能已过时的可能性——有人可能已将更新的副本写入数据库。

在某种程度上，这一问题通过事务支持得到解决（我们在第 418 页描述）。然而，仍会有需要手动刷新模型对象的时候。Active Record 使这变得很容易——只需调用其 reload 方法，对象的属性就会从数据库中刷新：

```
stock = Market.find_by_ticker("RUBY")
loop do
  puts "Price = #{stock.price}"
  sleep 60
  stock.reload
end
```

在实践中，reload 在单元测试的上下文之外很少使用。

##### 更新现有行

在讨论了这么多 finder 方法之后，你会很高兴知道，使用 Active Record 更新记录并没有太多可说的。

如果你有一个 Active Record 对象（可能代表我们 orders 表中的一行），你可以通过调用其 save 方法将其写入数据库。如果此对象

##### 删除行

Active Record 支持两种行删除样式。首先，它有两个类级方法，delete 和 delete_all，它们在数据库级别操作。delete 方法接受单个 id 或 id 数组，并删除底层表中对应的行（行）。delete_all 删除匹配给定条件的行（如果未指定条件则删除所有行）。两次调用的返回值取决于适配器，但通常是受影响的行数。如果在调用前行不存在，则不会抛出异常。

```
Order.delete(123)
User.delete([2,3,4,5])
Product.delete_all(["price > ?", @expensive_price])
```

destroy 方法是 Active Record 提供的第二种行删除形式。这些方法都通过 Active Record 模型对象工作。

destroy 实例方法从数据库中删除对应于特定模型对象的行。然后它冻结该对象的内容，防止未来对属性的更改。

```
order = Order.find_by_name("Dave")
order.destroy
# ... order is now frozen
```

有两个类级销毁方法，destroy（接受 id 或 id 数组）和 destroy_all（接受条件）。两者都将数据库表中的对应行读入模型对象，并调用这些对象的实例级 destroy 方法。两种方法都不返回有意义的值。

```
Order.destroy_all(["shipped_at < ?", 30.days.ago])
```

为什么我们需要 delete 和 destroy 这两种类方法？delete 方法绕过了各种 Active Record 回调和验证函数，而 destroy 方法确保它们都被调用。（我们从第 407 页开始讨论回调。）通常，如果你希望确保数据库根据模型类中定义业务规则保持一致，最好使用 destroy 方法。

#### 18.6 聚合和结构化数据

（本节包含可在首次阅读时安全跳过的材料。）

##### 存储结构化数据

有时将包含任意 Ruby 对象的属性直接存储到数据库表中会很有帮助。Active Record 支持的一种方式是将 Ruby 对象序列化为字符串（YAML 格式），并将该字符串存储在对应于该属性的数据库列中。在模式中，此列必须定义为 text 类型。

由于 Active Record 通常将字符或文本列映射为普通的 Ruby 字符串，因此如果你想利用此功能，需要告诉 Active Record 使用序列化。例如，我们可能想记录客户最近五次购买。我们将创建一个包含用于保存此信息的文本列的表：

```
create_table :purchases, :force => true do |t|
  t.string :name
  t.text   :last_five
end
```

在包装此表的 Active Record 类中，我们将使用 serialize 声明告诉 Active Record 将对象编组到此列并从此列编组出来：

```
class Purchase < ActiveRecord::Base
  serialize :last_five
  # ...
end
```

当我们创建新的 Purchase 对象时，我们可以将任何 Ruby 对象分配给 last_five 列。在本例中，我们将其设置为字符串数组：

```
purchase = Purchase.new
purchase.name = "Dave Thomas"
purchase.last_five = [ 'shoes', 'shirt', 'socks', 'ski mask', 'shorts' ]
purchase.save
```

当我们稍后读取它时，该属性会被设置回数组：

```
purchase = Purchase.find_by_name("Dave Thomas")
pp purchase.last_five
pp purchase.last_five[3]
```

此代码输出以下内容：

```
["shoes", "shirt", "socks", "ski mask", "shorts"]
"ski mask"
```

尽管功能强大且方便，但如果我们以后需要在 Ruby 应用程序之外使用序列化列中的信息，这种方法是有问题的。除非该应用程序理解 YAML 格式，否则列内容对它来说是不透明的。特别是，很难在 SQL 查询中使用这些列中的结构。出于这些原因，使用组合进行对象聚合通常是更好的方法。





##### 使用聚合组合数据

数据库列的类型是有限的：整数、字符串、日期等等。通常，我们的应用程序更加丰富——我们定义类来表示代码中的抽象。如果能够像将行数据封装到模型对象中那样，将数据库中的某些列信息映射到我们的高层抽象中，那就太好了。

例如，客户数据表可能包含用于存储客户姓名的列——名字、中间名首字母和姓氏。在程序中，我们希望将这些与姓名相关的列包装到单个 `Name` 对象中；这三列被映射到一个 Ruby 对象，该对象与所有其他客户字段一起包含在客户模型中。而且，当我们将模型写回时，我们希望将数据从 `Name` 对象中提取出来，放回数据库中的相应三列中。

![](img/a160fc3a330a0b3b2a764d41d614e688_347_0.png)

这种机制称为聚合（虽然有些人称其为组合——这取决于你是自上而下还是自下而上看待它）。毫不奇怪，Active Record 使这变得容易。我们定义一个类来保存数据，并在模型类中添加一个声明，告诉它如何将数据库列映射到数据持有者类的对象，以及反向映射。

持有组合数据的类（本例中是 `Name` 类）必须满足两个条件。首先，它必须有一个构造函数，能够接受数据库列中出现的数据，每列一个参数。其次，它必须提供返回这些数据的属性，同样是每列一个属性。在内部，它可以以任何需要的形式存储数据，只要能够将列数据映射进和映射出。

对于我们的姓名示例，我们将定义一个简单的类，将三个组件保存为实例变量。我们还将定义一个 `to_s` 方法，将完整姓名格式化为字符串。

```
Download e1/ar/aggregation.rb

class Name
  attr_reader :first, :initials, :last

  def initialize(first, initials, last)
    @first = first
    @initials = initials
    @last = last
  end

  def to_s
    [ @first, @initials, @last ].compact.join(" ")
  end
end
```

现在，我们必须告诉 `Customer` 模型类，三个数据库列 `first_name`、`initials` 和 `last_name` 应映射到 `Name` 对象。我们使用 `composed_of` 声明来实现这一点。

虽然 `composed_of` 可以只用一个参数调用，但最好先描述声明的完整形式，并展示各个字段如何默认：

```
composed_of :attr_name, :class_name => SomeClass, :mapping => mapping, :allow_nil => boolean, :constructor => SomeProc, :converter => SomeProc
```

`attr_name` 参数指定复合属性在模型类中将被赋予的名称。如果我们按如下方式定义客户：

```
class Customer < ActiveRecord::Base
  composed_of :name, ...
end
```

我们就可以通过 `customer` 对象的 `name` 属性访问复合对象：

```
customer = Customer.find(123)
puts customer.name.first
```

`:class_name` 选项指定持有复合数据的类的名称。该选项的值可以是类常量，也可以是包含类名的字符串或符号。在我们的例子中，类是 `Name`，因此我们可以这样指定：

```
class Customer < ActiveRecord::Base
  composed_of :name, :class_name => 'Name', ...
end
```

如果类名刚好就是属性名的驼峰式形式（在我们的例子中就是如此），我们可以省略它。

![](img/a160fc3a330a0b3b2a764d41d614e688_349_0.png)

`:mapping` 参数告诉 Active Record 表中的列如何映射到复合对象中的属性和构造函数参数。`:mapping` 的参数要么是两元素数组，要么是两元素数组的数组。每个两元素数组的第一个元素是数据库列的名称。第二个元素是复合属性中对应访问器的名称。`mapping` 参数中元素的出现顺序定义了数据库列内容传递给复合对象 `initialize` 方法的参数顺序。我们可以在图 18.2 中看到 `mapping` 选项的工作方式。如果省略此选项，Active Record 会假定数据库列和复合对象属性都与模型属性同名。

`:allow_nil` 参数如果设置，当值对象本身设置为 `nil` 时，会导致所有映射属性设置为 `nil`。此值的默认值为 `false`。

`:constructor` 参数指定一个指定方法名的符号，或一个被调用来初始化值对象的 `Proc`。构造函数按 `:mapping` 参数中定义的顺序接收所有映射属性。默认值是 `:new`。

`:converter` 参数指定一个指定方法名的符号，或一个当新值被赋给值对象时被调用的 `Proc`。转换器接收一个用于赋值的单一值，并且仅当新值不是 `:class_name` 的实例时才会被调用。

对于我们的 `Name` 类，我们需要将三个数据库列映射到复合对象中。

当我们运行这个时，我们可以看到 `last_five` 属性包含一个值数组：

```
Download e1/ar/aggregation.rb
Purchase.create(:last_five => LastFive.new("3,4,5"))
purchase = Purchase.find(:first)
puts purchase.last_five.list[1]    #=> 4
```

###### 复合对象是值对象

值对象是创建后状态不能改变的对象——它实际上是冻结的。Active Record 中聚合的理念是复合对象是值对象：你永远不应该改变它们的内部状态。

Active Record 或 Ruby 并不总能直接强制执行这一点——例如，你可以使用 `String` 类的 `replace` 方法来更改复合对象某个属性的值。但是，如果你这样做了，Active Record 会在随后保存模型对象时忽略该更改。

更改与复合属性相关联的列值的正确方法是向该属性分配一个新的复合对象：

```
customer = Customer.find(123)
old_name = customer.name
customer.name = Name.new(old_name.first, old_name.initials, "Smith")
customer.save
```

#### 18.7 杂项

本节包含各种与 Active Record 相关的主题，这些主题似乎不适合放在其他地方。

##### 对象标识

模型对象重新定义了 Ruby 的 `id` 和 `hash` 方法，以引用模型的主键。这意味着具有有效 `id` 的模型对象可以用作哈希键。这也意味着未保存的模型对象不能可靠地用作哈希键（因为它们还没有有效的 `id`）。

如果两个模型对象是同一个类的实例并且具有相同的主键，则它们被认为是相等的（使用 `==`）。这意味着未保存的模型对象即使具有不同的属性数据，也可能比较为相等。如果你发现自己需要比较未保存的模型对象（这不是一个特别频繁的操作），你可能需要覆盖 `==` 方法。

##### 使用原始连接

你可以使用底层的 Active Record 连接适配器执行 SQL 语句。这在那些（罕见的）需要与 Active Record 模型类上下文之外的数据库交互的情况下非常有用。

在最底层，你可以调用 `execute` 来运行（依赖于数据库的）SQL 语句。返回值取决于所使用的数据库适配器。如果你确实需要在如此低的层次上工作，你可能需要从代码本身阅读此调用的详细信息。幸运的是，你不必这样做，因为数据库适配器层提供了更高级别的抽象。

`select_all` 方法执行查询并返回一个与结果集对应的属性哈希数组：

```
res = Order.connection.select_all("select id, quantity*unit_price as total " +
" from line_items")
p res
```

这会生成如下内容：

```
[{"total"=>"29.95", "id"=>"91"},
{"total"=>"59.90", "id"=>"92"},
{"total"=>"44.95", "id"=>"93"}]
```

`select_one` 方法返回一个单一的哈希，该哈希取自结果集中的第一行。

请参阅 Rails API 文档中 `DatabaseStatements` 模块的说明，了解可用的低级连接方法的完整列表。

##### 缺失 id 的情况

当你使用自己的 finder SQL 将行检索到 Active Record 对象中时，存在一个隐藏的危险。

Active Record 使用行的 `id` 列来跟踪数据所属的位置。如果在使用 `find_by_sql` 时没有随列数据一起获取 `id`，你将无法将结果存储到数据库中。不幸的是，Active Record 仍然会尝试并静默失败。例如，以下代码不会更新数据库：

```
result = LineItem.find_by_sql("select quantity from line_items")
result.each do |li|
  li.quantity += 2
  li.save
end
```

也许有一天，Active Record 会检测到 `id` 缺失并在这些情况下抛出异常。与此同时，教训是明确的：如果你打算将 Active Record 对象保存到数据库中，务必获取主键列。事实上，除非你有特别的理由不这样做，否则在自定义查询中执行 `select *` 可能是最安全的。




Active Record 在这里派上了用场。其 ORM 魔法的一部分在于，它把数据库中底层的外键关系转换为高层次的对象间映射。它处理以下三种基本情形：

-   表 A 中的一行与表 B 中的零行或一行相关联。
-   表 A 中的一行与表 B 中的任意多行相关联。
-   表 A 中的任意多行与表 B 中的任意多行相关联。

在处理表间关系时，我们需要给 Active Record 一点点帮助。这其实不是 Active Record 的错——因为无法仅凭数据库模式推断出开发者原本打算建立何种表间关系。不过，我们需要提供的帮助量是很小的。

#### 19.1 创建外键

如前所述，当一个表中的某一列包含对另一个表主键的外键引用时，这两个表便产生了关联。在下面的迁移中，`line_items` 表包含了指向 `products` 和 `orders` 表的外键引用：

```
def self.up
  create_table :products do |t|
    t.string :title
    # ...
  end

  create_table :orders do |t|
    t.string :name
    # ...
  end

  create_table :line_items do |t|
    t.integer :product_id
    t.integer :order_id
    t.integer :quantity
    t.decimal :unit_price, :precision => 8, :scale => 2
  end
end
```

值得注意的是，这个迁移并没有定义任何外键约束。表间关系的建立仅仅是因为开发者会用来自 `products` 和 `orders` 表的主键值来填充 `product_id` 和 `order_id` 列。你也可以选择在迁移中建立这些约束（我们建议你这样做），但 Rails 中的外键支持并不需要它们。

#### 19.3 belongs_to 和 has_xxx 声明

各种关联声明（`belongs_to`、`has_one` 等）不仅指定了表之间的关系。它们各自还会向模型添加一些方法，帮助在关联对象之间进行导航。让我们更详细地了解一下这些方法。（如果你想直接看简短版本，我们在第 386 页的图 19.3 中对相关内容做了总结。）

##### belongs_to 声明

`belongs_to` 声明给定的类与包含该声明的类存在父子关系。尽管在思考这种关系时，`belongs_to` 可能不是首先想到的措辞，但 Active Record 的约定是：包含外键的表属于它所引用的表。如果这样有助于理解，你在编码时可以把 `belongs_to` 理解为 references（引用），但需要输入的是 `belongs_to`。

父类名被假定为属性名的混合大小写单数形式，外键字段是父类名的小写单数形式后附加 `_id`。下面是一些 `belongs_to` 声明示例，以及相应的外键字段、目标类和表名：

```
class LineItem < ActiveRecord::Base
  belongs_to :product
  belongs_to :invoice_item
end
```

| 子类中的声明 | 外键 | 父类 | 父表 |
|---|---|---|---|
| belongs_to :product | product_id | Product | products |
| belongs_to :invoice_item | invoice_item_id | InvoiceItem | invoice_items |

Active Record 将行项目与 `Product` 和 `InvoiceItem` 类关联起来。在底层数据库模式中，它分别使用外键 `product_id` 和 `invoice_item_id` 来引用 `products` 表和 `invoice_items` 表中的 `id` 列。

你可以通过在关联名后向 `belongs_to` 传递一个选项哈希来覆盖这些假设及其他默认假设：

```
class LineItem < ActiveRecord::Base
  belongs_to :paid_order,
    :class_name => "Order",
    :foreign_key => "order_id",
    :conditions => "paid_on is not null"
end
```

在这个例子中，我们创建了一个名为 `paid_order` 的关联，它引用 `Order` 类（因此也就是 `orders` 表）。该关联通过 `order_id` 外键建立，但还进一步受条件限制：仅当目标行中的 `paid_on` 列不为 null 时，才会找到对应的订单。在这个例子中，我们的关联并没有直接映射到底层 `line_items` 表中的单个列。`belongs_to` 还接受许多其他选项，我们将在讨论更高级的主题时介绍它们。

`belongs_to` 方法会创建多个用于管理该关联的实例方法。这些方法的名称都包含关联名。让我们来看 `LineItem` 类：

```
class LineItem < ActiveRecord::Base
  belongs_to :product
end
```

在这种情况下，将为行项目以及它们所属的产品定义以下方法：

`product(force_reload=false)`
返回关联的产品（如果不存在关联产品，则返回 nil）。结果会被缓存，之后再次使用该关联时不会重新查询数据库，除非传入 `true` 作为参数。

最常见的是，这个方法被当作（比如说）某个行项目对象的简单属性来调用：

```
li = LineItem.find(1)
puts "The product name is #{li.product.name}"
```

`product=obj`
将当前行项目与给定产品关联，把当前行项目的 `product_id` 列设置为该产品的主键。如果该产品尚未保存，则会在行项目保存时保存，届时键会建立关联。

`build_product(attributes={})`
构造一个新的产品对象，使用给定的 `attributes` 进行初始化。当前行项目会与之关联。该产品不会被立即保存。

`create_product(attributes={})`
构造一个新的产品对象，将当前行项目与之关联，并保存该产品。

下面来看一些自动生成的方法的实际使用。我们有如下模型：

```
class Product < ActiveRecord::Base
  has_many :line_items
end
```

```
class LineItem < ActiveRecord::Base
  belongs_to :product
end
```

包含该声明的类。下面的代码声明了 `invoices` 表为 `orders` 表的子表：

```
class Order < ActiveRecord::Base
  has_one :invoice
end
```

| 声明 | 外键 | 目标类 | 目标表 |
|---|---|---|---|
| has_one :invoice | order_id<br>（在 invoices 表中） | Invoice | invoices |

`has_one` 声明在模型对象中定义的方法集与 `belongs_to` 相同，因此给定前面的类定义，我们可以这样写：

```
order = Order.new(... attributes ...)
invoice = Invoice.new(... attributes ...)
order.invoice = invoice
```

如果某个父行没有对应的子行，`has_one` 关联将被设为 nil（在 Ruby 中视为 false）。这让你可以编写如下代码：

```
if order.invoice
  print_invoice(order.invoice)
end
```

如果你向 `has_one` 关联赋值一个新对象时，已经存在一个子对象，那么该已有对象将被更新以移除它与父行的外键关联（外键会被设为 null）。这如图 19.1（下一页）所示。

##### has_one 的选项

你可以通过向 `has_one` 传递选项哈希来修改其默认行为。除了我们在 `belongs_to` 中看到的 `:class_name`、`:foreign_key` 和 `:conditions` 选项之外，`has_one` 还有更多选项。其中大多数我们会稍后讨论，但有一个我们可以现在介绍。

`:dependent` 选项告诉 Active Record 在销毁父表中的某一行时该如何处理子行。它有三种可能的值：

- `:dependent => :destroy`
  子行会在父行被销毁的同时被销毁。
- `:dependent => :delete`
  子行会在父行被销毁时被删除，*不会*调用其 `destroy` 方法。
- `:dependent => :nullify`
  子行会在父行被销毁时成为孤儿，实现方式是设置子行的外键为 null。




图 19.1：向 has_one 关系添加内容

##### has_many 声明

has_many 定义一个行为类似于子对象集合的属性：

```
class Order < ActiveRecord::Base
  has_many :line_items
end
```

| 声明 | 外键 | 目标类 | 目标表 |
|---|---|---|---|
| has_many :line_items | order_id（在 line_items 中） | LineItem | line_items |

你可以将子对象作为数组访问、查找特定子对象以及添加新子对象。例如，以下代码向订单添加了一些订单项：

```
order = Order.new
params[:products_to_buy].each do |prd_id, qty|
  product = Product.find(prd_id)
  order.line_items << LineItem.new(:product => product,
                                  :quantity => qty)
end
order.save
```

追加运算符（<<）不仅仅是将一个对象追加到订单内部的列表中。它还会将这些订单项关联回当前订单，方法是将它们的外键设置为当前订单的 id，并在父订单保存时自动保存这些订单项。

我们可以遍历 has_many 关系的子对象——该属性充当数组：

```
order = Order.find(123)
total = 0.0

order.line_items.each do |li|
  total += li.quantity * li.unit_price
end
```

与 has_one 一样，你可以通过向 has_many 提供选项哈希来修改 Active Record 的默认行为。:class_name、:foreign_key 和 :conditions 选项的工作方式与它们在 has_one 方法中的工作方式相同。

:dependent 选项可以取 :destroy、:nullify 和 :delete_all 这些值——它们的含义与 has_one 中相同，只是应用于所有子行。

:dependent => :destroy 的工作方式是遍历子表，对每一行调用 destroy，这些行的外键引用父表中正在被删除的行。

然而，如果子表仅由父表使用（也就是说，它没有其他依赖项），并且没有在删除时执行任何操作的钩子方法，你可以改用 :dependent => :delete_all。此选项会在单个 SQL 语句中删除子行（这会更快）。

你可以通过设置 :finder_sql 和 :counter_sql 选项来覆盖 Active Record 用于获取和统计子行的 SQL。当仅使用 :conditions 选项添加 where 子句不够用时，这很有用。例如，你可以为特定产品创建所有订单项的集合：

```
class Order < ActiveRecord::Base
  has_many :rails_line_items,
    :class_name => "LineItem",
    :finder_sql => "select l.* from line_items l, products p " +
                   " where l.product_id = p.id " +
                   "       and p.title like '%rails%'"
end
```

:counter_sql 选项用于覆盖 Active Record 在统计行数时使用的查询。如果指定了 :finder_sql 而未指定 :counter_sql，Active Record 会通过将 finder SQL 的 select 部分替换为 select count(*) 来生成 counter SQL。

如果你希望在遍历集合时按特定顺序排列，则需要指定 :order 选项。你提供的 SQL 片段就是出现在 select 语句中 order by 子句之后的文本。它由一列或多列名称组成。集合将根据列表中的第一列排序。如果两行在该列中具有相同的值，则排序将使用列表中的第二项来决定它们的顺序，依此类推。每列的默认排序顺序为升序——在列名后面加上关键字 DESC 可反转此顺序。

以下代码可能用于指定订单的订单项按数量排序（数量最小的在前）：

```
class Order < ActiveRecord::Base
  has_many :line_items,
    :order => "quantity, unit_price DESC"
end
```

如果两个订单项数量相同，则单价最高的将排在前面。

之前讨论 has_one 时，我们提到它也支持 :order 选项。这似乎很奇怪——如果一个父对象只与一个子对象关联，那么获取该子对象时指定排序有什么意义呢？

事实证明，Active Record 可以在底层数据库不存在 has_one 关系的情况下创建这种关系。例如，一个客户可能有许多订单，这是一种 has_many 关系。但该客户只有一个最近订单。我们可以使用 has_one 结合 :order 选项来表达这一点：

```
class Customer < ActiveRecord::Base
  has_many :orders
  has_one  :most_recent_order,
    :class_name => 'Order',
    :order      => 'created_at DESC'
end
```

此代码在客户模型中创建了一个新属性 most_recent_order。它将引用具有最新 created_at 时间戳的订单。我们可以使用该属性来查找客户最近的订单：

```
cust = Customer.find_by_name("Dave Thomas")
puts "Dave last ordered on #{cust.most_recent_order.created_at}"
```

这之所以有效，是因为 Active Record 实际上使用如下 SQL 获取 has_one 关联的数据：

```
SELECT * FROM orders
WHERE  customer_id = ?
ORDER  BY created_at DESC
LIMIT  1
```

limit 子句意味着只返回一行，满足 has_one 声明中的“一”部分。order by 子句确保该行是最新的一行。

在探讨更高级的 Active Record 主题时，我们将介绍 has_many 支持的其他一些选项。

##### has_many() 添加的方法

与 belongs_to 和 has_one 一样，has_many 会向其宿主类添加许多与属性相关的方法。同样，这些方法的名称以属性名开头。在接下来的描述中，我们将列出该声明添加的方法：

```
class Customer < ActiveRecord::Base
  has_many :orders
end
```

- orders(force_reload=false)
  返回与此客户关联的订单数组（如果没有，则可能为空）。结果会被缓存，如果之前已获取过订单，则不会再次查询数据库，除非传入 true 作为参数。

- orders << order
  将 order 添加到此客户关联的订单列表中。

- orders.push(order1, ...)
  将一个或多个 order 对象添加到此客户关联的订单列表中。concat 是此方法的别名。

- orders.replace(order1, ...)
  用新的集合替换与此客户关联的订单集合，并检测当前子集合与新集合之间的差异，从而优化相应的数据库更改。

- orders.delete(order1, ...)
  从此客户关联的订单列表中移除一个或多个 order 对象。如果关联被标记为 :dependent => :destroy 或 :delete_all，则每个子对象都会被销毁。否则，它会将其 customer_id 外键设为 null，从而断开关联。

- orders.delete_all
  对所有子行调用关联的 delete 方法。

- orders.destroy_all
  对所有子行调用关联的 destroy 方法。

- orders.clear
  取消所有订单与此客户的关联。与 delete 类似，这会断开关联，但仅当订单被标记为 :dependent 时才会从数据库中删除这些订单。

- orders.find(options...)
  发出常规 find 调用，但结果被限制为仅返回与此客户关联的订单。这适用于 id、:all 和 :first 形式。

- orders.count(options...)
  返回子对象数量。如果你指定了自定义 finder 或 count SQL，则使用该 SQL。否则，使用标准的 Active Record count，并限制为具有相应外键的子行。可以提供 count 的任何可选参数。

- orders.size
  如果你已经加载了关联（通过访问它），则返回该集合的大小。否则，通过查询数据库返回数量。与 count 不同，size 方法会遵循传给 has_many 的任何 :limit 选项，并且不使用 finder_sql。

- orders.length
  强制重新加载关联，然后返回其大小。

- orders.empty?
  等同于 orders.size.zero?。

- orders.sum(options...)
  等同于对关联中的行调用常规的 Active Record sum 方法（见第 338 页）。请注意，这是使用 SQL 函数对数据库中的行进行操作，而不是遍历内存中的集合。

- orders.uniq
  返回具有唯一 id 的子对象数组。

- orders.build(attributes={})
  构造一个新的 order 对象，使用给定属性初始化，并与客户关联。该对象不会被保存。

- orders.create(attributes={})
  构造并保存一个新的 order 对象，使用给定属性初始化，并与客户关联。

##### has_and_belongs_to_many 声明

has_and_belongs_to_many（以下简称 “habtm”，以节省我们可怜的打字手指）在很多方面与 has_many 类似。“habtm” 创建一个本质上为集合的属性。该属性支持与 has_many 相同的方法。此外，“habtm” 允许你在关联两个对象时向连接表添加信息（尽管，我们稍后将看到，这种功能已逐渐不受青睐）。




# 是的，这令人困惑……

你可能已经注意到，通过 `has_many` 添加到 Active Record 类中的方法存在相当多的重复（或几乎重复）。例如，`count`、`size` 和 `length` 之间的差异，或者 `clear`、`destroy_all` 和 `delete_all` 之间的差异，都很微妙。这主要是因为 Active Record 中的功能随着时间的推移逐渐累积。随着新选项的加入，现有方法不一定能及时更新。我们猜测在某个时候这个问题会得到解决，这些方法将会被统一。值得研究一下在线的 Rails API 文档，因为本书出版后 Rails 很可能已经发生了变化。

让我们看看除了商店应用之外的另一个例子来说明“habtm”。也许我们正在使用 Rails 编写一个社区网站，用户可以阅读文章。有许多用户和许多文章，任何用户都可以阅读任何文章。为了跟踪目的，我们想知道阅读每篇文章的人以及每个人阅读过的文章。我们还想知道用户最后一次查看某篇特定文章的时间。我们将用一个简单的连接表来实现这一点。在 Rails 中，连接表的名字是两个被连接表的名字按字母顺序拼接而成：

![](img/a160fc3a330a0b3b2a764d41d614e688_370_0.png)

我们将两个模型类设置为通过这个表相互关联：

```
class Article < ActiveRecord::Base
  has_and_belongs_to_many :users
  # ...
end
```

```
class User < ActiveRecord::Base
  has_and_belongs_to_many :articles
  # ...
end
```

这允许我们执行诸如列出阅读过文章 123 的所有用户以及 pragdave 阅读过的所有文章等操作：

```
# Who has read article 123?
article = Article.find(123)
readers = article.users
```

```
# What has Dave read?
dave = User.find_by_name("pragdave")
articles_that_dave_read = dave.articles
```

```
# How many times has each user read article 123
counts = Article.find(123).users.count(:group => "users.name")
```

当我们的应用注意到有人阅读了一篇文章时，它将他们的用户记录与文章关联起来。我们将在 User 类中使用一个实例方法来实现这一点：

```
class User < ActiveRecord::Base
  has_and_belongs_to_many :articles

  # This user just read the given article
  def just_read(article)
    articles << article
  end

  # ...
end
```

如果我们想要在用户与文章之间的关联中记录更多信息，比如记录用户阅读文章的时间，那该怎么办？在这种情况下，你应该改用常规的 Active Record 模型作为连接表（请记住，在“habtm”中，连接表不是一个 Active Record 模型）。我们将在下一节讨论这种方案。

与其他关系方法一样，“habtm”支持一系列覆盖 Active Record 默认值的选项。`:class_name`、`:foreign_key` 和 `:conditions` 的工作方式与其他 `has_` 方法中的相同（`:foreign_key` 选项设置在连接表中指向该表的外键列的名称）。此外，“habtm”还支持覆盖连接表名称、连接表中外键列名称以及用于查找、插入和删除两个模型之间链接的 SQL 的选项。详情请参阅 API 文档。

##### 关联集合回调

我们还可以定义 `before_add`、`after_add`、`before_remove` 和 `after_remove` 回调，这些回调在我们向关联集合添加对象或从中移除对象时触发：

```
class User < ActiveRecord::Base
  has_and_belongs_to_many :articles, :after_add => :categorize

  def categorize(article)
    # ...
  end
end
```

也可以通过传递数组来定义多个回调。如果任何一个 `before_add` 或 `before_remove` 回调抛出异常，该对象将不会被添加或移除。

##### 使用模型作为连接表

目前 Rails 的思路是保持连接表的纯净——连接表应该只包含一对外键列。每当你觉得需要向这种表添加更多数据时，你实际上是在创建一个新模型，因为连接表从简单的链接机制变成了应用业务中一个成熟的参与者。让我们回顾之前关于文章和用户的例子。

在简单的“habtm”实现中，连接表记录了一篇文章被用户阅读的事实。连接表中的行没有独立的存在。但很快我们发现自己想向这个表添加信息。我们想记录读者何时阅读了文章，以及阅读完成后给了多少颗星。连接表突然有了自己的生命，值得拥有自己的 Active Record 模型。我们称之为 Reading。其模式如下所示：

![](img/a160fc3a330a0b3b2a764d41d614e688_372_0.png)

使用我们在本章中到目前为止看到的 Rails 工具，我们可以用以下方式对此建模：

```
class Article < ActiveRecord::Base
  has_many :readings
end
```

```
class User < ActiveRecord::Base
  has_many :readings
end
```

```
class Reading < ActiveRecord::Base
  belongs_to :article
  belongs_to :user
end
```

当用户阅读文章时，我们可以记录该事实：

```
reading = Reading.new
reading.rating  = params[:rating]
reading.read_at = Time.now
reading.article = current_article
reading.user    = session[:user]
reading.save
```

然而，与“habtm”解决方案相比，我们失去了一些东西。我们不再能轻松地询问一篇文章有哪些读者，或询问一个用户阅读了哪些文章。这就是 `:through` 选项的用武之地。让我们更新我们的文章和用户模型：

```
class Article < ActiveRecord::Base
  has_many :readings
  has_many :users, :through => :readings
end
```

```
class User < ActiveRecord::Base
  has_many :readings
  has_many :articles, :through => :readings
end
```

两个新的 `has_many` 声明上的 `:through` 选项告诉 Rails，`readings` 表可以用于从（例如）一篇文章导航到阅读过该文章的多个用户。现在我们可以编写如下代码：

```
readers = an_article.users
```

在幕后，Rails 构造必要的 SQL 来返回所有在 `readers` 表中被引用的用户行，这些 `readers` 行引用了原始文章。（呼！）

`:through` 参数指定在原始模型类中要导航通过的关联。因此，当我们这样说时：

```
class Article < ActiveRecord::Base
  has_many :readings
  has_many :users, :through => :readings
end
```

`:through => :readings` 参数告诉 Active Record 使用 `has_many :readings` 关联来查找名为 Reading 的模型。

我们给关联起的名字（此处为 `:users`）然后告诉 Active Record 使用哪个属性来查找用户（`user_id`）。你可以通过向 `has_many` 声明添加 `:source` 参数来更改这一点。例如，到目前为止，我们称阅读过文章的人为 `users`，仅仅因为这是 Reading 模型中关联的名字。然而，我们可以很容易地改称他们为 `readers`——我们只需要覆盖所使用的关联名称：

```
class Article < ActiveRecord::Base
  has_many :readings
  has_many :readers, :through => :readings, :source => :user
end
```

事实上，我们还可以更进一步。这仍然是一个 `has_many` 声明，所以它会接受所有 `has_many` 参数。

例如，让我们创建一个关联，返回所有给我们文章打了四星或更高评分的用户：

```
class Article < ActiveRecord::Base
  has_many :readings
  has_many :readers, :through => :readings, :source => :user
  has_many :happy_users, :through => :readings, :source => :user,
    :conditions => 'readings.rating >= 4'
end
```

##### 去除重复

`has_many :through` 返回的集合只是跟随底层连接关系的结果。如果某个用户阅读了一篇特定文章三次，那么向那篇文章询问其用户列表将返回该用户模型的三个副本（连同其他阅读过该文章的用户）。有两种方法可以去除这些重复。

首先，我们可以向 `has_many` 声明添加 `:uniq => true` 限定符：

```
class Article < ActiveRecord::Base
  has_many :readings
  has_many :users, :through => :readings, :uniq => true
end
```

这完全在 Active Record 内部实现；数据库返回完整的一组行，然后 Active Record 处理它并消除任何重复的对象。

还有一种技巧可以让我们在数据库中去重。我们可以覆盖 Active Record 生成的 SQL 的 `select` 部分，添加 `distinct` 限定符。我们必须记得添加表名，因为生成的 SQL 语句中包含一个连接。

```
class Article < ActiveRecord::Base
  has_many :readings
  has_many :users, :through => :readings, :select => "distinct users.*"
end
```

我们可以使用 `<<` 方法（别名为 `push`）创建新的 `:through` 关联。关联的两端都必须事先保存，这样才行。

```
class Article < ActiveRecord::Base
  has_many :readings
  has_many :users, :through => :readings
end
```

```
user = User.create(:name => "dave")
article = Article.create(:name => "Join Models")

article.users << user
```

我们还可以使用 `create!` 在关联的远端创建一行。




这段代码等价于之前的示例：

```
article = Article.create(:name => "Join Models")
article.users.create!(:name => "dave")
```

请注意，使用这种方法无法在中间表中设置属性。

##### 扩展关联

关联声明（belongs_to、has_xxx）是对模型对象之间业务关系的陈述。相当频繁地，与该特定关联相关联的是额外的业务逻辑。在之前的示例中，我们定义了文章与其读者之间的关系，称为 Reading。该关系包含了用户对刚读过的文章的评分。给定一个用户，我们如何获取他们评分在三颗星或更高的所有文章的列表？四颗星或更高？

我们已经看到了一种方法：我们可以构建新的关联，使结果集满足某些额外条件。我们在上一页的 happy_users 关联中就是这样做的。然而，这种方法受限——我们无法参数化查询，让调用者决定什么评分算作“happy”。

另一种方法是让使用我们模型的代码在查询本身上添加额外的条件：

```
user = User.find(some_id)
user.articles.find(:all, :conditions => [ 'rating >= ?', 3])
```

这可行，但会轻微破坏封装：我们真的希望将基于评分查找文章的想法封装在 articles 关联内部。Rails 允许我们通过向任何 has_many 声明添加一个块来实现这一点。在此块中定义的任何方法都将成为关联的方法。

以下代码向 user 模型中的 articles 关联添加了 finder 方法 rated_at_or_above：

```
class User < ActiveRecord::Base
  has_many :readings
  has_many :articles, :through => :readings do
    def rated_at_or_above(rating)
      find :all, :conditions => ['rating >= ?', rating]
    end
  end
end
```

给定一个 user 模型对象，我们现在可以调用此方法来检索他们高度评分的文章列表：

```
user = User.find(some_id)
good_articles = user.articles.rated_at_or_above(4)
```

合并到单个数据库表中。该表包含层次结构中所有类的所有属性的列。它还额外包含一个列，按惯例称为 type，用于标识任何特定行所代表的特定类。这在第 19.2 图中有所说明，见下一页。

在 Active Record 中使用单表继承非常简单。在模型类中定义你需要的继承层次结构，并确保对应于层次结构基类的表包含该层次结构中所有类的所有属性的列。表还必须额外包含一个 type 列，用于区分相应模型对象的类。

在定义表时，请记住子类的属性只会出现在对应于这些子类的表行中；例如，员工没有 balance 属性。因此，你必须定义表以允许任何不在所有子类中出现的列为空值。以下是创建第 19.2 图中所示表的迁移，见下一页：

```
create_table :people, :force => true do |t|
  t.string :type

  # common attributes
  t.string :name
  t.string :email

  # attributes for type=Customer
  t.decimal :balance, :precision => 10, :scale => 2

  # attributes for type=Employee
  t.integer :reports_to
  t.integer :dept

  # attributes for type=Manager
  # -- none --
end
```

我们可以定义我们的模型对象层次结构：

```
class Person < ActiveRecord::Base
end

class Customer < Person
end

class Employee < Person
  belongs_to :boss, :class_name => "Manager", :foreign_key => :reports_to
end
```

```
Customer.create(:name => 'Bert Public', :email => "b@public.net", :balance => 12.45)

barney = Employee.new(:name => 'Barney Rub', :email => "barney@here.com", :dept => 23)

barney.boss = wilma
barney.save!
```

```
manager = Person.find_by_name("Wilma Flint")
puts manager.class      #=> Manager
puts manager.email      #=> wilma@here.com
puts manager.dept       #=> 23
```

```
customer = Person.find_by_name("Bert Public")
puts customer.class    #=> Customer
puts customer.email    #=> b@public.net
puts customer.balance  #=> 12.45
```

注意我们如何要求基类 Person 查找一行，但在一种情况下返回对象的类是 Manager，在另一种情况下是 Customer；Active Record 通过检查行的 type 列并创建适当的对象来确定类型。

还请注意我们在 Employee 类中使用的一个小技巧。我们使用 belongs_to 创建了一个名为 boss 的属性。该属性使用 reports_to 列，该列指向 people 表。这就是让我们能够说 barney.boss = wilma 的原因。

使用单表继承时有一个相当明显的限制。两个子类不能具有名称相同但类型不同的属性，因为这两个属性将映射到底层模式中的同一列。

还有一个不太明显的限制。属性 type 也是内置 Ruby 方法的名称，因此直接访问它以设置或更改行的类型可能会导致奇怪的 Ruby 消息。相反，通过创建适当类的对象隐式访问它，或通过模型对象的索引接口访问它，使用类似以下内容：

```
person[:type] = 'Manager'
```

##### 多态关联

STI 的一个主要缺点是存在一个单一的底层表，其中包含继承树中所有子类的所有属性。我们可以使用 Rails 的第二种异构聚合形式——多态关联——来克服这个问题。

##### Joe 提问...

###### 如果我们想要真正的继承怎么办？

单表继承很聪明——只要我们子类化一个 Active Record 类，它就会自动启用。但如果我们想要真正的继承怎么办？如果我们想通过定义一个抽象基类和一组子类来在 Active Record 类的集合之间共享某些行为怎么办？

答案是在我们的抽象基类中定义一个名为 abstract_class? 的类方法。该方法应返回 true。这有两个效果。首先，Active Record 将永远不会尝试查找对应于此抽象类的数据库表。其次，此类的所有子类都将被视为独立的 Active Record 类——每个类都映射到自己的数据库表。

当然，更好的做法可能是使用包含共享功能的 Ruby 模块，并将此模块混入需要该行为的 Active Record 类中。

多态关联依赖于外键列只是一个整数这一事实。虽然有一个约定，即名为 user_id 的外键引用 users 表中的 id 列，但没有法律强制执行这一点。³

在计算机科学中，多态是一种机制，允许你抽象出某物接口的本质，而不管其底层实现如何。例如，加法方法就是多态的，因为它适用于整数、浮点数，甚至字符串。

在 Rails 中，多态关联是一种关联到不同类型对象的关联。假设这些对象都共享一些共同特征，但它们会有不同的表示。

为了具体说明，让我们看一个简单的资产管理系统。我们在简单的目录中索引我们的资产。每个目录条目包含一个名称、获取日期，以及对实际资源的引用：文章、图像、声音等等。不同资源类型对应不同的数据库表和不同的 Active Record 模型，但它们都是资产，并且都被编目。

3. 如果你指定数据库应强制执行外键约束，多态关联将无法工作。





请注意，这些模型类不需要继承自一个共同的基类（当然，除了 ActiveRecord::Base）。关键在于 `has_one` 的 `:as` 选项。它指定了目录条目与资源之间的关联是多态的，使用目录条目中的 resource 属性。让我们试试：

```
a = Article.new(:content => "This is my new article")
c = CatalogEntry.new(:name => 'Article One', :acquired_at => Time.now)
c.resource = a
c.save!
```

让我们看看数据库中发生了什么。文章没有什么特别之处：

```
depot> sqlite3 -line db/development.sqlite3 "select * from articles"
  id = 1
content = This is my new article
```

目录条目具有指向文章的外键引用，并且还记录了它引用的 Active Record 对象的类型（一个 Article）：

```
depot> sqlite3 -line db/development.sqlite3 "select * from catalog_entries"
  id = 1
  name = Article One
acquired_at = 2008-05-14 11:29:28
resource_id = 1
resource_type = Article
```

我们可以从关系的两边访问数据：

```
article = Article.find(1)
p article.catalog_entry.name    #=> "Article One"

cat = CatalogEntry.find(1)
resource = cat.resource
p resource                        #=> #<Article:0x640d80 @attributes={"id"=>"1", "content"=>"This is my new article"}>
```

这里巧妙的部分是 `resource = cat.resource` 这一行。我们要求目录条目提供其资源，它返回一个 Article 对象。它正确地确定了 Active Record 类，从适当的数据库表（articles）读取，并返回了正确的类对象。

让我们让它更有趣一些。让我们清空数据库，然后添加所有三种类型的资源：

```
c = CatalogEntry.new(:name => 'Article One', :acquired_at => Time.now)
c.resource = Article.new(:content => "This is my new article")
c.save!

c = CatalogEntry.new(:name => 'Image One', :acquired_at => Time.now)
c.resource = Image.new(:content => "some binary data")
c.save!

c = CatalogEntry.new(:name => 'Sound One', :acquired_at => Time.now)
c.resource = Sound.new(:content => "more binary data")
c.save!
```

现在我们的数据库看起来更有趣了：

```
depot> sqlite3 -line db/development.sqlite3 "select * from articles"
    id = 1
content = This is my new article

depot> sqlite3 -line db/development.sqlite3 "select * from images"
    id = 1
content = some binary data

depot> sqlite3 -line db/development.sqlite3 "select * from sounds"
    id = 1
content = more binary data

depot> sqlite3 -line db/development.sqlite3 "select * from catalog_entries"
    id = 2
    name = Article One
acquired_at = 2008-05-14 12:03:24
    resource_id = 2
resource_type = Article

    id = 3
    name = Image One
acquired_at = 2008-05-14 12:03:24
    resource_id = 1
resource_type = Image

    id = 4
    name = Sound One
acquired_at = 2008-05-14 12:03:24
    resource_id = 1
resource_type = Sound
```

注意目录中所有三个外键的 id 都是 1——它们通过 type 列来区分。

现在我们可以通过遍历目录来检索所有三个资源：

```
Download e1/ar/polymorphic.rb
CatalogEntry.find(:all).each do |c|
  puts "#{c.name}: #{c.resource.class}"
end
```

这会产生以下输出：

```
Article One:  Article
Image One:  Image
Sound One:  Sound
```

#### 19.5 自引用连接

表中的一行可以引用同一表中另一行。例如，公司中的每个员工可能都有一个经理和一个导师，而他们也是员工。你可以在 Rails 中使用以下 Employee 类来建模这一点：

```
class Employee < ActiveRecord::Base
  belongs_to :manager,
    :class_name => "Employee",
    :foreign_key => "manager_id"

  belongs_to :mentor,
    :class_name => "Employee",
    :foreign_key => "mentor_id"

  has_many :mentored_employees,
    :class_name => "Employee",
    :foreign_key => "mentor_id"

  has_many :managed_employees,
    :class_name => "Employee",
    :foreign_key => "manager_id"
end
```

让我们加载一些数据。Clem 和 Dawn 各自都有一个经理和一个导师：

```
Employee.delete_all

adam = Employee.create(:name => "Adam")
beth = Employee.create(:name => "Beth")

clem = Employee.new(:name => "Clem")
clem.manager = adam
clem.mentor  = beth
clem.save!

dawn = Employee.new(:name => "Dawn")
dawn.manager = adam
dawn.mentor  = clem
dawn.save!
```

然后我们可以遍历关系，回答诸如“X 的导师是谁？”和“Y 管理哪些员工？”这样的问题

```
p adam.managed_employees.map { |e| e.name }  # => [ "Clem", "Dawn" ]
p adam.mentored_employees                  # => []
p dawn.mentor.name                         # => "Clem"
```

你可能还想查看各种 acts as relationships。

接下来我们将创建模型类。请注意，在 Parent 类中，我们根据 position 列的值对子项进行排序。这确保了从数据库获取的数组按正确的列表顺序排列。

```
class Parent < ActiveRecord::Base
  has_many :children, :order => :position
end

class Child < ActiveRecord::Base
  belongs_to :parent
  acts_as_list :scope => :parent
end
```

在 Child 类中，我们有惯例的 belongs_to 声明，建立了与父级的连接。我们还有一个 acts_as_list 声明。我们用 `:scope` 选项对其进行限定，指定列表是按父记录划分的。如果没有这个作用域操作符，所有 children 表中的条目将有一个全局列表。

现在我们可以设置一些测试数据：我们将为特定父级创建四个子项，分别称为 One、Two、Three 和 Four：

```
parent = Parent.create
%w{ One Two Three Four}.each do |name|
  parent.children.create(:name => name)
end
parent.save
```

我们将编写一个方法来让我们检查列表的内容。这里有一个细微之处——注意我们将 true 传递给 children 关联。这强制它每次访问时都重新加载。这是因为各种 `move_` 方法会更新数据库中的子项，但由于它们直接操作子项，父级不会立即知道更改。重新加载会强制它们被带入内存。

```
def display_children(parent)
  puts parent.children(true).map {|child| child.name }.join(", ")
end
```

最后我们将玩弄我们的列表。注释显示了 display_children 的输出：

```
display_children(parent)      #=> One, Two, Three, Four

puts parent.children[0].first?   #=> true

two = parent.children[1]
puts two.lower_item.name        #=> Three
puts two.higher_item.name      #=> One

parent.children[0].move_lower
display_children(parent)       #=> Two, One, Three, Four

parent.children[2].move_to_top
display_children(parent)       #=> Three, Two, One, Four

parent.children[2].destroy
display_children(parent)       #=> Three, Two, Four
```

列表库使用术语 *lower* 和 *higher* 来指代元素的相对位置。Higher 表示更靠近列表前端；lower 表示更靠近列表末尾。因此列表顶部等同于前端，列表底部等同于末端。方法 `move_higher`、`move_lower`、`move_to_bottom` 和 `move_to_top` 在列表中移动特定项，并自动调整其他元素的位。

`higher_item` 和 `lower_item` 返回当前元素的下一个和上一个元素，而 `first?` 和 `last?` 如果当前元素位于列表的前端或末端则返回 true。

新创建的子项会自动添加到列表末尾。当子行被销毁时，列表中在其之后的子项随后会向上移动以填补空白。

##### Acts As Tree

Active Record 提供了将表的行组织成层次结构或树形结构的支持。这对于创建具有子条目的条目且这些子条目可能又有自己的子条目的结构很有用。分类列表通常具有这种结构，权限描述、目录列表等也是如此。

这种树状结构是通过在表中添加一列（默认称为 `parent_id`）实现的。该列是回指同一表的外键引用，将子行链接到其父行。这在第 19.4 图中有所说明，在下一页。

为了展示树的工作原理，让我们创建一个简单的 category 表，其中每个顶级类别可能有子类别，每个子类别可能有额外的子类别级别。请注意指向同一表的外部键。





![](img/a160fc3a330a0b3b2a764d41d614e688_390_0.png)

| categories |
| id | parent_id | rest_of_data |
| 1 | null | ... |
| 2 | 1 | ... |
| 3 | 1 | ... |
| 4 | 3 | ... |
| 5 | 1 | ... |
| 6 | 3 | ... |
| 7 | 2 | ... |
| 8 | 6 | ... |
| 9 | 6 | ... |

## Figure 19.4: Representing a tree using parent links in a table

```
Download e1/ar/acts_as_tree.rb
create_table :categories, :force => true do |t|
  t.string :name
  t.integer :parent_id
end
```

The corresponding model uses the method with the tribal name acts_as_tree to specify the relationship. The :order parameter means that when we look at the children of a particular node, we'll see them arranged by their name column:

```
Download e1/ar/acts_as_tree.rb
class Category < ActiveRecord::Base
  acts_as_tree :order => "name"
end
```

Normally you'd have some end-user functionality to create and maintain the category hierarchy. Here, we'll just create it using code. Note how we manipulate the children of any node using the children attribute:

```
Download e1/ar/acts_as_tree.rb
root        = Category.create(:name => "Books")
fiction     = root.children.create(:name => "Fiction")
non_fiction = root.children.create(:name => "Non Fiction")

non_fiction.children.create(:name => "Computers")
non_fiction.children.create(:name => "Science")
non_fiction.children.create(:name => "Art History")

fiction.children.create(:name => "Mystery")
fiction.children.create(:name => "Romance")
fiction.children.create(:name => "Science Fiction")
```

##### David Says. . .

###### Why Things in Associations Get Saved When They Do

It might seem inconsistent that assigning an order to the invoice will not save the association immediately, but the reverse will. This is because the invoices table is the only one that holds the information about the relationship. Hence, when you associate orders and invoices, it’s always the invoice rows that hold the information. When you assign an order to an invoice, you can easily make this part of a larger update to the invoice row that might also include the billing date. It’s therefore possible to fold what would otherwise have been two database updates into one. In an ORM, it’s generally the rule that fewer database calls is better.

When an order object has an invoice assigned to it, it still needs to update the invoice row. So, there’s no additional benefit in postponing that association until the order is saved. In fact, it would take considerably more software to do so. And Rails is all about less software.

the invoice that it’s associated with an order. The two are almost equivalent. The difference is in the way they save (or don’t save) objects to the database. If you assign an object to a has_one association in an existing object, that associated object will be automatically saved:

```
order = Order.find(some_id)
an_invoice = Invoice.new(...)
order.invoice = an_invoice      # invoice gets saved
```

If instead you assign a new object to a belongs_to association, it will never be automatically saved:

```
order = Order.new(...)      # Order will not be saved here
an_invoice.order = order    # both the invoice and the order get saved
an_invoice.save
```

Finally, there’s a danger here. If the child row cannot be saved (for example, because it fails validation), Active Record will not complain—you’ll get no indication that the row was not added to the database. For this reason, we strongly recommend that instead of the previous code, you write this:

```
invoice = Invoice.new
# fill in the invoice
invoice.save!
an_order.invoice = invoice
```

The save! method throws an exception on failure, so at least you’ll know that something went wrong.

And this example will bring it all down to as few queries, possibly even to the point of doing all the work in a single query:

```
for post in Post.find(:all, :include => [:author, :comments])
  puts "Post:           #{post.title}"
  puts "Written by:     #{post.author.name}"
  puts "Last comment on: #{post.comments.first.created_on}"
end
```

This preloading is not guaranteed to improve performance.⁵ And even if the optimization does work, the query can end up returning a lot of data to be converted into Active Record objects. If your application doesn’t use the extra information, you’ve incurred a cost for no benefit. You might also have problems if the parent table contains a large number of rows—compared with the row-by-row lazy loading of data, the preloading technique will consume a lot more server memory.

If you use :include, you’ll need to disambiguate all column names used in other parameters to find—prefix each with the name of the table that contains it. In the following example, the title column in the condition needs the table name prefix for the query to succeed:

```
for post in Post.find(:all, :conditions => "posts.title like '%ruby%'",
                     :include => [:author, :comments])
  # ...
end
```

#### 19.9 Counters

The has_many relationship defines an attribute that is a collection. It seems reasonable to be able to ask for the size of this collection: how many line items does this order have? And indeed you’ll find that the aggregation has a size method that returns the number of objects in the association. This method goes to the database and performs a select count(*) on the child table, counting the number of rows where the foreign key references the parent table row.

This works and is reliable. However, if you’re writing a site where you frequently need to know the counts of child items, this extra SQL might be an overhead you’d rather avoid. Active Record can help using a technique called counter caching. In the belongs_to declaration in the child model we can ask Active Record to maintain a count of the number of associated children in the parent table rows. This count will be automatically maintained—if we add a child row, the count in the parent row will be incremented, and if we delete a child row, it will be decremented.

5. In fact, it might not work at all! If your database doesn’t support left outer joins, you can’t use the feature. Oracle 8 users, for instance, will need to upgrade to version 9 to use preloading.

### Chapter 20

### Active Record Part III:
Object Life Cycle

So far we've looked at how to connect to Active Record, access data and attributes, and link together tables. This chapter rounds off our description of Active Record. It looks at the life cycle of Active Record objects; the validations and hooks that you can define affect how they are processed.

#### 20.1 Validation

Active Record can validate the contents of a model object. This validation can be performed automatically when an object is saved. You can also programmatically request validation of the current state of a model. If validation fails when you're saving an object, the object will not be written to the database; it will be left in memory in its invalid state. This allows you (for example) to pass the object back to a form so the user can correct the bad data.

Active Record distinguishes between models that correspond to an existing row in the database and those that don't. The latter are called new records (the new_record? method will return true for them). When you call the save method, Active Record will perform a SQL insert operation for new records and an update for existing ones.

This distinction is reflected in Active Record's validation workflow—you can specify validations that are performed on all save operations and other validations that are performed only on creates or updates.

At the lowest level you specify validations by listing one or more methods names as symbols on calls to the validate, validate_on_create, and validate_on_update class methods. validate methods are invoked on every save operation.

One of the other two is invoked depending on whether the record is new or whether it was previously read from the database.

You can also run validation at any time without saving the model object to the database by calling the valid? method. This invokes the same two validation methods that would be invoked if save had been called.

For example, the following code ensures that the username column is always set to something valid and that the name is unique for new User objects. (We’ll see later how these types of constraints can be specified more simply.)

```
class User < ActiveRecord::Base
  validate :valid_name?
  validate_on_create :unique_name?

private

  def valid_name?
    unless name && name =~ /^\w+$/
      errors.add(:name, "is missing or invalid")
    end
  end

  def unique_name?
    if User.find_by_name(name)
      errors.add(:name, "is already being used")
    end
  end
end
```

When a validate method finds a problem, it adds a message to the list of errors for this model object using errors.add. The first parameter is the name of the offending attribute, and the second is an error message. If you need to add an error message that applies to the model object as a whole, use the add_to_base method instead. (Note that this code uses the support method blank?, which returns true if its receiver is nil or an empty string.)

```
def one_of_name_or_email_required
  if name.blank? && email.blank?
    errors.add_to_base("You must specify a name or an email address")
  end
end
```

As we’ll see on page 536, Rails views can use this list of errors when displaying forms to end users—the fields that have errors will be automatically highlighted, and it’s easy to add a pretty box with an error list to the top of the form.

You can get the errors for a particular attribute using errors.on(:name) (aliased to errors[:name]), and you can clear the full list of errors using errors.clear. If you



查看 ActiveRecord::Errors 的 API 文档，你会发现许多其他方法。其中大部分已被更高级的验证辅助方法取代。

##### 验证辅助方法

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

##### validates_confirmation_of

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

###### 选项

| 选项 | 类型 | 描述 |
|------|------|------|
| :if | 代码 | 参见第 406 页的讨论。 |
| :unless | 代码 | 参见第 406 页的讨论。 |
| :message | 文本 | 默认为“doesn't match confirmation.” |
| :on | :save、:create 或 :update。 | |

##### validates_each

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

###### 选项

| 选项 | 类型 | 描述 |
|------|------|------|
| :allow_nil | 布尔 | 如果 :allow_nil 为 true，值为 nil 的属性将不会传入块中。默认情况下会传入。 |
| :if | 代码 | 参见第 406 页的讨论。 |
| :unless | 代码 | 参见第 406 页的讨论。 |
| :on | :save、:create 或 :update。 | |

##### validates_exclusion_of

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

###### 选项

| 选项 | 类型 | 描述 |
|------|------|------|
| :allow_nil | 布尔 | 如果为 true，nil 属性被视为有效。 |
| :allow_blank | 布尔 | 如果为 true，空白属性被视为有效。 |
| :if | 代码 | 参见第 406 页的讨论。 |
| :unless | 代码 | 参见第 406 页的讨论。 |
| :in（或 :within） | 可枚举 | 一个可枚举对象。 |
| :message | 文本 | 默认为“is not included in the list.” |
| :on | :save、:create 或 :update。 | |

##### validates_format_of

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

###### 选项

| 选项 | 类型 | 描述 |
|------|------|------|
| :if | 代码 | 参见第 406 页的讨论。 |
| :unless | 代码 | 参见第 406 页的讨论。 |
| :message | 文本 | 默认为“is invalid.” |
| :on | :save、:create 或 :update。 | |
| :with |  | 用于验证属性的正则表达式。 |

##### validates_inclusion_of

验证属性属于一组值。

```
validates_inclusion_of attr..., :in => enum [ options... ]
```

验证每个属性的值是否出现在 enum 中（支持 include? 谓词的任何对象）。

###### 选项（validates_uniqueness_of 的延续）

| 选项 | 类型 | 描述 |
|------|------|------|
| :message | 文本 | 默认为“has already been taken.” |
| :on | :save、:create 或 :update。 | |
| :scope | 属性 | 将检查限制为在列中具有与正在检查的行相同值的行。 |

##### 条件验证

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

##### 验证错误消息

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





```
:too_long      => "is too long (maximum is %d characters)",
:too_short      => "is too short (minimum is %d characters)",
:wrong_length  => "is the wrong length (should be %d characters)",
:taken          => "has already been taken",
:not_a_number   => "is not a number",
:greater_than   => "must be greater than %d",
:greater_than_or_equal_to => "must be greater than or equal to %d",
:equal_to       => "must be equal to %d",
:less_than      => "must be less than %d",
:less_than_or_equal_to => "must be less than or equal to %d",
:odd            => "must be odd",
:even           => "must be even"
```

要更改唯一性验证失败时返回的消息，你可以在你的 config/locales/en.yml 文件中编写如下代码：

```
en:
  activerecord:
    errors:
      taken: "is in use"
```

#### 20.2 回调

Active Record 控制着模型对象的生命周期——它创建模型对象，在它们被修改时进行监控，保存和更新它们，并目送它们被销毁。通过回调，Active Record 让我们的代码能够参与到这个监控过程中来。我们可以编写代码，在对象生命周期中的任何重要事件发生时被调用。借助这些回调，我们可以执行复杂的验证，在列值进出数据库时进行映射，甚至可以阻止某些操作完成。

Active Record 定义了二十个回调。其中十八个形成 before/after 对，环绕对 Active Record 对象的某个操作。例如，before_destroy 回调会在 destroy 方法被调用之前被调用，而 after_destroy 会在之后被调用。两个例外是 after_find 和 after_initialize，它们没有对应的 before_xxx 回调。（这两个回调在其他方面也有所不同，我们稍后会看到。）

在图 20.1 中（见下页），我们可以看到这十八个成对回调是如何环绕模型对象的基本 create、update 和 destroy 操作的。也许令人惊讶的是，验证前后的调用并不是严格嵌套的。

除了这十八个调用之外，after_find 回调会在任何 find 操作之后被调用，而 after_initialize 会在一个 Active Record 模型对象被创建之后被调用。

要让你的代码在回调期间执行，你需要编写一个处理器，并将其与相应的回调关联起来。

![](img/a160fc3a330a0b3b2a764d41d614e688_407_0.png)

## 图 20.1：Active Record 回调的顺序

实现回调有两种基本方式。

```
class Order < ActiveRecord::Base
  # ...
  def before_save
    self.payment_due ||= Time.now + 30.days
  end
end
```

定义回调的第二种基本方式是声明处理器。处理器可以是方法或块。¹ 你可以使用以事件命名的类方法将处理器关联到特定事件。要关联一个方法，请将其声明为 private 或 protected，并在处理器声明中将其名称指定为符号。要指定一个块，只需在声明后添加它。这个块会接收模型对象作为参数。

```
class Order < ActiveRecord::Base

  before_validation :normalize_credit_card_number

  after_create do |order|
    logger.info "Order #{order.id} created"
  end
```

1. 处理器也可以是包含要 eval 的代码的字符串，但这已弃用。

要完全禁用此行为，请使用以下代码：

```
ActiveRecord::Base.record_timestamps = false
```

##### 回调对象

作为直接在模型类中指定回调处理器的一种变体，你可以创建单独的处理器类来封装所有回调方法。这些处理器可以在多个模型之间共享。处理器类就是一个定义了回调方法（before_save、after_create 等）的类。在 app/models 中为这些处理器类创建源文件。

在使用处理器的模型对象中，你创建该处理器类的一个实例，并将该实例传递给各种回调声明。几个例子会让这一点更清楚。

```
class CreditCardCallbacks
  # Normalize the credit card number
  def before_validation(model)
    model.cc_number.gsub(/[-\s]/, '')
  end
end
```

现在，在我们的模型类中，我们可以安排调用这个共享回调：

```
class Order < ActiveRecord::Base
  before_validation CreditCardCallbacks.new
  # ...
end
```

```
class Subscription < ActiveRecord::Base
  before_validation CreditCardCallbacks.new
  # ...
end
```

在这个例子中，处理器类假设信用卡号存储在名为 cc_number 的模型属性中；Order 和 Subscription 都会有一个该名称的属性。但我们可以推广这个思路，使处理器类不那么依赖于使用它的类的实现细节。

现在我们可以安排从 orders 模型内部调用 Encrypter 类：

```
require "encrypter"

class Order < ActiveRecord::Base
  encrypter = Encrypter.new([:name, :email])

  before_save  encrypter
  after_save   encrypter
  after_find   encrypter

  protected
    def after_find
    end
end
```

我们创建一个新的 Encrypter 对象，并将其连接到 before_save、after_save 和 after_find 事件。这样，就在一个订单被保存之前，encrypter 中的 before_save 方法会被调用，依此类推。

那么，为什么我们要定义一个空的 after_find 方法呢？记住，我们说过出于性能原因，after_find 和 after_initialize 会被特殊对待。这种特殊对待的一个后果是，Active Record 只有在模型类中看到一个实际的 after_find 方法时，才会知道调用 after_find 处理器。我们必须定义一个空的占位符才能使 after_find 处理生效。

这一切都很好，但每个想要使用我们的加密处理器的模型类都需要包含大约八行代码，就像我们对 Order 类所做的那样。我们可以做得更好。我们将定义一个完成所有工作的辅助方法，并让该辅助方法可用于所有 Active Record 模型。为此，我们将它添加到 ActiveRecord::Base 类中：

```
Download e1/ar/encrypt.rb

class ActiveRecord::Base
  def self.encrypt(*attr_names)
    encrypter = Encrypter.new(attr_names)

    before_save  encrypter
    after_save   encrypter
    after_find   encrypter

    define_method(:after_find) { }
  end
end
```

有了这个，我们现在可以通过一次调用来为任何模型类的属性添加加密。

```
Download e1/ar/encrypt.rb
class Order < ActiveRecord::Base
  encrypt(:name, :email)
end
```

一个简单的驱动程序让我们可以对此进行实验：

```
Download e1/ar/encrypt.rb
o = Order.new
o.name = "Dave Thomas"
o.address = "123 The Street"
o.email = "dave@pragprog.com"
o.save
puts o.name

o = Order.find(o.id)
puts o.name
```

在控制台上，我们在模型对象中看到客户的名字（纯文本）：

```
ar> ruby encrypt.rb
Dave Thomas
Dave Thomas
```

然而，在数据库中，姓名和电子邮件地址被我们的工业级加密所掩盖：

```
depot> sqlite3 -line db/development.sqlite3 "select * from orders"
  id = 1
  user_id =
  name = Dbwf Tipnbt
  address = 123 The Street
  email = ebwf@qsbhq sph.dpn
```

##### 观察者

回调是一种很好的技术，但它们有时会导致模型类承担与模型本质并不真正相关的责任。例如，在第 408 页，我们创建了一个在订单创建时生成日志消息的回调。该功能并不是基本 Order 类的一部分——我们把它放在那里是因为回调在那个位置执行。

Active Record 观察器克服了这一限制。观察器会透明地将自身链接到模型类中，就像它是模型的一部分一样注册回调，但不需要对模型本身进行任何更改。下面是我们之前使用观察器编写的日志记录示例：

```
Download e1/ar/observer.rb
class OrderObserver < ActiveRecord::Observer
  def after_save(an_order)
    an_order.logger.info("Order #{an_order.id} created")
  end
end
```




当 Active Record 首次使用某个特定模型时，它会访问数据库并确定对应表的列集合。然后它会构建一组 `Column` 对象。这些对象可以通过 `columns` 类方法访问，而指定列的 `Column` 对象可以通过 `columns_hash` 方法获取。`Column` 对象编码了数据库列的名称、类型和默认值。

当 Active Record 从数据库读取信息时，它会构造一条 SQL `select` 语句。这条语句执行后，会返回零行或多行数据。Active Record 会为每一行构造一个新的模型对象，并将行数据加载到一个散列（hash）中，这个散列被称为属性数据（attribute data）。散列中的每个条目都对应于原始查询中的某一项，所使用的键值与结果集中该项的名称相同。

大多数时候，我们会使用标准的 Active Record finder 方法来从数据库检索数据。这些方法会返回所选中行的所有列。因此，返回的每个模型对象中的 attributes 散列都会包含每个列的条目，其中键是列名，值是列数据。

```
result = LineItem.find(:first)
p result.attributes
{"order_id"=>13, "quantity"=>1, "product_id"=>27,
"id"=>34, "unit_price"=>29.95}
```

通常，我们不会通过 attributes 散列来访问这些数据，而是使用属性方法：

```
result = LineItem.find(:first)
p result.quantity      #=> 1
p result.unit_price    #=> 29.95
```

但是，如果我们的查询返回了不对应表中任何列的值，会发生什么？例如，我们可能想在应用程序中执行以下查询：

```
select id, quantity, quantity*unit_price from line_items;
```

如果我们手动对数据库运行此查询，可能会看到类似下面这样的结果：

```
depot> sqlite3 -line db/development.sqlite3 \
"select id, quantity*unit_price from line_items"
        id = 3
quantity*unit_price = 29.95

        id = 4
quantity*unit_price = 59.9

        id = 5
quantity*unit_price = 44.95
```

请注意，结果集的列标题反映了我们在 select 语句中给出的表达式。Active Record 在填充 attributes 散列时使用的正是这些列标题。我们可以使用 Active Record 的 `find_by_sql` 方法运行同样的查询，然后查看生成的 attributes 散列：

```
result = LineItem.find_by_sql("select id, quantity, " +
							"quantity*unit_price " +
							"from line_items")
p result[0].attributes
```

输出显示，列标题已被用作 attributes 散列中的键：

```
{"id" => 23, "quantity*unit_price"=>"29.95", "quantity"=>1}
```

请注意，计算列的值是字符串。Active Record 知道表中列的类型，但许多数据库不会返回计算列的类型信息。在这个例子中，我们使用的是 MySQL，它不提供类型信息，因此 Active Record 将值保留为字符串。如果我们使用 Oracle，那么得到的会是一个 Float，因为 OCI 接口可以提取结果集中所有列的类型信息。

使用 `quantity*price` 这样的键来访问计算属性并不是特别方便，因此通常我们会使用 `as` 限定符重命名结果集中的列：

```
result = LineItem.find_by_sql("select id, quantity, " +
							" quantity*unit_price as total_price " +
							" from line_items")
p result[0].attributes
```

这将产生以下结果：

```
{"total_price"=>"29.95", "id"=>23 "quantity"=>1}
```

使用 `total_price` 属性会更方便：

```
result.each do |line_item|
  puts "Line item #{line_item.id}: #{line_item.total_price}"
end
```

但请记住，这些计算列的值会以字符串的形式存储在 attributes 散列中。如果你尝试类似下面的代码，可能会得到意想不到的结果：

```
TAX_RATE = 0.07
# ...
sales_tax = line_item.total_price * TAX_RATE
```

也许令人惊讶的是，上面示例中的代码将 `sales_tax` 设置为一个空字符串。`total_price` 的值是一个字符串，而字符串的 `*` 运算符会复制其内容。由于 `TAX_RATE` 小于 1，内容被复制了零次，结果就变成了空字符串。

不过还是有办法的！我们可以覆盖 Active Record 默认的属性访问器方法，为我们的计算字段执行所需的类型转换：

```
class LineItem < ActiveRecord::Base
  def total_price
    Float(read_attribute("total_price"))
  end
end
```

请注意，我们使用 `read_attribute` 方法而不是直接访问属性来取得属性的内部值。`read_attribute` 方法了解数据库列类型（包括包含序列化 Ruby 数据的列），并在需要时执行类型转换。这在我们当前的例子中并不特别有用，但在我们研究如何提供外观列（facade columns）时就会变得更有意义。

##### 外观列（Facade Columns）

有时候，我们使用的表结构中某些列的格式并不是最方便的。出于某种原因（也许是因为我们正在使用一个遗留数据库，或者因为其他应用程序依赖于这种格式），我们无法直接更改表结构。相反，我们的应用程序必须以某种方式处理它。如果我们能创建某种外观（facade），让列数据呈现出我们所希望的形式，那就再好不过了。

事实证明，我们可以通过覆盖 Active Record 提供的默认属性访问器方法来实现这一点。例如，假设我们的应用程序使用一个遗留的 `product_data` 表——这张表非常古老，以至于产品尺寸是以腕尺（cubits）³为单位存储的。在我们的应用程序中，我们更希望使用英寸（inches）⁴ 来处理，所以让我们定义一些执行必要转换的访问器方法：

```
class ProductData < ActiveRecord::Base
  CUBITS_TO_INCHES = 18
  def length
    read_attribute("length") * CUBITS_TO_INCHES
  end
  def length=(inches)
    write_attribute("length", Float(inches) / CUBITS_TO_INCHES)
  end
end
```

##### 简易记忆化（Easy Memoization）

如果你在 facade 列访问器中放入了大量逻辑，就可能面临这些方法被执行多次的情况。对于相对静态且访问开销较大的数据，这种开销会很快累积起来。另一种方法是请 Rails 在首次访问时为你“记忆化”（memoize，即缓存）这些数据：

```
class ProductData < ActiveRecord::Base
  def length
    # ...
  end

  memoize :length
end
```

你可以在一次 `memoize` 调用中传入多个符号（symbol），另外还有 `unmemoize_all` 和 `memoize_all` 可以用来强制刷新并重新加载缓存。

3. 腕尺的定义是：从你的手肘到最长手指指尖的距离。由于这显然带有主观性，埃及人基于当时在位的法老，将其标准化为“皇家腕尺”。他们甚至还有一个标准制定机构，将一根标准的腕尺测量并标记在花岗岩石上（http://www.ncsl.org/misc/cubit.cfm）。

4. 当然，英寸也是一种遗留的度量单位，但我们这里就不争论这个问题了。

#### 20.4 事务（Transactions）

数据库事务将一系列更改分组在一起，使得要么所有更改都被应用，要么所有更改都不被应用。事务需求最经典的例子（也是 Active Record 自身文档中使用的例子）是在两个银行账户之间转账。基本逻辑很简单：

```
account1.deposit(100)
account2.withdraw(100)
```

然而，我们必须小心。如果存款成功，但出于某种原因取款失败（也许客户透支了），会发生什么？我们会向 `account1` 的余额中增加了 100 美元，却没有从 `account2` 中做相应的扣减。实际上，我们就等于凭空创造了 100 美元。

这时就需要事务出马了。事务有点像《三个火枪手》和他们的座右铭“人人为我，我为人人”。在事务的范围内，要么每条 SQL 语句都成功，要么它们全部都不产生任何效果。换句话说，如果任何一条语句失败，整个事务对数据库都不产生任何影响。

在 Active Record 中，我们使用 `transaction` 方法在特定数据库事务的上下文中执行一个代码块。在代码块结束时，事务会被提交，从而更新数据库；除非在代码块中抛出了异常，在这种情况下，所有更改都会被回滚，数据库保持原样。由于事务存在于数据库连接的上下文中，我们必须用 Active Record 类作为接收者来调用它们。

5. 事务实际上比这更微妙。它们具有所谓的 ACID 特性：原子性（Atomic）、一致性（Consistency）、隔离性（Isolation）和持久性（Durable，即事务提交后其效果是永久性的）。如果你打算让一个数据库应用上线，那么找一本好的数据库书籍并仔细阅读关于事务的内容是很值得的。



因此，我们可以这样写：

```
Account.transaction do
  account1.deposit(100)
  account2.withdraw(100)
end
```

让我们来实验一下事务。我们首先创建一个新的数据库表。（确保你的数据库支持事务，否则这些代码对你无效。）

```
Download e1/ar/transactions.rb

create_table :accounts, :force => true do |t|
  t.string :number
  t.decimal :balance, :precision => 10, :scale => 2, :default => 0
end
```

接下来，我们将定义一个简单的银行账户类。该类定义了向账户存钱和取钱的实例方法。它还提供了一些基本的验证——对于这种特定类型的账户，余额永远不能为负。

```
Download e1/ar/transactions.rb

class Account < ActiveRecord::Base

  def withdraw(amount)
    adjust_balance_and_save(-amount)
  end

  def deposit(amount)
    adjust_balance_and_save(amount)
  end

  private

  def adjust_balance_and_save(amount)
    self.balance += amount
    save!
  end

  def validate  # validation is called by Active Record
    errors.add(:balance, "is negative") if balance < 0
  end
end
```

让我们看看辅助方法 adjust_balance_and_save。第一行只是更新 balance 字段。然后该方法调用 save! 来保存模型数据。（请记住，如果对象无法保存，save! 会抛出异常——我们利用这个异常来向事务发出信号，表明出现了问题。）

那么，现在让我们编写在两个账户之间转账的代码。这很简单：

```
Download e1/ar/transactions.rb

peter = Account.create(:balance => 100, :number => "12345")
paul  = Account.create(:balance => 200, :number => "54321")

Account.transaction do
  paul.deposit(10)
  peter.withdraw(10)
end
```

我们检查数据库，果然，钱被转过去了：

```
depot> sqlite3 -line db/development.sqlite3 "select * from accounts"
    id = 1
    number = 12345
    balance = 90

    id = 2
    number = 54321
    balance = 210
```

现在让我们来点极端的。如果我们重新开始，但这次尝试转账 350 美元，我们会让 Peter 的账户透支，而这正是验证规则所不允许的。让我们试试：

```
Download e1/ar/transactions.rb

peter = Account.create(:balance => 100, :number => "12345")
paul  = Account.create(:balance => 200, :number => "54321")
```

```
Download e1/ar/transactions.rb

Account.transaction do
  paul.deposit(350)
  peter.withdraw(350)
end
```

当我们运行这段代码时，控制台上会报告一个异常：

```
.../validations.rb:736:in `save!': Validation failed: Balance is negative
from transactions.rb:46:in `adjust_balance_and_save'
  :
  :
  :
from transactions.rb:80
```

查看数据库，我们可以看到数据保持不变：

```
depot> sqlite3 -line db/development.sqlite3 "select * from accounts"
    id = 1
    number = 12345
    balance = 100

    id = 2
    number = 54321
    balance = 200
```

然而，这里有一个陷阱在等着你。事务保护了数据库，使其不会出现不一致，但我们的模型对象呢？为了查看它们发生了什么，我们必须设法拦截这个异常，让程序得以继续运行：

```
Download e1/ar/transactions.rb

peter = Account.create(:balance => 100, :number => "12345")
paul  = Account.create(:balance => 200, :number => "54321")
```

```
Download e1/ar/transactions.rb

begin
  Account.transaction do
    paul.deposit(350)
    peter.withdraw(350)
  end
rescue
  puts "Transfer aborted"
end
```

```
puts "Paul has #{paul.balance}"
puts "Peter has #{peter.balance}"
```

我们看到的结果有点令人惊讶：

```
Transfer aborted
Paul has 550.0
Peter has -250.0
```

尽管数据库毫发无损，但我们的模型对象还是被更新了。这是因为 Active Record 并没有跟踪各个对象在事务前后的状态——事实上它也无法做到，因为它没有办法轻易知道究竟哪些模型参与了这些事务。⁶

##### 内置事务

在讨论父表和子表时，我们说过，当你保存父行时，Active Record 会负责保存所有关联的子行。这需要执行多条 SQL 语句（一条用于父行，每条用于任何更改或新建的子行）。显然，这种更改应该是原子的，但到目前为止，在保存这些相互关联的对象时，我们还没有使用事务。我们一直疏忽了吗？

幸运的是，没有。Active Record 足够聪明，它会将与某次保存相关的所有更新和插入（以及与某次销毁相关的删除）包装在一个事务中；要么全部成功，要么不会向数据库永久写入任何数据。只有当你自己管理多条 SQL 语句时，才需要显式地使用事务。

6. 如果这在你的应用中变成了一个问题，下面的插件可能会有所帮助：http://code.bitsweat.net/svn/object_transactions。

##### 多数据库事务

在 Rails 中，如何在多个不同的数据库之间同步事务呢？

目前的答案是：你做不到。Rails 不支持分布式两阶段提交（这个术语指的是让数据库相互同步的协议）。

不过，你（几乎）可以通过嵌套事务来模拟这种效果。记住，事务与数据库连接相关联，而连接又与模型相关联。因此，如果 accounts 表在一个数据库中，而 users 表在另一个数据库中，你可以使用类似下面的代码来模拟一个跨越这两个数据库的事务：

```
User.transaction(user) do
  Account.transaction(account) do
    account.calculate_fees
    user.date_fees_last_calculated = Time.now
    user.save
    account.save
  end
end
```

这只是一个近似解法。用户的数据库中的提交可能会失败（也许磁盘已满），但到那时，accounts 数据库中的提交已经完成，表也已经更新。这将使整个事务处于不一致的状态。尽管不令人愉快，但针对每套具体情况编写代码来解决这些问题是有可能的；但就目前而言，如果你正在编写并发更新多个数据库的应用程序，你可能不应该依赖 Active Record。

##### 乐观锁

在一个多个进程访问同一个数据库的应用程序中，如果另一个进程更新了底层数据库行，那么一个进程所持有的数据可能会变得陈旧。

例如，两个进程可能会获取对应于某个特定账户的行。在几秒钟的时间范围内，两个进程都要去更新该余额。每个进程都加载了一个带有初始行内容的 Active Record 模型对象。在不同时间，它们各自使用本地模型副本去更新底层行。结果是产生了一个竞态条件：最后更新该行的人获胜，而第一个人的更改丢失了。这如图 20.2 所示（见下一页）。

解决这个问题的一种方法是锁定正在更新的表或行。通过阻止他人访问或更新它们，锁定克服了并发问题

![](img/a160fc3a330a0b3b2a764d41e688_422_0.png)

# 图 20.2：竞态条件：第二次更新覆盖第一次

，但这样的做法相当粗暴。它假设会发生问题，然后为了以防万一而锁定。因此，这种方法通常被称为*悲观锁*。如果你需要确保跨多个用户请求的一致性，悲观锁对于 Web 应用程序来说并不可行，因为很难管理锁，使数据库不至于停滞不前。

*乐观锁*并不使用显式锁。相反，在将更新后的数据写回某一行之前，它会检查以确保没有其他人已经更改过那一行。在 Rails 的实现中，每一行都包含一个版本号。每当一行被更新，版本号就会递增。当你在应用程序中进行更新时，Active Record 会将表中行的版本号与正在进行更新的模型的版本号进行比较。如果两者不匹配，它就会放弃更新并抛出一个异常。

乐观锁默认在任何一个包含名为 `lock_version` 的整数列的表上启用。你应该让这个列对于新行初始化为零，否则你应该不去动它——Active Record 会为你管理这些细节。

让我们看看乐观锁的实际应用。我们将创建一个名为 `counters` 的表，其中包含一个简单的计数字段以及 `lock_version` 列。（注意 `lock_version` 列上的 `:default` 设置。）




### Action Controller：路由和 URL

Action Pack 是 Rails 应用的核心。它由两个 Ruby 模块组成：ActionController 和 ActionView。它们一起提供了处理传入请求和生成传出响应的支持。在本章和下一章中，我们将研究 ActionController 以及它在 Rails 中的工作方式。在接下来的那一章中，我们将讨论 ActionView。

当我们研究 Active Record 时，我们把它当作一个独立的库；你可以在非 Web 的 Ruby 应用中使用 Active Record。Action Pack 则不同。虽然可以直接作为框架使用，但你可能不会这样做。相反，你会利用 Rails 提供的紧密集成。诸如 Action Controller、Action View 和 Active Record 之类的组件处理请求的流程，而 Rails 环境将它们编织成一个连贯且易于使用的整体。因此，我们将在 Rails 的上下文中描述 Action Controller。让我们先看看 Rails 应用如何处理请求。然后我们将深入探讨路由和 URL 处理的细节。第 22 章《Action Controller 和 Rails》将介绍如何在控制器中编写代码。

#### 21.1 基础

最简单地说，一个 Web 应用接受来自浏览器的传入请求，处理它，并发送响应。

首先想到的问题是，应用如何知道对传入请求该做什么？一个购物车应用会收到显示目录、将商品加入购物车、结账等请求。它如何将这些请求路由到适当的代码？

事实证明，Rails 提供了两种定义请求路由的方式：一种全面方式，当你需要时使用；一种便捷方式，只要能用你就会一般使用。

rails 命令为应用生成初始文件集。其中一个文件是 config/routes.rb。它包含该应用的路由信息。如果你查看该文件的默认内容，忽略注释，你会看到以下内容：

```
ActionController::Routing::Routes.draw do |map|
  map.connect ':controller/:action/:id'
  map.connect ':controller/:action/:id.:format'
end
```

Routing 组件绘制了一张地图，让 Rails 将外部 URL 连接到应用内部。每个 map.connect 声明都指定了一条将外部 URL 与内部程序代码连接的路由。让我们看第一条 map.connect 行。字符串 ':controller/:action/:id' 作为模式，与请求 URL 的路径部分进行匹配。在这种情况下，该模式将匹配路径中包含三个组件的任何 URL。 （这实际上并不正确，但我们一会儿会澄清。）第一个组件将被分配给参数 :controller，第二个分配给 :action，第三个分配给 :id。将此模式应用于路径为 store/add_to_cart/123 的 URL，你将得到以下参数：

```
@params = { :controller => 'store',
             :action    => 'add_to_cart',
             :id        => 123 }
```

基于此，Rails 将在 store 控制器中调用 add_to_cart 方法。 :id 参数的值为 123。

##### 玩转路由

起初，路由可能有些令人望而生畏。随着你开始定义越来越复杂的路由，你会遇到一个问题——你如何知道你的路由按预期工作？

显然，一种方法是启动你的应用并在浏览器中输入 URL。然而，我们可以做得更好。对于路由的临时实验，我们可以使用 script/console 命令。 （对于更正式的验证，我们可以编写单元测试，正如我们从第 458 页开始将看到的那样。）我们现在将研究如何玩转路由，因为在我们后面研究路由的所有功能时它会派上用场。

应用的路由定义被加载到 ActionController::Routing 模块中的 RouteSet 对象中。有些令人困惑的是，我们可以通过 Routes 常量访问它（它最终并不是一个常量）。特别是，我们可以使用 script/console 访问路由定义，这让我们可以交互式地操作它们。

```
>> rs.generate :controller => :store
=> "/store"
>> rs.generate :controller => :store, :id => 123
=> "/store/index/123"
```

所有这些示例都使用了我们应用的路由，并且依赖于我们的应用已实现请求路径中引用的所有控制器——路由会检查控制器是否有效，因此不会解析对找不到的控制器的请求。例如，我们的 Depot 应用没有 coupon 控制器。如果我们尝试解析使用此控制器的传入路由，路径将无法识别：

```
>> rs.recognize_path "/coupon/show/1"
ActionController::RoutingError: no route found to match
"/coupon/show/1" with {}
```

我们可以使用 use_controllers! 方法告诉路由假装我们的应用包含尚未编写的控制器：

```
>> ActionController::Routing.use_controllers! ["store", "admin", "coupon"]
=> ["store", "admin", "coupon"]
```

然而，要使此更改生效，我们需要重新加载路由的定义：

```
>> load "config/routes.rb"
=> true
>> rs.recognize_path "/coupon/show/1"
=> {:action=>"show", :controller=>"coupon", :id=>"1"}
```

我们可以使用这个技巧来测试尚未成为我们应用一部分的路由方案：创建一个包含通常在 routes.rb 配置文件中 Routes.draw 块的新 Ruby 源文件，并使用 load 加载此新文件。

##### 使用 map.connect 定义路由

map.connect 接受的模式简单但功能强大：

- 组件由正斜杠字符和句点分隔。模式中的每个组件与 URL 中的一个或多个组件匹配。模式中的组件按顺序与 URL 匹配。
- 形式为 :name 的模式组件将参数 name 设置为 URL 中对应位置的任何值。
- 形式为 *name 的模式组件接受传入 URL 中的所有剩余组件。参数 name 将引用包含它们的值的数组。因为它吞噬了 URL 的所有剩余组件，所以 *name 必须出现在模式的末尾。

link_to 生成基于路由的 URL。我们在这里使用 generate 方法的唯一原因是它在控制台会话的上下文中有效。

在以下示例中，当 Rails 收到对 /store/checkout 的 GET 请求时，它将调用 display_checkout_form 动作，但如果它看到对同一 URL 的 POST 请求，则会调用 save_checkout_form 动作：

```
Download e1/routing/config/routes_with_conditions.rb
ActionController::Routing::Routes.draw do |map|
  map.connect 'store/checkout',
    :conditions => { :method => :get },
    :controller => "store",
    :action     => "display_checkout_form"

  map.connect 'store/checkout',
    :conditions => { :method => :post },
    :controller => "store",
    :action     => "save_checkout_form"
end
```

:name => value

为组件 :name 设置默认值。与使用 :defaults 设置的值不同，名称不必出现在模式本身中。这允许你向传入请求添加任意参数值。值通常是字符串或 nil。

:name => /regexp/

等同于使用 requirements 在 :name 的值上设置约束。

还有一条规则：路由尝试按顺序将传入 URL 与 routes.rb 中的每条规则匹配。第一个成功的匹配将被使用。如果没有匹配成功，则会引发错误。

现在让我们看一个更复杂的示例。在你的博客应用中，你希望所有 URL 都以单词 blog 开头。如果没有给出额外参数，你将显示索引页。如果 URL 看起来像 blog/show/nnn，你将显示文章 nnn。如果 URL 包含日期（可能是年、年/月或年/月/日），你将显示该日期的文章。否则，URL 将包含控制器和动作名称，允许你编辑文章并以其他方式管理博客。最后，如果你收到无法识别的 URL 模式，你将使用特殊动作处理它。

此路由包含每种单独情况的一行：

```
Download e1/routing/config/routes_for_blog.rb
ActionController::Routing::Routes.draw do |map|
  # Straight 'http://my.app/blog/' displays the index
  map.connect "blog/",
    :controller => "blog",
    :action => "index"
```





# 返回一年、年/月 或 年/月/日的文章
map.connect "blog/:year/:month/:day",
    :controller => "blog",
    :action => "show_date",
    :requirements => { :year => /(19|20)\d\d/,
                      :month => /[01]?\d/,
                      :day => /[0-3]?\d/},
    :day => nil,
    :month => nil

# 通过 id 显示一篇文章
map.connect "blog/show/:id",
    :controller => "blog",
    :action => "show",
    :id => /\d+/

# 管理后台的常规 Rails 路由
map.connect "blog/:controller/:action/:id"

# 兜底以优雅处理格式不正确的请求
map.connect "*anything",
    :controller => "blog",
    :action => "unknown_request"

end

注意这段代码中的两点。第一，我们对日期匹配规则进行了约束，使其只查找看起来合理的年、月和日值。如果没有这个约束，该规则也会匹配常规的 controller/action/id URL。第二，注意我们把兜底规则（"*anything"）放在了列表的末尾。因为该规则匹配任何请求，如果把它放在前面，后续规则将无法被检查。

我们可以看看这些规则如何处理一些请求 URL：

```
>> ActionController::Routing.use_controllers! [ "article", "blog" ]
=> ["article", "blog"]

>> load "config/routes_for_blog.rb"
=> []

>> rs.recognize_path "/blog"
=> {:controller=>"blog", :action=>"index"}

>> rs.recognize_path "/blog/show/123"
=> {:controller=>"blog", :action=>"show", :id=>"123"}

>> rs.recognize_path "/blog/2004"
=> {:year=>"2004", :controller=>"blog", :action=>"show_date"}

>> rs.recognize_path "/blog/2004/12"
=> {:month=>"12", :year=>"2004", :controller=>"blog", :action=>"show_date"}
```

```
>> rs.recognize_path "/blog/2004/12/25"
=> {:month=>"12", :year=>"2004", :controller=>"blog", :day=>"25", :action=>"show_date"}
```

```
>> rs.recognize_path "/blog/article/edit/123"
=> {:controller=>"article", :action=>"edit", :id=>"123"}
```

```
>> rs.recognize_path "/blog/article/show_stats"
=> {:controller=>"article", :action=>"show_stats"}
```

```
>> rs.recognize_path "/blog/wibble"
=> {:controller=>"blog", :anything=>["blog", "wibble"], :action=>"unknown_request"}
```

```
>> rs.recognize_path "/junk"
=> {:controller=>"blog", :anything=>["junk"], :action=>"unknown_request"}
```

我们还没有完全指定路由，但在查看创建命名路由之前，让我们先看看另一面——从应用程序内部生成 URL。

##### URL 生成

路由接收一个传入的 URL 并将其解码为一组参数，Rails 使用这些参数分发到适当的控制器和动作（在途中可能设置额外的参数）。但这只是故事的一半。我们的应用程序也需要创建指向自身的 URL。例如，每次显示表单时，该表单都需要链接回控制器和动作。但应用程序代码不一定知道编码此信息的 URL 的格式；它看到的只是路由工作完成后收到的参数。

我们可以将所有 URL 硬编码到应用程序中，但将请求格式的知识散布在多个地方会使代码更脆弱。这是 DRY 原则的违反；更改应用程序的位置或 URL 格式，我们就必须更改所有这些字符串。

幸运的是，我们不必担心这个问题，因为 Rails 也使用 url_for 方法（以及一些使用它的更高级别的助手）抽象了 URL 的生成。为了说明这一点，让我们回到一个简单的映射：

```
map.connect ":controller/:action/:id"
```

url_for 方法通过将其参数应用到映射来生成 URL。它在控制器和视图中都有效。让我们试试：

```
@link = url_for(:controller => "store", :action => "display", :id => 123)
```

2. DRY 代表 don’t repeat yourself，是在 The Pragmatic Programmer [HT00] 中创造的缩写。

这段代码会将 @link 设置为类似这样的内容：

```
http://pragprog.com/store/display/123
```

url_for 方法将我们的参数映射为与我们自己的路由兼容的请求。如果用户选择具有此 URL 的链接，它将调用我们应用程序中预期的动作。

url_for 背后的重写相当聪明。它知道默认参数并生成能实现你想要的最小 URL。而且，正如你可能猜到的，我们可以在 script/console 中使用它进行操作。我们不能直接调用 url_for，因为它只在控制器和视图内部可用。我们可以做的最好的事情是调用 routings 中的 generate 方法。再次，我们将使用之前使用的路由集。让我们看一些例子：

```
# 没有 action 或 id，重写使用默认值
>> rs.generate :controller => "store"
=> "/store"
```

```
# 如果 action 缺失，重写在 URL 中插入默认值（index）
>> rs.generate :controller => "store", :id => 123
=> "/store/index/123"
```

```
# id 是可选的
>> rs.generate :controller => "store", :action => :list
=> "/store/list"
```

```
# 完整的请求
>> rs.generate :controller => "store", :action => :list, :id => 123
=> "/store/list/123"
```

```
# 额外参数被添加到 URL 的末尾
>> rs.generate :controller => "store", :action => :list, :id => 123,
?>             :extra => "wibble"
=> "/store/list/123?extra=wibble"
```

默认机制会使用当前请求中的值，如果可以的话。这最常用于在省略 :controller 参数时填充当前控制器的名称。我们可以通过使用 generate 的可选第二个参数在 script/console 中演示这一点。该参数给出从当前活动请求解析的选项。因此，如果当前请求是 /store/index 并且我们生成一个仅给出 action 为 show 的新 URL，我们仍然会在 URL 的路径中看到 store 部分：

```
>> rs.generate({:action => "show"},
?>             {:controller => "store", :action => "index"})
=> "/store/show"
```

为了更具体，我们可以看到如果在（例如）视图中使用 url_for 在这些情况下会发生什么。请注意 url_for 方法通常只能用于控制器，但 script/console 为我们提供了一个 app 对象，其中有一个类似的方法，关键区别在于 app 对象上的方法没有默认请求。这意味着我们不能依赖为 :controller 和 :action 提供默认值：

```
>> app.url_for :controller => :store, :action => :display, :id => 123
=> http://example.com/store/status
```

URL 生成也适用于更复杂的路由。例如，我们的博客包含以下映射：

```
Download e1/routing/config/routes_for_blog.rb
# 返回一年、年/月 或 年/月/日的文章
map.connect "blog/:year/:month/:day",
  :controller => "blog",
  :action => "show_date",
  :requirements => { :year => /(19|20)\d\d/,
                     :month => /[01]?\d/,
                     :day => /[0-3]?\d/ },
  :day => nil,
  :month => nil
```

```
# 通过 id 显示一篇文章
map.connect "blog/show/:id",
  :controller => "blog",
  :action => "show",
  :id => /\d+/
```

```
# 管理后台的常规 Rails 路由
map.connect "blog/:controller/:action/:id"
```

假设传入的请求是 http://pragprog.com/blog/2006/07/28。这将被第一个规则映射到 Blog 控制器的 show_date 动作：

```
>> ActionController::Routing.use_controllers! [ "blog" ]
=> ["blog"]
>> load "config/routes_for_blog.rb"
=> true
>> last_request = rs.recognize_path "/blog/2006/07/28"
=> {:month=>"07", :year=>"2006", :controller=>"blog", :day=>"28", :action=>"show_date"}
```

让我们看看在这些情况下各种 url_for 调用会生成什么。

如果我们请求不同日期的 URL，映射调用将以传入请求中的值作为默认值，只更改 day 参数：

```
>> rs.generate({:day => 25}, last_request)
=> "/blog/2006/07/25"
```

现在让我们看看如果我们只给出一个年份会发生什么：

```
>> rs.generate({:year => 2005}, last_request)
=> "/blog/2005"
```




这相当聪明。映射代码假定URL表示一个值的层级结构。³ 一旦我们在该层级结构的某一层改变了默认值，它就不再为较低层级提供默认值。这是合理的：较低层级的参数只有在较高层级参数的上下文中才有意义，因此改变默认值会使较低层级的参数失效。通过在这个例子中覆盖年份，我们隐式地告诉映射代码，我们不需要月份和日期。

还要注意，映射代码选择了第一个可以合理用于渲染URL的规则。让我们看看如果给它一些无法与第一个基于日期的规则匹配的值，会发生什么：

```
>> rs.generate({:action => "edit", :id => 123}, last_request)
=> "/blog/blog/edit/123"
```

这里第一个blog是固定文本，第二个blog是控制器的名称，而edit是动作名称——映射代码应用了第三条规则。如果我们指定动作为show，它将使用第二条映射：

```
>> rs.generate({:action => "show", :id => 123}, last_request)
=> "/blog/show/123"
```

大多数时候，映射代码会按照你的期望工作。然而，它有时过于聪明。假设你想生成查看2006年博客条目的URL。你可以这样写：

```
>> rs.generate({:year => 2006}, last_request)
```

当映射代码输出一个也包含月份和日期的URL时，你可能会感到惊讶：

```
=> "/blog/2006/07/28"
```

你提供的年份值与当前请求中的相同。由于这个参数没有改变，映射继续使用月份和日期的默认值来完成URL的其余部分。要解决这个问题，将month参数设置为nil：

```
>> rs.generate({:year => 2006, :month => nil}, last_request)
=> "/blog/2006"
```

一般来说，如果你想生成一个部分URL，最好将第一个未使用的参数设置为nil；这样做可以防止来自传入请求的参数泄漏到传出的URL中。

有时候你想做相反的事情，改变层级结构中较高层参数的值，并强制路由代码继续使用较低层级的值。在我们的例子中，这就像指定一个不同的年份，并让它在其后添加现有的默认月份和日期值，在

3. 这在Web上是很自然的，静态内容存储在文件夹（目录）中，而文件夹本身可能又位于文件夹中，依此类推。

以下代码片段中的两个redirect调用具有相同的效果：

```
user = User.find_by_name("dave thomas")
redirect_to(:action => 'delete', :id => user.id)
```

# 可以写成

```
redirect_to(:action => 'delete', :id => user)
```

url_for也接受单个字符串或符号作为参数。Rails在内部使用这一点。

你可以通过在控制器中实现default_url_options方法来覆盖下表中参数的默认值。该方法应返回一个可以传递给url_for的参数哈希。

###### 选项：

| :anchor | 字符串 | 要附加到URL的锚点名称。Rails会自动添加#字符。 |
| :host | 字符串 | 设置URL中的主机名和端口。使用类似store.pragprog.com或helper.pragprog.com:8080的字符串。默认为传入请求中的主机。 |
| :only_path | 布尔值 | 仅生成URL的路径部分；省略协议、主机名和端口。 |
| :protocol | 字符串 | 设置URL的协议部分。使用类似"https://"的字符串。默认为传入请求的协议。 |
| :overwrite_params | 哈希 | 使用哈希中的选项来创建URL，但不从当前请求中获取默认值。 |
| :skip_relative_url_root | 布尔值 | 如果为true，则不会在生成的URL前添加相对URL根。更多详情请参见第441页的21.2节“根URL”。 |
| :trailing_slash | 布尔值 | 在生成的URL末尾添加斜杠。如果你还使用页面或动作缓存（从第496页开始描述），请谨慎使用:trailing_slash。据报道，额外的斜杠会混淆缓存算法。 |
| :port | 整数 | 设置要连接的端口。默认为基于协议。 |
| :user | 字符串 | 设置用户。用于内联认证。仅在同时指定:password时使用。 |
| :password | 字符串 | 设置密码。用于内联认证。仅在同时指定:user时使用。 |

##### 命名路由

到目前为止，我们一直在使用匿名路由，这些路由是通过routes.rb文件中的map.connect创建的。通常这已经足够了；Rails能够根据我们传递给url_for及其相关方法的参数，很好地选择要生成的URL。然而，我们可以通过给路由命名来使应用程序更易于理解。这不会改变传入URL的解析方式，但可以让我们在代码中明确地使用特定路由来生成URL。

要创建命名路由，只需在路由定义中使用connect以外的名称。你使用的名称将成为该特定路由的名称。

```
date_url(:year => 2003, :month => 2)
  #=>  http://pragprog.com/blog/2003/2
```

```
show_article_url(:id => 123)
  #=>  http://pragprog.com/blog/show/123
```

你可以在Rails期望URL参数的任何地方使用xxx_url方法。因此，你可以使用以下代码重定向到索引页面：

```
redirect_to(index_url)
```

在视图模板中，你可以使用以下代码创建指向索引的超链接：

```
<%= link_to("Index", index_url) %>
```

除了xxx_url方法之外，Rails还创建了xxx_path形式。这些只构造URL的路径部分（忽略协议、主机和端口）。

最后，如果命名URL生成方法的唯一参数是用于填充URL中命名字段的值，你可以将它们作为常规参数传递，而不是作为哈希。例如，我们的示例routes.rb文件为博客管理定义了一个命名URL：

```
Download e1/routing/config/routes_with_names.rb
```

```
map.blog_admin "blog/:controller/:action/:id"
```

我们已经看到了如何使用命名URL生成器链接到list users动作：

```
blog_admin_url :controller => 'users', :action => 'list'
```

因为我们只是使用选项来为命名参数提供值，所以我们也可以这样写：

```
blog_admin_url 'users', 'list'
```

也许令人惊讶的是，这种形式比传递值哈希的效率更低：

##### 控制器命名

回到第269页，我们说过控制器可以分组到模块中，传入的URL使用类似路径的约定来标识这些控制器。传入的URL http://my.app/admin/book/edit/123 将调用Admin模块中BookController的edit动作。

这种映射也影响URL生成：

- 如果你没有向url_for传递:controller参数，它会使用当前控制器。
- 如果你传递的控制器名称以/开头，那么该名称是绝对的。
- 所有其他控制器名称相对于发出请求的控制器的模块。

为了说明这一点，让我们假设一个这种格式的传入请求：

```
http://my.app/admin/book/edit/123
```

```
url_for(:action => "edit", :id => 123)
    #=> http://my.app/admin/book/edit/123
```

```
url_for(:controller => "catalog", :action => "show", :id => 123)
    #=> http://my.app/admin/catalog/show/123
```

```
url_for(:controller => "/store", :action => "purchase", :id => 123)
    #=> http://my.app/store/purchase/123
```

```
url_for(:controller => "/archive/book", :action => "record", :id => 123)
    #=> http://my.app/archive/book/record/123
```

##### 根URL

有时你想运行同一个应用程序的多个副本。也许你在运营一个服务局，有多个客户。或者你可能想同时运行应用程序的暂存版和生产版。

如果可能，最简单的方法是运行多个（子）域，每个域中都有一个应用程序实例。然而，如果这不可行，你也可以在URL路径中使用前缀来区分应用程序实例。例如，你可能在如下URL上运行多个用户的博客：

```
http://megablogworld.com/dave/blog
```

```
http://megablogworld.com/joe/blog
```

```
http://megablogworld.com/sue/blog
```

在这些情况下，前缀dave、joe和sue标识应用程序实例。应用程序的路由在此之后开始。你可以通过设置环境变量RAILS_RELATIVE_URL_ROOT，告诉Rails在接收到的URL上忽略路径的这一部分，并在生成的URL上添加这一部分。如果你的Rails应用程序运行在Apache上，此功能会自动启用。

#### 21.3 基于资源的路由

Rails路由支持基于URL内容以及用于调用请求的HTTP方法，在URL和动作之间进行映射。我们已经看到了如何使用匿名或命名路由逐个URL地完成这项工作。Rails还支持一种更高级的方式来创建相关路由组。为了理解其动机，我们需要稍微绕道进入表述性状态转移的世界。

##### REST：表述性状态转移

REST是一种思考分布式超媒体系统架构的方式。这与我们相关，因为许多Web应用程序都可以归为此类。




REST背后的思想在 Roy Fielding 2000 年博士论文的第 5 章中得到了形式化。⁴ 在 REST 方法中，服务器使用无状态连接与客户端通信。两者之间交互状态的所有信息都编码在它们之间的请求和响应中。长期状态作为一组可标识的资源保存在服务器上。客户端使用一组定义良好（且受到严格约束）的资源标识符（在我们的上下文中即 URL）来访问这些资源。REST 将资源的内容与内容的呈现区分开来。REST 旨在支持高度可扩展的计算，同时约束应用程序架构在本质上保持解耦。

这个描述中有很多抽象内容。REST 在实践中意味着什么？

首先，RESTful 方法的规范性意味着网络设计者知道何时何地可以缓存对请求的响应。这使负载能够通过网络推出去，在降低延迟的同时提高性能和韧性。

其次，REST 所施加的约束可以让应用程序更容易编写（和维护）。RESTful 应用程序不需要担心实现远程可访问的服务。相反，它们为一组资源提供常规（且简单）的接口。你的应用程序实现列出、创建、编辑和删除每个资源的方式，剩下的由客户端完成。

让我们更具体地说明。在 REST 中，我们使用一组简单的动词来操作一组丰富的名词。如果我们使用 HTTP，这些动词对应 HTTP 方法（通常是 GET、PUT、POST 和 DELETE）。名词是我们应用程序中的资源。我们使用 URL 来命名这些资源。

一个内容管理系统可能包含一组文章。这里隐含两个资源。首先，是单篇文章。每一篇都构成一个资源。还有第二个资源：文章集合。

要获取所有文章的列表，我们可以对这个集合发起 HTTP GET 请求，比如在路径 /articles 上。要获取单个资源的内容，我们必须标识它。Rails 的方式是给出其主键值（即 id）。我们再次发起 GET 请求，这次针对 URL /articles/1。到目前为止，这一切看起来都很熟悉。但是当我们想向集合中添加一篇文章时会发生什么？

在非 RESTful 应用程序中，我们可能会用动词短语作为名称来发明某个动作：articles/add_article/1。在 REST 的世界里，我们不应这样做。我们应该使用一组标准动词来告诉资源做什么。要使用 REST 在我们的集合中创建一篇新文章，我们会使用一个

4. http://www.ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm

HTTP POST 请求，指向 /articles 路径，POST 数据中包含要添加的文章。是的，这与我们用来获取文章列表的路径相同。如果你对它发起 GET，它会返回列表；如果你发起 POST，它会向集合中添加一篇新文章。

再进一步。我们已经看到，你可以检索文章的内容——只需对路径 /articles/1 发起 GET 请求。要更新这篇文章，你可以对同一个 URL 发起 HTTP PUT 请求。要删除它，你可以再次使用同一个 URL 发起 HTTP DELETE 请求。

更进一步。也许我们的系统还跟踪用户。同样，我们需要处理一组资源。REST 要求我们对一组看起来相似的 URL（/users, /user/1, ...）使用相同的动词集（GET、POST、PUT 和 DELETE）。

现在我们看到了 REST 所施加约束的一些强大之处。我们已经熟悉 Rails 以某种方式约束我们构建应用程序的方式。现在 REST 哲学也告诉我们要构建应用程序的接口。突然间，我们的世界变得简单多了。

##### REST 与 Rails

Rails 1.2 对这种接口添加了直接支持；它增加了一种称为 resources 的宏路由设施。让我们为文章示例创建一组 RESTful 路由：

```
ActionController::Routing::Routes.draw do |map|
  map.resources :articles
end
```

map.resources 这一行为我们的应用程序添加了七条新路由和四个新的路由辅助方法。同时，它假定应用程序将有一个名为 ArticlesController 的控制器，其中包含七个具有给定名称的动作。如何编写该控制器取决于我们。

在我们这样做之前，先看看为我们生成的路由。我们可以使用方便的 rake routes 命令来做到这一点。⁵

```
articles GET    /articles
            {:controller=>"articles", :action=>"index"}
formatted_articles GET /articles.:format
            {:controller=>"articles", :action=>"index"}
            POST   /articles
            {:controller=>"articles", :action=>"create"}
            POST   /articles.:format
            {:controller=>"articles", :action=>"create"}
```

> 5. 根据你所运行的 Rails 版本，你可能不会看到以 formatted_ 前缀开头的路由名称。人们发现这些路由很少被使用，并且消耗 CPU 和内存资源，因此计划在 Rails 2.3 中移除它们，代之以可选的 :format 参数。

show
返回 params[:id] 所标识资源的内容。

update
使用与请求关联的数据更新 params[:id] 所标识资源的内容。

edit
返回 params[:id] 所标识资源的内容，形式适合编辑。

destroy
销毁 params[:id] 所标识的资源。

你可以看到，这七个动作包含了四种基本的 CRUD 操作（create、read、update 和 delete）。它们还包含一个列出资源的动作，以及两个辅助动作，分别以适合在客户端编辑的形式返回新资源和现有资源。

如果出于某种原因你不需要或不想要全部七个动作，你可以通过 map.resource 上的 :only 或 :except 选项来限制生成的动作：

```
map.resources :comments, :except => [:update, :destroy]
```

这些路由中有几条是命名路由——参见第 438 页第 21.2 节“命名路由”——使你可以使用 articles_url 和 edit_article_url(:id=>1) 等辅助函数。每个控制器动作定义了两条路由：一条使用默认格式，一条使用显式格式。我们将在第 457 页第 21.3 节“选择数据表示”中更详细地介绍格式。

但首先，让我们创建一个简单的应用程序来试用一下。现在你已经熟悉流程了，所以我们会快速进行。我们将创建一个名为 restful 的应用程序：

```
work> rails restful
```

那么，现在我们将开始创建模型、控制器、视图等等。我们可以手动完成，但 Rails 已经准备好生成使用基于资源的路由的脚手架，所以让我们省点打字。生成器接受模型（资源）的名称，以及可选的字段名和类型列表。在我们的例子中，article 模型有三个属性：title、summary 和 content：

```
restful> ruby script/generate scaffold article \
  title:string summary:text content:text
exists    app/models/
exists    app/controllers/
exists    app/helpers/
create    app/views/articles
exists    app/views/layouts/
exists    test/functional/
exists    test/unit/
exists    public/stylesheets/
```

```
create  app/views/articles/index.html.erb
create  app/views/articles/show.html.erb
create  app/views/articles/new.html.erb
create  app/views/articles/edit.html.erb
create  app/views/layouts/articles.html.erb
create  public/stylesheets/scaffold.css
create  app/controllers/articles_controller.rb
create  test/functional/articles_controller_test.rb
create  app/helpers/articles_helper.rb
    route  map.resources :articles
dependency  model
exists     app/models/
exists     test/unit/
exists     test/fixtures/
create     app/models/article.rb
create     test/unit/article_test.rb
create     test/fixtures/articles.yml
create     db/migrate
create     db/migrate/20080601000001_create_articles.rb
```

看看此命令输出中以 route 开头的那行。它告诉我们，生成器已经自动将适当的映射添加到我们应用程序的路由中。让我们看看它做了什么。查看 config/ 目录中 routes.rb 文件的顶部：

```
Download restful/config/routes.rb
ActionController::Routing::Routes.draw do |map|
  map.resources :articles
  # ...
  map.connect ':controller/:action/:id'
  map.connect ':controller/:action/:id.:format'
end
```

迁移文件已自动创建，并填充了我们提供给生成器的信息：

```
Download restful/db/migrate/20080601000001_create_articles.rb
class CreateArticles < ActiveRecord::Migration
  def self.up
    create_table :articles do |t|
      t.string :title
      t.text :summary
      t.text :content
      t.timestamps
    end
  end
  def self.down
    drop_table :articles
  end
end
```





```ruby
respond_to do |format|
  if @article.save
    flash[:notice] = 'Article was successfully created.'
    format.html { redirect_to(@article) }
    format.xml { render :xml => @article, :status => :created,
                  :location => @article }
  else
    format.html { render :action => "new" }
    format.xml { render :xml => @article.errors,
                  :status => :unprocessable_entity }
  end
end
end

# PUT /articles/1
# PUT /articles/1.xml
def update
  @article = Article.find(params[:id])

  respond_to do |format|
    if @article.update_attributes(params[:article])
      flash[:notice] = 'Article was successfully updated.'
      format.html { redirect_to(@article) }
      format.xml { head :ok }
    else
      format.html { render :action => "edit" }
      format.xml { render :xml => @article.errors,
                    :status => :unprocessable_entity }
    end
  end
end

# DELETE /articles/1
# DELETE /articles/1.xml
def destroy
  @article = Article.find(params[:id])
  @article.destroy

  respond_to do |format|
    format.html { redirect_to(articles_url) }
    format.xml { head :ok }
  end
end
```

注意我们为每个 RESTful 操作都有一个动作。每个动作之前的注释显示了调用它的 URL 格式。

还要注意，许多动作都包含一个 respond_to 块。正如我们在第 185 页看到的那样，Rails 使用它来确定要在响应中发送的内容类型。脚手架生成器会自动创建代码，使其能够适当响应对 HTML 或 XML 内容的请求。我们稍后会玩一下。

生成器创建的视图相当直接。唯一棘手的是需要使用正确的 HTTP 方法向服务器发送请求。例如，index 动作的视图如下所示：

```erb
Download restful/app/views/articles/index.html.erb
<h1>Listing articles</h1>
<table>
  <tr>
    <th>Title</th>
    <th>Summary</th>
    <th>Content</th>
  </tr>

<% for article in @articles %>
  <tr>
    <td><%=h article.title %></td>
    <td><%=h article.summary %></td>
    <td><%=h article.content %></td>
    <td><%= link_to 'Show', article %></td>
    <td><%= link_to 'Edit', edit_article_path(article) %></td>
    <td><%= link_to 'Destroy', article, :confirm => 'Are you sure?', :method => :delete %></td>
  </tr>
<% end %>
</table>

<br />

<%= link_to 'New article', new_article_path %>
```

指向编辑文章动作和添加新文章动作的链接都应使用常规 GET 方法，因此标准的 link_to 就足够了。⁶ 然而，销毁文章的请求必须发出 HTTP DELETE，因此调用中包含 :method => :delete 选项来 link_to。⁷

6. 注意我们正在使用命名路由作为这些调用的参数。一旦你使用 RESTful，命名路由就是必备的。

7. 而这里实现变得混乱。浏览器无法发出 HTTP DELETE 请求，所以 Rails 模拟它。如果你查看生成的 HTML，你会看到 Rails 使用 JavaScript 生成一个动态表单。表单会发布到你指定的动作。但它还包含一个名为 _method 的额外隐藏字段，其值为 delete。当 Rails 应用程序接收到 _method 参数时，它会忽略真实的 HTTP 方法，并假装参数的值（这里是 delete）被使用了。

为完整起见，这里是其他视图：

```erb
Download restful/app/views/articles/edit.html.erb
<h1>Editing article</h1>

<% form_for(@article) do |f| %>
  <%= f.error_messages %>
```

```erb
<p>
  <b>Content:</b>
  <%= @article.content %>
</p>

<%= link_to 'Edit', edit_article_path(@article) %> |
<%= link_to 'Back', articles_path %>
```

##### 添加你自己的动作

在理想世界中，你会在应用程序的所有资源上使用一致的动作集，但这并不总是实际的。你有时需要为资源添加特殊处理。例如，我们可能需要创建一个界面，让人们获取最近的文章。要在 Rails 中做到这一点，我们使用对 map.resources 调用的扩展：

```ruby
ActionController::Routing::Routes.draw do |map|
  map.resources :articles, :collection => { :recent => :get }
end
```

这种语法需要一点时间来适应。它说“我们想要添加一个名为 recent 的新动作，通过 HTTP GET 调用。它适用于资源集合——在这种情况下是所有文章。”

| Method | URL Path | Action | Helper |
|--------|----------|--------|--------|
| GET | /articles/recent | recent | recent_articles_url |

事实上，我们已经见过这种通过斜杠附加特殊动作到 URL 的技术——edit 动作使用相同的机制。

你也可以为单个资源创建特殊动作；只需使用 :member 而不是 :collection。例如，我们可以创建将文章标记为 embargoed 或 released 的动作——embargoed 文章在发布前不可见：

```ruby
ActionController::Routing::Routes.draw do |map|
  map.resources :articles, :member => { :embargo => :put,
    :release => :put }
end
```

这会在 map.resources 添加的标准集合中添加以下路由：

| Method | URL Path | Action | Helper |
|--------|----------|--------|--------|
| PUT | /articles/1/embargo | embargo | embargo_article_url(:id => 1) |
| PUT | /articles/1/release | release | release_article_url(:id => 1) |

也可以创建创建新资源的特殊动作；使用 :new，传递与 :collection 和 :member 相同的 :action => :method 哈希。例如，我们可能需要仅使用标题和正文创建文章——摘要被省略。

我们可以为此创建一个特殊的简短表单动作：

```ruby
ActionController::Routing::Routes.draw do |map|
  map.resources :articles, :new => { :shortform => :post }
end
```

这会在 map.resources 添加的标准集合中添加以下路由：

| Method | URL Path | Action | Helper |
|--------|----------|--------|--------|
| POST | /articles/new/shortform | shortform | shortform_new_article_url |

##### 嵌套资源

通常我们的资源本身包含额外的资源集合。例如，我们可能希望允许人们对文章发表评论。在这种情况下，每条评论都是一个资源，评论集合与每个文章资源相关联。

Rails 提供了声明此类情况路由的便捷且直观的方法：

```ruby
ActionController::Routing::Routes.draw do |map|
  map.resources :articles do |article|
    article.resources :comments
  end

  # ...

  map.connect ':controller/:action/:id'
  map.connect ':controller/:action/:id.:format'
end
```

甚至还有最简单和最常见情况的简写，例如这种情况：

```ruby
map.resources :articles, :has_many => :comments
```

两种表达式是等价的，定义了顶层的文章路由集合，并额外创建了评论的子路由。因为评论资源出现在 articles 块内部，所以评论资源必须由文章资源限定。这意味着评论的路径必须始终以特定文章的路径为前缀。要获取 id 为 99 的文章的 id 为 4 的评论，你需要使用 /articles/99/comments/4 的路径。

再次，我们可以通过使用 rake routes 命令来查看配置生成的完整路由集：

```text
articles GET    /articles
            {:controller=>"articles", :action=>"index"}
formatted_articles GET    /articles.:format
            {:controller=>"articles", :action=>"index"}
POST   /articles
  {:controller=>"articles", :action=>"create"}
POST   /articles.:format
  {:controller=>"articles", :action=>"create"}
new_article GET    /articles/new
  {:controller=>"articles", :action=>"new"}
formatted_new_article GET    /articles/new.:format
  {:controller=>"articles", :action=>"new"}
edit_article GET    /articles/:id/edit
  {:controller=>"articles", :action=>"edit"}
formatted_edit_article GET    /articles/:id/edit.:format
  {:controller=>"articles", :action=>"edit"}
article GET    /articles/:id
  {:controller=>"articles", :action=>"show"}
formatted_article GET    /articles/:id.:format
  {:controller=>"articles", :action=>"show"}
PUT    /articles/:id
  {:controller=>"articles", :action=>"update"}
PUT    /articles/:id.:format
  {:controller=>"articles", :action=>"update"}
DELETE /articles/:id
  {:controller=>"articles", :action=>"destroy"}
DELETE /articles/:id.:format
  {:controller=>"articles", :action=>"destroy"}
article_comments GET    /articles/:article_id/comments
  {:controller=>"comments", :action=>"index"}
formatted_article_comments GET    /articles/:article_id/comments.:format
  {:controller=>"comments", :action=>"index"}
POST   /articles/:article_id/comments
  {:controller=>"comments", :action=>"create"}
POST   /articles/:article_id/comments.:format
  {:controller=>"comments", :action=>"create"}
new_article_comment GET    /articles/:article_id/comments/new
  {:controller=>"comments", :action=>"new"}
formatted_new_article_comment GET    /articles/:article_id/comments/new.:format
  {:controller=>"comments", :action=>"new"}
edit_article_comment GET    /articles/:article_id/comments/:id/edit
  {:controller=>"comments", :action=>"edit"}
formatted_edit_article_comment GET    /articles/:article_id/comments/:id/edit.:format
  {:controller=>"comments", :action=>"edit"}
article_comment GET    /articles/:article_id/comments/:id
  {:controller=>"comments", :action=>"show"}
formatted_article_comment GET    /articles/:article_id/comments/:id.:format
  {:controller=>"comments", :action=>"show"}
PUT    /articles/:article_id/comments/:id
  {:controller=>"comments", :action=>"update"}
PUT    /articles/:article_id/comments/:id.:format
  {:controller=>"comments", :action=>"update"}
DELETE /articles/:article_id/comments/:id
  {:controller=>"comments", :action=>"destroy"}
DELETE /articles/:article_id/comments/:id.:format
  {:controller=>"comments", :action=>"destroy"}
  /:controller/:action/:id
  /:controller/:action/:id.:format
```




下载 restful2/app/views/articles/show.html.erb

<p>
  <b>标题：</b>
  <%=h @article.title %>
</p>

<p>
  <b>摘要：</b>
  <%=h @article.summary %>
</p>

<p>
  <b>内容：</b>
  <%=h @article.content %>
</p>

<% unless @article.comments.empty? %>
  <%= render :partial => "/comments/comment",
    :collection => @article.comments %>
<% end %>

<%= link_to "添加评论", new_article_comment_url(@article) %> |
<%= link_to '编辑', edit_article_path(@article) %> |
<%= link_to '返回', articles_path %>

这段代码展示了几项有趣的技术。我们使用一个局部模板来显示评论，但该模板位于目录 `app/views/comments` 中。我们通过在该 `render` 调用中加上前导的 `/` 和相对路径来告诉 Rails 到哪里查找。该代码还利用了路由辅助方法接受位置参数这一事实。我们不必这样写：

```
new_article_comment_url(:article_id => @article.id)
```

而可以利用 `:article` 字段是路由中第一个参数这一事实，这样写：

```
new_article_comment_url(@article)
```

不过，这些动作的形式略有不同；因为评论只能在文章的上下文中访问，所以我们在处理评论本身之前先获取文章。我们还使用了 `has_many` 声明的集合方法，来确保我们只处理属于当前文章的评论。

下载 restful2/app/controllers/comments_controller.rb

```ruby
class CommentsController < ApplicationController
  before_filter :find_article

  def new
    @comment = Comment.new
  end

def edit
  @comment = @article.comments.find(params[:id])
end

def create
  @comment = Comment.new(params[:comment])
  if (@article.comments << @comment)
    redirect_to article_url(@article)
  else
    render :action => :new
  end
end

def update
  @comment = @article.comments.find(params[:id])
  if @comment.update_attributes(params[:comment])
    redirect_to article_url(@article)
  else
    render :action => :edit
  end
end

def destroy
  comment = @article.comments.find(params[:id])
  @article.comments.delete(comment)
  redirect_to article_url(@article)
end

private

def find_article
  @article_id = params[:article_id]
  return(redirect_to(articles_url)) unless @article_id
  @article = Article.find(@article_id)
end

end
```

这个应用的完整源代码（包括用于评论的附加视图）可以在网上找到。

##### 浅层路由嵌套

有时，嵌套资源会产生冗长的 URL。解决方法之一是使用浅层路由嵌套：

```
map.resources :articles, :shallow => true do |article|
  article.resources :comments
end
```

这将启用以下路由的识别：

```
/articles/1          => article_path(1)
/articles/1/comments => article_comments_path(1)
/comments/2          => comment_path(2)
```

##### assert_routing(path, options, defaults={}, extras={}, message=nil)

结合了前面两个断言，验证路径能生成这些选项，并且这些选项也能生成该路径。

下载 e1/routing/test/unit/routing_test.rb

```ruby
def test_routing
  ActionController::Routing.use_controllers! ["store"]
  load "config/routes.rb"

  assert_routing("/store", :controller => "store", :action => "index")
  assert_routing("/store/list", :controller => "store", :action => "list")
  assert_routing("/store/add_to_cart/1",
    :controller => "store", :action => "add_to_cart", :id => "1")
end
```

重要的一点是，在选项散列中使用符号作为键，使用字符串作为值。如果不这样做，那些将你的选项与路由返回的选项进行比较的断言将会失败。

### 第22章

### Action Controller 与 Rails

在上一章中，我们探讨了 Action Controller 如何将传入的请求路由到应用程序中相应的代码。现在让我们看看那段代码内部发生了什么。

#### 22.1 动作方法

当控制器对象处理请求时，它会查找与传入动作同名的公共实例方法。如果找到，就调用该方法。如果没有找到，但控制器实现了 `method_missing`，则会调用该方法，并将动作名称作为第一个参数、一个空参数列表作为第二个参数传入。如果没有方法可调用，控制器会查找以当前控制器和动作命名的模板。如果找到，会直接渲染该模板。如果上述情况都没有发生，就会生成一个“未知动作（Unknown Action）”错误。

默认情况下，控制器中的任何公共方法都可以作为动作方法来调用。你可以通过将特定方法设为 protected 或 private 来阻止它们作为动作访问。如果出于某种原因，你必须在控制器中将某个方法设为公共方法，但又不希望它作为动作被访问，可以使用 `hide_action` 将其隐藏：

```
class OrderController < ApplicationController

  def create_order
    order = Order.new(params[:order])
    if check_credit(order)
      order.save
    else
      # ...
    end
  end
```

- `delete?`、`get?`、`head?`、`post?` 和 `put?` 根据请求方法返回 true 或 false。
- `xml_http_request?` 和 `xhr?` 如果此请求是由某个 Ajax 辅助方法发出的，则返回 true。请注意，此参数与 method 参数无关。
- `url`，返回用于请求的完整 URL。
- `protocol`、`host`、`port`、`path` 和 `query_string`，返回用于请求的 URL 的组成部分，基于以下模式：`protocol://host:port/path?query_string`。
- `domain`，返回请求域名最后两个组成部分。
- `host_with_port`，是请求的 `host:port` 字符串。
- `port_string`，如果端口不是默认端口，则为请求返回 `:port` 字符串。
- `ssl?`，如果这是 SSL 请求则返回 true；换句话说，该请求是通过 HTTPS 协议发出的。
- `remote_ip`，以字符串形式返回远程 IP 地址。如果客户端位于代理之后，该字符串可能包含多个地址。
- `path_without_extension`、`path_without_format_and_extension`、`format_and_extension` 和 `relative_path` 返回完整路径的各个部分。
- `env`，请求的环境。你可以使用它来访问浏览器设置的值，例如：
  `request.env['HTTP_ACCEPT_LANGUAGE']`
- `accepts`，请求的 accepts MIME 类型的值。
- `format`，请求的 accepts MIME 类型的值。如果没有可用的格式，则使用 accept 类型中的第一个。
- `mime_type`，与扩展名关联的 MIME 类型。
- `content_type`，请求的 MIME 类型。这对 put 和 post 请求很有用。
- `headers`，完整的 HTTP 头集合。
- `body`，作为 I/O 流的请求体。

`render(:inline =>string, [:type =>'erb'|'builder'|'rjs'], [:locals =>hash])`

将 `string` 解释为指定类型的模板源代码，并将渲染结果返回给客户端。如果给出了 `:locals` 散列，则其内容用于设置模板中局部变量的值。

如果应用程序正在开发模式下运行，以下代码会向控制器添加 `method_missing`。如果控制器被一个无效动作调用，该方法会渲染一个内联模板来显示动作名称和请求参数的格式化版本。

```
class SomeController < ApplicationController
  if RAILS_ENV == "development"
    def method_missing(name, *args)
      render(:inline => %{
<h2>Unknown action: #{name}</h2>
Here are the request parameters:<br/>
<%= debug(params) %> })
    end
  end
end
```

`render(:action =>action_name)`

渲染此控制器中给定动作的模板。有时人们会在应该使用重定向时使用 `render` 的 `:action` 形式。请参阅第470页开始的讨论，了解为什么这是一个坏主意。

```
def display_cart
  if @cart.empty?
    render(:action => :index)
  else
    # ...
  end
end
```

请注意，调用 `render(:action...)` 并不会调用该动作方法；它只是显示模板。如果模板需要实例变量，这些变量必须由调用 `render` 的方法来设置。

让我们重复这一点，因为这是初学者常犯的错误：调用 `render(:action...)` 并不会调用该动作方法。它只是渲染该动作的默认模板。

`render(:file =>path, [:use_full_path =>true|false], [:locals =>hash])`

渲染给定路径中的模板（该路径必须包含文件扩展名）。默认情况下，这应该是模板的绝对路径，但如果 `:use_full_path` 选项为 true，视图会在你传入的路径前加上模板基路径的值。模板基路径在应用程序的配置中设置。如果指定了 `:locals` 散列，其值将用于设置模板中的局部变量。





render(:template =>name, [:locals =>hash])

渲染模板并安排将生成的文本发送回客户端。:template 值必须同时包含新名称的控制器和动作部分，以正斜杠分隔。以下代码将渲染模板 app/views/blog/short_list：

```
class BlogController < ApplicationController
  def index
    render(:template => "blog/short_list")
  end
end
```

render(:partial =>name, ...)

渲染部分模板。我们在第 552 页深入讨论了部分模板。

render(:nothing => true)

返回空内容——向浏览器发送空主体。

render(:xml =>stuff)

将 stuff 渲染为文本，强制内容类型为 application/xml。

render(:json =>stuff, [:callback =>hash])

将 stuff 渲染为 JSON，强制内容类型为 application/json。指定 :callback 将导致结果被包装在名为的回调函数的调用中。

render(:update) do |page| ... end

将块作为 RJS 模板渲染，并传入 page 对象。

```
render(:update) do |page|
  page[:cart].replace_html :partial => 'cart', :object => @cart
  page[:cart].visual_effect :blind_down if @cart.total_items == 1
end
```

所有形式的 render 都接受可选的 :status、:layout 和 :content_type 参数。:status 参数用于设置 HTTP 响应中的状态头。默认为 "200 OK"。不要使用 3xx 状态的 render 来进行重定向；Rails 为此目的提供了 redirect 方法。

:layout 参数决定渲染结果是否会被布局包装（我们首次在第 99 页遇到布局，并将从第 548 页开始深入研究它们）。如果参数为 false，则不应用布局。如果设置为 nil 或 true，则仅在当前动作关联有布局时才应用布局。如果 :layout 参数的值为字符串，则将其视为渲染时使用的布局名称。当 :nothing 选项生效时，布局永远不会被应用。

:content_type 参数允许您指定将通过 Content-Type HTTP 头传递给浏览器的值。

有时能够将本应发送到浏览器的内容捕获到字符串中会很有用。render_to_string 方法接受与 render 相同的参数，但返回渲染结果作为字符串——渲染结果不会存储在响应对象中，因此除非您采取额外步骤，否则不会发送给用户。调用 render_to_string 不算作真正的渲染。您可以在之后调用真正的 render 方法，而不会出现 DoubleRender 错误。

##### 发送文件和其他数据

我们已经研究了在控制器中渲染模板和发送字符串。第三种响应类型是向客户端发送数据（通常，但不一定是文件内容）。

##### send_data

向客户端发送包含二进制数据的字符串。

```
send_data(data, options...)
```

向客户端发送数据流。通常浏览器会结合内容类型和 disposition，两者均在 options 中设置，来确定如何处理此数据。

```
def sales_graph
  png_data = Sales.plot_for(Date.today.month)
  send_data(png_data, :type => "image/png", :disposition => "inline")
end
```

###### 选项：

| :disposition | string | 建议浏览器将文件内联显示（选项 inline）或下载并保存（选项 attachment，默认值）。 |
| :filename | string | 向浏览器建议保存此数据时使用的默认文件名。 |
| :status | string | 状态代码（默认为 '200 OK'）。 |
| :type | string | 内容类型，默认为 application/octet-stream。 |
| :url_based_filename | boolean | 如果为 true 且未设置 :filename，则阻止 Rails 在 Content-Disposition 头中提供文件的基名。指定此项对于使某些浏览器正确处理 i18n 文件名是必要的。 |

##### send_file

向客户端发送文件的内容。

```
send_file(path, options...)
```

向客户端发送给定文件。该方法设置 Content-Length、Content-Type、Content-Disposition 和 Content-Transfer-Encoding 头。

很诱人使用如下逻辑来编码：

```
class BlogController
  def display
    @article = Article.find(params[:id])
  end

  def add_comment
    @article = Article.find(params[:id])
    comment  = Comment.new(params[:comment])
    @article.comments << comment
    if @article.save
      flash[:note] = "Thank you for your valuable comment"
    else
      flash[:note] = "We threw your worthless comment away"
    end
    # DON'T DO THIS
    render(:action => 'display')
  end
end
```

这里的意图显然是在评论发布后显示文章。为此，开发者在 add_comment 方法末尾调用了 render(:action=>display')。这会渲染 display 视图，向最终用户显示更新后的文章。但从浏览器的角度思考。它发送以 blog/add_comment 结尾的 URL 并得到一个索引列表作为返回。就浏览器而言，当前 URL 仍然是以 blog/add_comment 结尾的那个。这意味着如果用户点击刷新或重新加载（也许想看看是否有人发布了其他评论），add_comment URL 将再次发送到应用程序。用户本意是刷新显示，但应用程序看到的是添加另一条评论的请求。在博客应用中，这种无意的重复提交很不方便。在在线商店中，它可能代价高昂。

在这种情况下，正确地在索引列表中显示已添加的评论的方法是重定向浏览器到 display 动作。我们使用 Rails 的 redirect_to 方法来做到这一点。如果用户随后点击刷新，它只会重新调用 display 动作，而不会添加另一条评论：

```
def add_comment
  @article = Article.find(params[:id])
  comment = Comment.new(params[:comment])
  @article.comments << comment
  if @article.save
    flash[:note] = "Thank you for your valuable comment"
  else
    flash[:note] = "We threw your worthless comment away"
  end
  redirect_to(:action => 'display')
end
```

Rails 具有简单而强大的重定向机制。它可以重定向到给定控制器中的动作（传递参数）、到 URL（当前服务器上或之外），或到上一页。让我们依次查看这三种形式。

##### redirect_to

重定向到动作。

```
redirect_to(:action => ..., options...)
```

基于 options hash 中的值向浏览器发送临时重定向。目标 URL 使用 url_for 生成，因此这种形式的 redirect_to 拥有 Rails 路由代码背后的所有智能。有关描述，请参阅第 426 页第 21.2 节、Routing Requests。

##### redirect_to

重定向到 URL。

```
redirect_to(path)
```

重定向到给定的路径。如果路径不以协议（如 http://）开头，则当前请求的协议和端口将被前置。此方法不对 URL 执行任何重写，因此不应用于创建 intended 链接到应用程序中动作的路径（除非您使用 url_for 或命名路由 URL 生成器生成路径）。

```
def save
  order = Order.new(params[:order])
  if order.save
    redirect_to :action => "display"
  else
    session[:error_count] ||= 0
    session[:error_count] += 1
    if session[:error_count] < 4
      flash[:notice] = "Please try again"
    else
      # Give up -- user is clearly struggling
      redirect_to("/help/order_entry.html")
    end
  end
end
```

##### redirect_to

重定向到引用者。

```
redirect_to(:back)
```

重定向到当前请求中 HTTP_REFERER 头给出的 URL。

```
def save_details
  unless params[:are_you_sure] == 'Y'
    redirect_to(:back)
  else
    ...
  end
end
```





我们需要做的第一件事是把 `SESSION_KEY` 定义为一个常量，以便在应用程序后面引用。在 `config/environment.rb` 文件中，这个值目前被硬编码在 `config.action_controller.session` 的赋值里。我们需要把它重构出来：

```
Download e1/cookies/cookie2/config/environment.rb
# Be sure to restart your server when you modify this file

# Uncomment below to force Rails into production mode when
# you don't control web/app server and can't set it the proper way
# ENV['RAILS_ENV'] ||= 'production'

# Specifies gem version of Rails to use when vendor/rails is not present
RAILS_GEM_VERSION = '2.2.2' unless defined? RAILS_GEM_VERSION

# Bootstrap the Rails environment, frameworks, and default configuration
require File.join(File.dirname(__FILE__), 'boot')

# Define session key as a constant
SESSION_KEY = '_cookie2_session'

Rails::Initializer.run do |config|
  # ...

  # Your secret key for verifying cookie session data integrity.
  # If you change this key, all old sessions will become invalid!
  # Make sure the secret is at least 30 characters and all random,
  # no regular words or you'll be exposed to dictionary attacks.
  config.action_controller.session = {
    :session_key => SESSION_KEY,
    :secret      => 'cbd4061f23fe1dfeb087dd38c...888cdd186e23c9d7137606801cb7665'
  }

  # ...
end
```

现在我们需要做两件事。

首先，我们需要定义一个 `cookies_required` 过滤器，应用于应用程序中所有需要 cookies 的动作。为简单起见，我们将对除 cookies 测试本身之外的所有动作应用该过滤器。如果你的应用程序有不同的需求，请相应调整。如果 session 已经定义，这个方法什么也不做；否则，它会尝试将请求 URI 保存到一个新的 session 中，并重定向到 cookies 测试。

然后我们需要定义 `cookies_test` 方法本身。这个方法也很直接：如果没有 session，就记下日志并渲染一个简单的模板，告知用户必须启用 cookies 才能使用本应用程序。如果此时已有 session，我们只需重定向回去，并注意提供一个默认目的地，以防某个捣蛋鬼直接访问这个动作后把信息从 session 中删除。根据需求调整默认目的地：

```
Download el/cookies/cookie2/app/controllers/application.rb

# Filters added to this controller apply to all controllers in the application.
# Likewise, all the methods added will be available for all controllers.

class ApplicationController < ActionController::Base
  helper :all # include all helpers, all the time

  before_filter :cookies_required, :except => [:cookies_test]

  # See ActionController::RequestForgeryProtection for details
  # Uncomment the :secret if you're not using the cookie session store
  protect_from_forgery # :secret => 'cde978d90e26e7230552d3593d445759'

  # See ActionController::Base for details
  # Uncomment this to filter the contents of submitted sensitive data parameters
  # from your application log (in this case, all fields with names like "password").
  # filter_parameter_logging :password

  def cookies_test
    if request.cookies[SESSION_KEY].blank?
      logger.warn("** Cookies are disabled for #{request.remote_ip} at #{Time.now}")
      render :template => 'cookies_required'
    else
      redirect_to(session[:return_to] || {:controller => "store"})
      session[:return_to] = nil
    end
  end

  protected

  def cookies_required
    return unless request.cookies[SESSION_KEY].blank?
    session[:return_to] = request.request_uri
    redirect_to :action => "cookies_test"
  end
end
```

我们还有最后一件事需要处理。虽然前面的代码运行得很好，但它有一个不好的副作用：我们几乎所有的功能测试都会开始失败，因为无论它们之前期望什么，它们都没有预料到会被重定向到 cookies 测试。这可以通过创建一个伪 session 来修正。当然，既然我们在这里，任何有自尊心的敏捷开发者都会为 cookies 测试本身编写一个功能测试：

```
Download el/cookies/cookie2/test/functional/store_controller_test.rb

require 'test_helper'

class StoreControllerTest < ActionController::TestCase
  def setup
```

```
@request.cookies[SESSION_KEY] = "faux session"
end

test "existing functional tests should continue to work" do
  get :hello
  assert_response :success
end

test "when cookies are disabled a redirect results" do
  @request.cookies.delete SESSION_KEY
  get :hello
  assert_response :redirect
  assert_equal 'http://test.host/store/cookies_test', redirect_to_url
end
end
```

##### Rails 会话

Rails session 是一种类似哈希的结构，它能在多个请求之间持续存在。与原始 cookies 不同，session 可以保存任何对象（只要这些对象可以被序列化），这使得它们非常适合在 Web 应用程序中保存状态信息。例如，在我们的商店应用程序中，我们使用 session 在请求之间保存购物车对象。Cart 对象可以像任何其他对象一样在我们的应用程序中使用。但 Rails 做出安排，使得购物车在每个请求处理结束时被保存，更重要的是，当 Rails 开始处理传入请求时，会恢复正确的购物车。借助 session，我们可以假装应用程序在请求之间一直存在。

这就引出一个有趣的问题：这些数据到底在请求之间保存在哪里？一种选择是服务器将其作为 cookie 发送到客户端。这是 Rails 2.0 的默认做法。它会限制大小并增加带宽，但意味着服务器需要管理和清理的东西更少。请注意，内容经过加密签名，但（默认）不加密，这意味着用户可以看到内容，但不能篡改。

另一种选择是在服务器上存储数据。这包含两部分。首先，Rails 必须跟踪 session。它通过创建一个（默认）32 位十六进制字符的键来实现（这意味着有 16³² 种可能的组合）。这个键称为 session id，它实际上是随机的。Rails 会把这个 session id 作为 cookie（键为 `_session_id`）存储在用户的浏览器中。由于后续请求都来自这个浏览器，Rails 可以恢复 session id。

其次，Rails 在服务器上维护一个按 session id 索引的持久化 session 数据存储。当请求到来时，Rails 使用 session id 查找数据存储。它在其中找到的数据是一个序列化的 Ruby 对象。

marshal → 第 677 页

它会对此对象进行反序列化，并将结果存储在控制器的 session 属性中，应用程序代码可以访问这些数据。应用程序可以任意添加和修改这些数据。当每个请求处理完毕时，Rails 会把 session 数据写回数据存储。数据会一直保存在那里，直到这个浏览器的下一个请求到来。

应该在 session 中存储什么？只要遵守一些限制和注意事项，你可以存储任何你想要的东西：

- 对于可以在 session 中存储的对象类型有一些限制。具体细节取决于你所选择的存储机制（我们稍后会讲到）。一般情况下，session 中的对象必须是

##### David 说...

###### 基于 Cookie 的会话的奇妙之处

Rails 默认的 session 存储方案初听起来像个疯狂的想法。你竟然要把值存储在客户端？！但如果我想在 session 里存放核弹发射代码，而又不能让客户端真正知道这些代码，那该怎么办？

是的，默认存储不适合存放需要对客户端保密的秘密。但这实际上是一个有价值的约束，能引导你避免在 session 中保存可能过期的复杂对象所带来的风险。而且，所谓核弹发射代码这种纸老虎，几乎从来都不是一个真实、相关的担忧。

大小限制也不是问题。Cookie 大约只有 4KB，所以你不能把各种各样的废话塞进去。这再次符合最佳实践：只存储引用，比如 `cart_id`，而不是真正的购物车对象。

你最应该担心的关键安全问题是客户端是否真的能够修改 session。你需要确保你放入的值的完整性。如果客户端能把他的 `cart_id` 从 5 改成 8，然后拿到别人的购物车，那可就糟了。幸运的是，Rails 正好能保护你免受这种情况：它会对 session 进行签名，如果签名不匹配，就会抛出异常，警告发生了篡改。

你获得的好处是，每次请求都不需要从数据库读取和保存 session，从而减轻数据库负载，而且也没有清理工作。如果你把 session 保存在文件系统或数据库中，就必须处理如何清理过期 session 的问题，这真的很麻烦。没有人喜欢做清理工作。基于 cookie 的 session 懂得自己清理自己。这还有什么理由不爱呢？





serializable（使用 Ruby 的 Marshal 函数）。这意味着，例如，你不能将 I/O 对象存储在 session 中。

+   - 你可能不想在 session 数据中存储庞大的对象——将其放在数据库中，并从 session 中引用它。这对于基于 cookie 的 session 尤其重要，其中整体限制为 4KB。
+   - 你可能不想在 session 数据中存储易变的对象。例如，你可能想统计博客中的文章数量并将其存储在 session 中以提高性能。但，如果你这样做，计数不会在其他用户添加文章时得到更新。

将当前登录用户的对象存储在 session 数据中似乎很诱人。如果你的应用程序需要能够使用户失效，这可能并不明智。即使用户在数据库中被禁用，他们的 session 数据仍会反映有效状态。

将易变数据存储在数据库中，并从 session 中引用它。

+   - 你可能不想仅将关键信息存储在 session 数据中。例如，如果你的应用程序在一项请求中生成订单确认号并将其存储在 session 数据中，以便在处理下一项请求时保存到数据库，你就有可能在用户从浏览器中删除 cookie 时丢失该号码。关键信息必须在数据库中。

还有一个需要注意的问题，而且是一个很大的问题。如果你将一个对象存储在 session 数据中，那么下次你回到该浏览器时，你的应用程序将最终检索该对象。然而，如果在这期间你更新了应用程序，session 数据中的对象可能与应用程序中该对象类的定义不一致，应用程序在处理请求时将会失败。这里有三种选择。一种是将对象使用常规模型存储在数据库中，并在 session 中只保留该行的 id。模型对象比 Ruby marshaling 库更能容忍模式更改。第二种选择是每当你更改存储在该数据中的类的定义时，手动删除服务器上存储的所有 session 数据。

第三种选择稍微复杂一些。如果你为 session 键添加版本号，并在更新存储的数据时更改该号码，你将只加载与应用程序当前版本相对应的数据。你可以对存储在 session 中的对象的类进行版本控制，并根据每个请求关联的 session 键使用适当的类。这个最后的想法可能需要大量工作，因此你需要决定是否值得付出努力。

```
# Enable sessions for all actions except show and list
session .except => [ .show, .list ]

# Disable sessions on Sundays :)
session .off, .if => proc { Time.now.wday == 0 }
```

##### Comparing Session Storage Options

面对这么多 session 选项，你应该在应用程序中使用哪一个？正如 always 所说，答案是“视情况而定”。

如果你是一个高流量站点，保持 session 数据大小小，将敏感数据移出 session，并使用 cookie_store 是正确的做法。

如果我们排除 memory store 过于简单、file store 过于受限、memcached 过于夸张，那么服务器端选择就归结为 PStore、Active Record store 和基于 DRb 的存储。我们可以在这些选项之间比较性能和功能。

Scott Barron 对这些存储选项的性能进行了引人入胜的分析。⁸ 他的发现有些令人惊讶。对于少量 session，PStore 和 DRb 大致相等。随着 session 数量的增加，PStore 性能开始下降。这可能是因为主机操作系统难以维护包含数万个 session 数据文件的目录。DRb 性能保持相对平稳。使用 Active Record 作为后端存储的性能较低，但随着 session 数量的增加保持平稳。

这对你意味着什么？评论员 Bill Katz 在以下段落中总结了这一点：

> “如果你预计会成为一个大型网站，关键问题是可扩展性，你可以通过‘纵向扩展’（为现有服务器增加额外的 CPU、内存等）或‘横向扩展’（添加新服务器）来解决它。当前由 Google 等公司推广的哲学是通过添加廉价的商品服务器进行横向扩展。理想情况下，每个服务器都应该能够处理任何传入请求。由于单个 session 的请求可能在多个服务器上处理，我们需要我们的 session 存储能够在整个服务器场中访问。你选择的 session 存储选项应反映你优化整个服务器系统的计划。鉴于硬件和软件的丰富可能性，你可以在影响 session 存储选择的多个轴上进行优化。例如，你可以使用具有超快内存事务的新 MySQL 集群数据库；这与 Active Record 方法配合得很好。你也可以拥有一个高性能的存储区域网络，这

⁸. Mirrored at http://media.pragprog.com/titles/ror/sessions

可能会与 PStore 配合良好。memcached 方法被 LiveJournal、Slashdot 和 Wikipedia 等高流量网站使用。优化效果最好是在分析你试图扩展的特定应用程序并运行基准测试来调整你的方法时实现。简而言之，视情况而定。”

性能方面几乎没有绝对的真理，每个人情况都不同。你的硬件、网络延迟、数据库选择，甚至可能天气都会影响 session 存储各组件的交互。我们的最佳建议是先从最简单的可行解决方案开始，然后对其进行监控。如果它开始拖慢你的速度，在跳出煎锅之前先弄清楚原因。

我们建议你从 Active Record 解决方案开始。如果随着应用程序的增长，你发现它成为瓶颈，你可以迁移到基于 DRb 的解决方案。

##### Session Expiry and Cleanup

所有服务器端 session 存储解决方案的一个问题是，每个新 session 都会在 session 存储中添加一些内容。这意味着你最终需要做一些 housekeeping，否则你会耗尽服务器资源。

整理 session 还有另一个原因。许多应用程序不希望 session 永远持续。一旦用户从特定浏览器登录，应用程序可能希望强制执行规则，即用户仅在活动时保持登录状态；当他们注销或在最后一次使用应用程序后的固定时间后，他们的 session 应该终止。

你有时可以通过使保存 session id 的 cookie 过期来实现这种效果。然而，这容易受到终端用户滥用。更糟糕的是，很难将浏览器上 cookie 的过期与服务器上 session 数据的清理同步。

因此，我们建议你通过简单地删除其服务器端 session 数据来使 session 过期。如果随后浏览器请求包含已被删除的数据的 session id，应用程序将不会收到任何 session 数据；session 实际上将不存在。

实现此过期取决于所使用的存储机制。

对于基于 PStore 的 session，最简单的方法是定期运行 sweeper 任务（例如在类 Unix 系统下使用 cron(1)）。此任务应检查 session 数据目录中文件的最后修改时间，删除早于给定时间的文件。

对于基于 Active Record 的 session 存储，使用 sessions 表中的 updated_at 列。你可以通过让 sweeper 任务发出如下 SQL 来删除所有在最后一小时内未被修改的 session（忽略夏令时更改）：

```
delete from sessions
where now() - updated_at > 3600;
```

对于基于 DRb 的解决方案，过期发生在 DRb 服务器进程内。你可能希望在 session 数据哈希中的条目旁边记录时间戳。你可以运行一个单独的线程（甚至是单独的进程）定期删除此哈希中的条目。

在所有情况下，你的应用程序可以通过在不再需要 session 时调用 reset_session 来帮助此过程（例如，当用户注销时）。

#### 22.3 Flash: Communicating Between Actions

当我们使用 redirect_to 将控制权转移到另一个 action 时，浏览器会生成一个单独的请求来调用该 action。该请求将由我们的应用程序在一个全新的控制器对象实例中处理——在原始 action 中设置的实例变量对处理重定向 action 的代码不可用。但有时我们需要在这两个实例之间进行通信。我们可以使用一个称为 flash 的设施来做到这一点。

flash 是一个临时 scratchpad，用于存储值。它像哈希一样组织并存储在 session 数据中，因此你可以存储与键关联的值并稍后检索它们。它有一个特殊属性。默认情况下，在处理请求期间存储到 flash 中的值将在紧接着的下一个请求的处理期间可用。一旦该第二个请求处理完毕，这些值就会从 flash 中删除。⁹

flash 最常见的用途可能是将错误和信息字符串从一个 action 传递到下一个。意图是第一个 action 注意到某种条件，创建描述该条件的消息，并重定向到单独的 action。通过将消息存储在 flash 中，第二个 action 能够访问消息文本并在视图中使用它。

```
class BlogController
  def display
    @article = Article.find(params[:id])
  end
```

> 9. 如果你阅读 flash 功能的 RDoc，你会看到它谈到值仅对下一个 action 可用。这并不完全准确：flash 在处理下一个请求结束时被清除，而不是按 action 为基础。





`flash.now` 会创建一条瞬时的 flash 条目，而 `flash.keep` 则相反，它会让当前存在于 flash 中的条目再保留一个请求周期：

```
class SillyController
  def one
    flash[:notice] = "Hello"
    flash[:error] = "Boom!"
    redirect_to :action => "two"
  end

  def two
    flash.keep(:notice)
    flash[:warning] = "Mew!"
    redirect_to :action => "three"
  end

  def three
    # At this point,
    # flash[:notice]     => "Hello"
    # flash[:warning] => "Mew!"
    # and flash[:error] is unset
    render
  end
end
```

如果你没有向 `flash.keep` 传递任何参数，那么所有 flash 内容都会被保留。

Flash 不仅可以存储文本消息——你还可以用它来在动作之间传递各种信息。当然，对于需要长期保存的信息，你通常会使用 session（可能还要结合数据库）来存储数据；但如果只是想将参数从一个请求传递到下一个请求，flash 是非常合适的。

由于 flash 数据存储在 session 中，因此所有常规规则同样适用。特别是，每个对象都必须可序列化。我们强烈建议只在 flash 中传递简单的对象。

#### 22.4 过滤器与验证

过滤器允许你在控制器中编写代码来包装动作所执行的处理过程——你可以编写一段代码，然后让它在控制器（或控制器的子类）中的任意多个动作执行之前或之后被调用。这确实是一个非常强大的功能。利用过滤器，我们可以实现身份验证机制、日志记录、响应压缩，甚至响应定制。

Rails 支持三种类型的过滤器：前置（before）、后置（after）和环绕（around）。过滤器会在动作执行之前和/或之后被调用。根据定义方式的不同，它们可以以控制器内方法的形式运行，也可以作为参数传入：

```
# ...

class SomeController < ApplicationController

  before_filter do |controller|
    logger.info("Processing #{controller.action_name}")
  end

  after_filter AuditFilter

  # ...
end
```

默认情况下，过滤器应用于控制器中的所有动作（以及该控制器的任何子类）。你可以通过 `:only` 选项（指定一个或多个需要过滤的动作）和 `:except` 选项（列出需要排除在过滤之外的动作）来修改这一行为。

```
class BlogController < ApplicationController

  before_filter :authorize, :only => [ :delete, :edit_comment ]

  after_filter :log_access, :except => :rss

  # ...
```

##### 后置过滤器与响应修改

后置过滤器可用于修改出站响应，在需要时更改响应头和内容。有些应用程序使用这种技术在控制器模板生成的内容中执行全局替换（例如，将响应体中的字符串 `<customer/>` 替换为客户的姓名）。另一个用途是在用户浏览器支持的情况下压缩响应。

下面的代码就是一个示例，展示了这种技术的可能用法。¹⁰ 控制器将 `compress` 方法声明为后置过滤器。该方法会检查请求头，以确定浏览器是否接受压缩响应。如果接受，它就会使用 Zlib 库将响应体压缩成字符串。¹¹ 如果压缩后的字符串比原始响应体更短，它就用压缩版本替换原始内容，并更新响应的编码类型。

10. 这段代码并不是压缩的完整实现。特别是，它不会压缩通过 `send_file` 下载到客户端的流式数据。
11. 请注意，Zlib Ruby 扩展在你的平台上可能不可用——它依赖于底层 `libzlib.a` 库的存在。

例如，下面是一个简单的环绕过滤器，用于记录某个动作执行所花费的时间：

```
Download e1/filter/app/controllers/blog_controller.rb
class BlogController < ApplicationController
  around_filter :time_an_action

  def index
    # ...
    render :text => "hello"
  end

  def bye
    # ...
    render :text => "goodbye"
  end

  private

  def time_an_action
    started = Time.now
    yield
    elapsed = Time.now - started
    logger.info("#{action_name} took #{elapsed} seconds")
  end
end
```

我们将一个方法名 `time_an_action` 传递给 `around_filter` 声明。每当该控制器中的某个动作即将被调用时，这个过滤器方法就会被调用。它记录开始时间，然后第 19 行的 `yield` 语句会调用原始动作。当该动作返回后，它计算并记录在动作中花费的时间。

除了向 `around_filter` 传递方法名之外，你还可以传递一个块或一个过滤器类。

如果你使用块作为过滤器，它会被传入两个参数：控制器对象和一个动作代理。通过对第二个参数调用 `call` 来调用原始动作。例如，下面是上述过滤器的块版本：

```
Download e1/filter/app/controllers/blog_controller.rb
around_filter do |controller, action|
  started = Time.now
  action.call
  elapsed = Time.now - started
  controller.logger.info("#{controller.action_name} took #{elapsed} seconds")
end
```

第三种形式允许你传递一个对象作为过滤器。这个对象应当实现一个名为 `filter` 的方法。该方法会被传入控制器对象。它通过 `yield` 来调用动作。例如，下面将我们的计时过滤器实现为一个类：

```
Download e1/filter/app/controllers/blog_controller.rb
class BlogController < ApplicationController
  class TimingFilter
    def filter(controller)
      started = Time.now
      yield
      elapsed = Time.now - started
      controller.logger.info("#{controller.action_name} took #{elapsed} seconds")
    end
  end
  around_filter TimingFilter.new
end
```

还有一种替代形式的环绕过滤器，你需要传递一个实现了 `before` 和 `after` 方法的对象。这种形式已略有弃用。

与 before 和 after 过滤器一样，环绕过滤器也接受 `:only` 和 `:except` 参数。

环绕过滤器（默认情况下）以不同的方式添加到过滤器链中：第一个添加的环绕过滤器会最先执行。随后添加的环绕过滤器会被嵌套在已有的环绕过滤器内部。因此，给定以下代码：

```
around_filter :one, :two

def one
  logger.info("start one")
  yield
  logger.info("end one")
end

def two
  logger.info("start two")
  yield
  logger.info("end two")
end
```

日志消息的顺序将如下所示：

```
start one
start two
... 
end two
end one
```

这个声明将对 `post_comment` 动作应用验证。如果 session 中不包含 `:user_id` 键，则会向 flash 中添加一条提示信息，并将请求重定向到 `index` 动作。

`verify` 的参数可以分为三类。

##### 适用性

这些选项用于选择哪些动作需要进行验证：

- `:only => :name 或 [ :name, ... ]`
  仅验证列出的一个或多个动作。

- `:except => :name 或 [ :name, ... ]`
  验证除列出的动作之外的所有动作。

##### 测试条件

这些选项描述了对请求要执行的测试条件。如果指定了多个条件，则所有条件都必须为真，验证才能通过。

- `:flash => :key 或 [ :key, ... ]`
  flash 必须包含给定的一个或多个键。

- `:method => :symbol 或 [ :symbol, ... ]`
  请求方法（`:get`、`:post`、`:head` 或 `:delete`）必须匹配给定的符号之一。

- `:params => :key 或 [ :key, ... ]`
  请求参数必须包含给定的一个或多个键。

- `:session => :key 或 [ :key, ... ]`
  session 必须包含给定的一个或多个键。

- `:xhr => true 或 false`
  请求必须（或必须不）来自 Ajax 调用。

##### 动作

这些选项描述了验证失败时应执行的操作。如果未指定任何操作，则验证失败时会向浏览器返回一个空响应。

- `:add_flash => hash`
  将给定的键/值对哈希合并到 flash 中。这可以用于向用户生成错误响应。

- `:add_headers => hash`
  将给定的键/值对哈希合并到响应头中。





- `:redirect_to => params` — 使用给定的参数哈希进行重定向。
- `:render => params` — 使用给定的参数哈希进行渲染。

#### 22.5 缓存，第一部分

许多应用程序似乎花费大量时间重复做同样的任务。一个博客应用程序会为每个访客渲染当前文章列表。一个商店应用程序会为每个请求者显示相同的产品信息页面。

所有这些重复都会消耗我们的资源和服务器时间。渲染博客页面可能需要半打数据库查询，并且可能在多个 Ruby 方法和 Rails 模板中运行。对于单个请求来说这不是大问题，但乘以每小时数千次访问，服务器就会开始发出暗红色的光。用户会将其视为响应速度变慢。

在这种情况下，我们可以使用缓存来大大减轻服务器的负载并提高应用程序的响应能力。与其一次又一次地从头生成相同的内容，我们只需创建一次并记住结果。下一次收到对同一页面的请求时，我们将从缓存中提供它，而不是重新创建它。

Rails 提供了三种缓存方法。在本章中，我们将描述其中两种，即页面缓存和动作缓存。我们将在 Action View 章节第 555 页查看第三种，即片段缓存。

页面缓存是 Rails 缓存中最简单也最高效的形式。用户第一次请求特定 URL 时，我们的应用程序会被调用并生成一个 HTML 页面。此页面的内容会被存储在缓存中。下一次收到包含该 URL 的请求时，页面的 HTML 将直接从缓存中提供。你的应用程序永远看不到该请求。事实上，Rails 根本不参与其中。请求完全在 Web 服务器内部处理，这使得页面缓存非常、非常高效。你的应用程序以服务器提供任何其他静态内容的速度提供这些页面。

有时，我们的应用程序需要至少部分参与处理这些请求。例如，你的商店可能只向特定用户子集显示某些产品的详细信息（也许高级客户可以更早访问新产品）。在这种情况下，你显示的页面内容相同，但你不想向任何人显示——你需要过滤对缓存内容的访问。Rails 为此提供了动作缓存。

使用动作缓存时，你的应用程序控制器仍会被调用，并且其 before 过滤器会被运行。但是，如果存在已缓存的页面，则不会调用该动作本身。

让我们在具有公开内容和高级、仅限会员内容的网站的上下文中查看这一点。我们有两个控制器：一个 admin 控制器，用于验证某人是否为会员，以及一个 content 控制器，其中包含用于显示公开内容和高级内容的动作。公开内容由一个包含指向高级文章链接的单个页面组成。如果有人请求高级内容而他们不是会员，我们会将他们重定向到 admin 控制器中的一个动作，让他们注册。

忽略缓存一分钟，我们可以使用 before 过滤器来验证用户状态，以及用于两种内容的几个动作方法来实现此应用程序的内容部分：

```text
Download e1/cookies/cookie1/app/controllers/content_controller.rb
class ContentController < ApplicationController
  before_filter :verify_premium_user, :except => :public_content

  def public_content
    @articles = Article.list_public
  end

  def premium_content
    @articles = Article.list_premium
  end

  private

  def verify_premium_user
    user = session[:user_id]
    user = User.find(user) if user
    unless user && user.active?
      redirect_to :controller => "login", :action => "signup_new"
    end
  end
end
```

由于内容页面是固定的，因此可以被缓存。我们可以在页面级别缓存公开内容，但我们必须将对缓存的高级内容的访问限制为会员，因此我们需要为其使用动作级别缓存。要启用缓存，我们只需向我们的类添加两个声明：

```text
Download e1/cookies/cookie1/app/controllers/content_controller.rb
class ContentController < ApplicationController
  before_filter :verify_premium_user, :except => :public_content

  caches_page  :public_content
  caches_action :premium_content
end
```

caches_page 指令告诉 Rails 在第一次生成时缓存 public_content 的输出。此后，此页面将直接从 Web 服务器提供。

第二个指令 caches_action 告诉 Rails 缓存执行 premium_content 的结果，但仍执行过滤器。这意味着我们仍会验证请求页面的人是否被允许这样做，但我们不会实际执行该动作超过一次。[12]

caches_action 可以接受多个选项。:cache_path 选项允许你修改动作缓存路径。这对于处理多种不同条件且缓存需求不同的动作非常有用。:if 和 :unless 允许你传递一个 Proc 来控制何时应通过动作。最后，如果 :layout 选项为 false，Rails 将仅缓存你的动作内容。这在你的布局包含动态信息时很有用。

缓存默认仅在生产环境中启用。你可以通过设置以下内容手动打开或关闭它：

```text
ActionController::Base.perform_caching = true | false
```

你可以在应用程序的环境文件中进行此更改（在 config/environments 中），尽管那里的首选语法略有不同：

```text
config.action_controller.perform_caching = true
```

##### 要缓存的内容

Rails 的动作缓存和页面缓存严格基于 URL。页面根据首次生成它的 URL 的内容进行缓存，后续对同一 URL 的请求将返回保存的内容。

这意味着依赖于 URL 中不存在的信息的动态页面是缓存的较差候选者。这些包括以下内容：

- 内容基于时间的页面（尽管请参阅第 502 页第 22.5 节，缓存页面的基于时间的过期）。
- 内容依赖于会话信息的页面。例如，如果你为每个用户自定义页面，你可能无法缓存它们（尽管你可能能够利用从第 555 页开始描述的片段缓存）。
- 从你无法控制的数据生成的页面。例如，如果非 Rails 应用程序也可以更新该数据库，则从我们数据库中显示信息的页面可能无法缓存。我们的缓存页面会在应用程序不知情的情况下变得过时。

12. 动作缓存是 around_filter 的一个很好的例子，描述于第 491 页。过滤器的 before 部分检查缓存项是否存在。如果存在，它会直接将其渲染给用户，防止真实动作运行。过滤器的 after 部分将运行动作的结果保存到缓存中。

然而，缓存可以处理来自你控制下的易变内容生成的页面。正如我们在下一节中将看到的那样，这只是当它们变得过时时删除缓存页面的问题。

##### 过期页面

创建缓存页面只是等式的一半。如果用于创建这些页面的初始内容发生变化，缓存版本将变得过时，我们需要一种使它们过期的方法。

诀窍是让应用程序在用于创建动态页面的数据发生变化时注意到，然后删除缓存版本。下一次对该 URL 的请求到来时，缓存页面将基于新内容重新生成。

##### 显式过期页面

删除缓存页面的低级方法是使用 expire_page 和 expire_action 方法。这些接受与 url_for 相同的参数，并使与生成的 URL 匹配的缓存页面过期。

例如，我们的内容控制器可能有一个允许我们创建文章的动作，以及另一个更新现有文章的动作。当我们创建文章时，公开页面上的文章列表将变得过时，因此我们调用 expire_page，传入显示公开页面的动作名称。当我们更新现有文章时，公开索引页面保持不变（至少在我们的应用程序中是这样），但此特定文章的任何缓存版本都应被删除。由于此缓存是使用 caches_action 创建的，我们需要使用 expire_action 使页面过期，传入动作名称和文章 id。

```text
Download e1/cookies/cookie1/app/controllers/content_controller.rb
def create_article
  article = Article.new(params[:article])
  if article.save
    expire_page :action => "public_content"
  else
    # ...
  end
end

def update_article
  article = Article.find(params[:id])
  if article.update_attributes(params[:article])
    expire_action :action => "premium_content", :id => article
  else
    # ...
  end
end
```





你会例如，将 public/products 链接到你的网络驱动器，以保持 products 控制器的页面缓存。

##### 隐式过期页面

expire_xxx 方法运行良好，但它们也将缓存功能与控制器中的代码耦合在一起。每次你在数据库中更改某些内容时，你还必须弄清楚这可能会影响哪些缓存页面。虽然对于较小的应用程序来说这很容易，但随着应用程序的增长，这会变得更加困难。在一个控制器中进行的更改可能会影响另一个控制器中缓存的页面。帮助器方法中的业务逻辑，本不应该关心 HTML 页面，现在需要担心过期缓存页面。

幸运的是，Rails 清理器可以简化这种耦合。清理器是作用于你的模型对象的一种特殊类型的观察者。当模型中发生重要事件时，清理器会过期依赖于该模型数据的缓存页面。

你的应用程序可以根据需要拥有任意多的清理器。你通常会为每个控制器创建一个单独的清理器来管理缓存。将清理器代码放在 app/sweepers 中：

Download e1/cookies/cookie1/app/sweepers/article_sweeper.rb

```
class ArticleSweeper < ActionController::Caching::Sweeper

  observe Article

  # If we create a new article, the public list of articles must be regenerated
  def after_create(article)
    expire_public_page
  end

  # If we update an existing article, the cached version of that article is stale
  def after_update(article)
    expire_article_page(article.id)
  end

  # Deleting a page means we update the public list and blow away the cached article
  def after_destroy(article)
    expire_public_page
    expire_article_page(article.id)
  end

  private

  def expire_public_page
    expire_page(:controller => "content", :action => 'public_content')
  end
```

下一次请求到来时，这些页面将不会从缓存中满足，应用程序将处理它。在此过程中，它会自动重新填充缓存中的该特定页面，减轻后续获取该页面的负载。

你在哪里找到要删除的缓存文件？不出所料，这也是可配置的。页面缓存文件默认存储在应用程序的 public 目录中。它们将以它们缓存的 URL 命名，并带有 .html 扩展名。例如，content/show/1 的页面缓存文件将在这里：

```
app/public/content/show/1.html
```

这种命名方案并非巧合；它允许 Web 服务器自动找到缓存文件。你可以通过以下方式覆盖默认值：

```
config.action_controller.page_cache_directory = "dir/name"
config.action_controller.page_cache_extension = ".html"
```

Action 缓存文件默认不会存储在常规文件系统目录结构中，并且无法使用此技术过期。

##### 与客户端缓存友好共存

我们之前说过创建缓存页面只是方程式的一半，我们没有提到其实有三半。哎呀。

客户端（通常，但不总是浏览器）也经常有缓存。服务器和客户端之间的中间件也可能提供缓存服务。你可以通过提供 HTTP 头来帮助优化这些缓存（从而减少服务器负载）。这样做完全是可选的，并不总是能减少带宽，但另一方面，有时节省可能相当可观。

##### 过期头

最有效率的请求是不发出的请求。许多页面（尤其是图像、脚本和样式表）很少更改，但可能被频繁引用。确保在重新检索到达服务器之前就被优化掉的一种方法是提供 Expires 头。

虽然 Expires 头可能提供多种不同的选项，但最常见的用法是表示给定响应应被视为“有效”的时长，建议客户端在此期间无需重新请求此数据。在控制器中调用 expires_in 方法即可实现此结果：

```
expires_in 20.minutes
expires_in 1.year
```

服务器不应在 Expires 头中提供超过一年后的日期。

#### 22.6 GET 请求的问题

定期地，关于 Web 应用程序使用链接触发操作的方式的争论会重新出现。

问题如下。几乎自 HTTP 发明以来，就已经认识到 HTTP GET 和 HTTP POST 请求之间存在根本区别。蒂姆·伯纳斯-李在 1996 年就写过这件事。13 使用 GET 请求从服务器检索信息，使用 POST 请求请求服务器的状态更改。

问题是，这个规则已被 Web 开发人员广泛忽视。每当你看到一个带有“添加到购物车”链接的应用程序时，你就看到了违规，因为点击该链接会生成一个更改应用程序状态的 GET 请求（它在此示例中将某物添加到购物车）。而且大多数情况下，我们都逃脱了惩罚。

这在 2005 年春季对 Rails 社区发生了变化，当时 Google 发布了其 Google Web Accelerator（GWA）。14 这是一段客户端代码，可加快终端用户的浏览速度。它部分通过预缓存页面来实现这一点。在用户阅读当前页面的同时，加速器软件会扫描其中的链接并安排在后台读取和缓存相应的页面。

现在想象一下，你正在查看一个包含“添加到购物车”链接的在线商店。在你决定是购买酒红色热裤还是紫色背心时，加速器正忙于跟随链接。每个被跟随的链接都会向你的购物车添加新商品。

问题一直存在。搜索引擎和其他蜘蛛会不断跟随公共网页上的链接。通常，这些在应用程序中调用状态更改操作的链接（例如我们的“添加到购物车”链接）只有在用户开始某种交易后才会暴露，因此蜘蛛不会看到或跟随它们。GWA 在客户端运行的事实突然暴露了所有这些链接。

在理想的世界里，每个有副作用的请求都是 POST。15 而不是 GET。Web 页面将使用表单和按钮，只要它们希望服务器执行某些主动操作。世界并非理想，成千上万（数百万？）的页面在 GET 请求方面违反了规则。

13. http://www.w3.org/DesignIssues/Axioms
14. http://radar.oreilly.com/2005/05/google-web-accelerator-conside.html
15. 或更罕见的 PUT 或 DELETE 请求

Rails 中默认的 link_to 方法会生成一个常规链接，点击时创建 GET 请求。但这绝对不是 Rails 特有的问题。许多大型且成功的站点也是如此。

这真的是个问题吗？正如往常一样，答案是“视情况而定”。如果你编写了带有危险链接的应用程序（例如“删除订单”、“解雇员工”或“发射导弹”），则存在这些链接被无意跟随的风险，你的应用程序将忠实地执行请求的操作。

##### 修复 GET 问题

遵循一个简单的规则可以有效消除与危险链接相关的风险。基本公理很简单：永远不要允许一个直接的 <a href="..." 链接在没有某种人工干预的情况下被跟随，而该链接会执行危险操作。以下是使其在实践中生效的一些技术：

- 使用表单和按钮：不要使用超链接，使用表单和按钮来执行更改服务器状态的操作。表单使用 POST 请求提交，这意味着它们不会被跟随链接的蜘蛛提交，并且浏览器会在你重新加载页面时发出警告。

在 Rails 中，这意味着使用 button_to 辅助方法指向危险操作。但是，你需要仔细设计你的网页。HTML 不允许嵌套表单，因此你不能在另一个表单中使用 button_to。

- 使用确认页面：对于无法使用表单的情况，创建一个引用确认页面的链接。此确认应由表单的提交按钮触发；因此，破坏性操作不会被自动触发。

- 使用 :method 参数：使用 :post、:put 或 :delete 的值。这将防止请求被缓存或被网络爬虫触发。

一些人还使用以下技术，希望能防止问题。它们不起作用。

- 不要认为你的操作受保护只是因为你在链接上安装了 JavaScript 确认框。例如，Rails 允许你写这个：

```
link_to(:action => :delete, :confirm => "Are you sure?")
```

这将阻止用户因点击链接而意外造成损害，但前提是他们在浏览器中启用了 JavaScript。它也无助于防止蜘蛛和自动化工具盲目跟随链接。





你也可以拥有不是以动作命名的模板。这些模板可以从控制器中使用如下调用进行渲染：

```
render(:action => 'fake_action_name')
render(:template => 'controller/name')
render(:file => 'dir/template')
```

最后一种允许你将模板存储在文件系统的任何位置。如果你想在多个应用之间共享模板，这很有用。

#### 模板环境

模板包含固定文本和代码的混合。代码用于向模板添加动态内容。该代码在由控制器设置的信息可供访问的环境中运行。

- 控制器所有的实例变量在模板中也都可用。这是动作向模板传递数据的途径。
- 控制器的 flash、headers、logger、params、request、response 和 session 作为访问方法在视图中可用。除了 flash 之外，视图代码通常不应直接使用这些，因为处理它们的责任应由控制器承担。然而，在调试时我们发现这很有用。例如，下面的 html.erb 模板使用 debug 方法来显示 session 的内容、参数的细节以及当前的响应：

```
<h4>Session</h4> <%= debug(session) %>
<h4>Params</h4> <%= debug(params) %>
<h4>Response</h4> <%= debug(response) %>
```

- 当前的控制器对象可通过名为 controller 的属性访问。这允许模板调用控制器中的任何公共方法（包括 ActionController 中的方法）。
- 模板的基目录路径存储在属性 base_path 中。

##### 模板中放什么

开箱即用，Rails 支持三种类型的模板：

- Builder 模板使用 Builder 库构建 XML 响应。
- ERb 模板是内容和嵌入式 Ruby 的混合。它们通常用于生成 HTML 页面。
- RJS 模板创建在浏览器中执行的 JavaScript，通常用于与 Ajax 化网页交互。

我们将简要讨论 Builder，然后再看 ERb。我们将在第 24 章《Web，v2.0》中第 563 页讨论 RJS 模板。

##### Builder 模板

Builder 是一个独立的库，让你可以用代码表达结构化文本（如 XML）。¹ 一个 builder 模板（文件扩展名为 .xml.builder）包含使用 Builder 库生成 XML 的 Ruby 代码。

下面是一个简单的 builder 模板，输出产品名称和价格的 XML 列表：

Download erb/products.xml.builder

```
xml.div(:class => "productlist") do
  xml.timestamp(Time.now)
  @products.each do |product|
    xml.product do
      xml.productname(product.title)
      xml.price(product.price, :currency => "USD")
    end
  end
end
```

使用从控制器传递的适当产品集合，模板可能会产生如下内容：

```
<div class="productlist">
  <timestamp>Sun Oct 01 09:13:04 EDT 2006</timestamp>
  <product>
    <productname>Pragmatic Programmer</productname>
    <price currency="USD">12.34</price>
  </product>
  <product>
    <productname>Rails Recipes</productname>
    <price currency="USD">23.45</price>
  </product>
</div>
```

注意 Builder 如何将方法名转换为 XML 标签；当我们写 xml.price 时，它创建了一个名为 <price> 的标签，其内容为第一个参数，后续的哈希设置其属性。如果你想要使用的标签名与现有的方法名冲突，你需要使用 tag! 方法来生成标签：

```
xml.tag!("id", product.id)
```

Builder 可以生成你需要的几乎任何 XML。它支持命名空间、实体、处理指令，甚至 XML 注释。查看 Builder 文档了解详情。

1. Builder 可在 RubyForge（http://builder.rubyforge.org/）上获取，也可通过 RubyGems 获取。Rails 自带 Builder 的副本，因此我们无需下载任何东西即可开始。

##### ERb 模板

最简单地说，ERb 模板只是一个普通的 HTML 文件。如果模板不包含动态内容，它会原样发送给用户的浏览器。以下是一个完全有效的 html.erb 模板：

```
<h1>Hello, Dave!</h1>
<p>
  How are you, today?
</p>
```

然而，只渲染静态模板的应用使用起来往往有点无聊。我们可以使用动态内容让它们更生动：

```
<h1>Hello, Dave!</h1>
<p>
  It's <%= Time.now %>
</p>
```

如果你是 JSP 程序员，你会认识到这是一个内联表达式：<%= 和 %> 之间的任何代码都会被求值，结果使用 to_s 转换为字符串，然后该字符串被替换到结果页面中。标签内的表达式可以是任意代码：

```
<h1>Hello, Dave!</h1>
<p>
  It's <%= require 'date'
    DAY_NAMES = %w{ Sunday Monday Tuesday Wednesday
                    Thursday Friday Saturday }
    today = Date.today
    DAY_NAMES[today.wday]
  %>
</p>
```

在模板中放入大量业务逻辑通常被认为是非常糟糕的做法，如果被抓到，你会冒着招致编码警察愤怒的风险。我们在第 514 页讨论 helpers 时会看一个更好的处理方式。

有时你需要在模板中编写不直接生成任何输出的代码。如果在开始标签中去掉等号，内容会被执行，但不会插入到模板中。我们可以按如下方式重写前面的示例：

```
<% require 'date'
  DAY_NAMES = %w{ Sunday Monday Tuesday Wednesday
                  Thursday Friday Saturday }
  today = Date.today
%>
<h1>Hello, Dave!</h1>
<p>
  It's <%= DAY_NAMES[today.wday] %>.
  Tomorrow is <%= DAY_NAMES[(today + 1).wday] %>.
</p>
```

我们希望消除模板之间的重复。如果商店的默认名称发生变化，我们不想编辑每个视图。所以，让我们将计算页面标题的代码移到一个 helper 方法中。因为我们在 store 控制器中，我们编辑 app/helpers 中的文件 store_helper.rb（如下一页所示）。

```
module StoreHelper
  def page_title
    @page_title || "Pragmatic Store"
  end
end
```

现在视图代码只需调用 helper 方法：

```
<h3><%= page_title %></h3>
<!-- ... -->
```

（我们可能还想通过将整个标题的渲染移到一个由所有控制器视图共享的单独 partial 模板中来消除更多重复，但我们要到第 23.9 节《Partial-Page Templates》，第 552 页才讨论它们。）

#### 23.3 用于格式化、链接和分页的 Helpers

Rails 附带了一堆内置的 helper 方法，可供所有视图使用。在本节中我们会触及重点，但你可能想查看 Action View RDoc 了解具体细节——里面有很多功能。

##### 格式化 Helpers

一组 helper 方法处理日期、数字和文本。

```
<%= distance_of_time_in_words(Time.now, Time.local(2005, 12, 25)) %>
  248 days
```

```
<%= distance_of_time_in_words(Time.now, Time.now + 33, false) %>
  1 minute
```

```
<%= distance_of_time_in_words(Time.now, Time.now + 33, true) %>
  half a minute
```

```
<%= time_ago_in_words(Time.local(2004, 12, 25)) %>
  116 days
```

```
<%= number_to_currency(123.45) %>
  $123.45
```

```
<%= number_to_currency(234.56, :unit => "CAN$", :precision => 0) %>
  CAN$235
```

```
<%= number_to_human_size(123_456) %>
    120.6 KB
```

```
<%= number_to_percentage(66.66666) %>
    66.667%
```

```
<%= number_to_percentage(66.66666, :precision => 1) %>
    66.7%
```

```
<%= number_to_phone(2125551212) %>
    212-555-1212
```

```
<%= number_to_phone(2125551212, :area_code => true, :delimiter => " ") %>
    (212) 555 1212
```

```
<%= number_with_delimiter(12345678) %>
    12,345,678
```

```
<%= number_with_delimiter(12345678, "_") %>
    12_345_678
```

```
<%= number_with_precision(50.0/3) %>
    16.667
```

debug 方法使用 YAML 转储其参数并转义结果以便在 HTML 页面中显示。这在尝试查看模型对象或请求参数中的值时很有帮助。

```
<%= debug(params) %>
--- !ruby/hash:HashWithIndifferentAccess
name: Dave
language: Ruby
action: objects
controller: test
```

还有另一组处理文本的 helpers。有用于截断字符串和在字符串中突出显示单词的方法。

```
<%= simple_format(@trees) %>
```

格式化字符串，尊重换行和段落换行。你可以给它 Joyce Kilmer 诗歌《Trees》的纯文本，它会添加 HTML 将其格式化如下。

```
<p> I think that I shall never see
<br />A poem lovely as a tree.</p>

<p>A tree whose hungry mouth is prest
<br />Against the sweet earth's flowing breast;
</p>
```


take a condition parameter, followed by the regular parameters to link_to. If the condition is true (for link_to_if) or false (for link_to_unless), a regular link will be created using the remaining parameters. If not, the name will be added as plain text (with no hyperlink).

The link_to_unless_current helper is used to create menus in sidebars where the current page name is shown as plain text and the other entries are hyperlinks:

```
<ul>
  <%w{ create list edit save logout }.each do |action| -%>
    <li>
      <%= link_to_unless_current(action.capitalize, :action => action) %>
    </li>
  <% end -%>
</ul>
```

The link_to_unless_current helper may also be passed a block that is evaluated only if the current action is the action given, effectively providing an alternative to the link. There also is a current_page helper method that simply tests whether the current request URI was generated by the given options.

As with url_for, link_to and friends also support absolute URLs:

```
<%= link_to("Help", "http://my.site/help/index.html") %>
```

The image_tag helper can be used to create <img> tags. The image size may be specified using a single :size parameter (of the form widthxheight) or by explicitly giving the width and height as separate parameters:

```
<%= image_tag("/images/dave.png", :class => "bevel", :size => "80x120") %>
<%= image_tag("/images/andy.png", :class => "bevel", :width => "80", :height => "120") %>
```

If you don't give an :alt option, Rails synthesizes one for you using the image's filename.

If the image path doesn't start with a / character, Rails assumes that it lives under the /images directory.

You can make images into links by combining link_to and image_tag:

```
<%= link_to(image_tag("delete.png", :size => "50x22"),
    { :controller => "admin",
      :action     => "delete",
      :id         => @product},
    { :confirm   => "Are you sure?",
      :method    => :delete})
%>
```

The mail_to helper creates a mailto: hyperlink that, when clicked, normally loads the client's e-mail application. It takes an e-mail address, the name of the link, and a set of HTML options. Within these options, you can also use :bcc, :cc, :body, and :subject to initialize the corresponding e-mail fields. Finally, the

magic option :encode=>"javascript" uses client-side JavaScript to obscure the generated link, making it harder for spiders to harvest e-mail addresses from your site.⁵

```
<%= mail_to("support@pragprog.com", "Contact Support",
    :subject => "Support question from #{@user.name}",
    :encode => "javascript") %>
```

As a weaker form of obfuscation, you can use the :replace_at and :replace_dot options to replace the at sign and dots in the displayed name with other strings. This is unlikely to fool harvesters.

The AssetTagHelper module also includes helpers that make it easy to link to stylesheets and JavaScript code from your pages and to create autodiscovery Atom feed links. We created a stylesheet link in the layouts for the Depot application, where we used stylesheet_link_tag in the head:

Download depot_r/app/views/layouts/store.html.erb

```
<%= stylesheet_link_tag "depot", :media => "all" %>
```

The stylesheet_include_tag method can also take a parameter named :all indicating that all styles in the stylesheet directory will be included. Adding :recursive => true will cause Rails to include all styles in all subdirectories too.

The javascript_include_tag method takes a list of JavaScript filenames (assumed to live in public/javascripts) and creates the HTML to load these into a page. In addition to :all and :defaults, javascript_include_tag accepts as a parameter the value :defaults, which acts as a shortcut and causes Rails to load the files prototype.js, effects.js, dragdrop.js, and controls.js, along with application.js if it exists. Use the latter file to add your own JavaScript to your application’s pages.⁶

An RSS or Atom link is a header field that points to a URL in our application. When that URL is accessed, the application should return the appropriate RSS or Atom XML:

```
<html>
  <head>
    <%= auto_discovery_link_tag(:atom, :action => 'feed') %>
  </head>
  . . .
```

Finally, the JavaScriptHelper module defines a number of helpers for working with JavaScript. These create JavaScript snippets that run in the browser to generate special effects and to have the page dynamically interact with our

5. But it also means your users won’t see the e-mail link if they have JavaScript disabled in their browsers.

6. Writers of plug-ins can arrange for their own JavaScript files to be loaded when an application specifies :defaults, but that’s beyond the scope of this book.

application. That's the subject of a separate chapter, Chapter 24, The Web, v2.0, on page 563.

By default, image and stylesheet assets are assumed to live in the images and stylesheets directories relative to the application's public directory. If the path given to an asset tag method includes a forward slash, then the path is assumed to be absolute, and no prefix is applied. Sometimes it makes sense to move this static content onto a separate box or to different locations on the current box. Do this by setting the configuration variable asset_host:

```
config.action_controller.asset_host = "http://media.my.url/assets"
```

##### Pagination Helpers

A community site might have thousands of registered users. We might want to create an administration action to list these, but dumping thousands of names to a single page is somewhat rude. Instead, we'd like to divide the output into pages and allow the user to scroll back and forth in these.

As of Rails 2.0, pagination is no longer part of Rails; instead, this functionality is provided by a gem. You can add this gem to an existing application by adding the following to the end of config/environment.rb:

```
Rails::Initializer.run do |config|
  config.gem 'mislav-will_paginate', :version => '~> 2.3.2',
  :lib => 'will_paginate', :source => 'http://gems.github.com'
end
```

To install this gem (and any other missing gem dependencies), run this:

```
sudo rake gems:install
```

Now pagination is ready to use.

Pagination works at the controller level and at the view level. In the controller, it controls which rows are fetched from the database. In the view, it displays the links necessary to navigate between different pages.

Let's start in the controller. We've decided to use pagination when displaying the list of users. In the controller, we declare a paginator for the users table:

```
Download e1/views/app/controllers/pager_controller.rb
```

```
def user_list
  @users = User.paginate :page => params[:page], :order => 'name'
end
```

Other than requiring a :page parameter, paginate works just like find—it just doesn't fetch all of the records.

paginate returns a PaginatedCollection proxy object paginator. This object can be used by our view to display the users, thirty at a time. The paginator knows which set of users to show by looking for a request parameter, by default called

#### 23.4 How Forms Work

Rails features a fully integrated web stack. This is most apparent in the way that the model, controller, and view components interoperate to support creating and editing information in database tables.

In Figure 23.1, we can see how the various attributes in the model pass through the controller to the view, on to the HTML page, and back again into the model. The model object has attributes such as name, country, and password. The template uses helper methods (which we'll discuss shortly) to construct an HTML form to let the user edit the data in the model. Note how the form fields are named. The country attribute, for example, is mapped to an HTML input field with the name user[country].

Figure 23.1: Models, controllers, and views work together.

```
myapp_controller.rb
def edit
  @user = User.find(params[:id])
end
```

```
edit.html.erb
<% form_for :user,
  :url => { :action => 'save', :id => @user } do |f| %>
<%= f.text_field 'name' %>
<%= f.text_field 'country' %>
<%= f.password_field 'password' %>
...
<% end %>
```

```
<form action="/myapp/save/1234">
<input name="user[name]" ... >
<input name="user[country]" ... >
<input name="user[password]" ... >
...
</form>
```

```
@params = {
  :id => 1234,
  :user => {
    :name => "...",
    :country => "...",
    :password => "..."
  }
}
```

```
def save
  user = User.find(params[:id])
  if user.update_attributes(params[:user])
  ...
  end
end
```

- 1 The application receives a request to edit a user. It reads the data into a new User model object.
- 2 The edit.html.erb template is called. It uses the information in the user object to generate...
- 3 the HTML is sent to the browser. When the response is received...
- 4 the parameters are extracted into a nested hash.
- 5 The save action uses the parameters to find the user record and update it.




当用户提交表单时，原始的 POST 数据会被发送回我们的应用程序。Rails 从表单中提取字段并构建 params 哈希。简单的值（例如 id 字段，由路由从表单动作中提取）作为标量存储在哈希中。但是，如果参数名称中包含方括号，Rails 会认为它是更结构化数据的一部分，并构建一个哈希来保存这些值。在这个哈希内部，方括号内的字符串将作为键。如果参数名称中包含多组方括号，该过程可以重复进行。

| 表单参数 | params |
|---|---|
| id=123 | { :id => "123" } |
| user[name]=Dave | { :user => { :name => "Dave" } } |
| user[address][city]=Wien | { :user => { :address => { :city => "Wien" } } } |

在集成整体的最后部分，模型对象可以接受来自哈希的新属性值，这让我们可以这样写：

```ruby
user.update_attributes(params[:user])
```

Rails 的集成远不止于此。查看图 23.1 中的 .html.erb 文件，我们可以看到模板使用了一组辅助方法来创建表单的 HTML；这些方法包括 form_for 和 text_field。

实际上，Rails 的表单支持有点像“分裂人格”。当你编写映射到数据库资源的表单时，可能会使用 form_for 风格的表单。当你编写的表单不容易映射到数据库表时，你可能会使用更底层的 form_tag 风格。（事实上，这种命名在 Rails 大多数表单辅助方法中是一致的；以 _tag 结尾的方法通常比不带 _tag 的对应方法更底层。）

让我们先来看高层次、面向资源的 form_for 类型的表单。

#### 23.5 包装模型对象的表单

包装单个 Active Record 模型对象的表单应使用 form_for 辅助方法创建。（注意，form_for 应放在 `<%...%>` 结构中，而不是 `<%=...%>`。）

```ruby
<% form_for :user do |form| %>
  ...
<% end %>
```

第一个参数身兼两职。它告诉 Rails 被操作对象的名称（此处为 :user），同时也是持有该对象引用的实例变量名称（@user）。因此，在渲染包含此表单的模板的控制器动作中，我们可以这样写：

```ruby
def new
  @user = User.new
end
```

接收表单数据的动作将使用该名称从请求参数中选择数据：

```ruby
def create
  @user = User.new(params[:user])
  ...
end
```

如果由于某种原因，保存模型对象的变量没有以模型类命名，我们可以将该变量作为可选的第二个参数传给 form_for：

```ruby
<% form_for :user, @account_holder do |form| %>
  ...
<% end %>
```

初次使用 form_for 的人常常会被一个事实绊倒：它不应在 ERb 替换块中使用。你应该这样写：

```ruby
<% form_for :user, @account_holder do |form| %>
```

而不是下面这种带等号的变体：

```ruby
<%= form_for :user, @account_holder do |form| %><!-- 不要这样做 -->
```

form_for 接受一个选项哈希。最常用的两个选项是 :url 和 :html。:url 选项采用与 url_for 和 link_to 方法相同的字段。它指定提交表单时要调用的 URL。

```ruby
<% form_for :user, :url => { :action => :create } %>
  ...
```

它也适用于命名路由（这也是你应该使用它的方式）。

如果我们不指定 :url 选项，form_for 会将表单数据提交回原始动作：

```ruby
<% form_for :user, :url => users_url %>
  ...
```

:html 选项允许我们向生成的表单标签添加 HTML 属性：

```ruby
<% form_for :product,
    :url => { :action => :create, :id => @product },
    :html => { :class => "my_form" } do |form| %>
```

作为特殊情况，如果 :html 哈希包含 :multipart => true，表单将返回多部分表单数据，从而可用于文件上传（参见第 544 页的 23.8 节“向 Rails 应用程序上传文件”）。

我们可以使用 :html 选项中的 :method 参数来模拟使用 POST 以外的方法发送表单数据：

```ruby
<% form_for :product,
    :url => { :action => :create, :id => @product },
    :html => { :class => "my_form", :method => :put } do |form| %>
```

##### 字段辅助方法和 form_for

form_for 接受一个块（位于它和 `<% end %>` 之间的代码）。它将一个表单构建器对象传给这个块。在块内部，我们可以使用模板中任何地方可用的正常 HTML 和 ERb 混合体。但是，我们也可以使用表单构建器对象来添加表单元素。例如，这里有一个简单表单，用于捕获新产品信息：

```ruby
Download e1/views/app/views/form_for/new.html.erb
<% form_for :product, :url => { :action => :create } do |form| %>
<p>Title:     <%= form.text_field :title, :size => 30 %></p>
<p>Description: <%= form.text_area :description, :rows => 3 %></p>
<p>Image URL:  <%= form.text_field :image_url %></p>
<p>Price:      <%= form.text_field :price, :size => 10 %></p>
<%= form.select :title, %w{ one two three } %>
<p><%= submit_tag %></p>
<% end %>
```

这里的关键是使用表单构建器辅助方法来构造表单上的 HTML `<input>` 标签。当我们创建包含如下内容的模板时：

```ruby
<% form_for :product, :url => { :action => :create } do |form| %>
  <p>
    Title:     <%= form.text_field :title, :size => 30 %>
  </p>
<% end %>
```

Rails 将生成如下 HTML：

```html
<form action="/form_for/create" method="post">
  <p>
    Title: <input id="product_title" name="product[title]"
                   size="30" type="text" />
  </p>
```

注意 Rails 如何自动将输入字段命名为模型对象名（product）和字段名（title）的组合。

Rails 为文本字段（普通、隐藏、密码和文本区域）、单选按钮和复选框提供辅助支持。（它还支持 type="file" 的 `<input>` 标签，但我们将在第 544 页的 23.8 节“向 Rails 应用程序上传文件”中讨论。）

所有表单构建器辅助方法至少需要一个参数：设置字段值时模型中要查询的属性名称。当我们这样写：

```ruby
<% form_for :product, :url => { :action => :create } do |form| %>
  <p>
    Title:     <%= form.text_field :title, :size => 30 %>
  </p>
<% end %>
```

Rails 将用 @product.title 的值填充 `<input>` 标签。name 参数可以是字符串或符号；惯用的 Rails 使用符号。

所有辅助方法还接受一个选项哈希，通常用于设置 HTML 标签的类。这通常是可选的第二个参数；对于单选按钮，它是第三个参数。不过，在着手设计使用类和 CSS 标记无效字段的复杂方案之前，请继续阅读。正如我们稍后将看到的，Rails 使这变得很容易。

###### 文本字段

```ruby
form.text_field(:attribute, options)

form.hidden_field(:attribute, options)

form.password_field(:attribute, options)
```

分别构造类型为 text、hidden 或 password 的 `<input>` 标签。默认内容将取自 @variable.attribute。常见选项包括 :size => "nn" 和 :maxlength => "nn"。

###### 文本区域

```ruby
form.text_area(:attribute, options)
```

构造一个二维文本区域（使用 HTML `<textarea>` 标签）。常见选项包括 :cols => "nn" 和 :rows => "nn"。

###### 单选按钮

```ruby
form.radio_button(:attribute, tag_value, options)
```

创建一个单选按钮。通常，一个属性会有多个单选按钮，每个按钮具有不同的标签值。其标签值与属性当前值匹配的按钮将在显示时被选中。如果用户选择了不同的单选按钮，该按钮的标签值将存储在字段中。

###### 复选框

```ruby
form.check_box(:attribute, options, on_value, off_value)
```

创建一个与给定属性关联的复选框。如果属性值为 true，或者属性值转换为整数后非零，则复选框将被选中。

随后返回给应用程序的值由第三个和第四个参数设置。默认值在复选框被选中时将属性设置为 "1"，否则设置为 "0"。

注意，由于浏览器不会发送未选中的复选框，Rails 还会生成一个与复选框同名的隐藏字段，并将其放在复选框之前，这样如果复选框被选中，浏览器就会发送复选框。这种方法仅在复选框不是类似数组的参数时有效。在这种情况下，你可能需要显式检查 params 数组中的这一条件，或者在使用 update_attributes 等方法之前单独清空目标数组属性。





##### 选择列表

选择列表是那些带有内置人工智能的下拉列表框，保证你想要的选择只能通过滚动过去其他人的选择才能到达。

选择列表包含一组选择项。每个选择项都有一个显示字符串和一个可选的 value 属性。显示字符串是用户看到的内容，而 value 属性是如果选择该项则发送回应用程序的内容。对于常规选择列表，一个选择项可以被标记为已选择；其显示字符串将是显示给用户的默认值。对于多选列表，可以选择多个项，在这种情况下，它们的全部值都将发送到应用程序。基本的选择列表是使用 select 辅助方法创建的：

```
form.select(:attribute, choices, options, html_options)
```

choices 参数填充选择列表。该参数可以是任何可枚举对象（因此数组、哈希和数据库查询的结果都是可以接受的）。

最简单的 choices 形式是一个字符串数组。每个字符串在下拉列表中成为一个选择项，如果其中一个与 @variable.attribute 的当前值匹配，则会被选中。（这些示例假设 @user.name 被设置为 Dave。）

Download e1/views/app/views/test/select.html.erb

```
<% form_for :user do |form| %>
  <%= form.select(:name, %{ Andy Bert Chas Dave Eric Fred }) %>
<% end %>
```

这会生成以下 HTML：

```
<select id="user_name" name="user[name]">
  <option value="Andy">Andy</option>
  <option value="Bert">Bert</option>
  <option value="Chas">Chas</option>
  <option value="Dave" selected="selected">Dave</option>
  <option value="Eric">Eric</option>
  <option value="Fred">Fred</option>
</select>
```

如果 choices 参数中的元素各自响应 first 和 last（如果每个元素本身就是一个数组，则会如此），选择将使用第一个值作为显示文本，最后一个值作为内部键：

Download e1/views/app/views/test/select.html.erb

```
<%= form.select(:id, [ ['Andy', 1],
  ['Bert', 2],
  ['Chas', 3],
  ['Dave', 4],
  ['Eric', 5],
  ['Fred', 6]]) %>
```

此示例显示的列表与第一个相同，但它传回应用程序的值将是 1，或 2，或 3，或.... 而不是 Andy、Bert 或 Chas。生成的 HTML 如下：

```
<select id="user_id" name="user[id]">
  <option value="1">Andy</option>
  <option value="2">Bert</option>
  <option value="3">Chas</option>
  <option value="4" selected="selected">Dave</option>
  <option value="5">Eric</option>
  <option value="6">Fred</option>
</select>
```

最后，如果你将哈希作为 choices 参数传递，键将用作显示文本，值用作内部键。因为它是哈希，所以你无法控制生成的列表中条目的顺序。

应用程序通常需要根据数据库表中存储的信息构建选择框。一种方法是让模型的 find 方法填充 choices 参数。虽然我们在本代码片段中将 find 调用与 select 放在一起，但在现实中 find 可能在控制器或 helper 模块中。

```
<%= @users = User.find(:all, :order => "name").map { |u| [u.name, u.id] } form.select(:name, @users) %>
```

注意我们如何将结果集转换为数组的数组，其中每个子数组包含名称和 id。

实现相同效果的更高层方式是使用 collection_select。它接受一个集合，其中每个成员都有返回选项显示字符串和键的属性。在此示例中，集合是用户模型对象的列表，我们使用这些模型的 id 和 name 属性构建选择列表。

```
<%= @users = User.find(:all, :order => "name") form.collection_select(:name, @users, :id, :name) %>
```

##### 分组选择列表

分组是选择列表中很少使用但功能强大的特性。你可以用它为列表中的条目提供标题。在下一页的图 23.2 中，我们可以看到一个带有三个分组的选择列表。

完整的选择列表表示为一组组的数组。每个组都是一个具有名称和子选项集合的对象。在下面的

![](img/a160fc3a330a0b3b2a764d41d614e688_529_0.png)

图 23.2：带有分组选项的选择列表

示例中，我们将设置一个按送达速度分组的运输选项列表。我们将创建一个非数据库模型 Shipping 来封装运输选项。在其中我们将定义一个结构来保存每个运输选项，以及一个定义选项组的类。我们将静态初始化它（在实际应用程序中你可能会从表中提取数据）。

Download e1/views/app/models/shipping.rb

```
class Shipping
  ShippingOption = Struct.new(:id, :name)

  class ShippingType
    attr_reader :type_name, :options
    def initialize(name)
      @type_name = name
      @options = []
    end
    def <<(option)
      @options << option
    end
  end

  ground  = ShippingType.new("SLOW")
  ground  << ShippingOption.new(100, "Ground Parcel")
  ground  << ShippingOption.new(101, "Media Mail")

  regular  = ShippingType.new("MEDIUM")
  regular  << ShippingOption.new(200, "Airmail")
  regular  << ShippingOption.new(201, "Certified Mail")

  priority  = ShippingType.new("FAST")
  priority << ShippingOption.new(300, "Priority")
  priority << ShippingOption.new(301, "Express")

  OPTIONS = [ ground, regular, priority ]
end
```

在视图中我们将创建选择控件来显示列表。没有高层包装器同时创建 <select> 标签并填充一组分组选项，也没有表单构建器 helper，因此我们必须使用（名字惊人地）option_groups_from_collection_for_select 方法。它接受组集合、用于查找组和项目的访问器名称，以及模型中的当前值。

我们将其放在为模型和属性命名的 <select> 标签内：

```
Download e1/views/app/views/test/select.html.erb
<label for="order_shipping_option">Shipping: </label>
<select name="order[shipping_option]" id="order_shipping_option">
<%= 
  option_groups_from_collection_for_select(Shipping::OPTIONS,
    :options, :type_name,  # <- groups
    :id, :name,            # <- items
    @order.shipping_option)
%>
</select>
```

最后，一些高层 helper 使为国家和时区创建选择列表变得容易。详情请参阅 Rails API 文档。

##### 日期和时间字段

```
form.date_select(:attribute, options)
form.datetime_select(:attribute, options)

select_date(date = Date.today, options)
select_day(date, options)
select_month(date, options)
select_year(date, options)

select_datetime(time = Time.now, options)
select_hour(time, options)
select_minute(time, options)
select_second(time, options)
select_time(time, options)
```

有两组日期选择小部件。第一组 date_select 和 datetime_select 用于 Active Record 模型的日期和日期时间属性。第二组 select_xxx 变体在没有 Active Record 支持的情况下也适用。

我们可以在这里看到一些这些方法的使用：

```
form.date_select(:created_on, :order => [:day, :month, :year])
```

```
form.datetime_select(:created_on, :discard_minute => true, :start_year => 1990)
```

```
select_datetime(Time.now, :include_blank => true, :add_month_numbers => 1)
```

```
select_year(2015, :prefix => "year", :discard_type => true)
```

select_xxx 小部件默认使用 date/xxx 作为名称，因此在控制器中你可以将分钟选择作为 params[:date][:minute] 访问。你可以使用 :prefix 选项更改前缀，并使用 :discard_type 选项禁用在方括号中添加字段类型。:include_blank 选项在列表中添加一个空选项。

select_minute 方法支持 :minute_step => nn 选项。将其设置为 15，例如，将只列出选项 0、15、30 和 45。

select_month 方法通常列出月份名称。要同时显示月份数字，请将选项 :add_month_numbers => true 设置为 true。要仅显示数字，请将 :use_month_numbers => true 设置为 true。

select_year 方法默认列出从当前年份前五年到后五年的年份。这可以使用 :start_year => yyyy 和 :end_year => yyyy 选项更改。

date_select 和 datetime_select 创建小部件，允许用户使用选择列表在 Active Record 模型中设置日期（或日期时间）。@variable.attribute 中存储的日期用作默认值。显示包括年份、月份、日期（以及小时、分钟、秒）的单独选择列表。可以通过设置选项 :discard_month => 1、:discard_day => 1 等来从显示中移除特定字段的选择列表。只需要一个 discard 选项——所有较低级别的单位都会自动移除。date_select 的字段显示顺序可以使用 :order => ( symbols... ) 选项设置，其中符号为 :year、:month 和 :day。此外，还支持所有来自 select_xxx 小部件的选项。

##### 标签

```
form.label(:object, :method, 'text', options)
```

返回一个标签标签，用于为分配给模板的对象（由 :object 标识）上的指定属性（由 :method 标识）标记输入字段。标签的文本默认为属性名，除非你指定


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

##### 错误处理和模型对象

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

##### 包含集合的表单

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

#### 23.7 使用非模型字段

到目前为止，我们一直专注于 Rails 中模型、控制器和视图之间的集成。但 Rails 也提供了创建没有对应模型的字段的支持。这些辅助方法记录在 FormTagHelper 中，它们都接受一个简单的字段名称，而不是模型对象和属性。当表单提交到控制器时，字段的内容将以该名称存储在 params 哈希中。这些非模型辅助方法的名字都以 _tag 结尾。

我们需要创建一个表单来使用这些字段辅助方法。到目前为止我们一直在使用 form_for 来实现这一点，但这假设我们在围绕模型对象构建表单，而这在使用低级辅助方法时不一定是这种情况。

我们本可以把 <form> 标签硬编码到我们的 HTML 中，但 Rails 有更好的方法：使用 form_tag 辅助方法创建一个表单。就像 form_for 一样，form_tag 应该


出现在 `<%..%>` 序列中，并且应接受一个包含表单内容的块：⁷

```
<% form_tag :action => 'save', :id => @product do %>
  Quantity: <%= text_field_tag :quantity, '0' %>
<% end %>
```

`form_tag` 的第一个参数是一个哈希，用于标识表单提交时要调用的动作。此哈希接受与 `url_for` 相同的选项（参见第437页）。可选的第二个参数是另一个哈希，用于设置 HTML form 标签本身的属性。（注意：如果 Ruby 方法的参数列表包含两个字面哈希，则必须用括号括起来。）

```
<% form_tag({ :action => :save }, { :class => "compact" }) do ...%>
```

我们可以用一个简单的计算器来说明非模型表单。它提示我们输入两个数字，让我们选择一个运算符，并显示结果。

![](img/a160fc3a330a0b3b2a764d41d614e688_541_0.png)

`app/views/test` 目录下的 `calculate.html.erb` 文件使用 `text_field_tag` 显示两个数字字段，并使用 `select_tag` 显示运算符列表。注意，我们必须使用 `params` 哈希中的当前值来初始化所有三个字段的默认值。我们还需要显示在处理控制器中的表单数据时发现的任何错误列表，并显示计算结果。

```
Download e1/views/app/views/test/calculate.html.erb
<% unless @errors.blank? %>
<ul>
  <% for error in @errors %>
    <li><p><%= h(error) %></p></li>
  <% end %>
</ul>
<% end %>

<% form_tag(:action => :calculate) do %>
  <%= text_field_tag(:arg1, params[:arg1], :size => 3) %>
  <%= select_tag(:operator,
    options_for_select(%w{ + - * / },
    params[:operator])) %>
  <%= text_field_tag(:arg2, params[:arg2], :size => 3) %>
<% end %>
<strong><%= @result %></strong>
```

7. 这是 Rails 1.2 中的一个更改。

如果没有错误检查，控制器代码将非常简单：

```
def calculate
  if request.post?
    @result = Float(params[:arg1]).send(params[:operator], params[:arg2])
  end
end
```

然而，在没有错误检查的情况下运行网页是我们承担不起的奢侈，所以我们必须使用更长的版本：

```
Download e1/views/app/controllers/test_controller.rb

def calculate
  if request.post?
    @errors = []
    arg1 = convert_float(:arg1)
    arg2 = convert_float(:arg2)
    op = convert_operator(:operator)

    if @errors.empty?
      begin
        @result = op.call(arg1, arg2)
      rescue Exception => err
        @result = err.message
      end
    end
  end
end

private

def convert_float(name)
  if params[name].blank?
    @errors << "#{name} missing"
  else
    begin
      Float(params[name])
    rescue Exception => err
      @errors << "#{name}: #{err.message}"
      nil
    end
  end
end

def convert_operator(name)
  case params[name]
  when "+" then proc {|a,b| a+b}
  when "-" then proc {|a,b| a-b}
  when "*" then proc {|a,b| a*b}
  when "/" then proc {|a,b| a/b}
  else
    @errors << "Missing or invalid operator"
    nil
  end
end
```

有趣的是，如果我们使用 Rails 模型对象，这段代码大部分都会消失，因为很多这种内务处理已经内置了。

##### 旧式 form_tag

在 Rails 1.2 之前，`form_tag` 不接受块。相反，它将 `<form>` 元素生成为字符串。你可以像这样调用它：

```
<%= form_tag :action => :save %>
... form contents ...
<%= end_form_tag %>
```

在 Rails 1.2 中你仍然可以这样使用 `form_tag`，但这种用法是不被认可的，除非你有充分理由避开块形式。（而且很难找到一个块形式无法处理的现实需求——也许是一个表单在一个文件中开始、在另一个文件中结束的模板？）

为了让这一点深入人心，Rails 已经弃用了 `end_form_tag` 辅助方法。你现在不得不这样做：

```
<%= form_tag :action => :save %>
... form contents ...
</form>
```

这种丑陋的写法应该会让你停下来思考……

#### 23.8 向 Rails 应用程序上传文件

您的应用程序可能允许用户上传文件。例如，一个缺陷报告系统可以让用户将日志文件和代码样例附加到问题单上，或者一个博客应用程序可以让用户上传一张小图片，显示在他们的文章旁边。

在 HTTP 中，文件以 multipart/form-data POST 消息的形式上传。顾名思义，这种类型的消息由表单生成。在该表单中，您将使用一个或多个 `<input>` 标签，其 `type="file"`。当浏览器渲染此标签时，用户可以通过名称选择文件。随后提交表单时，文件会与其余表单数据一起发送回服务器。

为了说明文件上传过程，我们将展示一些代码，允许用户上传图片并将该图片与评论一起显示。为此，我们首先需要一个 `pictures` 表来存储数据：

```
Download e1/views/db/migrate/003_create_pictures.rb

class CreatePictures < ActiveRecord::Migration
  def self.up
    create_table :pictures do |t|
      t.string :comment
      t.string :name
```

```
def uploaded_picture=(picture_field)
  self.name        = base_part_of(picture_field.original_filename)
  self.content_type = picture_field.content_type.chomp
  self.data        = picture_field.read
end

def base_part_of(file_name)
  File.basename(file_name).gsub(/[^\w._-]/, '')
end
end
```

我们定义一个名为 `uploaded_picture=` 的访问器来接收表单上传的文件。表单返回的对象是一个有趣的混合体。它类似于文件，因此我们可以使用 `read` 方法读取其内容；这样我们就能将图片数据存入 `data` 列。它还具有 `content_type` 和 `original_filename` 属性，让我们获取上传文件的元数据。所有这些拆分工作都由我们的访问器方法执行：一个对象以独立的属性存储在数据库中。

请注意，我们还添加了一个简单的验证，以检查内容类型是否为 `image/xxx` 形式。我们不希望有人上传 JavaScript。

控制器中的 `save` 动作完全符合常规：

```
def save
  @picture = Picture.new(params[:picture])
  if @picture.save
    redirect_to(:action => 'show', :id => @picture.id)
  else
    render(:action => :get)
  end
end
```

那么，现在数据库中有了图片，我们如何显示它呢？一种方法是给它一个自己的 URL，然后只需在图片标签中链接到该 URL。例如，我们可以使用像 `upload/picture/123` 这样的 URL 来返回图片 123 的图片。这将使用 `send_data` 将图片返回给浏览器。注意我们如何设置内容类型和文件名——这能让浏览器解释数据，并在用户选择保存图片时提供一个默认名称：

```
def picture
  @picture = Picture.find(params[:id])
  send_data(@picture.data,
            :filename => @picture.name,
            :type => @picture.content_type,
            :disposition => "inline")
end
```

在布局中可用（因为常规模板在布局被调用之前渲染）。这可以用来参数化布局中的标题或菜单。例如，布局可能包含以下内容：

```
<html>
  <head>
    <title><%= @title %></title>
    <%= stylesheet_link_tag 'scaffold' %>
  </head>
  <body>
    <h1><%= @title %></h1>
    <%= yield :layout %>
  </body>
</html>
```

各个模板可以通过赋值给 `@title` 变量来设置标题：

```
<% @title = "My Wonderful Life" %>
<p>
  Dear Diary:
</p>
<p>
  Yesterday I had pizza for dinner. It was nice.
</p>
```

事实上，我们可以更进一步。允许我们使用 `yield :layout` 将模板渲染嵌入布局的同一机制，也允许您在模板中生成任意内容，然后这些内容可以被嵌入到任何其他模板中。

例如，不同的模板可能需要向标准页面侧边栏添加各自模板特定的项目。我们将在这些模板中使用 `content_for` 机制来定义内容，然后在布局中使用 `yield` 将此内容嵌入侧边栏。

在每个常规模板中，使用 `content_for` 为块内渲染的内容命名。此内容将存储在 Rails 内部，并且不会对模板生成的输出产生贡献。

```
<h1>Regular Template</h1>

<% content_for(:sidebar) do %>
  <ul>
    <li>this text will be rendered</li>
    <li>and saved for later</li>
    <li>it may contain <%= "dynamic" %> stuff</li>
  </ul>
<% end %>

<p>
  Here's the regular stuff that will appear on
  the page rendered by this template.
</p>
```


其他模板使用 render(:partial=>) 方法来调用它：

```
<%= render(:partial => "article", :object => @an_article) %>
<h3>Add Comment</h3>
. . .
```

render 的 :partial 参数是需要渲染的模板名称（但不带前导下划线）。该名称必须同时是有效的文件名和有效的 Ruby 标识符（因此 a-b 和 20042501 不是 partial 的有效名称）。:object 参数标识要传递给 partial 的对象。该对象在模板内将通过与模板同名的局部变量访问。在此示例中，@an_article 对象将被传递给模板，并且模板可以使用局部变量 article 访问它。这就是为什么我们可以在 partial 中写诸如 article.title 之类的内容。

惯用的 Rails 开发者会使用与模板同名的变量（本例中为 article）。事实上，通常会更进一步。如果要传递给 partial 的对象在控制器实例变量中，并且该实例变量的名称与 partial 相同，则可以省略 :object 参数。如果在前面的示例中，我们的控制器已在实例变量 @article 中设置了 article，那么视图就可以仅使用以下方式渲染 partial：

```
<%= render(:partial => "article") %>
<h3>Add Comment</h3>
. . .
```

你可以通过向 render 传递 :locals 参数来在模板中设置额外的局部变量。它接受一个哈希，其中条目表示要设置的局部变量的名称和值。

```
render(:partial => 'article',
    :object => @an_article,
    :locals => { :authorized_by => session[:user_name],
                  :from_ip       => request.remote_ip })
```

#### Partials and Collections

应用程序通常需要显示格式化的条目集合。博客可能会显示一系列文章，每篇都有文本、作者、日期等。商店可能会显示目录中的条目，每个条目都有图像、描述和价格。

render 的 :collection 参数可以与 :partial 参数结合使用。:partial 参数让我们使用 partial 来定义单个条目的格式，而 :collection 参数将此模板应用于集合中的每个成员。要使用我们之前定义的 _article.html.erb partial 显示 article 模型对象的列表，我们可以这样写：

```
<%= render(:partial => "article", :collection => @article_list) %>
```

在 partial 内部，局部变量 article 将被设置为集合中当前 article——变量名取自模板。此外，变量 article_counter 将被设置为集合中当前 article 的索引。

可选的 :spacer_template 参数让你指定一个将在集合中各元素之间渲染的模板。例如，视图可能包含以下内容：

```
Download e1/views/app/views/partial/list.html.erb

<%= render(:partial => "animal",
    :collection => %w{ ant bee cat dog elk },
    :spacer_template => "spacer") %>
```

这使用 _animal.html.erb 渲染给定列表中的每个动物，并在每个之间渲染 partial _spacer.html.erb。如果 _animal.html.erb 包含以下内容：

```
Download e1/views/app/views/partial/_animal.html.erb

<p>The animal is <%= animal %></p>
```

而 _spacer.html.erb 包含以下内容：

```
Download e1/views/app/views/partial/_spacer.html.erb

<hr />
```

你的用户将看到动物名称的列表，每个之间有一条线。

#### Shared Templates

如果 render 调用的第一个选项或 :partial 参数是一个简单名称，Rails 假定目标模板位于当前控制器的视图目录中。然而，如果名称包含一个或多个 / 字符，Rails 假定直到最后一个斜杠的部分是目录名，其余部分是模板名。目录假定在 app/views 下。这使得在控制器之间共享 partial 和子模板变得容易。

Rails 应用程序之间的惯例是将这些共享 partial 存储在 app/views 的一个子目录中，称为 shared。它们可以使用如下方式渲染：

```
<%= render("shared/header", :title => @article.title) %>
<%= render(:partial => "shared/post", :object => @article) %>
. . .
```

在此前面的示例中，@article 对象将被分配给模板中的局部变量 post。

这是我们的模拟 Article 类。它模拟了一个在正常情况下会从数据库获取文章的模型类。我们安排了列表中的第一篇文章显示其创建的时间。

```
Download e1/views/app/models/article.rb
class Article
  attr_reader :body

  def initialize(body)
    @body = body
  end

  def self.find_recent
    [ new("It is now #{Time.now.to_s}"),
      new("Today I had pizza"),
      new("Yesterday I watched Spongebob")
      new("Did nothing on Saturday") ]
  end
end
```

现在我们想设置一个使用已缓存的渲染文章版本的模板，但仍更新动态数据。事实证明这很简单。

```
Download e1/views/app/views/blog/list.html.erb
<%= @dynamic_content %>    <!-- Here's dynamic content. -->

<% cache do %>            <!-- Here's the content we cache -->
  <ul>
    <% for article in Article.find_recent -%>
      <li><p><%= h(article.body) %></p></li>
    <% end -%>
  </ul>
<% end %>                 <!-- End of cached content -->

<%= @dynamic_content %>   <!-- More dynamic content. -->
```

魔力在于 cache 方法。与此方法关联的块中生成的所有输出都将被缓存。下次访问此页面时，动态内容仍将被渲染，但块内的内容将直接来自缓存——不会重新生成。我们可以在几秒后刷新骨架应用程序后看到这一点，如下一页图 23.4 所示。页面顶部和底部的時間——我们数据的动态部分——在刷新时发生变化。然而，中间部分的时间保持不变，因为它是从缓存中提供服务的。（如果你在家尝试并且看到三个时间字符串都发生了变化，很可能你在开发模式下运行应用程序。缓存默认仅在生产模式下启用。如果你使用 WEBrick 进行测试，-e production 选项即可。）

```
Download e1/views/app/views/blog1/list.html.erb

<%= @dynamic_content %> <!-- Here's dynamic content. -->

<% cache do %>        <!-- Here's the content we cache -->
  <ul>
    <% for article in @articles -%>
      <li><p><%= h(article.body) %></p></li>
    <% end -%>
  </ul>
<% end %>
        <!-- End of the cached content -->

<%= @dynamic_content %> <!-- More dynamic content. -->
```

#### Expiring Cached Fragments

现在我们有了文章列表的缓存版本，我们的 Rails 应用程序将能够在每次引用此页面时提供它。然而，如果文章被更新，缓存版本将过时并且应该过期。我们使用 expire_fragment 方法来做到这一点。默认情况下，片段使用渲染页面的控制器和操作名称进行缓存（我们第一种情况中的 blog 和 list）。要使片段过期（例如，当文章列表发生变化时），控制器可以调用以下内容：

```
Download e1/views/app/controllers/blog_controller.rb

expire_fragment(:controller => 'blog', :action => 'list')
```

显然，这种命名方案仅在页面上只有一个片段时才有效。幸运的是，如果你需要更多，可以通过向 cache 方法添加参数（使用 url_for 约定）来覆盖与片段关联的名称：

```
Download e1/views/app/views/blog2/list.html.erb

<% cache(:action => 'list', :part => 'articles') do %>
  <ul>
    <% for article in @articles -%>
      <li><p><%= h(article.body) %></p></li>
    <% end -%>
  </ul>
<% end %>

<% cache(:action => 'list', :part => 'counts') do %>
  <p>
    There are a total of <%= @article_count %> articles.
  </p>
<% end %>
```

在此示例中，缓存了两个片段。第一个保存时额外的 :part 参数设置为 articles，第二个保存时设置为 counts。




现在我们需要注册处理器。这可以放在你的环境文件中，或者你可以在 app/controllers 目录下的 application.rb 中设置它。

Download e1/views/app/controllers/application.rb

```
require "rdoc_template"
```

```
ActionView::Template.register_template_handler("rdoc", RDocTemplate)
```

注册调用表示任何以 .rdoc 结尾的模板文件都将由 RDocTemplate 类处理。我们可以通过创建一个名为 example.rdoc 的模板并通过一个新生成的测试控制器访问它来测试这一点：

![](img/a160fc3a330a0b3b2a764d41d614e688_560_0.png)

#### Making Dynamic Templates

html.erb 和 xml.builder 模板与控制器共享其环境：它们可以访问控制器实例变量。它们也可以在作为 partials 调用时传入局部变量。我们可以赋予自己的模板同样的权限。你实现这一点的方式取决于你希望模板做什么。这里我们构造一个相当人为的东西：一个 reval 模板，其中包含 Ruby 代码行。渲染时，每一行都会显示出来，并附带其值。以下代码展示了一个名为 test.reval 的模板：

```
a = 1
3 + a
@request.path
```

这可能会产生以下输出：

```
a = 1 => 1
3 + a => 4
@request.path => /text/example1
```

注意模板如何访问 @request 变量。我们通过创建一个 Ruby binding（基本上是变量值的范围）并用控制器设置到视图中的实例变量和局部变量的值来填充它来实现这种魔术。请注意渲染器还将响应内容类型设置为 text/plain；我们不希望我们的结果被解释为 HTML。我们可以

本章由 Justin Gehtland（http://relevancellc.com）撰写，他是一名软件开发者、演讲者和作家，居住在北卡罗来纳州达勒姆市。他是 Streamlined 项目的创始人，该项目用于 Rails 上的高级 CRUD 应用（http://streamlinedframework.org）。它基于他和 Relevance 的 Stuart Halloway 为 RailsConf '06 所写的作品。

### Chapter 24

### The Web, v2.0

我们已经了解了 Action View 如何用于将模板渲染到浏览器。我们已经看到了如何通过布局和 partials 的组合创建页面；大多数情况下，我们的操作都是向浏览器返回整个页面并强制浏览器刷新当前屏幕。这是 Web 的一个核心基础原则：对服务器的请求返回整个页面，浏览器必须完整显示。这章是关于打破 Web 的这一核心原则，并允许你的应用程序处理更小的粒度单元，在浏览器和服务器之间传输数据、部分页面和代码，以提供更具响应性和交互性的用户体验。

Rails 的 Ajax 支持可以分为三个主要领域：

- Prototype 支持 DOM 交互和远程对象调用
- Script.aculo.us 支持视觉效果
- RJS 模板用于以代码为中心的 Ajax

对于前两者，我们必须记住我们学到的关于 helpers 的所有内容，因为几乎所有对 Prototype 和 Script.aculo.us 的支持都可以在 ActionView::Helpers::PrototypeHelper 和 ActionView::Helpers::ScriptaculousHelper 中找到。RJS 模板则完全是另一种生物，结合了一点 Action View 模板和一种全新的调用 render 的方式。

#### 24.1 Prototype

Prototype，由 Sam Stephenson 编写的开源 JavaScript 框架，主要用于简化 JavaScript 中的两个任务：

- 使用 XMLHttpRequest（及其朋友）进行 Ajax 调用
- 与页面 DOM 交互

Ajax 是在浏览器背后进行操作。浏览器只是受训的猴子：发出请求，重新加载页面；提交表单，重新加载页面。如果你

```
<% for user in @users %>
<tr>
<td><%=h user.username %></td>
<td><%=h user.favorite_language %></td>
<td><%= link_to 'Show', :action => 'show', :id => user %></td>
<td><%= link_to 'Edit', :action => 'edit', :id => user %></td>
<td><%= link_to 'Destroy', { :action => 'destroy', :id => user },
:confirm => 'Are you sure?', :method => :post %></td>
</tr>
<% end %>
</table>

<%= link_to 'Previous page',
{ :page => @users.previous_page } if @users.previous_page %>
<%= link_to 'Next page',
{ :page => @users.next_page } if @users.next_page %>

<br />

<%= link_to 'New user', :action => 'new' %>
```

我们希望允许用户通过在文本字段中输入来过滤当前列表。应用程序应监视字段的变化，将字段的值提交到服务器，并更新列表以仅显示与当前过滤条件匹配的程序员。

与非 Ajax 页面一样，第一步是添加一个表单来收集用户的输入。然而，与标准表单不同，我们将添加一个所谓的 no-op 表单；这是一个本身无法提交到服务器的表单。旧的做法是创建一个 action 属性设置为 # 的表单。这可以防止请求发布到服务器，但它有一个不幸的副作用，即在地址栏中通过在 URL 末尾添加 # 字符来破坏 URL。现代的方法是将 action 设置为 javascript:void(0)：

```
<% form_tag('javascript:void(0)') do %>
```

其次，我们需要用一个命名元素包装渲染的 partial，以便我们可以轻松地用更新后的数据替换它。在我们的例子中，我们添加一个简单的 <div> 标签，id='ajaxWrapper'，以便为新数据提供一个位置：

```
<div id='ajaxWrapper'>
<%= render :partial=>'search' %>
</div>
```

如果返回的数据很复杂，你也可以选择注册一个回调函数来按你希望的方式处理数据。在我们的例子中，服务器将返回一个包含匹配过滤条件的用户的表格，我们只想将该数据显示在名为 ajaxWrapper 的元素内部。

在第 4 行和第 5 行，我们克服了 Ajax 的主要问题之一。用户可能很敏感。如果他们点击链接或提交表单，或者其他什么，唯一阻止他们无意识地疯狂点击链接或按钮的东西就是浏览器窗口东北角的喷火蜥蜴或旋转地球仪。这告诉用户正在发生有用的事情，请等待其完成。这是在每个浏览器中内置的功能，用户期望这种对否则透明过程的通知。

使用 XHR 时，你必须提供自己的进度指示器。before 选项在向服务器发送请求之前调用一个 JavaScript 函数。在这种情况下，我们使用 Prototype 的 Element.show 来显示一个图形，该图形已在初始化时加载到页面上（但其 style 属性设置为 display:none）。complete 回调同样在响应完全接收后触发。在这种情况下，我们再次使用 Element.hide 隐藏进度指示器。还有其他潜在的回调函数钩子，我们将在第 24.1 节 Callbacks，第 572 页中讨论。（这个 spinner 在哪里？我们一会儿就会看到。）

最后，在第 6 行和第 7 行，我们定义 Ajax 调用将针对的服务器端点以及要发送给它的数据。在第 6 行，我们指定 url 参数并告诉它调用当前控制器的 search action。发送到 url 的选项与 url_for helper 方法相同。

在第 7 行，我们使用 with 参数提供了将发送到服务器的数据。此参数的值是一个包含一个或多个名称/值对的字符串。仔细查看提供的字符串文字：

```
"search=' + encodeURIComponent(value)"
```

该字符串是一段可执行的 JavaScript 代码，将在目标字段的值发生变化时运行。encodeURIComponent 是一个 JavaScript 方法，它接受一个值并用其 UTF-8 对应字符转义某些字符，以使其成为有效的 URL 组件。在这种情况下，value 将是目标字段的当前值，结果是一个名称/值对，其中名称为 search，值为目标字段值的 UTF-8 编码值。

还记得我们用作进度指示器的 spinner 吗？我们还没有编写显示它的代码。通常你会直接将其放在包含引用它的字段的页面上。事实证明，在我们的示例代码中，我们会在各处使用它，所以与其在每个页面上都包含它，我们将改为将其一次添加到布局中。





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

##### conditions_by_like

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

##### Using Prototype Helpers

Rails 提供了一整套 Prototype 辅助方法，为你的应用程序提供各种各样的 Ajax 解决方案。它们都需要你在页面中包含 prototype.js 文件。Rails 自带了该文件的一个版本，你可以使用 javascript_include_tag 辅助方法将其包含在页面中：

```
<%= javascript_include_tag "prototype" %>
```

许多应用程序将 Prototype 包含在默认布局中；如果你在整个应用程序中大量使用 Ajax，这是有意义的。如果你更关心带宽限制，你可能会选择更谨慎地仅在需要时包含它。如果你遵循标准的 Rails 生成器风格，你的 application.html.erb 文件将包含以下声明：

```
<%= javascript_include_tag :defaults %>
```

这将包含 Prototype、Script.aculo.us 以及用于应用程序特定 JavaScript 的生成的 application.js 文件。在任何一种情况下，一旦页面包含 Prototype，你就可以使用各种 Prototype 辅助方法向页面添加 Ajax。

##### Common Options

在我们检查不同的辅助方法及其用途之前，让我们花一点时间了解我们可以传递给许多辅助方法的一些常见选项。由于大多数辅助方法最终会使用 XHR 向服务器发出调用，因此它们共享大量用于控制调用方式以及在调用前后做什么的选项。

##### Synchronicity

大多数时候，你希望 Ajax 调用是异步的。这意味着用户可以继续与页面交互，而页面中的 JavaScript 在请求传输和处理期间可以继续执行操作。有时，你可能会发现需要同步 Ajax 调用（尽管我们强烈不建议这样做）。如果是这样，你可以传递 :type 选项，它有两个可能的值：:asynchronous（默认值）和 :synchronous：

```
<%= link_to_remote "Wait for it...",
    :url => {:action => 'synchronous_action'},
    :update => 'results_div',
    :type => :synchronous %>
```

##### Updating the Page

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

##### periodically_call_remote

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




##### link_to_function

虽然从严格意义上讲，link_to_function 并不是一个 Prototype helper，但它来自标准 Rails helper 库，是一个常用的支持 Ajax 的 helper。它允许你提供链接文本，以及点击链接时要执行的一段 JavaScript 代码。它不接受我们前面提到的那些花哨选项；相反，你可以传入更标准的 link_to helper 所接受的任何 HTML 选项。

link_to_function 允许你创建任意链接来调用客户端函数。不过，JavaScript 不必仅限于客户端活动。你也可以提供一段调用 XHR 的 JavaScript 代码。这个 helper（以及它的同类 button_to_function）用于创建比普通 Prototype helpers 和选项所能表达的更为定制的交互模型。

例如，你可能正在使用 Sébastien Gruhier 编写的优秀 Prototype Window Class 框架（http://prototype-window.xilinus.com/）。这个框架构建在 Prototype 和 Script.aculo.us 之上，允许你在应用程序内创建纯 JavaScript 窗口。你可能想创建一个链接，启动一个 Prototype 窗口来显示应用程序的“关于”信息：

```
<%= link_to_function "About...",
  "Dialog.alert({url: 'about.html', options: {method: 'get'}},
  {windowParameters: {className: 'default'}, 
okLabel: 'Close'});" %>
```

##### remote_function

事实证明，前面描述的 Prototype helpers 实际上都使用另一个 Prototype helper——remote_function——来生成 XHR 调用。如果你想在链接和周期性执行器之外的其他上下文中嵌入 XHR 调用，你也可以自己使用这个 helper。

假设你的用户已经检查了收件箱的状态，并想查看消息。标准界面可能是显示消息主题列表，然后允许用户选择一条来查看。但是，你知道你的用户习惯了胖客户端邮件界面，标准交互方式是双击电子邮件主题来查看消息。你想提供同样的功能，但需要向服务器发起 XHR 调用来获取特定的电子邮件。这个示例是你可能用来渲染列表的局部视图：

```
<table>
  <% for email in @emails %>
  <tr ondblclick="<%= remote_function(:update => 'email_body',
                                    :url => {:action => 'get_email',
                                    :id => email}) %>">
    <td><%= email.id %></td><td><%= email.body %></td>
  </tr>
  <% end %>
</table>
<div id="email_body"></div>
```

```
<div id="email_form">
  <% form_remote_tag(:url => {:action => 'send_email'},
    :update => 'email_form') do %>
    To: <%= text_field 'email', 'to' %><br/>
    From: <%= text_field 'email', 'from' %><br/>
    Body: <%= text_area 'email', 'body' %><br/>
    <%= submit_tag 'Send Email' %>
  <% end %>
</div>
```

以下是生成的页面：

```
<div id="email_form">
  <form action="/user/send_email" method="post"
    onsubmit="new Ajax.Updater('email_form',
      '/user/send_email',
      {asynchronous:true, evalScripts:true,
      parameters:form.serialize(this)});
      return false;">
    To: <input id="email_to" name="email[to]" size="30" type="text" /><br/>
    From: <input id="email_from" name="email[from]" size="30" type="text" /><br/>
    Body: <textarea cols="40" id="email_body" name="email[body]" rows="20"></textarea><br/>
    <input name="commit" type="submit" value="Send Email" />
  </form>
</div>
```

注意，onsubmit 的值实际上是两条 JavaScript 命令。第一条创建 Ajax.Updater，发送 XHR 请求并用响应更新页面。第二条让处理程序返回 false。这正是防止表单通过非 Ajax POST 提交的机制。如果没有这个返回值，表单会同时通过 Ajax 调用和常规 POST 提交，这将导致收件人收到两封完全相同的电子邮件；如果邮件正文是“请从我的账户中扣除 1000.00 美元”，那可能会造成灾难性后果。

helper remote_form_for 的工作方式与 form_remote_tag 完全相同，只是它允许你使用更新的 form_for 语法来定义表单元素。你可以在第 524 页的 23.5 节“包装模型对象的表单”中了解更多关于这种替代语法的信息。

##### submit_to_remote

最后，你可能会面对一个已经生成的表单，出于种种原因，你无法将其修改为远程表单。也许是其他部门或团队负责该代码，你没有权限更改它；又或者你完全无法将 JavaScript 绑定到 onsubmit 事件。在这些情况下，替代策略是向表单添加一个 submit_to_remote。

这个 helper 会在表单内创建一个按钮，点击时会序列化表单数据，并将其 POST 到通过 helper 选项指定的目标。它不会影响包含它的表单，也不会干扰任何 <submit>。

但是等等，还记得 UserController.send_email 做什么吗？它返回一段局部 HTML 片段，只包含与该特定电子邮件关联的状态消息。该片段被设计为注入当前页面，替换表单本身。如果表单通过非 Ajax 方法 POST，浏览器将被迫把状态消息作为整个页面渲染。真糟糕。

于是，另一只靴子落地了：你不仅需要在客户端制定降级策略，还需要在服务器端制定降级策略。你可以采用两种方法：让 Ajax 和非 Ajax 调用使用相同的操作，或者将 Ajax 调用发送到专门为它们构建的第二组操作。无论选择哪种方式，你都需要一条路径返回用于注入页面的局部 HTML 片段，以及第二条路径在完整页面的上下文中返回局部 HTML 片段，这样浏览器才有合理的内容可供渲染。

##### 降级到不同的 URL

如果选择降级到不同的 URL，你必须为操作提供两组端点。使用 form_remote_tag 时，这非常容易：

```
<% form_remote_tag({:url => {:action => 'send_email'}, :update => 'email_form',
:html => {:action => url_for({:action => 'send_email_no_ajax'})} } do %>
...
```

该调用会生成以下 HTML：

```
<form action="/user/send_email_no_ajax" method="post"
onsubmit="new Ajax.Updater('email_form', '/user/send_email',
{asynchronous:true, evalScripts:true,
parameters:Form.serialize(this)});
return false;"
>
```

如果启用了 JavaScript，onsubmit 代码就会被执行，将序列化后的表单数据发送到 /user/send_email，并取消表单正常的 POST 提交。如果禁用了 JavaScript，表单将改为 POST 到 /user/send_email_no_ajax。前者会使用 render :partial 只返回所需的 HTML 片段。后者会渲染完整的 .html.erb 模板，包括布局。

降级到不同的 URL 可能是个好办法，因为这可以让你的服务器端操作非常干净：每个操作只渲染一个模板，而且你可以针对 Ajax 和非 Ajax 方法创建不同的访问规则或过滤策略。缺点是最终可能会产生大量重复代码（两个发送电子邮件的不同方法）或大量杂乱代码（两个方法都调用一个 helper 方法发送电子邮件，除此之外只是垫片）。

```
after_filter :gzip_compress, :only => [:send_email_no_ajax]

def send_email
  actually_send_email params[:email]
  render :text => 'Email sent.'
end

def send_email_no_ajax
  actually_send_email params[:email]
  flash[:notice] = 'Email sent.'
  render :template => 'list_emails'
end

private

def actually_send_email(email)
  # send the email
end
```

##### 降级到相同的 URL

或者，你可以将调用降级到相同的 URL。这样做时，必须有某个数据伴随请求，以区分 Ajax 调用和非 Ajax 调用。有了这个数据，你的控制器就可以在渲染局部视图、渲染整个布局或完全做其他事情之间做出决定。目前还没有行业标准的方法。Prototype 提供了一个 Rails 直接集成使用的解决方案。每当你使用 Prototype 发起 XHR 请求时，Prototype 都会在请求中嵌入一个专有的 HTTP 头。

```
HTTP_X_REQUESTED_WITH=XMLHttpRequest
```

Rails 在入站请求头中查找这个值，并根据其是否存在来设置 Rails 请求对象上的 xhr? 方法¹ 的返回值。当请求头存在时，该调用返回 true。有了这个工具，你就可以根据请求类型来决定如何渲染内容：

```
def send_email
  actually_send_email params[:email]
  if request.xhr?
    render :text => 'Email sent.'
  else
    flash[:notice] = 'Email sent.'
    render :template => 'list_emails'
  end
end
```

1. 对于那些非常想了解其内部机制的人：如果请求的 X-Requested-With 头包含 XMLHttpRequest，则此方法返回 true。Prototype JavaScript 库会在每个 Ajax 请求中发送这个头。





![](img/a160fc3a330a0b3b2a764d41d614e688_586_0.png)

## Figure 24.3: Choosing the first item

Autocomplete is just another server-side callback. As we've learned already, it is important to notify your users when these asynchronous calls are being made on their behalf. You can use the :indicator option to specify the DOM id of a graphic to toggle on at the start of the call and toggle off upon completion:

```
<%= text_field :user, :language %>
<img id='language_spinner' src='spinner.gif' style='display:none;' />
<div class="auto_complete" id="user_language_auto_complete"></div>
<%= auto_complete_field :user_language,
    :indicator => 'language_spinner' %>
```

If the user needs to enter more than one value per autocompleting text field, you can specify one or more tokens that can be used to reset the behavior as they type. For example, we could allow the user to choose multiple favorite languages for the programmer by using a comma to separate the values:

```
<%= text_field :user, :languages %>
<div class="auto_complete" id="user_languages_auto_complete"></div>
<%= auto_complete_field :user_languages,
    :tokens => ',' %>
```

As the user starts to enter a value, they'll get the list of choices, as shown in Figure 24.3. Then, if they make a selection and type in one of the tokens (in this case, a comma), the list will show again, and they can pick a second item, as shown in Figure 24.4, on the next page.

Finally, you can specify a JavaScript expression to be called when the target <div> is either shown or hidden (:on_show, :on_hide) or after the text field has been updated by the user's selection (:after_update_element). These callbacks allow you to specify other visual effects or even server-side actions in response to the user's interaction with the autocomplete field.

On the server, you will want to write an action that can turn a partial value into a list of potential matches and return them as an HTML snippet containing

## Todo list for anders gosling

### Pending

- Find Waldo

### Completed

- Compose a Symphony
- Solve NP-Complete problem
- Run a marathon

Figure 24.5: Drag-and-drop to-do lists

It is worth highlighting that there is no JavaScript to enable the arrow-up, arrow-down, highlight behavior of the list. It is enough to provide the stylesheet shown previously; all <ul> tags support that behavior (in relatively modern browsers) and just need styles to show off the changing state.

##### Drag-and-Drop and Sortable Elements

The point of all this Ajax and Web 2.0 stuff is to make your web applications more interactive—to make them more like desktop applications. There may be no more impressive example of this than drag-and-drop behavior.

There are two distinct styles of drag-and-drop behavior: moving items around within a list (sorting) and moving items around between lists (categorizing). In either case, you want to be able to specify three types of actors:

- The original container list
- The target container list (when sorting, it will be the same as the original)
- The elements that can be dragged

Additionally, you will need to specify the following behaviors:

- What to do when an item is dragged
- What to do when an item is dropped
- What information to send to the server upon completion

Let's look at dragging and dropping between lists to start with, and then we can see how much simpler sorting operations are. In this example, we'll manage the to-do list for a programmer. There are two categories of to-do items: pending and completed. We want to be able to drag items between the two lists and update the server whenever an item is moved.

```
<%= drop_receiving_element('completed_todos',
    :accept     => 'pending_todo',
    :complete   => "$('spinner').hide();",
    :before     => "$('spinner').show();",
    :hoverclass => 'hover',
    :with       => "'todo=' + encodeURIComponent(element.id.split('_').last())",
    :url        => {:action=>:todo_completed, :id=>@user})%>
```

This helper defines a target DOM element to receive dropped items and further defines the application behavior based on those events. In addition to the id of the target, the following options are available:

- `:accept` => string — The CSS class of the items that can be dropped on this container
- `:before` => snippet — A JavaScript snippet to execute prior to firing the server-side call
- `:complete` => snippet — A JavaScript snippet to execute just after completing the XHR call
- `:hoverclass` => string — Applies this CSS class to the drop target whenever a candidate item is hovering over it
- `:with` => snippet — A JavaScript snippet that executes to create the query string parameters to send to the server
- `:url` => url — Either the literal URL of the server endpoint or an url_for construct
- `:update` => string — The DOM element to update as a result of the XHR call (in our example, we're using RJS to update the page, which we will see in Section 24.3, RJS Templates, on page 600)

In general, the Script.aculo.us helpers take all the same options as the Prototype helpers, since the former is built on top of the latter.

In our example, we specified that the pending_todos container accepts only completed_todo items, and vice versa. That's because the purpose of the drag-and-drop behavior is to recategorize the items. We want to fire the XHR request to the server only if an item is moved to the other category, not if it is returned to its original location. By specifying the revert attribute on the individual draggable items, they will snap to their original locations if dropped somewhere other than a configured receiving target, and no extra round-trip to the server will be caused.

We're also constructing our query string by parsing out the draggable item's database id from its DOM id. Look at that JavaScript snippet:

```
"'todo=' + encodeURIComponent(element.id.split('_').last())"
```

The with parameter takes a snippet and feeds it the actual DOM element that was dropped as a variable called element. In our partial, we defined the ids of those elements as todo_database id, so when we want to send the server information on which item was dropped, we split the todo back off and send only the database id.

We've also defined a simple style for the drop targets and draggable elements:

```
<style>
.hover {
  background-color: #888888;
}
#pending_todos ul li, #completed_todos ul li {
  list-style: none;
  cursor: -moz-grab;
}
#pending_todos, #completed_todos {
  border: 1px solid gray;
}
</style>
```

The hover class causes the drop target to highlight when a draggable item is poised on top of it. The second rule specifies that any <li> elements within the pending_todos or completed_todos will use the -moz-grab cursor, the grasping hand icon, in order to provide a visual cue to the user that the item has a special property (draggability). The last rule just draws a border around our drop targets to make them obvious.

What if you wanted to create a sortable list instead of two or more categories of items? Sorting usually involves a single list whose order you want sent back to the server whenever it is changed. To create one, you need only to be able to create an HTML list and then specify what to do when the order changes. The helper takes care of the rest.

```
<ul id="priority_todos">
  <% for todo in @todos %>
  <li id="todo_<%= todo.id %>"><%= todo.name %></li>
  <% end %>
</ul>
<%= sortable_element 'priority_todos',
  :url => {:action => 'sort_todos'} %>
```

The sortable_element helper can take any of the standard Prototype options for controlling what happens before, during and after the XHR call to the server.

In many cases, there isn't anything to do in the browser since the list is already in order. Here is the output of the previous code:

```
<ul id="priority_todos">
    <li id="todo_421">Climb Baldwin Auditorium</li>
    <li id="todo_359">Find Waldo</li>
</ul>
<script type="text/javascript">
//<![CDATA[
Sortable.create("priority_todos", {onUpdate:function(){
    new Ajax.Request('/user/sort_todos',
        {asynchronous:true, evalScripts:true,
        parameters:Sortable.serialize("priority_todos")})}})
//]]>
</script>
```

Script.aculo.us provides a helper JavaScript method called Sortable.serialize. It takes a list and creates a JSON dump of the ids of its contained elements in their current order, which is sent back to the server. Here are the parameters the action receives on re-order:

```
Processing UserController#sort_todos (for 127.0.0.1 at 2006-09-15 07:32:16) [POST]
Session ID: 00dd9070b55b89aa8ca7c0507030139d
Parameters: {"action"=>"sort_todos", "controller"=>"user", "priority_todos"=>["359", "421"]}
```

Notice that the priority_todos parameter contains an array of database ids, not the DOM ids from the list (which were formatted as todo_421, not 421). The Sortable.serialize helper automatically uses the underscore as a delimiter to parse out the actual database id, leaving you less work to do on the server. There is a problem with this behavior, however. The default is to eliminate everything before and including the first underscore character in the DOM id. If your DOM is formatted as priority_todo_database id, then the serializer will send "priority_todos"=>["todo_359", "todo_421"] to the server. To override that, you have to provide the format option to the helper, which is just one of many sortable-specific options. In addition, you can pass any of the options that we have seen previously.

- `:format` => regexp — A regular expression to determine what to send as the serialized id to the server (the default is `/^[^_]*_(.*)$/`).
- `:constraint` => value — Whether to constrain the dragging to either `:horizontal` or `:vertical` (or `false` to make it unconstrained).
- `:overlap` => value — Calculates the item overlap in the `:horizontal` or `:vertical` direction.
- `:tag` => string — Determines which children of the container element to treat as sortable (default is `LI`).





:containment => target
接受一个元素或元素数组作为潜在的放置目标（默认为原始目标元素）。

:only => string
用于过滤子元素作为候选者的 CSS 类名或类名数组。

:scroll => boolean
如果列表在拖拽操作中超出可视边界，则确定是否滚动列表。

:tree => boolean
确定是否将嵌套列表视为主可排序列表的一部分。这意味着你可以创建多层列表，并在同一层级对项目进行排序，也可以跨层级拖拽和排序项目。

例如，如果你的列表使用类似 priority_todo_database_id 的 DOM id，并且其中包含无法排序的项目，你的声明可能如下所示：

```
<%= sortable_element 'priority_todos',
  :url => {:action => 'sort_todos'},
  :only => 'sortable',
  :format => '/^priority_todo_(.*)$/' %>
```

##### In-place Editing

原位编辑是在你不想为页面上的每个小数据片段创建完整编辑屏幕时的便利功能。有时，屏幕上只有一两个项目需要可编辑；与其将它们渲染为丑陋且破坏样式的输入字段，你可以将其渲染为样式化文本，但为用户提供一种快速将其切换为可编辑版本然后在编辑完成后切换回来的方式。

从 Rails 2.0 开始，此功能从核心迁移到插件。到现在为止，你应该已经熟悉流程了：

```
script/plugin install git://github.com/rails/in_place_editing.git
```

Script.aculo.us 为视图和控制器都提供了辅助方法，以帮助创建原位编辑器。我们先来看一下页面应该如何表现。以下是使用原位字段的用户的编辑页面，处于正常模式：

Username: anders gosling

Favorite language: Rails

Edit | Back

用户将鼠标悬停在姓名字段上，得到该字段可编辑的提示：

Username: anders gosling
Favorite language: [Click to edit]
Edit | Back

而当姓名字段处于完全编辑模式时，页面如下所示：

Username: anders gosling ok cancel
Favorite language: Rails
Edit | Back

如果你使用默认设置，创建起来非常简单。在控制器中，指定你希望控制器支持原位编辑的模型类名和列名：

```
class UserController < ApplicationController
  in_place_edit_for :user, :username
  in_place_edit_for :user, :favorite_language
  # ...
```

这些辅助方法实际上会在你的控制器中创建名为 set_user_username 和 set_user_favorite_language 的方法，表单将与之交互以更新字段数据。这些生成的方法会使用新数据更新当前模型实例并返回新保存的值。

使用 in_place_editor_field 辅助方法创建控件。在我们的示例中，我们只需遍历模型上的所有列并为每个列创建一个：

Download pragforms/app/views/user/inplace_demo.html.erb

```
<% for column in User.user_columns %>
<p>
  <b><%= column.human_name %>:</b>
  <%= in_place_editor_field "user", column.name, {}, {
    :load_text_url=> url_for(:action=>"get_user_#{column.name}", :id=>@user)
  } %>
</p>
<% end %>

<%= link_to 'Edit', :action => 'edit', :id => @user %> |
<%= link_to 'Back', :action => 'list' %>
```

这就是创建默认版本所需的一切。你可以指定大量选项来更改默认行为。

此外，在空白值的情况下，你可能希望在用户进入编辑模式时在编辑器字段中提供某种默认文本。要提供该文本，你必须创建一个服务器端操作，编辑器可以调用它来请求字段的值，然后在 load_text_url 选项中提供该值。以下是创建自己的辅助方法、类似于 in_place_edit_for 以提供默认值示例：

```
class UserController < ApplicationController
  def self.in_place_loader_for(object, attribute, options = {})
    define_method("get_#{object}_#{attribute}") do
      @item = object.to_s.camelize.constantize.find(params[:id])
      render :text => @item.send(attribute) || "[No Name]"
    end
  end
end
in_place_edit_for    :user, :username
in_place_loader_for :user, :username
in_place_edit_for   :user, :favorite_language
in_place_loader_for :user, :favorite_language
```

在视图中，你只需传递适当的选项：

```
<% for column in User.user_columns %>
<p>
  <input type="button" id="edit_<%= column.name %>" value="edit"/>
  <b><%= column.human_name %>:</b>
  <%= in_place_editor_field "user", column.name, {},
      {:external_control => "edit_#{column.name}",
       :load_text_url=> url_for(:action=>"get_user_#{column.name}",
                               :id=>@user) } %>
</p>
<% end %>
```

它看起来像这样：

![](img/a160fc3a330a0b3b2a764d41d614e688_597_0.png)

请注意，编辑器字段在文本字段中显示了 [No Name]，因为没有从数据库检索到值。此外，你可以看到原位编辑器会在编辑模式下隐藏外部按钮控件。

##### Visual Effects

Script.aculo.us 还提供了大量可应用于 DOM 元素的视觉效果。效果大致可分为显示元素的效果、隐藏元素的效果和突出显示元素的效果。方便的是，它们大多共享相同的可选参数，并且可以串行或并行组合以创建更复杂的效果。

Script.aculo.us 辅助方法 visual_effect 生成等效的 JavaScript。它主要用于将值分配给标准 Prototype 辅助方法的生命周期回调之一（complete、success、failure 等）。

要获取所有可用效果的完整列表，请访问 http://script.aculo.us。与其做详尽的参考，我们将从实践中看一些应用。

回想一下拖放示例。假设你还想在元素更新后突出显示放置目标。我们已经绑定到 complete 回调以关闭进度指示器：

```
<%= drop_receiving_element('pending_todos', :accept=>'completed_todo',
    :complete=>"$('spinner').hide();",
    :before=>"$('spinner').show();",
    :hoverclass=>'hover',
    :with=>"'todo=' + encodeURIComponent(element.id.split('_').last())",
    :url=>{:action=>:todo_pending, :id=>@user})%>
```

要添加视觉高亮效果，我们只需将其附加到 complete 选项：

```
<%= drop_receiving_element('pending_todos', :accept=>'completed_todo',
    :complete=>"$('spinner').hide();" + 
                visual_effect(:highlight, 'pending_todos'),
    :before=>"$('spinner').show();",
    :hoverclass=>'hover',
    :with=>"'todo=' + encodeURIComponent(element.id.split('_').last())",
    :url=>{:action=>:todo_pending, :id=>@user})%>
```

我们还可以使用 appear/disappear 效果使进度指示器淡入淡出：

```
<%= drop_receiving_element('pending_todos', :accept=>'completed_todo',
    :complete=>visual_effect(:fade, 'spinner', :duration => 0.5),
    :before=>visual_effect(:appear, 'spinner', :duration => 0.5),
    :hoverclass=>'hover',
    :with=>"'todo=' + encodeURIComponent(element.id.split('_').last())",
    :url=>{:action=>:todo_pending, :id=>@user})%>
```

三种视觉效果允许我们将它们指定为切换效果。这些是可逆的效果对，允许我们显示/隐藏元素。如果我们指定切换效果，生成的 JavaScript 将负责在状态之间交替。可用切换器如下：

- :toggle_appear   使用 appear 和 fade 切换
- :toggle_slide    使用 slide_down 和 slide_up 切换
- :toggle_blind    使用 blind_down 和 blind_up 切换

你几乎可以在任何可以提供 JavaScript 片段的地方使用 visual_effect 辅助方法。

#### 24.3 RJS Templates

到目前为止，我们几乎完全从服务器在 XHR 调用期间返回 HTML 的角度来介绍 Prototype 和 Script.aculo.us。此 HTML 几乎总是用于更新某个 DOM 元素的 innerHTML 属性以更改页面的状态。事实证明，还有另一种强大的技术，你可以用它来解决否则需要在客户端使用大量复杂 JavaScript 的问题：你的 XHR 调用可以返回在浏览器中执行的 JavaScript。

事实上，这种模式在 2005 年变得如此普遍，以至于 Rails 团队想出了在服务器上以与使用 .html.erb 文件处理 HTML 输出相同的方式对其进行规范化的方法。这种技术被称为 RJS 模板。随着人们开始使用 RJS 模板，他们意识到他们希望在控制器内联拥有模板提供的相同能力。因此诞生了 render :update 构造。

什么是 RJS 模板？它只是一个存储在 app/views 层次结构中的文件，扩展名为 .js.rjs。它包含发出 JavaScript 以供浏览器执行的命令。模板本身的解析方式与 .html.erb 模板相同。当收到操作请求时，分派器会尝试查找匹配的 .html.erb 模板。如果请求来自 XHR，分派器会优先查找 .js.rjs 模板。模板被解析，JavaScript 被生成并返回到浏览器，在那里最终执行。

RJS 模板可用于在多个页面之间提供标准交互行为，或最小化嵌入在给定页面上的自定义 JavaScript 代码量。RJS 的主要使用模式之一是导致单个操作的结果在客户端产生多个效果。

让我们重新审视之前的拖放示例。当用户从一个列表拖动待办项目到另一个列表时，该项目的 id 会发送到服务器。服务器必须通过将其从原始列表中移除并添加到新列表中来重新分类该特定项目。这意味着服务器必须随后更新视图上的两个列表。然而，服务器只能对给定的请求返回一个响应。

这意味着你可以执行以下操作：

- 构建页面，使两个放置目标都包含在更大的元素中，并在更新时更新该父元素的全部内容。
- 返回结构化数据给复杂的客户端 JavaScript 函数，该函数解析数据并将其分配给两个放置目标。





The call to page.sortable also takes the id of the element to make sortable, followed by all of the possible options to the original sortable_element helper.

Here is the resulting response from the server as passed back across to the browser (reformatted slightly to make it fit):

```
try {
Element.update("pending_todos", "<ul id='pending_todo_list'>
<li class=\"pending_todo\" id='todo_38'>Build a house</li>
<script type=\"text/javascript\">\n//<![CDATA[\nnew Draggable(\"todo_38\",
{ghosting:true, revert:true})\n//]]>\n</script>
<li class=\"pending_todo\" id='todo_39'>Read the Hugo Award Winners</li>
<script type=\"text/javascript\">\n//<![CDATA[\nnew Draggable(\"todo_39\",
{ghosting:true, revert:true})\n//]]></script>\n  </ul>\n");
Sortable.create(\"pending_todo_list\",
{onUpdate:function(){new Ajax.Request(\"/user/sort_pending_todos/10\",
{asynchronous:true, evalScripts:true,
parameters:Sortable.serialize(\"pending_todo_list\")})}});
} catch (e) { alert(e.message); }
]]>
```

The response is pure JavaScript; the Prototype helper methods on the client must be set to execute JavaScripts, or nothing will happen on the client. It updates the drop targets with new HTML, which was rendered back on the server into string format. It then creates the new sortable element on top of the pending to-dos. The code is wrapped in a try/catch block. If something goes wrong on the client, a JavaScript alert box will pop up and attempt to describe the problem.

If you don't like the inline style of render :update, you can use the original version, an .js.rjs template. If you switch to the template style, the action code would reduce to this:

```
def update_todo_completed_date(newval)
@user = User.find(params[:id])
@todo = @user.todos.find(params[:todo])
@todo.completed = newval
@todo.save!
@completed_todos = @user.completed_todos
@pending_todos = @user.pending_todos
end
```

Then, add a file called todo_completed.js.rjs in app/views/user/ that contains this:

```
page.replace_html 'pending_todos', :partial => 'pending_todos'
page.replace_html 'completed_todos', :partial => 'completed_todos'
page.sortable "pending_todo_list",
:url=>{:action=>:sort_pending_todos, :id=>@user}
```

Rails will autodiscover the file, create an instance of JavaScriptGenerator called page, and pass it in. The results will be rendered back to the client, just as with the inline version.

On the server, you would store the to-do item and then add the new value into the existing list at the bottom:

```
def add_todo
  todo = Todo.new(params[:todo])
  if todo.save
    render :update do |page|
      page.insert_html :bottom, 'todo_list', "<li>#{todo.name}</li>"
    end
  end
end
```

##### Showing/Hiding Data

You'll often need to toggle the visibility of DOM elements after the completion of an XHR call. Showing and hiding progress indicators are a good example; toggling between an Edit button and a Save button is another. We can use three methods to handle these states: show, hide, and toggle. Each takes a single id or an array of ids to modify.

For example, when using Ajax calls instead of standard HTML requests, the standard Rails pattern of assigning a value to flash[:notice] doesn't do anything because the code to display the flash is executed only the first time the page is rendered. Instead, you can use RJS to show and hide the notification:

```
def add_todo
  todo = Todo.new(params[:todo])
  if todo.save
    render :update do |page|
      page.insert_html :bottom, 'todo_list',
        "<li>#{todo.name}</li>"
      page.replace_html 'flash_notice', "Todo added: #{todo.name}"
      page.show 'flash_notice'
    end
  end
end
```

Alternatively, you can choose to delete an element from the page entirely by calling remove. Successful execution of remove means that the node or nodes specified will be removed from the page entirely. This does not mean just hidden; the element is removed from the DOM and cannot be retrieved.

Here's an example of our to-do list again, but now the individual items have an id and a Delete button. Delete will make an XHR call to remove the item from the database, and the controller will respond by issuing a call to delete the individual list item:

```
<ul id="todo_list">
  <% for item in @todos %>
    <li id='todo_<%= item.id %>'>
      <%= item.name %>
      <%= link_to_remote 'Delete',
          :url => {:action => 'delete_todo',
```
##### Script.aculo.us Helpers

In addition to all the Prototype and raw JavaScript helpers, RJS also provides support for most of the functions of Script.aculo.us. By far the most common is the visual_effect method. This is a straightforward wrapper around the different visual effects supplied by Script.aculo.us. You pass in the name of the visual effect desired, the DOM id of the element to perform the effect on, and a hash containing the standard effect options.

In this example, we add a pulsate effect to the flash notice after we show it and then fade it away to remove it:

```
def add_todo
  todo = Todo.new(params[:todo])
  if todo.save
    render :update do |page|
      page.insert_html :bottom, 'todo_list',
        "<li>#{todo.name}</li>"
      page.replace_html 'flash_notice', "Todo added: #{todo.name}"
      page.show 'flash_notice'
      page.visual_effect :pulsate, 'flash_notice'
      page.delay(3) do
        page.replace_html 'flash_notice', ''
        page.visual_effect :fade, 'flash_notice'
      end
    end
  end
end
```

You can also manipulate the sort and drag-and-drop characteristics of items on your page. To create a sortable list, use the sortable method, and pass in the id of the list to be sortable and a hash of all the options you need. draggable creates an element that can be moved, and drop_receiving creates a drop target element.

#### 24.4 Conclusion

Ajax is all about making web applications feel more like interactive client applications and less like a physics white paper. It is about breaking the hegemony of the page and replacing it with the glorious new era of data. That data doesn’t have to stream back and forth on the wire as XML (no matter what Jesse James Garrett said back in February 2005). It just means that users get to interact with their data in appropriate-sized chunks, not in the arbitrary notion of a page.

Rails does a great job of integrating Ajax into the regular development flow. It is no harder to make an Ajax link than a regular one, thanks to the wonders of the helpers. What is hard, and will remain hard for a very long time, is making Ajax work efficiently and safely. So although it is great to be able to rely on the Rails helpers to hide the bulk of the JavaScript from you, it is also great to know what is actually being done on your behalf.

And remember: use Ajax to benefit your users! Your motto should be the same as a doctor's: first, do no harm. Use Ajax where it makes your users' lives better, not where it just confuses them or makes it harder to get things done. Follow that simple rule, and Ajax on Rails can be wonderful.

The :sendmail setting delegates mail delivery to your local system's sendmail program, which is assumed to be in /usr/sbin. This delivery mechanism is not particularly portable, because sendmail is not always installed in this directory on different operating systems. It also relies on your local sendmail supporting the -i and -t command options.

You achieve more portability by leaving this option at its default value of :smtp. If you do so, though, you'll need also to specify some additional configuration to tell Action Mailer where to find an SMTP server to handle your outgoing e-mail. This may be the machine running your web application, or it may be a separate box (perhaps at your ISP if you're running Rails in a noncorporate environment). Your system administrator will be able to give you the settings for these parameters. You may also be able to determine them from your own mail client's configuration.

```
config.action_mailer.smtp_settings = {
  :address      => "domain.of.smtp.host.net",
  :port         => 25,
  :domain       => "domain.of.sender.net",
  :authentication => :login,
  :user_name    => "dave",
  :password     => "secret"
}
```

- :address => and :port =>

  Determines the address and port of the SMTP server you'll be using. These default to localhost and 25, respectively.

- :domain =>

  The domain that the mailer should use when identifying itself to the server. This is called the HELO domain (because HELO is the command the client sends to the server to initiate a connection). You should normally use the top-level domain name of the machine sending the e-mail, but this depends on the settings of your SMTP server (some don't check, and some check to try to reduce spam and so-called open-relay issues).

- :authentication =>

  One of :plain, :login, or :cram_md5. Your server administrator will help choose the right option.¹ This parameter should be omitted if your server does not require authentication. If you do omit this parameter, also omit (or comment out) the :user_name and :password options.

- :user_name => and :password =>

  Required if :authentication is set.

Other configuration options apply to all delivery mechanisms.

> 1. TLS (SSL) support requires Ruby 1.8.7. If you are running Ruby 1.8.6, consider installing Marc Chung's Action Mailer TLS plug-in (script/plugin install http://code.openrain.com/rails/action_mailer_tls).





```
config.action_mailer.perform_deliveries = true | false
```

如果 perform_deliveries 为 true（默认值），邮件将正常投递。如果为 false，投递邮件的请求将被静默忽略。这在测试时可能有助于禁用电子邮件。

```
config.action_mailer.raise_delivery_errors = true | false
```

如果 raise_delivery_errors 为 true（默认值），则在最初发送电子邮件时发生的任何错误都会向你的应用程序抛出一个异常。如果为 false，错误将被忽略。请记住，并非所有电子邮件错误都是立即发生的——一封邮件可能在发送三天后被退回，而你（希望）到那时应用已经继续处理其他事情了。

使用以下设置用于新电子邮件的字符集：

```
config.action_mailer.default_charset = "utf-8"
```

与所有配置更改一样，如果你对环境文件做了任何更改，都需要重新启动你的应用程序。

### 发送邮件

既然我们已经完成了所有配置，让我们编写一些代码来发送电子邮件。

到目前为止，你不应对 Rails 有一个生成邮件器的脚本感到惊讶。可能令人惊讶的是它创建它们的位置。在 Rails 中，邮件器是存储在 app/models 目录中的一个类。它包含一个或多个方法，每个方法对应一个电子邮件模板。为了创建电子邮件的正文，这些方法反过来使用视图（就像控制器操作使用视图来创建 HTML 和 XML 一样）。因此，让我们为我们的商店应用创建一个邮件器。我们将用它来发送两种不同类型的电子邮件：一种是在订单下达时，另一种是在订单发货时。generate mailer 脚本接受邮件器类的名称，以及电子邮件操作方法的名称：

```
depot> ruby script/generate mailer OrderMailer confirm sent
exists  app/models/
exists  app/views/order_mailer
exists  test/unit/
create  test/fixtures/order_mailer
create  app/models/order_mailer.rb
create  test/unit/order_mailer_test.rb
create  app/views/order_mailer/confirm.erb
create  test/fixtures/order_mailer/confirm
create  app/views/order_mailer/sent.erb
create  test/fixtures/order_mailer/sent
```

注意，我们在 app/models 中创建了一个 OrderMailer 类，并在 app/views/order_mailer 中创建了两个模板文件，每种邮件类型一个。（我们还创建了一个

当指定了 headers ‘return-path’ 时，该值将用作“信封发件人”地址。当你希望将投递通知发送到与 from 中不同的地址时，设置此值非常有用。

```
headers "Organization" => "Pragmatic Programmers, LLC"
```

recipients 数组或字符串
一个或多个收件人电子邮件地址。这些可以是简单的地址，如 dave@pragprog.com，也可以是某个标识短语后跟尖括号中的电子邮件地址。

```
recipients [ "andy@pragprog.com", "Dave Thomas <dave@pragprog.com>" ]
```

reply_to 数组或字符串
在回复你的邮件时，这些地址将被列为默认收件人。设置电子邮件的 Reply-To: 头。

sent_on 时间
一个 Time 对象，用于设置电子邮件的 Date: 头。如果未指定，将使用当前日期和时间。

subject 字符串
电子邮件的主题行。

body 接受一个哈希，用于向包含电子邮件的模板传递值。我们很快将了解它是如何工作的。

#### 邮件模板

generate 脚本在 app/views/order_mailer 中创建了两个电子邮件模板，分别对应 OrderMailer 类中的每个操作。这些是常规的 .erb 文件。我们将用它们来创建纯文本电子邮件（稍后我们会看到如何创建 HTML 电子邮件）。与我们用来创建应用网页的模板一样，这些文件包含静态文本和动态内容的组合。我们可以自定义 confirm.erb 中的模板；这是用于确认订单的电子邮件：

```
Download e1/mailer/app/views/order_mailer/confirm.erb
```

```
Dear <%= @order.name %>

Thank you for your recent order from The Pragmatic Store.

You ordered the following items:

<%= render(:partial => "/line_item", :collection => @order.line_items) %>

We'll send you a separate e-mail when your order ships.
```

这个模板中有一个小问题。我们必须为 render 提供模板的显式路径（开头的 ./），因为我们不是从真正的控制器调用视图，Rails 无法猜测默认位置。

create_confirm 调用会调用我们的 confirm 实例方法来设置电子邮件的详细信息。我们的模板用于生成正文文本。正文和头信息一起被添加到一个新的电子邮件对象中，create_confirm 会返回该对象。该对象是 TMail::Mail 类的一个实例。² email.encoded 调用返回我们刚刚创建的电子邮件的文本。我们的浏览器将显示类似下面的内容：

```
Date: Thu, 12 Oct 2006 12:17:36 -0500
From: orders@pragprog.com
To: dave@pragprog.com
Subject: Pragmatic Store Order Confirmation
Mime-Version: 1.0
Content-Type: text/plain; charset=utf-8

Dear Dave Thomas

Thank you for your recent order from The Pragmatic Store.

You ordered the following items:

1 x Programming Ruby, 2nd Edition
1 x Pragmatic Project Automation

We'll send you a separate e-mail when your order ships.
```

如果我们想发送电子邮件，而不是仅仅创建一个电子邮件对象，我们可以调用 OrderMailer.deliver_confirm(order)。

##### 发送 HTML 格式的电子邮件

创建 HTML 电子邮件的一种方法是创建一个为电子邮件正文生成 HTML 的模板，然后在投递消息之前将 TMail::Mail 对象的内容类型设置为 text/html。

我们将从在 OrderMailer 中实现 sent 方法开始。（实际上，这个方法与最初的 confirm 方法之间有太多共同之处，以至于我们很可能会将两者重构为使用一个共享的辅助方法。）

```
Download e1/mailer/app/models/order_mailer.rb

class OrderMailer < ActionMailer::Base
  def sent(order)
    subject    'Pragmatic Order Shipped'
    recipients order.email
    from       'orders@pragprog.com'
    sent_on    Time.now

    body       :order => order
  end
end
```

2. TMail 是 Minero Aoki 编写的优秀电子邮件库；Rails 附带了一个版本。

接下来，我们将编写 sent.erb 模板：

```
Download e1/mailer/app/views/order_mailer/sent.erb
<h3>Pragmatic Order Shipped</h3>
<p>
This is just to let you know that we've shipped your recent order:
</p>
<table>
<tr><th colspan="2">Qty</th><th>Description</th></tr>
<%= render(:partial => "html_line_item", :collection => @order.line_items) %>
</table>
```

我们将需要一个生成表格行的新局部模板。该模板放在文件 _html_line_item.erb 中：

```
Download e1/mailer/app/views/order_mailer/_html_line_item.erb
<tr>
<td><%= html_line_item.quantity %></td>
<td>&times;</td>
<td><%= html_line_item.product.title %></td>
</tr>
```

最后，我们将使用一个操作方法对其进行测试，该方法渲染电子邮件，将内容类型设置为 text/html，并调用邮件器来投递它：

```
Download e1/mailer/app/controllers/test_controller.rb
class TestController < ApplicationController
  def ship_order
    order = Order.find_by_name("Dave Thomas")
    email = OrderMailer.create_sent(order)
    email.set_content_type("text/html")
    OrderMailer.deliver(email)
    render(:text => "Thank you...")
  end
end
```

生成的电子邮件将类似于下一页的图 25.1。

##### 发送多种内容类型

有些人更喜欢接收纯文本格式的电子邮件，而另一些人则喜欢 HTML 电子邮件的外观。Rails 允许你轻松发送包含备用内容格式的电子邮件消息，允许用户（或其电子邮件客户端）决定他们更愿意查看哪种格式。

在上一节中，我们通过生成 HTML 内容然后将内容类型设置为 text/html 来创建 HTML 电子邮件。事实证明，Rails 有一个约定可以自动完成这一切，甚至更多。

![](img/a160fc3a330a0b3b2a764d41d614e688_616_0.png)

## 图 25.1：一封 HTML 格式的电子邮件

我们的 sent 操作的视图文件被称为 sent.erb。这是标准的 Rails 命名约定。但是，对于电子邮件模板，还有更多的命名魔法。如果你像这样命名模板文件：

```
name.content.type.erb
```

那么 Rails 将自动将电子邮件的内容类型设置为文件名中的内容类型。对于之前的示例，我们可以将视图文件名设置为 sent.html.erb，Rails 会自动将其作为 HTML 电子邮件发送。但还有更多。如果你创建多个同名但文件名中嵌入不同内容类型的模板，Rails 将在一封邮件中发送所有模板，并安排内容，以便电子邮件客户端能够区分每个模板。因此，通过创建 sent.text.plain.erb 和 sent.text.html.erb 模板，我们可以让用户选择以文本或 HTML 格式查看电子邮件。

让我们试试这个。我们将设置一个新的操作：

```
Download e1/mailer/app/controllers/test_controller.rb

def survey
  order = Order.find_by_name("Dave Thomas")
  email = OrderMailer.deliver_survey(order)
  render(:text => "E-Mail sent")
end
```





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

#### 25.2 接收电子邮件

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

#### 25.3 测试电子邮件

电子邮件测试有两个层次。在单元测试层面，你可以验证 Action Mailer 类是否正确生成电子邮件。在功能层面，你可以测试应用是否在你期望发送电子邮件时发送这些电子邮件。

##### 单元测试电子邮件

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

##### 电子邮件的功能测试

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




### 第26章
### Active Resources

前面几章主要关注服务器与人类之间的通信，大多通过 HTML 进行。但并非所有 Web 交互都需要直接涉及人类。本章聚焦于程序到程序之间的协议。

在编写应用程序时，你很可能会遇到这样的情况：并非所有数据都整齐地存放在数据库中并分好了类。这些数据可能不在数据库里，甚至根本不在你的机器上。这就是 Web 服务的意义所在。Active Resource 是 Rails 对 Web 服务的一种实现方案。请注意，这里说的是小写字母 w 和小写字母 s 的 web services，而不是 SOAP、WSDL 和 UDDI 中所指的大写 Web Services。由于这容易造成混淆，在开始之前，我们需要区分这两者，以及其他解决客户端连接远程模型（也就是业务对象；或者在 Rails 中，它们被称为 ActiveRecords）这一基本问题的方法。

#### 26.1 Active Resource 的替代方案

确实，从这个角度开始讨论并不寻常。但既然其他人无疑会提倡不同的方法来解决这个问题，我们选择直面这一讨论，首先简要概述一些替代技术，并说明在什么情况下应该使用它们而不是 Active Resource。没错，是“应该”，因为一种方案并不适用于所有情况。

此外，许多使用 Rails 进行部署的人并不需要本章描述的任何方法，而许多需要的人会选择 Active Resource 之外的替代方案。这完全正常且合适。但如果你发现自己正面临 Active Resource 恰好是手头任务的正确工具的情况，你很可能会觉得它简单而令人愉快，甚至还有几分神奇。

##### XML

许多人认为 XML 是在 Web 上构建程序到程序协议的默认选择。如果使用得当，它实际上可以自我描述、人类可读，并且天然可扩展。但与其他任何事情一样，并非所有人都能正确使用它。

XML 最适合用于文档，尤其是包含标记和/或持久化到磁盘的文档。如果文档主要包含标记，可以考虑使用 XHTML（甚至 HTML，尽管有些人认为后者更难通过程序解析）。

虽然没有严格的限制，但通过 Web 交换的 XML 文档的大小通常从几十 KB 到数百 MB 不等。

将 XML 用作程序到程序协议的最佳方法如下：首先就 XML 应有的样子达成一致，用文字描述或模式（schema）将其记录下来，然后进而编写生成或消费 XML 的代码，最好使用 REXML（或 libxml2）和 Builder。使用 XPath 提取数据是保持客户端和服务器松散耦合的绝佳方式。

ActiveRecord 提供的 to_xml 方法在这种情况下通常没有帮助，因为它在数据布局方式上做了太多假设。

最佳实践是通过统一资源标识符（即 URI；通常也称为统一资源定位符，即 URL）来标识每个文档，然后通过 HTTP 的 GET、POST、PUT 和 DELETE 方法为这些数据提供统一接口。

Atom 发布协议（RFC 5023）就是这种方法的一个例子。这类方法能够很好地扩展到互联网规模的运作。

##### JSON

近年来 JSON 越来越受欢迎，有些人将其视为对 XML 的反驳。只有在有人宣扬 XML 是一刀切策略的情况下才如此，而事实上并没有这样的人。

JSON 最适合用于数据，特别是那些已经以哈希、数组、字符串、整数等形式存在于应用程序内部的数据。JSON 不直接支持日期或小数，但在必要时，String 或 Fixnum 也可以应付。

同样，这里也没有严格的限制，但 JSON 通常可轻松部署在数据量预计从几个字节到几百 KB 的场景中。JSON 往往比 XML 更紧凑，解析速度也更快。有少数（罕见的）语言或平台无法方便地使用 JSON 解析库。虽然这在理论上可能是个问题，但在实践中问题不大。

在撰写本书时，JSON 往往不会被直接存储在磁盘上¹，至少不像 XML 那样经常存储。相反，JSON 的使用往往集中在临时用途上，例如对单个请求的响应。

实际上，JSON 的典型用例是：同一台服务器既提供客户端应用（以 JavaScript 形式），又提供响应客户端请求的服务器实现。在这种设置下，ActiveRecord 的 from_json 和 to_json 方法非常合适。通常，这类设置只依赖两种 HTTP 方法：GET 和 POST。

##### SOAP

理论上，SOAP 就是 XML，只不过标准化了三个元素名称，并定义了一个统一的故障响应。实际上，在 Java 和 C# 中有大量用于消费和生成 SOAP 的支持基础设施，而这些基础设施往往决定了其典型用法。

这种机制针对静态类型语言进行了优化，并且严重依赖模式（schema）。这类机制产生的请求和响应往往比手工编写的 XML 更冗长，也更不便于人类阅读。

请求和响应的大小往往与 XML 差不多，不过 SOAP 中的请求（通常以 XML 文档形式通过 POST 发送，而非使用 HTTP GET）可能会稍微小一些。当以 RPC 风格使用时，参数按名称匹配。

虽然最佳实践是在编写任何代码之前先定义好模式，但在实践中，XML 模式很难通过其他方式正确生成，而那些从运行代码中有选择地暴露内部结构的模式生成器已被证明过于诱人；因此，大多数基于 SOAP 的 Web 服务都是以这种方式定义的。然后从该模式生成客户端存根，这会导致系统变得相当紧密耦合。这对于受控的企业内部网可能合适，但在互联网上则不太适合。

SOAP 表现出色的一个领域是某些安全领域，因为全球最顶尖的一些人才已经为通过替代传输方式进行单向消息传递设计了细节，包括不可否认签名和联合身份。然而，这些扩展是可选的，并非每个平台都可用。

你可以通过 `gem install actionwebservice` 在 Rails 中启用 SOAP 支持。该支持不提供高级功能，例如单向消息传递、替代传输、不可否认签名或联合身份。

1. CouchDB 是一个明显的例外。

##### XML-RPC

XML-RPC 的出现略早于 SOAP 的标准化，它既没有基于模式的工具的优势，也没有其包袱。它通常在脚本语言（一个明显的例外是 JavaScript）中比在静态类型语言中更受欢迎，其使用场景大致与 JSON 相同，只不过它通常部署在服务器不提供客户端应用的地方。

由于 XML-RPC 仅使用 HTTP POST，因此它无法受益于 HTTP GET 的缓存机制。

在 XML-RPC 中，参数值是按位置传递的。如果你想要更松散的耦合方式，可以考虑使用单个结构体而不是多个参数。与 SOAP 类似，Rails 通过 `gem install action-webservice` 提供 XML-RPC 支持。

#### 26.2 给我看代码！

好了，理论讲得够多了，让我们看一些代码。为此，我们将从 Depot 应用上次停下的地方继续，这次通过一个客户端应用远程访问 Depot 应用。而作为客户端，我们将使用 `script/console`。首先，检查并确保 depot 服务器正在运行。然后我们来创建客户端：

```
work> rails depot_client
work> cd depot_client
```

现在，让我们为 Product 模型编写一个存根：

下载 depot_client/app/models/product.rb

```
class Product < ActiveResource::Base
  self.site = 'http://dave:secret@localhost:3000/'
end
```

其实这并没有多少内容。Product 类继承自 ActiveResource::Base 类。类内部只有一个语句，用来标识用户名、密码、主机名和端口号。在实际运行的应用程序中，用户和密码会分开获取，而不会硬编码到模型中，但在目前阶段，我们只是在探讨概念。让我们把这个存根用起来：

```
depot_client> ruby script/console
Loading development environment (Rails 2.2.2)
>> Product.find(:all)
ActiveResource::Redirection: Failed with 302 Moved Temporarily => http://localhost:3000/admin/login
```





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

#### 26.3 关系和集合

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

#### 26.4 整合一切

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

### Chapter 27

### Securing Your Rails Application

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

### Chapter 27

### Securing Your Rails Application

Web 上的应用程序处于持续攻击之下。Rails 应用程序也不例外。

安全性是一个很大的主题——足以写成整本书的主题。我们在仅一章中无法做到公正。在将应用程序放到可怕、险恶的网络上之前，你可能需要做一些研究。关于 Web 安全性的一个很好的阅读起点是开放 Web 应用程序安全项目（OWASP），网址为 http://www.owasp.org/。这是一个志愿者团体，他们整理了与安全相关的“免费、专业质量、开源文档、工具和标准”。一定要查看他们关于 Web 应用程序安全问题的十大列表。如果你遵循一些基本准则，你可以使你的 Rails 应用程序更加安全。

#### 27.1 SQL Injection

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

##### Protecting Against SQL Injection

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

##### Extracting Queries into Model Methods

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

#### 27.2 Creating Records Directly from Form Parameters

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





这段代码假设 before 过滤器已在 `@user` 实例变量中设置了当前用户的信息：

```
def show
  @order = Order.find(params[:id], :conditions => [ "user_id = ?", @user.id])
rescue
  redirect_to :action => "index"
end
```

更好的是，考虑使用新的基于集合的查找方法，它们将结果限制为仅属于该集合的行。例如，如果我们假设 user 模型 has_many :orders，那么 Rails 允许我们将之前的代码写成这样：

```
def show
  id     = params[:id]
  @order = @user.orders.find(id)
rescue
  redirect_to :action => "index"
end
```

此解决方案不仅限于 find 方法。基于表单返回的 id（或 ids）删除或销毁行的操作同样危险。养成使用类似以下方式限制对 delete 和 destroy 的调用的习惯：

```
def destroy
  id     = params[:id]
  @order = @user.orders.find(id).destroy
rescue
  redirect_to :action => "index"
end
```

#### 27.4 不要暴露控制器方法

一个 action 只是控制器中的一个公共方法。这意味着如果不小心，你可能会将本意仅在应用程序内部调用的方法暴露为 action。例如，控制器可能包含以下代码：

```
class OrderController < ApplicationController

  # Invoked from a webform
  def accept_order
    process_payment
    mark_as_paid
  end

  def process_payment
    @order = Order.find(params[:id])
    CardProcessor.charge_for(@order)
  end
```

```
def mark_as_paid
  @order = Order.find(params[:id])
  @order.mark_as_paid
  @order.save
end
end
```

好吧，这不是很好的代码，但它说明了一个问题。显然，accept_order 方法 intended 用于处理来自表单的 POST 请求。开发人员决定通过将其两个职责封装在两个独立的控制器方法 process_payment 和 mark_as_paid 中来对其进行拆分。

不幸的是，开发人员将这两个辅助方法保留为 public 可见。这意味着任何人都可以在其浏览器中输入以下内容：

http://unlucky.company/order/mark_as_paid/123

并且订单 123 将神奇地被标记为已付款，绕过了所有信用卡处理。每天都是 Unlucky Company 的免费赠送日。

基本规则很简单：控制器中唯一的公共方法应该是可以从浏览器调用的 action。

此规则也适用于你添加到 application.rb 中的方法。这是所有控制器类的父类，其公共方法也可以作为 action 调用。

#### 27.5 跨站脚本攻击 (CSS/XSS)

许多 Web 应用程序使用 session cookie 来跟踪用户的请求。cookie 用于识别请求并将其连接到 session 数据（Rails 中的 session）。通常此 session 数据包含当前登录用户的引用。

跨站脚本是一种“窃取”网站另一位访客的 cookie 的技术，从而可能窃取该人的登录信息。

cookie 协议具有少量内置安全功能；浏览器仅向 cookie 最初创建的域发送 cookie。但这种安全性可以被绕过。获取他人 cookie 的最简单方法是向网站放置一段精心制作的 JavaScript 代码；脚本可以读取访客的 cookie 并将其发送给攻击者（例如，通过将数据作为 URL 参数传输到另一个网站）。

##### 典型的攻击

任何显示来自应用程序外部的数据的站点，除非应用程序注意过滤该数据，否则都容易受到 XSS 攻击。有时攻击的路径很复杂且微妙。例如，考虑一个允许用户为

#### 27.6 避免 Session Fixation 攻击

如果你知道某人的 session id，那么你就可以创建使用它的 HTTP 请求。当 Rails 收到这些请求时，它认为它们与原始用户相关联，因此会让你做该用户能做的任何事情。

Rails 在很大程度上防止人们猜测他人的 session id，因为它使用安全哈希函数构造这些 id。实际上，它们是非常大的随机数。然而，仍有办法实现几乎相同的效果。

在 session fixation 攻击中，坏人从我们的应用程序获取一个有效的 session id，然后以这样的方式将其传递给第三方，即第三方将使用相同的 session。如果该人使用该 session 登录我们的应用程序，坏人也会登录，因为他也有访问该 session id 的权限。⁴

有几种技术有助于消除 session fixation 攻击。首先，你可能会发现将创建 session 的请求的 IP 地址保存在 session 数据中很有帮助。如果此地址发生变化，你可以取消该 session。这将惩罚在网络间移动笔记本电脑的用户以及在 PPPOE 租约到期时 IP 地址发生变化的家庭用户。

其次，你应该考虑每次有人登录时通过 reset_session 创建一个新 session。这样，合法用户将继续使用应用程序，而坏人将被留下一个孤立的 session id。

#### 27.7 文件上传

一些面向社区的网站允许其参与者上传文件供其他参与者下载。除非你小心，否则这些上传的文件可能会被用来攻击你的站点。

例如，想象有人上传一个文件名以 .rhtml 或 .cgi 结尾的文件（或与站点上可执行内容关联的任何其他扩展名）。如果你在下载页面直接链接到这些文件，当选择该文件时，你的 Web 服务器可能会被诱惑执行其内容，而不是简单地下载它。这将允许攻击者在你的服务器上运行任意代码。

解决方案是永远不要允许用户上传随后直接对其他用户可访问的文件。相反，将文件上传到 Web 服务器无法访问的目录（在 Apache 术语中，位于 DocumentRoot 之外）。然后提供一个 Rails action 允许人们查看这些文件。

> 4. Session fixation 攻击在 ACROS Security 的一份文档中有详细描述，可在 http://www.secinft.net/uplarticle/11/session_fixation.pdf 获取。

##### 输入验证很难

Johannes Brodwall 在对本章的评论中写道：

当你验证输入时，重要的是要记住以下几点：

- *使用白名单进行验证*：有许多编码点和斜杠的方法可能会逃避你的验证，但会被底层系统解释。例如，../、\、%2e%2e%2f、%2e%2e%5c 和 ..%c0%af（Unicode）可能会使你上升一个目录级别。接受非常小的字符集（从 [a-zA-Z][a-zA-Z0-9_]* 开始）。
- *不要尝试通过替换、剥离等来从奇怪的路径中恢复*：例如，如果你剥离字符串 ../，像 ....// 这样的恶意输入仍然会通过。如果发生任何奇怪的事情，有人正在尝试一些聪明的手段。只需用简短、无信息的消息将其踢出，例如 “检测到入侵尝试。事件已记录。”

我们经常检查 dirname(full_file_name_from_user) 是否与预期目录相同。这样我们就知道文件名是卫生的。

在此 action 中，请确保执行以下操作：

- 验证请求中的名称是一个简单的、有效的文件名，与目录中的现有文件或表中的行匹配。不要接受诸如 ../../../etc/passwd 之类文件名（参见侧边栏 输入验证很难）。你甚至可能想将上传的文件存储在数据库表中，并使用 id 而不是名称来引用它们。
- 当你下载将在浏览器中显示的文件时，请确保转义其中包含的任何 HTML 序列，以消除 XSS 攻击的可能性。如果你允许下载二进制文件，请确保设置适当的 Content-Type HTTP 头，以确保文件不会意外地在浏览器中显示。

从第 469 页开始的描述说明了如何从 Rails 应用程序下载文件，而从第 544 页开始的关于上传文件的部分展示了一个示例，该示例将图像文件上传到数据库表并提供一个 action 来显示它们。

#### 27.8 不要明文存储敏感信息

你可能正在编写受外部法规管辖的应用程序（在美国，如果你处理信用卡数据，CISP 规则可能适用，如果你处理医疗数据，HIPAA 可能适用）。这些法规对你处理信息的方式施加了一些严重的限制。即使你



安装完成后，通过在应用程序控制器中添加一个 include 来为所有应用程序的控制器添加支持：

```
class ApplicationController < ActionController::Base
  include SslRequirement
end
```

现在你可以在每个控制器的各个操作中设置策略。以下代码直接取自插件的 README 文件：

```
class AccountController < ApplicationController
  ssl_required :signup, :payment
  ssl_allowed :index

  def signup
    # 非 SSL 访问将被重定向到 SSL
  end

  def payment
    # 非 SSL 访问将被重定向到 SSL
  end

  def index
    # 此操作可以使用或不使用 SSL
  end

  def other
    # SSL 访问将被重定向到非 SSL
  end
end
```

ssl_required 声明列出了只能通过 HTTPS 请求调用的操作。ssl_allowed 声明列出了可以用 HTTP 或 HTTPS 调用的操作。

ssl_requirement 插件的技巧在于它处理不符合声明要求的请求的方式。如果针对已声明需要 SSL 的方法发出常规 HTTP 请求，插件会拦截它并立即重定向回同一 URL，但协议为 HTTPS。这样用户将被自动切换到安全连接，而无需在应用程序的视图中执行任何显式的协议设置。⁶ 同样，如果针对不应使用 SSL 的操作发出 HTTPS 请求，插件将自动重定向回同一 URL，但协议为 HTTP。

> 6. 但是，当然，这种易用性是以初始重定向为代价的，即从 HTTP 到 HTTPS 世界的重定向。请注意，此重定向只发生一次。一旦你使用 HTTPS，常规的 link_to 助手将自动继续生成 HTTPS 协议请求。

#### 28.3 安装 Passenger

以下说明假定你已经按照第 3 章《安装 Rails》，第 31 页的说明进行操作；此外，你应该在服务器上安装了一个可运行的 Rails 应用程序。¹

第一步是确保 Apache Web 服务器已安装。对于 Mac OS X 用户和许多 Linux 用户，它已随操作系统一起安装。²

下一步是安装 Passenger：

```
$ sudo gem install passenger
$ sudo passenger-install-apache2-module
```

后者命令会导致编译多个源文件并更新配置文件。在此过程中，它会要求我们两次更新 Apache 配置。第一次是为了启用我们刚刚构建的模块，并涉及在 Apache 配置中添加如下行。（注意：Passenger 会告诉你确切要复制并粘贴到此文件中的行，请使用那些行，而不是这些行。此外，我们不得不将 LoadModule 行换行以使其适应页面。当你输入时，它全部在一行上。）

```
LoadModule passenger_module /opt/local/lib/ruby/gems/1.8/gems/passenger-2.0.6→
/ext/apache2/mod_passenger.so
PassengerRoot /opt/local/lib/ruby/gems/1.8/gems/passenger-2.0.6
PassengerRuby /opt/local/bin/ruby
```

要找到你的 Apache 配置文件的位置，请尝试发出以下命令：³

```
$ apachectl -V | grep SERVER_CONFIG_FILE
```

下一步是部署我们的应用程序。与上一步每台服务器只做一次不同，这一步是每个应用程序一次。在本章的剩余部分，我们将假设应用程序的名称为 depot。由于你的应用程序名称无疑不同，只需将其替换为你的应用程序的实际名称即可。

```
<VirtualHost *:80>
    ServerName www.yourhost.com
    DocumentRoot /home/rubys/work/depot/public/
</VirtualHost>
```

1. 如果你部署到已安装 Passenger 的主机，请随意跳到第 28.4 节，使用 Capistrano 实现无忧部署，第 657 页。

2. 尽管 Windows 用户可以在 http://httpd.apache.org/docs/2.2/platform/windows.html#inst 找到安装此产品的说明，但 Windows 作为服务器平台不受 Passenger 支持。如果在 Windows 上部署是你的安装要求，那么你可以在《Deploying Rails Applications: A Step-by-Step Guide》[ZT08] 的第 6 章找到很好的建议。

3. 在某些系统上，命令名为 apache2ctl；在其他系统上，它是 httpd。

请注意，这里 DocumentRoot 设置为 Rails 应用程序中的 public 目录。

如果我们想用同一个 Apache Web 服务器提供多个应用程序，我们首先需要启用命名虚拟主机：

```
NameVirtualHost *:80
```

一旦就位，只需为每个应用程序重复此 VirtualHost 块，并在每个块中调整 ServerName 和 DocumentRoot。我们还需要将 public 目录标记为可读。最终版本看起来会像以下这样：

```
<VirtualHost *:80>
    ServerName depot.yourhost.com
    DocumentRoot /home/rubys/work/depot/public/

    <Directory /home/rubys/work/depot/public>
        Order allow,deny
        Allow from all
    </Directory>
</VirtualHost>
```

最后一步是重启我们的 Apache Web 服务器：⁴

```
$ sudo apachectl restart
```

就这样！我们现在可以使用我们指定的主机（或虚拟主机）访问你的应用程序。除非我们使用了 80 以外的端口号，否则我们无需在 URL 上再指定端口号。

有几件事需要注意：

- 如果我们想在生产环境以外的环境中运行，我们可以在 Apache 配置中每个 VirtualHost 中包含一个 RailsEnv 指令：
  RailsEnv development

- 我们可以在任何时候仅通过创建一个名为 tmp/restart.txt 的文件来在不重启 Apache 的情况下重启你的应用程序：
  $ touch tmp/restart.txt
  一旦服务器重启，此文件将被删除。

- passenger-install-apache2-module 命令的输出会告诉我们在哪里可以找到额外的文档。

- 特别需要注意的是，Passenger 与 mod_rewrite 和 mod_alias 冲突。这些功能在包含 Rails 应用程序的虚拟主机之外可以正常工作，但在包含 Rails 应用程序的虚拟主机内部不应使用。

4. 同样，在某些系统上，命令名为 apache2ctl；在其他系统上，它是 httpd。

这意味着如果我们控制自己的服务器，我们将不得不调整 httpd.conf 中的 DocumentRoot，或者在共享主机的控制面板中进行调整：

```
DocumentRoot /home/rubys/work/depot/current/public/
```

我们还应该借此机会重新评估部署的数据库选项。大多数大型应用程序和许多共享托管提供商使用单独的数据库服务器机器，通常运行 MySQL。PostgreSQL 也有热情的追随者。SQLite 3 虽然非常适合开发和测试，但通常不被认为适用于大规模部署。我们已经在第 6.1 节《创建数据库》，第 70 页看到了如何为应用程序配置数据库；部署的过程没有不同。

如果我们有多个开发人员在开发中协作，我们可能会不舒服地将数据库配置的详细信息（包括密码）放入我们的配置管理系统。如果是这样，我们只需将完成的 database.yml 放在部署服务器上，但不在当前目录中。我们很快就会向你展示如何指示 Capistrano 在每次部署时将此文件复制到你的当前目录。

如果你选择继续使用 SQLite 3，你仍需要更改 database.yml，因为 Capistrano 每次部署时都会替换你的应用程序目录。只需指定你希望数据库保存的完整路径，同样不在当前目录中即可。

服务器就到这里！从现在开始，我们将从你的开发机器上完成所有操作。

##### 将应用程序置于控制之下

如果尚未将你的应用程序置于配置控制之下，现在就这样做。首先进入你的应用程序目录，然后创建一个名为 .gitignore 的文件，内容如下：

```
db/*.sqlite3
log/*.log
tmp/**/*
```

现在将所有内容提交到本地仓库：

```
$ cd your_application_directory
$ git init
$ git add .
$ git commit -m "initial commit"
```

下一步是可选的，但如果你没有完全控制部署服务器或你有许多部署服务器，这可能是一个好主意



manage. What it does is put the version of the software that you are dependent on into the repository:

```
$ rake rails:freeze:gems
$ rake gems:unpack
$ git add vendor
$ git commit -m "freeze gems"
```

From here, it is a simple matter to push all your code out to the server:

```
$ git remote add origin ssh://user@host/~/git/depot.git
$ git push origin master
```

##### Deploying the Application

The prep work is now done. Our code is now on the SCM server where it can be accessed by the app server.⁵ Now we can install Capistrano via gem install capistrano.

To add the necessary files to the project for Capistrano to do its magic, execute the following command:

```
$ capify .
[add] writing './Capfile'
[add] writing './config/deploy.rb'
[done] capified!
```

From the output, we can see that Capistrano set up two files. The first, Capfile, is Capistrano's analog to a Rakefile. We won't need to touch this file further. The second, config/deploy.rb, contains the recipes needed to deploy our application. Capistrano will provide us with a minimal version of this file, but the following is a somewhat more complete version that you can download and use as a starting point:

Download config/deploy.rb

```
# be sure to change these
set :user, 'rubys'
set :domain, 'depot.pragprog.com'
set :application, 'depot'

# file paths
set :repository, "#{user}@#{domain}:git/#{application}.git"
set :deploy_to, "/home/#{user}/#{domain}"

# distribute your applications across servers (the instructions below put them
# all on the same server, defined above as 'domain', adjust as necessary)
role :app, domain
role :web, domain
role :db, domain, :primary => true
```

> 5. It matters not whether these two servers are the same; what is important here is the roles that are being performed.

```
# you might need to set this if you aren't seeing password prompts
# default_run_options[:pty] = true

# As Capistrano executes in a non-interactive mode and therefore doesn't cause
# any of your shell profile scripts to be run, the following might be needed
# if (for example) you have locally installed gems or applications. Note:
# this needs to contain the full values for the variables set, not simply
# the deltas.
# default_environment['PATH']='<your paths>:/usr/local/bin:/usr/bin:/bin'
# default_environment['GEM_PATH']='<your paths>:/usr/lib/ruby/gems/1.8'

# miscellaneous options
set :deploy_via, :remote_cache
set :scm, 'git'
set :branch, 'master'
set :scm_verbose, true
set :use_sudo, false
```

```
# task which causes Passenger to initiate a restart
namespace :deploy do
  task :restart do
    run "touch #{current_path}/tmp/restart.txt"
  end
end
```

```
# optional task to reconfigure databases
after "deploy:update_code", :configure_database
desc "copy database.yml into the current release path"
task :configure_database, :roles => :app do
  db_config = "#{deploy_to}/config/database.yml"
  run "cp #{db_config} #{release_path}/config/database.yml"
end
```

We will need to edit several properties to match our application. We certainly will need to change the :user, :domain, and :application. The :repository matches where we put our Git file earlier. The :deploy_to may need to be tweaked to match where we told Apache it could find the config/public directory for the application.

The default_run_options and default_environment are to be used only if you have specific problems. The “miscellaneous options” provided are based on Git.

Two tasks are defined. One tells Capistrano how to restart Passenger. The other updates the file database.yml from the copy that we previously placed on the sever. Feel free to adjust these tasks as you see fit.

The first time we deploy our application, we have to perform an additional step to set up the basic directory structure to deploy into on the server:

```
$ cap deploy:setup
```

When we execute this command, Capistrano will prompt us for our server's password. If it fails to do so and fails to log in, we might need to uncomment out the default_run_options line in our deploy.rb file and try again. Once it can

##### Looking at Log Files

To get a quick look at what’s happening in our application, we can use the tail command to examine log files as requests are made against our application. The most interesting data will usually be in the log files from the application itself. Even if Apache is running multiple applications, the logged output for each application is placed in the production.log file for that application.

Assuming that our application is deployed into the location we showed earlier, here’s how we look at our running log file:

```
# On your server
$ cd /home/rubys/work/depot/
$ tail -f log/production.log
```

Sometimes, we need lower-level information—what’s going on with the data in our application? When this is the case, it’s time to break out the most useful live server debugging tool.

##### Using Console to Look at a Live Application

We’ve already created a large amount of functionality in our application’s model classes. Of course, we created these to be used by our application’s controllers. But we can also interact with them directly. The gateway to this world is the script/console script. We can launch it on our server with this:

```
# On your server
$ cd /home/rubys/work/depot/
$ ruby ./script/console production
Loading production environment.
irb(main):001:0> p = Product.find_by_title("Pragmatic Version Control")
=> #<Product:0x24797b4 @attributes={. . .}>
irb(main):002:0> p.price = 32.95
=> 32.95
irb(main):003:0> p.save
=> true
```

Once we have a console session open, we can poke and prod all the various methods on our models. We can create, inspect, and delete records. In a way, it’s like having a root console to your application.

#### 28.6 Production Application Chores

Once you put an application into production, we need to take care of a few chores to keep your application running smoothly. These chores aren’t automatically taken care of for us, but, luckily, we can automate them.

##### Dealing with Log Files

As an application runs, it will constantly add data to its log file. Eventually, the log files can grow extremely large. To overcome this, most logging solutions

can roll over log files to create a progressive set of log files of increasing age. This will break up our log files into manageable chunks that can be archived off or even deleted after a certain amount of time has passed.

The Logger class supports rollover. We simply need to decide how many (or how often) log files we want and the size of each. To enable this, simply add a line like one of the following to the file config/environments/production.rb:

```
```ruby
config.logger = Logger.new(config.log_path, 10, 10.megabytes)
config.logger = Logger.new(config.log_path, 'daily')
```
```

Alternately, we can direct our logs to the system logs for our machine:

```
```ruby
config.logger = SyslogLogger.new
```
```

Find more options at [http://wiki.rubyonrails.com/rails/pages/DeploymentTips](http://wiki.rubyonrails.com/rails/pages/DeploymentTips).

##### Clearing Out Sessions

If you are not using cookie-based session management, be aware that the session handler in Rails doesn’t do automated housekeeping. This means that once the data for a session is created, it isn’t automatically cleared out after the session expires. This can quickly spell trouble. The default file-based session handler will run into trouble long before the database-based session handler will, but both handlers will create an endless amount of data.

Since Rails doesn’t clean up after itself, we’ll need to do it ourselves. The easiest way is to run a script periodically. If we keep sessions in files, the script needs to look at when each session file was last touched and then delete the older ones. For example, we could put the following command into a script that will delete files that haven’t been touched in the last twelve hours:

```
```bash
# On your server
$ find /tmp/ -name 'ruby_sess:*' -ctime +12h -delete
```
```

If our application keeps session data in the database, our script can look at the updated_at column and delete rows accordingly. We can use script/runner to execute this command:

```
```bash
> RAILS_ENV=production ./script/runner  \
    CGI::Session::ActiveRecordStore::Session.delete_all( \
      ["updated_at < ?", 12.hours.ago])
```
```

##### Keeping on Top of Application Errors

Controller actions that fail are handled differently in development vs. production. In development, we get tons of debugging information. In production, the default behavior is to render a static HTML file with the name of the error code thrown. Custom rescue behavior can be achieved by overriding the rescue_action_in_public and rescue_action_locally methods. We can override what is



通过在我们自己的控制器中重写 `local_request?` 方法，可以将其视为本地请求。

与其编写我们自己的自定义恢复机制，我们可能希望查看异常通知插件，以便在应用程序中抛出异常时设置向支持人员发送电子邮件的方式。使用以下命令安装：

```
depot> ruby script/plugin install git://github.com/rails/exception_notification.git
```

然后我们在应用程序控制器中添加以下内容：

```
class ApplicationController < ActionController::Base
  include ExceptionNotifiable
  # ...
```

然后在我们的 `environment.rb` 文件中设置接收通知电子邮件的人员列表：

```
ExceptionNotifier.exception_recipients =
%w(support@my-org.com dave@cell-phone.company)
```

我们需要确保 Action Mailer 已配置为发送电子邮件，如第 609 页开始所述。

#### 28.7 迈向发布及以后

一旦我们设置了初始部署，我们就可以完成应用程序的开发并将其发布到生产环境。我们可能会设置额外的部署服务器，而从第一次部署中学到的经验将告诉我们如何构建后续部署。例如，我们可能会发现 Rails 是我们系统中最慢的组件之一——请求时间中大部分花费在 Rails 上，而非等待数据库或文件系统。这表明扩展的方法是添加机器来分摊 Rails 的负载。

然而，我们可能会发现请求花费的大部分时间在数据库上。如果是这种情况，我们需要查看如何优化数据库活动。也许我们需要改变访问数据的方式。或者也许我们需要自定义制作一些 SQL 来替换默认的 Active Record 行为。

有一点是肯定的：每个应用程序在其生命周期中都需要不同的调整。最重要的活动是随着时间的推移倾听它并发现需要做什么。我们的工作在发布应用程序时并没有结束。它实际上才刚刚开始。

如果您最终想要探索替代部署选项，您可以在《Deploying Rails Applications: A Step-by-Step Guide [ZT08]》中找到大量好的建议。

最后，我们可以简化此方法。Ruby 方法返回的值是最后一个求值的表达式的值，因此我们可以完全去掉临时变量和 return 语句：

```
def say_goodnight(name)
"Good night, #{name.capitalize}"
end
puts say_goodnight('ma')
```

#### A.4 类

这是一个 Ruby 类定义：

```
class Order < ActiveRecord::Base
  has_many :line_items
  def self.find_all_unpaid
    find(:all, 'paid = 0')
  end
  def total
    sum = 0
    line_items.each {|li| sum += li.total}
  end
end
```

类定义以关键字 class 开头，后跟类名（必须以大写字母开头）。此 Order 类被定义为 ActiveRecord 模块中 Base 类的子类。

Rails 大量使用类级声明。这里的 has_many 是 Active Record 定义的方法。它在 Order 类被定义时被调用。通常这类方法对类做出断言，因此在本书中我们称它们为声明。

在类体内部，您可以定义类方法和实例方法。用 self. 前缀方法名（如第 5 行所示）使其成为类方法；它可以在类上调用。在这种情况下，我们可以在应用程序中的任何位置进行以下调用：

```
to_collect = Order.find_all_unpaid
```

常规方法定义创建实例方法（如第 9 行的 total 定义）。这些方法在类的对象上调用。在以下示例中，变量 order 引用一个 Order 对象。我们在前面的类定义中定义了 total 方法。

```
puts "The total is #{order.total}"
```

注意 find_all_unpaid 和 total 方法之间的区别。第一个不特定于某个订单，因此我们在类级别定义它并通过类本身调用它。第二个适用于一个订单，因此我们将其定义为实例方法并在特定的订单对象上调用它。

类的对象在其 *实例变量* 中保存状态。这些变量名都以 @ 开头，可供类的所有实例方法使用。每个对象都有自己的一组实例变量。

```
class Greeter
  def initialize(name)
    @name = name
  end
  def say(phrase)
    puts "#{phrase}, #{@name}"
  end
end

g1 = Greeter.new("Fred")
g2 = Greeter.new("Wilma")

g1.say("Hello")     #=> Hello, Fred
g2.say("Hi")        #=> Hi, Wilma
```

实例变量在类外部不能直接访问。要使其可用，请编写返回其值的方法：

```
class Greeter
  def initialize(name)
    @name = name
  end

  def name
    @name
  end

  def name=(new_name)
    @name = new_name
  end
end

g = Greeter.new("Barney")
puts g.name   #=> Barney
g.name = "Betty"
puts g.name   #=> Betty
```

Ruby 提供了便捷方法为您编写这些访问器方法（这对厌倦编写所有那些 getter 和 setter 的人来说是个好消息）：

```
class Greeter
  attr_accessor :name      # create reader and writer methods
  attr_reader   :greeting  # create reader only
  attr_writer   :age       # create writer only
```

##### 私有和受保护

类的实例方法默认是公开的；任何人都可以调用它们。您可能希望对此进行覆盖，以用于仅打算由其他类实例方法使用的情况：

```
class MyClass
  def m1      # this method is public
  end

  protected

  def m2      # this method is protected
  end

  private

  def m3      # this method is private
  end
end
```

private 指令是最严格的；私有方法只能从同一实例内部调用。受保护方法既可以在同一实例中调用，也可由同一类的其他实例及其子类调用。

#### A.5 模块

模块与类相似，因为它们包含一组方法、常量以及其他模块和类定义。与类不同，您不能基于模块创建对象。

模块有两个用途。首先，它们充当命名空间，让您可以定义方法名不会与其他地方定义的方法冲突。其次，它们允许您在类之间共享功能——如果一个类混入一个模块，该模块的实例方法就变得可用，就好像它们是在类中定义的一样。多个类可以混入同一个模块，共享模块的功能而无需使用继承。您还可以将多个模块混入单个类。

Rails 大量使用模块。例如，辅助方法是在模块中编写的。Rails 会自动将这些辅助模块混入适当的视图模板中。例如，如果您想编写一个可在 store 控制器调用的视图中调用的辅助方法，您可以在 app/helpers 目录中的 store_helper.rb 文件中定义以下模块：

```
module StoreHelper
  def capitalize_words(string)
    string.gsub(/\b\w/) { $&.upcase }
  end
end
```

## A.6 数组和哈希

Ruby 的数组和哈希都是索引集合。两者都存储可通过键访问的对象集合。对于数组，键是整数，而哈希支持任何对象作为键。数组和哈希在需要容纳新元素时会按需增长。访问数组元素更高效，但哈希提供更大的灵活性。任何特定的数组或哈希都可以保存不同类型的对象；例如，您可以有一个包含整数、字符串和浮点数的数组。

您可以使用数组字面量——方括号之间的一组元素——创建并初始化新的数组对象。给定一个数组对象，您可以通过在方括号之间提供索引来访问单个元素，如下一个示例所示。Ruby 数组索引从零开始。

```
a = [ 1, 'cat', 3.14 ]    # array with three elements
a[0]                    # access the first element (1)
a[2] = nil              # set the third element
                        # array now [ 1, 'cat', nil ]
```

您可能已经注意到我们在本示例中使用了特殊值 nil。在许多语言中，nil（或 null）的概念意味着“无对象”。在 Ruby 中并非如此；nil 是一个对象，就像其他对象一样，只是恰好代表 nothing。

方法 << 通常与数组一起使用。它将值附加到其接收者。

```
ages = []
for person in @people
  ages << person.age
end
```

Ruby 有一个创建单词数组的快捷方式：

```
a = [ 'ant', 'bee', 'cat', 'dog', 'elk' ]
# this is the same:
a = %w{ ant bee cat dog elk }
```

Ruby 哈希与数组类似。哈希字面量使用大括号而不是方括号。字面量必须为每个条目提供两个对象：一个作为键，另一个作为值。例如，您可能想将乐器映射到其管弦乐队声部：

```
inst_section = {
  :cello    => 'string',
  :clarinet => 'woodwind',
  :drum     => 'percussion',
  :oboe     => 'woodwind',
  :trumpet  => 'brass',
  :violin   => 'string'
}
```




Ruby *statement* modifiers are a useful shortcut if the body of an if or while statement is just a single expression. Simply write the expression, followed by if or while and the condition:

```
puts "Danger, Will Robinson" if radiation > 3000
```

```
distance = distance * 1.2 while distance < 100
```

## A.8 Regular Expressions

A regular expression lets you specify a *pattern* of characters to be matched in a string. In Ruby, you typically create a regular expression by writing /pattern/ or %r(pattern).

For example, you could write a pattern that matches a string containing the text Perl or the text Python using the regular expression /Perl|Python/.

The forward slashes delimit the pattern, which consists of the two things we're matching, separated by a vertical bar (|). This bar character means "either the thing on the left or the thing on the right," in this case either Perl or Python. You can use parentheses within patterns, just as you can in arithmetic expressions, so you could also have written this pattern as /(Per|ython)/. Programs typically test strings against regular expressions using the =~ match operator:

```
if line =~ /(Per|ython)/
  puts "There seems to be another scripting language here"
end
```

You can specify *repetition* within patterns. /ab+c/ matches a string containing an a followed by one or more b's, followed by a c. Change the plus to an asterisk, and /ab*c/ creates a regular expression that matches one a, zero or more b's, and one c.

Ruby's regular expressions are a deep and complex subject; this section barely skims the surface. See the PickAxe book for a full discussion.

## A.9 Blocks and Iterators

Code blocks are just chunks of code between braces or between do...end. A common convention is that people use braces for single-line blocks and do/end for multiline blocks:

```
{ puts "Hello" }    # this is a block
```

```
do
  club.enroll(person)  # and so is this
  person.socialize
end
```

A block must appear after the call to a method; put the start of the block at the end of the source line containing the method call. For example, in the following code, the block containing puts "Hi" is associated with the call to the method greet:

```
greet { puts "Hi" }
```

If the method has parameters, they appear before the block:

```
verbose_greet("Dave", "loyal customer") { puts "Hi" }
```

A method can invoke an associated block one or more times using the Ruby yield statement. You can think of yield as being something like a method call that calls out to the block associated with the method containing the yield. You can pass values to the block by giving parameters to yield. Within the block, you list the names of the arguments to receive these parameters between vertical bars (|).

Code blocks appear throughout Ruby applications. Often they are used in conjunction with iterators: methods that return successive elements from some kind of collection, such as an array:

```
animals = %w( ant bee cat dog elk )    # create an array
animals.each {|animal| puts animal }    # iterate over the contents
```

Each integer N implements a times method, which invokes an associated block N times:

```
3.times { print "Ho! " }    #=> Ho! Ho! Ho!
```

## A.10 Exceptions

Exceptions are objects (of class Exception or its subclasses). The raise method causes an exception to be raised. This interrupts the normal flow through the code. Instead, Ruby searches back through the call stack for code that says it can handle this exception.

Exceptions are handled by wrapping code between begin and end keywords and using rescue clauses to intercept certain classes of exception:

```
begin
  content = load_blog_data(file_name)
rescue BlogDataNotFound
  STDERR.puts "File #{file_name} not found"
rescue BlogDataFormatError
  STDERR.puts "Invalid blog data in #{file_name}"
rescue Exception => exc
  STDERR.puts "General error loading #{file_name}: #{exc.message}"
end
```

## A.11 Marshaling Objects

Ruby can take an object and convert it into a stream of bytes that can be stored outside the application. This process is called marshaling. This saved object can later be read by another instance of the application (or by a totally separate application), and a copy of the originally saved object can be reconstituted.

There are two potential issues when you use marshaling. First, some objects cannot be dumped. If the objects to be dumped include bindings, procedure or method objects, instances of class IO, or singleton objects or if you try to dump anonymous classes or modules, a TypeError will be raised.

Second, when you load a marshaled object, Ruby needs to know the definition of the class of that object (and of all the objects it contains).

Rails uses marshaling to store session data. If you rely on Rails to dynamically load classes, it is possible that a particular class may not have been defined at the point it reconstitutes session data. For that reason, you'll use the model declaration in your controller to list all models that are marshaled. This preemptively loads the necessary classes to make marshaling work.

## A.12 Interactive Ruby

irb—Interactive Ruby—is the tool of choice for executing Ruby interactively. irb is a Ruby shell, complete with command-line history, line-editing capabilities, and job control. You run irb from the command line. Once it starts, just type in Ruby code. irb shows you the value of each expression as it evaluates it:

```
% irb
irb(main):001:0> def sum(n1, n2)
irb(main):002:1>   n1 + n2
irb(main):003:1> end
=> nil
irb(main):004:0> sum(3, 4)
=> 7
irb(main):005:0> sum("cat", "dog")
=> "catdog"
```

You can run irb on Rails applications, letting you experiment with methods (and sometimes undo damage to your database). However, setting up the full Rails environment is tricky. Rather than do it manually, use the script/console wrapper, as shown on page 272.

## A.13 Ruby Idioms

Ruby is a language that lends itself to idiomatic usage. There are many good resources on the Web showing Ruby idioms and Ruby gotchas. Here are just a few.

- http://www.ruby-lang.org/en/documentation/ruby-from-other-languages/
- http://en.wikipedia.org/wiki/Ruby_programming_language
- http://www.zenspider.com/Languages/Ruby/QuickRef.html

This section shows some common Ruby idioms that we use in this book:

Methods such as empty! and empty?

Ruby method names can end with an exclamation mark (a bang method) or a question mark (a predicate method). Bang methods normally do something destructive to the receiver. Predicate methods return true or false depending on some condition.

a || b

The expression a || b evaluates a. If it isn't false or nil, then evaluation stops and the expression returns a. Otherwise, the statement returns b. This is a common way of returning a default value if the first value hasn't been set.

a ||= b

The assignment statement supports a set of shortcuts: a op= b is the same as a = a op b. This works for most operators.

```
count += 1        # same as count = count + 1
price *= discount  #        price = price * discount
count ||= 0        #        count = count || 0
```

So, count ||= 0 gives count the value 0 if count doesn't already have a value.

obj = self.new

Sometimes a class method needs to create an instance of that class.

```
class Person < ActiveRecord::Base
  def self.for_dave
    Person.new(:name => 'Dave')
  end
end
```

This works fine, returning a new Person object. But later, someone might subclass our class:

```
class Employee < Person
  # ..
end
```

```
dave = Employee.for_dave  # returns a Person
```

The for_dave method was hardwired to return a Person object, so that's what is returned by Employee.for_dave. Using self.new instead returns a new object of the receiver's class, Employee.

```
require File.dirname(__FILE__) + '../test_helper'
```

Ruby's require method loads an external source file into our application. This is used to include library code and classes that our application relies on. In normal use, Ruby finds these files by searching in a list of directories, the LOAD_PATH.

Sometimes we need to be specific about what file to include. We can do that by giving require a full filesystem path. The problem is, we don't know what that path will be—our users could install our code anywhere.

Wherever our application ends up getting installed, the relative path between the file doing the requiring and the target file will be the same. Knowing this, we can construct the absolute path to the target by taking the absolute path to the file doing the requiring (available in the special variable __FILE__), stripping out all but the directory name, and then appending the relative path to the target file.

## A.14 RDoc Documentation

RDoc is a documentation system for Ruby source code. Just like JavaDoc, RDoc takes a bunch of source files and generates HTML documentation, using syntactic information from the source and text in comment blocks. Unlike JavaDoc, RDoc can produce fairly good content even if the source contains no comments. It's fairly painless to write RDoc documentation as you write the source for your applications. RDoc is described in Chapter 16 of the PickAxe book.

RDoc is used to document Ruby's built-in and standard libraries. Depending on how your Ruby was installed, you might be able to use the ri command to access the documentation:

```
dave> ri String.capitalize
--------------------------------------------- String#capitalize
    str.capitalize   => new_str
---------------------------------------------
Returns a copy of str with the first character converted to uppercase and the remainder to lowercase.

"hello".capitalize   #=> "Hello"
"HELLO".capitalize   #=> "Hello"
"123ABC".capitalize  #=> "123abc"
```

If you used RubyGems to install Rails, you can access the Rails API documentation by running gem server and then pointing your browser at the URL http://localhost:8808.

The rake doc:app task creates the HTML documentation for a Rails project, leaving it in the doc/app directory.




```
config.plugin_locators = Rails::Plugin::FileSystemLocator
```

这些是用于查找你希望为应用程序加载的所需插件的类。

```
config.plugin_paths = "vendor/plugins"
```

这是插件目录的根路径。

```
config.plugins = nil
```

这是要加载的插件列表。如果设置为 nil，则会加载所有插件。如果设置为 []，则不会加载任何插件。否则，插件将按指定的顺序加载。

```
config.routes_configuration_file = "config/routes.rb"
```

这是要使用的路由配置文件路径。

```
config.time_zone = "UTC"
```

这设置默认时区。设置后将为 Active Record 模型启用时区感知，并将 Active Record 默认时区设置为 :utc。

如果你想使用其他时区，以下 Rake 任务可能会有所帮助：time:zones:all、time:zones:us 和 time:zones:local。time:zones:local 将尝试根据系统本地时间缩小可能性范围。

```
config.view_path = "app/views"
```

这是查找视图模板的位置。

```
config.whiny_nils = true | false
```

如果设置为 true，Rails 将尝试拦截你在未初始化对象上调用方法时的情况。例如，如果你的 @orders 变量未设置且你调用 @orders.each，Ruby 通常只会说类似 undefined method `each' for nil 的内容。启用 whiny_nils 后，Rails 会拦截此情况并改为提示你可能期望一个数组。默认情况下在开发环境中是开启的。

### B.2 Active Record 配置

```
config.active_record.allow_concurrency = true | false
```

如果设置为 true，每个线程将使用单独的数据库连接。由于 Rails 在用于提供 Web 应用程序时不是线程安全的，因此此变量默认为 false。你可能会考虑（谨慎地）将其设置为 true，如果你正在编写使用 Active Record 的多线程应用程序，且在 Rails 其余部分范围之外使用。

```
config.active_record.colorize_logging = true | false
```

默认情况下，Active Record 日志消息包含嵌入的 ANSI 控制序列，当使用支持这些序列的终端应用程序查看时，会对某些行进行着色。将选项设置为 false 可移除此着色。

```
config.active_record.default_timezone = :local | :utc
```

将其设置为 :utc 可使从数据库加载和保存的日期和时间被视为 UTC。

```
config.active_record.lock_optimistically = true | false
```

如果为 false，则乐观锁定被禁用。参见第 20.4 节、乐观锁定，第 422 页。

```
config.active_record.logger = logger
```

这接受一个 logger 对象，应与 Log4R 接口兼容。内部用于记录数据库活动。它也可在应用程序希望通过 logger 属性记录活动时使用。

```
config.active_record.pluralize_table_names = true | false
```

如果设置为 false，创建对应表名时类名将不会被复数化。

```
config.active_record.primary_key_prefix_type = option
```

如果 option 为 nil，每个表的默认主键列名为 id。如果为 :table_name，则在前面加上表名。通过将 option 设置为 :table_name_with_underscore，可在表名和 id 部分之间添加下划线。

```
config.active_record.record_timestamps = true | false
```

将其设置为 false 可禁用 created_at、created_on、updated_at 和 updated_on 列的自动更新。这在第 409 页有描述。

```
config.active_record.table_name_prefix = "prefix"
```

在生成表名时添加给定的字符串。例如，如果模型名为 User 且前缀字符串为 "myapp-"，Rails 将查找表 myapp-users。如果必须在不同应用程序之间共享数据库或必须在同一数据库中进行开发和测试，这可能很有用。

```
config.active_record.table_name_suffix = "suffix"
```

在生成表名时附加给定的字符串。

```
config.active_record.timestamped_migrations = true | false
```

将其设置为 false 可使用递增整数代替时间戳作为迁移前缀。

```
config.active_record.schema_format = :sql | :ruby
```

这控制转储数据库架构时使用的格式。这在运行测试时很重要，因为 Rails 使用从开发环境转储的架构来填充测试数据库。:ruby 格式创建

```
config.action_mailer.default_content_type = "text/plain"
```

这是电子邮件的默认内容类型。

```
config.action_mailer.default_implicit_parts_order =
%w( text/html text/enriched text/plain)
```

我们曾在第 616 页看到，如果找到名为 xxx.text.plain.rhtml、xxx.text.html.rhtml 等的模板文件，Rails 会自动生成多部分消息。此参数决定这些部分添加到电子邮件中的顺序，从而决定电子邮件客户端赋予它们的优先级。

```
config.action_mailer.default_mime_version = "1.0"
```

这是电子邮件的默认 mime 版本。

```
config.action_mailer.delivery_method = :smtp | :sendmail | :test
```

这决定电子邮件的投递方式。与 smtp 设置一起使用。参见第 610 页开始的描述。

```
config.action_mailer.logger = logger
```

将其设置为覆盖邮件程序使用的默认记录器。未设置时，使用整个应用程序的记录器。

```
config.action_mailer.perform_deliveries = true | false
```

如果为 false，邮件程序将不会投递电子邮件。

```
config.action_mailer.raise_delivery_errors = true | false
```

如果为 true，电子邮件投递失败时会引发异常。请注意，Rails 只知道电子邮件向邮件传输代理的初始交接。它无法判断邮件是否真正到达收件人。此参数在测试环境中为 true，但在其他环境中默认为 false。

```
config.action_mailer.register_template_extension extension
```

这注册模板扩展，以便使用 ERb 或 Builder 以外的模板语言编写的邮件程序模板得到支持。

```
config.action_mailer.sendmail_settings = hash
```

这是一个包含以下设置的哈希：

-   :location 这是 sendmail 可执行文件的路径。默认为 /usr/sbin/sendmail。

-   :arguments 这包含命令行参数。默认为 -i -t。

```
config.action_mailer.smtp_settings = hash
```

参见第 610 页开始的描述。

## 附录 C

### 源代码

本附录包含我们为最终 Depot 应用程序创建的文件的完整列表，以及我们修改的生成文件。

所有代码均可从我们的网站下载：

- http://pragprog.com/titles/rails3/code.html

### C.1 完整的 Depot 应用程序

### 数据库配置和迁移

Download depot_f/config/database.yml

```
# SQLite version 3.x
# gem install sqlite3-ruby (not necessary on OS X Leopard)
development:
  adapter: sqlite3
  database: db/development.sqlite3
  pool: 5
  timeout: 5000

# Warning: The database defined as "test" will be erased and
# re-generated from your development database when you run "rake".
# Do not set this db to the same as development or production.
test:
  adapter: sqlite3
  database: db/test.sqlite3
  pool: 5
  timeout: 5000

production:
  adapter: sqlite3
  database: db/production.sqlite3
  pool: 5
  timeout: 5000
```

Download depot_t/db/migrate/20080601000001_create_products.rb

```
class CreateProducts < ActiveRecord::Migration
  def self.up
    create_table :products do |t|
      t.string :title
      t.text :description
      t.string :image_url

      t.timestamps
    end
  end

  def self.down
    drop_table :products
  end
end
```

Download depot_t/db/migrate/20080601000002_add_price_to_product.rb

```
class AddPriceToProduct < ActiveRecord::Migration
  def self.up
    add_column :products, :price, :decimal,
      :precision => 8, :scale => 2, :default => 0
  end

  def self.down
    remove_column :products, :price
  end
end
```

Download depot_t/db/migrate/20080601000003_add_test_data.rb

```
class AddTestData < ActiveRecord::Migration
  def self.up
    Product.delete_all
    Product.create(:title => 'Pragmatic Project Automation',
      :description =>
        %{
          <p>
            <em>Pragmatic Project Automation</em> shows you how to improve the
            consistency and repeatability of your project's procedures using
            automation to reduce risk and errors.
          </p>
          <p>
            Simply put, we're going to put this thing called a computer to work
            for you doing the mundane (but important) project stuff. That means
            you'll have more time and energy to do the really
            exciting---and difficult---stuff, like writing quality code.
          </p>},
      :image_url => '/images/auto.jpg',
      :price => 29.95)

    Product.create(:title => 'Pragmatic Version Control',
      :description =>
        %{
          <p>
            This book is a recipe-based approach to using Subversion that will
            get you up and running quickly---and correctly. All projects need
```




```
version control: it's a foundational piece of any project's infrastructure. Yet half of all project teams in the U.S. don't use any version control at all. Many others don't use it well, and end up experiencing time-consuming problems.
</p>},
:image_url => '/images/svn.jpg',
:price => 28.50)
# ...

Product.create(:title => 'Pragmatic Unit Testing (C#)',
:description =>
%{<p>
Pragmatic programmers use feedback to drive their development and personal processes. The most valuable feedback you can get while coding comes from unit testing.
</p>
<p>
Without good tests in place, coding can become a frustrating game of "whack-a-mole." That's the carnival game where the player strikes at a mechanical mole; it retreats and another mole pops up on the opposite side of the field. The moles pop up and down so fast that you end up flailing your mallet helplessly as the moles continue to pop up where you least expect them.
</p>};
:image_url => '/images/utc.jpg',
:price => 27.75)

end

def self.down
  Product.delete_all
end
end
下载 depot1/db/migrate/20080601000004_create_sessions.rb
class CreateSessions < ActiveRecord::Migration
  def self.up
    create_table :sessions do |t|
      t.string :session_id, :null => false
      t.text :data
      t.timestamps
    end

    add_index :sessions, :session_id
    add_index :sessions, :updated_at
  end

  def self.down
    drop_table :sessions
  end
end

## 控制器

下载 depot_t/app/controllers/application.rb

```
# Filters added to this controller apply to all controllers in the application.
# Likewise, all the methods added will be available for all controllers.

class ApplicationController < ActionController::Base
  layout "store"
  before_filter :authorize, :except => :login
  before_filter :set_locale
  #...
  helper :all # include all helpers, all the time

  # See ActionController::RequestForgeryProtection for details
  # Uncomment the :secret if you're not using the cookie session store
  protect_from_forgery :secret => '8fc080370e56e929a2d5afca5540a0f7'

  # See ActionController::Base for details
  # Uncomment this to filter the contents of submitted sensitive data parameters
  # from your application log (in this case, all fields with names like "password").
  # filter_parameter_logging :password

  protected
  def authorize
    unless User.find_by_id(session[:user_id])
      if session[:user_id] != :logged_out
        authenticate_or_request_with_http_basic('Depot') do |username, password|
          user = User.authenticate(username, password)
          session[:user_id] = user.id if user
        end
      else
        flash[:notice] = "Please log in"
        redirect_to :controller => 'admin', :action => 'login'
      end
    end
  end

  def set_locale
    session[:locale] = params[:locale] if params[:locale]
    I18n.locale = session[:locale] || I18n.default_locale

    locale_path = "#{LOCALES_DIRECTORY}/#{I18n.locale}.yml"

    unless I18n.load_path.include? locale_path
      I18n.load_path << locale_path
      I18n.backend.send(:init_translations)
    end

    rescue Exception => err
      logger.error err
      flash.now[:notice] = "#{I18n.locale} translation not available"

      I18n.load_path -= [locale_path]
      I18n.locale = session[:locale] = I18n.default_locale
    end
  end
```

下载 depot_t/app/controllers/admin_controller.rb

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

  def logout
    session[:user_id] = :logged_out
    flash[:notice] = "Logged out"
    redirect_to(:action => "login")
  end

  def index
    @total_orders = Order.count
  end
end

下载 depot_t/app/controllers/info_controller.rb

class InfoController < ApplicationController
  def who_bought
    @product = Product.find(params[:id])
    @orders  = @product.orders
    respond_to do |format|
      format.html
      format.xml { render :layout => false }
    end
  end

  protected

  def authorize
  end
end

下载 depot_t/app/controllers/store_controller.rb

class StoreController < ApplicationController
  before_filter :find_cart, :except => :empty_cart
  def index
    @products = Product.find_products_for_sale
  end

def add_to_cart
  product = Product.find(params[:id])
  @current_item = @cart.add_product(product)
  respond_to do |format|
    format.js if request.xhr?
    format.html { redirect_to_index }
  end
rescue ActiveRecord::RecordNotFound
  logger.error("Attempt to access invalid product #{params[:id]}")
  redirect_to_index("Invalid product")
end

def checkout
  if @cart.items.empty?
    redirect_to_index("Your cart is empty")
  else
    @order = Order.new
  end
end

def save_order
  @order = Order.new(params[:order])
  @order.add_line_items_from_cart(@cart)
  if @order.save
    session[:cart] = nil
    redirect_to_index(I18n.t('flash.thanks'))
  else
    render :action => 'checkout'
  end
end

def empty_cart
  session[:cart] = nil
  redirect_to_index
end

private

def redirect_to_index(msg = nil)
  flash[:notice] = msg if msg
  redirect_to :action => 'index'
end

def find_cart
  @cart = (session[:cart] ||= Cart.new)
end

#...
protected

def authorize
end
end

下载 depot_t/app/controllers/line_items_controller.rb

class LineItemsController < ApplicationController
  # GET /line_items
  # GET /line_items.xml
  def index
    @line_items = LineItem.find(:all)

    respond_to do |format|
      format.html # index.html.erb
      format.xml  { render :xml => @line_items }
    end
  end

  # GET /line_items/1
  # GET /line_items/1.xml
  def show
    @line_item = LineItem.find(params[:id])

    respond_to do |format|
      format.html # show.html.erb
      format.xml  { render :xml => @line_item }
    end
  end

  # GET /line_items/new
  # GET /line_items/new.xml
  def new
    @line_item = LineItem.new

    respond_to do |format|
      format.html # new.html.erb
      format.xml  { render :xml => @line_item }
    end
  end

  # GET /line_items/1/edit
  def edit
    @line_item = LineItem.find(params[:id])
  end

  # POST /line_items
  # POST /line_items.xml
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
        format.xml { render :xml => @line_item.errors,
                      :status => :unprocessable_entity }
      end
    end
  end

  # PUT /line_items/1
  # PUT /line_items/1.xml
  def update
    @line_item = LineItem.find(params[:id])

    respond_to do |format|
      if @line_item.update_attributes(params[:line_item])
        flash[:notice] = 'LineItem was successfully updated.'
        format.html { redirect_to(@line_item) }
        format.xml { head :ok }
      else
        format.html { render :action => "edit" }
        format.xml { render :xml => @line_item.errors,
                    :status => :unprocessable_entity }
      end
    end
  end

  # DELETE /line_items/1
  # DELETE /line_items/1.xml
  def destroy
    @line_item = LineItem.find(params[:id])
    @line_item.destroy

    respond_to do |format|
      format.html { redirect_to(line_items_url) }
      format.xml { head :ok }
    end
  end

下载 depot_t/app/controllers/users_controller.rb

class UsersController < ApplicationController
  # GET /users
  # GET /users.xml
  def index
    @users = User.find(:all, :order => :name)

    respond_to do |format|
      format.html # index.html.erb
      format.xml { render :xml => @users }
    end
  end

  # GET /users/1
  # GET /users/1.xml
  def show
    @user = User.find(params[:id])
```




```ruby
def self.authenticate(name, password)
  user = self.find_by_name(name)
  if user
    expected_password = encrypted_password(password, user.salt)
    if user.hashed_password != expected_password
      user = nil
    end
  end
  user
end

# 'password' is a virtual attribute
def password
  @password
end

def password=(pwd)
  @password = pwd
  return if pwd.blank?
  create_new_salt
  self.hashed_password = User.encrypted_password(self.password, self.salt)
end

def after_destroy
  if User.count.zero?
    raise "Can't delete last user"
  end
end

private

def password_non_blank
  errors.add(:password, "Missing password") if hashed_password.blank?
end

def create_new_salt
  self.salt = self.object_id.to_s + rand.to_s
end

def self.encrypted_password(password, salt)
  string_to_hash = password + "wibble" + salt
  Digest::SHA1.hexdigest(string_to_hash)
end
```

## 布局和视图

`Download depot_f/app/views/layouts/store.html.erb`

```html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
                      "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">

<html>
<head>
  <title>Pragprog Books Online Store</title>
  <%= stylesheet_link_tag "depot", :media => "all" %>
```

```
<%= javascript_include_tag :defaults %>
</head>
<body id="store">
<div id="banner">
  <%= form_tag '', :method => 'GET', :class => 'locale' do %>
    <%= select_tag 'locale', options_for_select(LANGUAGES, I18n.locale),
      :onchange => 'this.form.submit()' %>
    <%= submit_tag 'submit' %>
    <%= javascript_tag "$('.locale input').each(Element.hide)" %>
  <% end %>
  <%= image_tag("logo.png") %>
  <%= @page_title || I18n.t('layout.title') %>
</div>
<div id="columns">
  <div id="side">
    <% if @cart %>
      <% hidden_div_if(@cart.items.empty?, :id => "cart") do %>
        <%= render(:partial => "cart", :object => @cart) %>
      <% end %>
    <% end %>

    <a href="http://www...."> <%= I18n.t 'layout.side.home' %> </a><br />
    <a href="http://www..../faq"> <%= I18n.t 'layout.side.questions' %> </a><br />
    <a href="http://www..../news"> <%= I18n.t 'layout.side.news' %> </a><br />
    <a href="http://www..../contact"> <%= I18n.t 'layout.side.contact' %> </a><br />
    <% if session[:user_id] %>
      <br />
      <%= link_to 'Orders', :controller => 'orders' %><br />
      <%= link_to 'Products', :controller => 'products' %><br />
      <%= link_to 'Users', :controller => 'users' %><br />
      <br />
      <%= link_to 'Logout', :controller => 'admin', :action => 'logout' %>
    <% end %>
  </div>
  <div id="main">
    <% if flash[:notice] -%>
      <div id="notice"><%= flash[:notice] %></div>
    <% end -%>

    <%= yield :layout %>
  </div>
</div>
</body>
</html>
```

## 管理员视图

Download depot_t/app/views/admin/index.html.erb

```
<h1>Welcome</h1>

It's <%= Time.now %>
We have <%= pluralize(@total_orders, "order") %>.

```

```
Download depot_f/app/views/admin/login.html.erb
<div class="depot-form">
  <% form_tag do %>
    <fieldset>
      <legend>Please Log In</legend>

      <div>
        <label for="name">Name:</label>
        <%= text_field_tag :name, params[:name] %>
      </div>

      <div>
        <label for="password">Password:</label>
        <%= password_field_tag :password, params[:password] %>
      </div>

      <div>
        <%= submit_tag "Login" %>
      </div>
    </fieldset>
  <% end %>
</div>
```

```
Download depot_f/app/views/admin/login.html.erb
<div class="depot-form">
  <% form_tag do %>
    <fieldset>
      <legend>Please Log In</legend>

      <div>
        <label for="name">Name:</label>
        <%= text_field_tag :name, params[:name] %>
      </div>

      <div>
        <label for="password">Password:</label>
        <%= password_field_tag :password, params[:password] %>
      </div>

      <div>
        <%= submit_tag "Login" %>
      </div>
    </fieldset>
  <% end %>
</div>
```

## 产品视图

```
Download depot_f/app/views/products/edit.html.erb
<h1>Editing product</h1>

<% form_for(@product) do |f| %>
  <%= f.error_messages %>
```

```
<p>
  <%= f.label :title %><br />
  <%= f.text_field :title %>
</p>
<p>
  <%= f.label :description %><br />
  <%= f.text_area :description %>
</p>
<p>
  <%= f.label :image_url %><br />
  <%= f.text_field :image_url %>
</p>
<p>
  <%= f.label :price %><br />
  <%= f.text_field :price %>
</p>
<p>
  <%= f.submit "Update" %>
</p>
<% end %>

<%= link_to 'Show', @product %> |
<%= link_to 'Back', products_path %>

Download depot_t/app/views/products/index.html.erb

<div id="product-list">
  <h1>Listing products</h1>

  <table>
  <% for product in @products %>
    <tr class="<%= cycle('list-line-odd', 'list-line-even') %>">

      <td>
        <%= image_tag product.image_url, :class => 'list-image' %>
      </td>

      <td class="list-description">
        <dl>
          <dt><%=h product.title %></dt>
          <dd><%=h truncate(product.description.gsub(/<.*?>/,''),
            :length => 80) %></dd>
        </dl>
      </td>

      <td class="list-actions">
        <%= link_to 'Show', product %><br />
        <%= link_to 'Edit', edit_product_path(product) %><br />
        <%= link_to 'Destroy', product,
          :confirm => 'Are you sure?',
          :method => :delete %>
      </td>
    </tr>
  <% end %>

```

```
</table>
</div>

<br />

<%= link_to 'New product', new_product_path %>
Download depot_t/app/views/products/new.html.erb
<h1>New product</h1>

<%= form_for(@product) do |f| %>
  <%= f.error_messages %>

  <p>
    <%= f.label :title %><br />
    <%= f.text_field :title %>
  </p>
  <p>
    <%= f.label :description %><br />
    <%= f.text_area :description, :rows => 6 %>
  </p>
  <p>
    <%= f.label :image_url %><br />
    <%= f.text_field :image_url %>
  </p>
  <p>
    <%= f.label :price %><br />
    <%= f.text_field :price %>
  </p>

  <p>
    <%= f.submit "Create" %>
  </p>
<% end %>

<%= link_to 'Back', products_path %>
Download depot_t/app/views/products/show.html.erb
<p>
  <b>Title:</b>
  <%=h @product.title %>
</p>

<p>
  <b>Description:</b>
  <%= @product.description %>
</p>

<p>
  <b>Image url:</b>
  <%=h @product.image_url %>
</p>
```

```
<p>
  <b>Price:</b>
  <%=h @product.price %>
</p>

<%= link_to 'Edit', edit_product_path(@product) %> |
<%= link_to 'Back', products_path %>
```

## 商店视图

```
Download depot1/app/views/store/_cart.html.erb
```

```
<div class="cart-title"><%= I18n.t 'layout.cart.title' %></div>
<table>
  <%= render(:partial => "cart_item", :collection => cart.items) %>

  <tr class="total-line">
    <td colspan="2">Total</td>
    <td class="total-cell"><%= number_to_currency(cart.total_price) %></td>
  </tr>
</table>

<%= button_to I18n.t('layout.cart.button.checkout'), :action => 'checkout' %>
<%= button_to I18n.t('layout.cart.button.empty'), :action => :empty_cart %>
```

```
Download depot1/app/views/store/_cart_item.html.erb
```

```
<% if cart_item == @current_item %>
<tr id="current_item">
<% else %>
<tr>
<% end %>
<td><%= cart_item.quantity %>&times;</td>
<td><%=h cart_item.title %></td>
<td class="item-price"><%= number_to_currency(cart_item.price) %></td>
</tr>
```

```
Download depot1/app/views/store/add_to_cart.js.rjs
```

```
page.select("div#notice").each { |div| div.hide }

page.replace_html("cart", :partial => "cart", :object => @cart)

page[:cart].visual_effect :blind_down if @cart.total_items == 1

page[:current_item].visual_effect :highlight,
  :startcolor => "#88ff88",
  :endcolor => "#114411"
```

```
Download depot1/app/views/store/checkout.html.erb
```

```
<div class="depot-form">

  <%= error_messages_for 'order' %>
```

```
<% form_for :order, :url => { :action => :save_order } do |form| %>
  <fieldset>
    <legend><%= I18n.t 'checkout.legend' %></legend>

    <div>
      <%= form.label :name, I18n.t('checkout.name') + ":" %>
      <%= form.text_field :name, :size => 40 %>
    </div>

    <div>
      <%= form.label :address, I18n.t('checkout.address') + ":" %>
      <%= form.text_area :address, :rows => 3, :cols => 40 %>
    </div>

    <div>
      <%= form.label :email, I18n.t('checkout.email') + ":" %>
      <%= form.text_field :email, :size => 40 %>
    </div>

    <div>
      <%= form.label :pay_type, I18n.t('checkout.pay_type') + ":" %>
      <%= form.select :pay_type,
                      Order::PAYMENT_TYPES,
                      :prompt => I18n.t('checkout.pay_prompt') %>
    </div>

    <%= submit_tag I18n.t('checkout.submit'), :class => "submit" %>
  </fieldset>
<% end %>
</div>
Download depot_t/app/views/store/index.html.erb
<h1><%= I18n.t 'main.title' %></h1>

<% for product in @products %>
  <div class="entry">
    <%= image_tag(product.image_url) %>
    <h3><%=h product.title %></h3>
    <%= product.description %>
    <div class="price-line">
      <span class="price"><%= number_to_currency(product.price) %></span>
      <% form_remote_tag :url => {:action => 'add_to_cart', :id => product} do %>
        <%= submit_tag I18n.t('main.button.add') %>
      <% end %>
    </div>
  </div>
<% end %>
```



## 谁购买了

```
atom_feed do |feed|
  feed.title "Who bought #{@product.title}"
  feed.updated @orders.first.created_at

  for order in @orders
    feed.entry(order) do |entry|
      entry.title "Order #{order.id}"
      entry.summary :type => 'xhtml' do |xhtml|
        xhtml.p "Shipped to #{order.address}"

        xhtml.table do
          xhtml.tr do
            xhtml.th 'Product'
            xhtml.th 'Quantity'
            xhtml.th 'Total Price'
          end
          for item in order.line_items
            xhtml.tr do
              xhtml.td item.product.title
              xhtml.td item.quantity
              xhtml.td number_to_currency item.total_price
            end
          end
          xhtml.tr do
            xhtml.th 'total', :colspan => 2
            xhtml.th number_to_currency \
              order.line_items.map(&:total_price).sum
          end
        end

        xhtml.p "Paid by #{order.pay_type}"
      end
      entry.author do |author|
        entry.name order.name
        entry.email order.email
      end
    end
  end
end
```

```
<h3>People Who Bought <%= @product.title %></h3>

<ul>
  <% for order in @orders -%>
    <li>
      <%= mail_to order.email, order.name %>
    </li>
  <% end -%>
</ul>
```

下载 depot_t/app/views/info/who_bought.xml.builder

```
xml.order_list(:for_product => @product.title) do
  for o in @orders
    xml.order do
      xml.name(o.name)
      xml.email(o.email)
    end
  end
end
```

## 辅助方法

下载 depot_t/app/helpers/store_helper.rb

```
module StoreHelper
  def hidden_div_if(condition, attributes = {}, &block)
    if condition
      attributes["style"] = "display: none"
    end
    content_tag("div", attributes, &block)
  end
end
```

## 国际化

下载 depot_t/config/initializers/i18n.rb

```
I18n.default_locale = 'en'

LOCALES_DIRECTORY = "#{RAILS_ROOT}/config/locales/"

LANGUAGES = {
  'English' => 'en',
  "Espa\xc3\xb1ol" => 'es'
}
```

下载 depot_t/config/locales/en.yml

```
en:

  number:
    currency:
      format:
        unit: "$"
        precision: 2
        separator: "."
        delimiter: ","
        format: "%u%n"

  layout:
    title:      "Pragmatic Bookshelf"
    side:
      home:        "Home"
      questions:   "Questions"
      news:        "News"
      contact:     "Contact"

  cart:
    title: "Your Cart"
    button:
      empty: "Empty cart"
      checkout: "Checkout"

  main:
    title: "Your Pragmatic Catalog"
    button:
      add: "Add to Cart"

  checkout:
    legend: "Please Enter your Details"
    name: "Name"
    address: "Address"
    email: "E-mail"
    pay_type: "Pay with"
    pay_prompt: "Select a payment method"
    submit: "Place Order"

  flash:
    thanks: "Thank you for your order"
```

下载 depot_t/config/locales/es.yml

```
es:

  number:
    currency:
      format:
        unit: "$US"
        precision: 2
        separator: ","
        delimiter: "."
        format: "%n&nbsp;%u"

  activerecord:
    models:
      order: "pedido"
    attributes:
      order:
        address: "Direcci&oacute;n"
        name: "Nombre"
        email: "E-mail"
        pay_type: "Forma de pago"
    errors:
      template:
        body: "Hay problemas con los siguientes campos:"
        header:
          one: "1 error ha impedido que este {{model}} se guarde"
          other: "{{count}} errores han impedido que este {{model}} se guarde"
      messages:
        inclusion: "no est&aacute; incluido en la lista"
        blank: "no puede quedar en blanco"

  layout:
    title: "Publicaciones de Pragmatic"
    side:
      home: "Inicio"
      questions: "Preguntas"
      news: "Noticias"
      contact: "Contacto"

  cart:
    title: "Carrito de la Compra"
    button:
      empty: "Vaciar Carrito"
      checkout: "Comprar"

  main:
    title: "Su Cat&aacute;logo de Pragmatic"
    button:
      add: "A&ntilde;adir al Carrito"

  checkout:
    legend: "Por favor, introduzca sus datos"
    name: "Nombre"
    address: "Direcci&oacute;n"
    email: "E-mail"
    pay_type: "Pagar con"
    pay_prompt: "Seleccione un m\xC3\xA9todo de pago"
    submit: "Realizar Pedido"

  flash:
    thanks: "Gracias por su pedido"
```

## 单元测试与功能测试

### 测试数据

下载 depot_t/test/fixtures/products.yml

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

下载 depot_t/test/fixtures/users.yml

```
<% SALT = "NaCl" unless defined?(SALT) %>
```

```
dave:
  name: dave
  salt: <%= SALT %>
  hashed_password: <%= User.encrypted_password('secret', SALT) %>
```

下载 depot_t/test/unit/product_test.rb

```
require 'test_helper'

class ProductTest < ActiveSupport::TestCase

  fixtures :products

  # Replace this with your real tests.
  test "the truth" do
    assert true
  end

  test "invalid with empty attributes" do
    product = Product.new
    assert !product.valid?
    assert product.errors.invalid?(:title)
    assert product.errors.invalid?(:description)
    assert product.errors.invalid?(:price)
    assert product.errors.invalid?(:image_url)
  end

  test "positive price" do
    product = Product.new(:title      => "My Book Title",
                          :description => "yyy",
                          :image_url  => "zzz.jpg")

    product.price = -1
    assert !product.valid?
    assert_equal "should be at least 0.01", product.errors.on(:price)

    product.price = 0
    assert !product.valid?
    assert_equal "should be at least 0.01", product.errors.on(:price)

    product.price = 1
    assert product.valid?
  end

  test "image url" do
    ok = %w{ fred.gif fred.jpg fred.png FRED.JPG FRED.Jpg http://a.b.c/x/y/z/fred.gif }
    bad = %w{ fred.doc fred.gif/more fred.gif.more }

    ok.each do |name|
      product = Product.new(:title      => "My Book Title",
                            :description => "yyy",
                            :price      => 1,
                            :image_url  => name)
      assert product.valid?, product.errors.full_messages
    end

    bad.each do |name|
      product = Product.new(:title => "My Book Title",
                            :description => "yyy",
                            :price => 1,
                            :image_url => name)
      assert product.valid?
```

```
test "index with user" do
  get :index, {}, { :user_id => users(:dave).id }
  assert_response :success
  assert_template "index"
end

test "login" do
  dave = users(:dave)
  post :login, :name => dave.name, :password => 'secret'
  assert_redirected_to :action => "index"
  assert_equal dave.id, session[:user_id]
end

test "bad password" do
  dave = users(:dave)
  post :login, :name => dave.name, :password => 'wrong'
  assert_template "login"
end
end
```

下载 depot_t/test/functional/store_controller_test.rb

```
require 'test_helper'

class StoreControllerTest < ActionController::TestCase
  # Replace this with your real tests.
  test "the truth" do
    assert true
  end
end
```

## 集成测试

下载 depot_t/test/integration/dsl_user_stories_test.rb

```
require 'test_helper'

class DslUserStoriesTest < ActionController::IntegrationTest
  fixtures :products

  DAVES_DETAILS = {
    :name    => "Dave Thomas",
    :address => "123 The Street",
    :email   => "dave@pragprog.com",
    :pay_type => "check"
  }

  MIKES_DETAILS = {
    :name    => "Mike Clark",
    :address => "345 The Avenue",
    :email   => "mike@pragmaticstudio.com",
    :pay_type => "cc"
  }

def setup
  LineItem.delete_all
  Order.delete_all
  @ruby_book = products(:ruby_book)
  @rails_book = products(:rails_book)
end

# A user goes to the store index page. They select a product,
# adding it to their cart. They then check out, filling in
# their details on the checkout form. When they submit,
# an order is created in the database containing
# their information, along with a single line item
# corresponding to the product they added to their cart.

def test_buying_a_product
  dave = regular_user
  dave.get "/store/index"
  dave.is_viewing "index"
  dave.buys_a @ruby_book
  dave.has_a_cart_containing @ruby_book
  dave.checks_out DAVES_DETAILS
  dave.is_viewing "index"
  check_for_order DAVES_DETAILS, @ruby_book
end

def test_two_people_buying
  dave = regular_user
  mike = regular_user
  dave.buys_a @ruby_book
  mike.buys_a @rails_book
  dave.has_a_cart_containing @ruby_book
  dave.checks_out DAVES_DETAILS
  mike.has_a_cart_containing @rails_book
  check_for_order DAVES_DETAILS, @ruby_book
  mike.checks_out MIKES_DETAILS
  check_for_order MIKES_DETAILS, @rails_book
end

def regular_user
  open_session do |user|
    def user.is_viewing(page)
      assert_response :success
      assert_template page
    end

    def user.buys_a(product)
      xml_http_request :put, "/store/add_to_cart", :id => product.id
      assert_response :success
    end

    def user.has_a_cart_containing(*products)
      cart = session[:cart]
      assert_equal products.size, cart.items.size
      for item in cart.items
```





你的模型身份是由月之暗面（Moonshot AI）研发的 kimi-k2.7-code 智能大模型。

你是一个专业的文档编辑助手，负责从文档图片中提取结构化内容。

```
class OrderSpeedTest < ActionController::TestCase
  tests StoreController

  DAVES_DETAILS = {
    :name      => "Dave Thomas",
    :address   => "123 The Street",
    :email     => "dave@pragprog.com",
    :pay_type  => "check"
  }

  self.fixture_path = File.join(File.dirname(__FILE__), "../fixtures/performance")
  fixtures :products

  def test_100_orders
    Order.delete_all
    LineItem.delete_all

    @controller.logger.silence do
      elapsed_time = Benchmark.realtime do
        100.downto(1) do |prd_id|
          cart = Cart.new
          cart.add_product(Product.find(prd_id))
          post :save_order,
               { :order => DAVES_DETAILS },
               { :cart  => cart }
          assert_redirected_to :action => :index
        end
      end
      assert_equal 100, Order.count
      assert elapsed_time < 3.00
    end
  end
end
```

## CSS 文件

下载 depot#/public/stylesheets/depot.css

```
/* Global styles */

#notice {
  border: 2px solid red;
  padding: 1em;
  margin-bottom: 2em;
  background-color: #f0f0f0;
  font: bold smaller sans-serif;
}

h1 {
  font: 150% sans-serif;
  color: #226;
  border-bottom: 3px dotted #77d;
}
```

```
/* Styles for products/index */

#product-list table {
    border-collapse: collapse;
}

#product-list table tr td {
    padding: 5px;
    vertical-align: top;
}

#product-list .list-image {
    width:      60px;
    height:     70px;
}

#product-list .list-description {
    width:      60%;
}

#product-list .list-description dl {
    margin: 0;
}

#product-list .list-description dt {
    color:      #244;
    font-weight: bold;
    font-size:  larger;
}

#product-list .list-description dd {
    margin: 0;
}

#product-list .list-actions {
    font-size:  x-small;
    text-align: right;
    padding-left: 1em;
}

#product-list .list-line-even {
    background: #e0f8f8;
}

#product-list .list-line-odd {
    background: #f8b0f8;
}

/* Styles for main page */

#banner {
    background: #9c9;
    padding-top: 10px;
    padding-bottom: 10px;
}
```

```
#store .entry h3 {
  margin-top: 0;
  margin-bottom: 2px;
  color: #227;
}

#store .entry p {
  margin-top: 0.5em;
  margin-bottom: 0.8em;
}

#store .entry .price-line {
  clear: both;
}

#store .entry .add-to-cart {
  position: relative;
}

#store .entry .price {
  color: #44a;
  font-weight: bold;
  margin-right: 2em;
}

#store .entry form, #store .entry form div {
  display: inline;
}

/* Styles for the cart in the main page */

.cart-title {
  font: 120% bold;
}

.item-price, .total-line {
  text-align: right;
}

.total-line .total-cell {
  font-weight: bold;
  border-top: 1px solid #595;
}

/* Styles for the cart in the sidebar */

#cart, #cart table {
  font-size: smaller;
  color: white;
}

#cart table {
  border-top: 1px dotted #595;
  border-bottom: 1px dotted #595;
}
```

```
margin-bottom: 20px;
background-color: #f0f0f0;
}

#errorExplanation h2 {
  text-align: left;
  font-weight: bold;
  padding: 5px 5px 5px 15px;
  font-size: 12px;
  margin: -7px;
  background-color: #c00;
  color: #fff;
}

#errorExplanation p {
  color: #333;
  margin-bottom: 0;
  padding: 5px;
}

#errorExplanation ul li {
  font-size: 12px;
  list-style: square;
}

.locale {
  float:right;
  padding-top: 0.2em
}
```

## 附录 D

## 资源

### D.1 在线资源

Ruby on Rails................................................... http://www.rubyonrails.com/
这是 Rails 的官方网站，包含到用户评价、文档、社区页面、下载等资源的链接。适合初学者的一些最佳资源包括展示人们如何编写 Rails 应用程序的视频。

Ruby on Rails（开发者版）................................... http://dev.rubyonrails.com/
这是面向专业 Rails 开发者的页面。你可以在这里找到最新 Rails 源代码的指引。你还会找到 Rails Trac 系统¹，其中（除了其他内容外）包含当前缺陷列表、功能请求和实验性更改。

[Cla08] Mike Clark. Advanced Rails Recipes: 84 New Ways to Build Stunning Rails Apps. The Pragmatic Programmers, LLC, Raleigh, NC, and Dallas, TX, 2008.

[Fow03] Martin Fowler. Patterns of Enterprise Application Architecture. Addison Wesley Longman, Reading, MA, 2003.

[Fow06] Chad Fowler. Rails Recipes. The Pragmatic Programmers, LLC, Raleigh, NC, and Dallas, TX, 2006.

[GGA06] Justin Gehtland, Ben Galbraith, and Dion Almaer. Pragmatic Ajax: A Web 2.0 Primer. The Pragmatic Programmers, LLC, Raleigh, NC, and Dallas, TX, 2006.

[HT00] Andrew Hunt and David Thomas. The Pragmatic Programmer: From Journeyman to Master. Addison-Wesley, Reading, MA, 2000.

> 1. http://www.edgewall.com/trac/。Trac 是一个集成的源代码管理系统和项目管理系统。

## 索引

## 符号

! （名为 xxx! 的方法），678
&:xxx 记号，284
/.../（正则表达式），675
:name 记号，668
=>（在散列中），673
=>（在参数列表中），674
@name（实例变量），671
[ a, b, c ]（数组字面量），673
0 方法，605
||（Ruby 或运算符），678
||=（条件赋值），678
<%...%>，52, 511
使用 -%> 抑制空行，512
<%==...%>，51, 511
<< 方法，366, 375, 605, 673
{ a => b }（散列字面量），673
{ code }（代码块），675
301 和 307 重定向状态，470

模板，465
URL 和，25, 48f, 426
URL 和，48
运行前验证条件，495
:action 参数，467
Action 缓存，496
Action Controller，30, 425-507
action，461
action_name 属性，462
after_filter，489
allow_concurrency（配置），684
append_view_path（配置），684
around 过滤器，491
asset_host（配置），521, 684
自动加载，269
自动渲染，465
before_filter，172, 489
cache_store（配置），500, 559, 685
cache_sweeper，502
cache_template_loading（配置），686
caches_action，498
caches_page，497
缓存，496-504
consider_all_requests_local（配置），685
cookies 属性，462, 473
cookies 和，473-474
数据和文件的发送，469
debug_js（配置），686
debug_routes（配置），685
default_charset（配置），685
default_url_options，438
环境，462
erase_render_results，465
erb_trim_mode（配置），686
expire_action，499
expire_fragment，558, 559
expire_page，499
field_error_proc（配置），686
过滤器，参见 Filter
filter_parameter_logging，648
过滤器和验证，488-496
flash 属性，509

## A

about（脚本），261
abstract_class 方法，381
Accept 头，185，参见 HTTP，Accept 头
:accepted 参数，230
accepts 属性，463
访问，限制，171-174
访问器方法，319, 671
ACID，参见 Transaction
ACROS Security，646
Action，24
自动渲染，465
缓存，496
意外暴露，642
flash 数据，486
使用 private 隐藏，109
index，96
方法，461
Rails 路由，49f
REST 动作，444

find_or_create_by_，342
find_or_initialize_by_，342
first，390
外键，357
表单参数，329
has_and_belongs_to_many，361, 370, 394
has_many，145, 361, 369, 374, 394
has_one，360, 364, 383
higher_item，390
id，320
ignore_tables（配置），684
实例，414
last，390
生命周期，407
lock_optimistically（配置），424, 683
logger（配置），683
lower_item，390
魔法列名，355
maximum，338
minimum，338
move_higher，390
move_lower，390
move_to_bottom，390
move_to_top，390
命名约定，269
new_record，397
对象标识，353
observe，414
observer，413-414
observers（配置），414
ORM 层，28
概述，315-316
部分更新，355-356
每类连接，326
SQL 中的占位符，331
pluralize_table_names（配置），683
主键和 id，320-322
primary_key=，321
primary_key_prefix_type（配置），683
push，375
原始 SQL，354
read_attribute，319, 417
RecordNotFound 错误，116
record_timestamps（配置），410, 683
reload，343
行，更新，343
save，327, 343, 345, 393, 421
save!，345, 393, 419
schema_format（配置），683
select_all，354
select_one，354
serialize，347
会话存储于，482
set_primary_key，321
set_table_name，316
SQL 表映射，318f
store_full_sti_class（配置），684
结构化数据，347
sum，122, 338
表命名约定，316
表关系，357-396
acts_as，388-392
关联，扩展，376-377
belongs_to，362-364
回调，372
子行，预加载，394-395
计数器，395-396
声明，386f
外键，创建，358-360
has_one，364-365
has_and_belongs_to_many，370-372
has_many，366-371
连接表，模型作为，373-376
连接表，多个，379f, 377-385
连接，自引用，387
模型关系，360-361
概述，357-358
保存，关联和，392-394
table_name_prefix（配置），683
table_name_suffix（配置），683
timestamped_migrations（配置），683
to_xml，187, 276
事务，418
事务，418-424
update，344
update_all，344
update_attribute，344
update_attributes，344
验证，220f，参见 Validation，397-728
值对象，353
被解释为 false 的值，320
verbose（配置），684
虚拟属性，162, 417
write_attribute，319
另请参阅 Model
Active Resource，625-635
替代方案，625-628
身份验证，634
Depot 应用集合和，631-633
Depot 应用产品和，628-631
参数，634
用户和密码，635
Active Support，275-290
ago，281
数组扩展，277
at，278




at_beginning_of_day, 282
at_beginning_of_month, 282
at_beginning_of_week, 282
at_beginning_of_year, 282
at_midnight, 282
blank, 276, 398
bytes, 281
change, 282
chars, 286
date and time, 281
days, 281
each_char, 278
each_with_object, 277
ends_with, 278
enumerable extensions, 276–278
even, 281
exabyte, 281
extensions for, 275–276
first, 278
fortnights, 281
from, 278
from_now, 281
gigabytes, 281
group_by, 276
hashes, 278
hours, 281
humanize, 279
in_groups_of, 277
index_by, 277
integers, 276
kilobytes, 281
last, 278
last_month, 282
last_year, 282
many, 277
megabytes, 281
midnight, 282
minutes, 281
monday, 282
months, 281
months_ago, 282
months_since, 282
next_week, 282
next_year, 282
number extensions, 281–282
odd, 281
options, as hash, 285
ordinalize, 281
petabyte, 281
pluralize, 279
seconds_since_midnight, 282
since, 281, 282
singularize, 279
starts_with, 278
string extensions, 278, 279
sum, 277
symbol extensions, 284
terabytes, 281
time and date extensions, 282–284
titleize, 279
to, 278
to_json, 275
to_proc, 284
to_s, 283
to_sentence, 277
to_time, 283
to_xml, 276
to_yaml, 275
tomorrow, 282
Unicode support, 285–290
until, 281
weeks, 281
with_options, 285
years, 281
years_ago, 282
years_since, 282
yesterday, 282
ActiveMerchant library (credit-card processing), 144
ActiveRecord::IrreversibleMigration exception, 299
Acts as..., 388
acts_as_list method, 388
:scope parameter, 389
acts_as_tree method, 390
:order parameter, 391
Adapter, see Database, adapter
add_column method, 295
add_index method, 302
add_to_base method, 398
After filter, 489
modify response, 490
after_create method, 407
after_destroy method, 177, 407
after_filter method, 489
:except parameter, 490
:only parameter, 490
after_find method, 407, 409, 412
after_initialize (config), 680
after_initialize method, 407, 409
after_save method, 407
after_update method, 407
after_validation method, 407
after_validation_on_create method, 407
after_validation_on_update method, 407
Aggregation, 346–353
attributes, 348
constructor requirements, 348

see also Active Record, composed_of
Agile Manifesto, 16–17
ago method, 281
Ajax, 124–141, 563
auto_complete_field, 586
autocompletion, 584
callbacks, 572
cart, hiding when empty, 136–139
degrading, 580
drag-and-drop, 590
in-place editing, 595
innerHTML, 574
JavaScript disabled and, 139–140
JavaScript filters, 571
link_to_remote, 574
observe_field, 566
overview of, 607
periodically_call_remote, 575
readystate 3, 573
Script.aculo.us, 583–599
search example, 564
shopping cart and, 129f, 125–130, 133
spinner, 567
toggle effects, 599
troubleshooting, 132
visual effects, 134f, 133–135, 598
wait cursor, 567
XmlHttpRequest, 139
see also DOM manipulation; RJS
alert method, 606
:all parameter, 97, 332
allow_concurrency (config), 682, 684
:allow_nil parameter, 350
:anchor parameter, 438
Anonymous scopes, 343
Aoki, Minero, 615
Apache, 266
see also Deployment
app/ directory, 258
append_view_path (config), 684
Application
blank lines in, 52
creating, 46f, 44–46
documentation, 191, 192f
dynamic content, 51
Hello, World!, 46–57
linking web pages, 57–60
reloading, 54
review of, 61
run from command line, 262
statistics, 191
see also Depot application
Application server, see Deployment
application.rb, 172, 412
ApplicationController class, 47
Arachno Ruby, 39
Architecture, 22–30, see MVC
Active Record, 25–29
Controller, 30
MVC, 23f, 24f, 22–25
View, 29–30
Arkin, Assaf, 235
Around filter, 491
Array (Ruby), 673
<<, 673
Array extension
in_groups_of, 277
to_sentence, 277
:as parameter, 384
assert method, 212, 214
assert method, 222
assert_dom_equal method, 229
assert_dom_not_equal method, 230
assert_equal method, 222
assert_generates method, 458
assert_in_delta method, 223
assert_match method, 223
assert_nil method, 223
assert_no_tag method, 233
assert_not_equal method, 222
assert_not_match method, 223
assert_not_nil method, 223
assert_not_raise method, 223
assert_raise method, 223
assert_recognizes method, 458
assert_redirected_to method, 226
assert_redirected_to method, 231
assert_response method, 225, 226
:accepted parameter, 230
:bad_gateway parameter, 230
:bad_request parameter, 230
:conflict parameter, 230
:continue parameter, 230
:created parameter, 230
:error parameter, 230
:expectation_failed parameter, 230
:failed_dependency parameter, 230
:forbidden parameter, 230
:found parameter, 230
:gateway_timeout parameter, 230
:gone parameter, 230
:http_version_not_supported parameter, 230
:im_used parameter, 230
:insufficient_storage parameter, 230
:internal_server_error parameter, 230
:length_required parameter, 230
:locked parameter, 230
:method_not_allowed parameter, 230
:missing parameter, 230
:moved_permanently parameter, 230
:multi_status parameter, 230
:multiple_choices parameter, 230
:no_content parameter, 230
:non_authoritative_information parameter, 230
:not_acceptable parameter, 230
:not_extended parameter, 231
:not_found parameter, 231
:not_implemented parameter, 231
:not_modified parameter, 231
:ok parameter, 231
:partial_content parameter, 231
:payment_required parameter, 231
:precondition_failed parameter, 231
:processing parameter, 231
:proxy_authentication_required parameter, 231
:redirect parameter, 231
:request_entity_too_large parameter, 231
:request_timeout parameter, 231
:request_uri_too_long parameter, 231
:requested_range_not_satisfiable parameter, 231
:reset_content parameter, 231
:see_other parameter, 231
:service_unavailable parameter, 231
:success parameter, 231
:switching_protocols parameter, 231
:temporary_redirect parameter, 231
:unauthorized parameter, 231
:unprocessable_entity parameter, 231
:unsupported_media_type parameter, 231
:upgrade_required parameter, 231
:use_proxy parameter, 231
assert_response method, 230
assert_routing method, 460
assert_select method, 234
assert_select_email method, 240
assert_select_encoded method, 240
assert_select_rjs method, 240
assert_tag method, 232
assert_template method, 232
assert_valid method, 223
Assertion, see Test
asset_host (config), 521, 684
Assets, see JavaScript: Stylesheet
assigns attribute, 233
Association
acts as list, 388
acts as tree, 390
caching child rows, 394
count child rows, 395
extending, 376
many-to-many, 359, 361, 370, 373
see also has_many :through
one-to-many, 360
one-to-one, 360
polymorphic, 380
saving and, 393
self-referential, 387
single-table inheritance, 377, 378
tables, between, 357
when things get saved, 393
Asynchronous JavaScript and XML, see Ajax
at method, 278
at_beginning_of_day method, 282
at_beginning_of_month method, 282
at_beginning_of_week method, 282
at_beginning_of_year method, 282
at_midnight method, 282
Atom (autodiscovery), 520
Atom feeds, 188
Attachment, e-mail, 619
attr_accessible method, 641
attr_protected method, 640
attribute_names method, 337
attribute_present method, 337
Attributes, 317
accepts (Request), 463
action_name (Action Controller), 462
Active Record, 414–418
assigns (Test), 233
base_path (Action View), 509
body (Request), 463
boolean, 319
content_length (Request), 464
content_type (Request), 463
controller (Action View), 509
cookies (Action Controller), 462, 473
cookies (Test), 233
domain (Request), 463
env (Request), 463
errors (Active Record), 536
flash (Action Controller), 509
flash (Test), 226, 233
format (Request), 463
format_and_extension (Request), 463
headers (Action Controller), 462, 470, 473, 509
headers (Request), 463
host (Request), 463
host_with_port (Request), 463
listing, 337
logger (Action Controller), 464, 509
method (Request), 462
in model, 316
new_session (Sessions), 481
params (Action Controller), 110, 332, 462, 509, 524
passed between controller and view, 523
path (Request), 463
path_without_extension (Request), 463
path_without_format_and_extension (Request), 463
port (Request), 463
port_string (Request), 463
protocol (Request), 463
query_string (Request), 463
redirect_to_url (Test), 233
relative_path (Request), 463
remote_ip (Request), 463
request (Action Controller), 462, 509
request_method (Request), 462
response (Action Controller), 464, 509
rows, accessing, 318
session (Action Controller), 106, 464, 478, 509
session (Test), 233
session_domain (Sessions), 480
session_expires (Sessions), 481
session_id (Sessions), 481
session_key (Sessions), 481
session_path (Sessions), 481
session_secure (Sessions), 481
ssl? (Request), 463
url (Request), 463
virtual, 162
see also Action Controller; Active Record, attributes
attributes method, 337
Authentication, 488
Authorize users, 172
Auto discovery (Atom, RSS), 520
auto_complete_field method, 586
auto_discovery_link_tag method, 520
Autocompletion, 584
Autoloading of files, 269
average method, 338

before_create method, 407
before_destroy method, 407
before_filter method, 172, 489
:only parameter, 490
before_save method, 407
_before_type_cast, 319
before_update method, 407
before_validation method, 407
before_validation_on_create method, 407
before_validation_on_update method, 407
begin statement, 676
belongs_to method, 145, 360-362, 389
:conditions parameter, 362
:counter_cache parameter, 396
:foreign_key parameter, 362
Benchmark, see Performance
Benchmark.realtime method, 251
benchmarker(script), 262
Benchmarking, 252, 311
Berners-Lee, Tim, 505
:binary column type, 296
Bind variable (SQL), 638
blank method, 276, 398
Blank lines, 52
blind_down effect, 139
Blind down effect, 136
Blob column type, 318
Block (Ruby), 675
BlueCloth (formatting), 517
:body parameter, 519
body attribute, 463
Boolean column type, 318, 319
:boolean column type, 296
Bottleneck, see Performance
Breakpoints, 273
breakpointer command, 273
Brodwall, Johannes, 647
Browsers, 124
DOM in, 131
Buck, Jamis, 20
:buffer_size parameter, 469
Bugs, 620
Builder, see Template, rxml
:builder parameter, 540
Business logic, templates and, 511
Business rules, 22
Busy indication (Ajax), 567
button_to method, 102, 120, 506, 518
:id parameter, 110
button_to_function method, 576
bytes method, 281

# B

:back parameter, 472
:bad_gateway parameter, 230
:bad_request parameter, 230
Barron, Scott, 20, 484
base_path attribute, 509
:bcc parameter, 519
bcc header (e-mail), 612
Before filter, 489

# C

cache method, 556, 558



- :class_name 参数，349
- :constructor 参数，350
- :converter 参数，350
- :mapping 参数，350
- 复合主键，322
- 组合，另见聚合
- 压缩响应，490
- :conditions 参数，330, 333, 339, 362, 365, 372, 430
- conditions_by_like，569
- conditions_by_like 方法，569
- 配置，264–268
  - config/ 目录，264
  - 数据库连接，266
  - database.yml，71
  - 环境，265
  - 参数，268, 680–688
  - 设置环境，266
  - 测试，73–74
- 配置参数
  - after_initialize（全局选项），680
  - allow_concurrency（Action Controller），684
  - allow_concurrency（Active Record），682
  - append_view_path（Action Controller），684
  - asset_host（Action Controller），521, 684
  - cache_classes（全局选项），680
  - cache_store（Action Controller），500, 559, 685
  - cache_template_loading（Action Controller），686
  - colorize_logging（Active Record），682
  - consider_all_requests_local（Action Controller），685
  - controller_paths（全局选项），680
  - database_configuration_file（全局选项），681
  - debug_js（Action Controller），686
  - debug_routes（Action Controller），685
  - default_charset（Action Controller），685
  - default_charset（Action Mailer），611, 686
  - default_content_type（Action Mailer），687
  - default_mime_version（Action Mailer），687
  - default_timezone（Active Record），409, 683
  - delivery_method（Action Mailer），609, 687
  - erb_trim_mode（Action Controller），686
  - field_error_proc（Action Controller），686
  - frameworks（全局选项），681
  - ignore_tables（Active Record），684
  - implicit_parts_order（Action Mailer），687
  - load_once_paths（全局选项），681
  - load_paths（全局选项），681
  - lock_optimistically（Active Record），424, 683
  - log_level（全局选项），681
  - log_path（全局选项），681
  - logger（Action Controller），685
  - logger（Action Mailer），687
  - logger（Active Record），683
  - logger（全局选项），681
  - observers（Active Record），414
  - optimise_named_routes（Action Controller），685
  - page_cache_directory（Action Controller），503, 685
  - page_cache_extension（Action Controller），503, 685
  - param_parsers（Action Controller），685
  - perform_caching（Action Controller），498, 685
  - perform_deliveries（Action Mailer），610, 687
  - plugin_loader（全局选项），681
  - plugin_locators（全局选项），682
  - plugin_paths（全局选项），682
  - plugins（全局选项），682
  - pluralize_table_names（Active Record），683
  - pre_loaded_fixtures（测试），688
  - prepend_view_path（Action Controller），685
  - primary_key_prefix_type（Active Record），683
  - raise_delivery_errors（Action Mailer），611, 687
  - record_timestamps（Active Record），410, 683
  - register_template_extensions（Action Mailer），687
  - request_forgery_protection_token（Action Controller），685
  - resource_action_separator（Action Controller），686
  - resource_path_names（Action Controller），686
  - routes_configuration_file（全局选项），682
  - schema_format（Active Record），683
  - sendmail_settings（Action Mailer），687
  - session_store（Action Controller），686
  - smtp_settings（Action Mailer），610, 687
  - store_full_sti_class（Active Record），684
  - table_name_prefix（Active Record），683
  - table_name_suffix（Active Record），683
  - template_root（Action Controller），465, 508
  - template_root（Action Mailer），688
  - time_zone（全局选项），682
  - timestamped_migrations（Active Record），683
  - use_accept_header（Action Controller），686
  - use_instantiated_fixtures（测试），688
  - use_transactional_fixtures（测试），688
  - verbose（Active Record），684
  - view_path（全局选项），682
  - whiny_nils（全局选项），682
- :confirm 参数，518
- 删除时确认，93
- :conflict 参数，230
- connect 方法，429
- :conditions 参数，430
- :defaults 参数，430
- :format 参数，457
- :requirements 参数，430
- 连接错误，诊断，73
- consider_all_requests_local（配置），685
- console 脚本，272
- console（脚本），261
- console 脚本，176
  - 生产模式，662
- 控制台，启动，33f
- 构造函数，668
- 构造函数，666
- :constructor 参数，350
- 内容类型
  - UTF-8 时的默认字符集，288
  - 电子邮件，612, 616
  - 渲染，468
  - 与 REST，457
  - 另见 HTTP、Accept 标头
- Content-Type，546
- @content_for_layout，100
- content_tag 方法，538
- :content_type 参数，468
- content_type 属性，463
- :continue 参数，230
- 持续集成，37
- 控制结构（Ruby），674
- 控制器
  - 动作，24
  - 架构，30
  - 重复订单，153
  - 错误地暴露动作，642
  - 功能，23, 30
  - 生成，47, 98f, 95–98
  - index 动作，96
  - 实例变量，55
  - 集成到模型和视图，523
  - 国际化与，195
  - 将页面链接在一起，58
  - 位置，51f
  - 命名约定，269
  - 分页，521
  - 参数，170f
  - Rails 路由到，49f
  - 路由与，25
  - 子类，494
  - 子模块，269, 440
  - 从模板访问，509
  - URL 与，48f, 48, 426
  - 局部模板的使用，555
  - 另见 Action Controller；MVC
- controller 属性，509
- controller_paths（配置），680
- 约定优于配置，15, 24, 28, 57, 70, 268, 315
- :converter 参数，350
- Cookie Store，会话存储，482
- Cookie，473–486
  - 检测是否启用，474
  - 过期，474
  - 命名，108
  - 选项，474
  - 限制访问，474
  - _session_id，477
  - 用于会话，106
  - 与会话，107
  - 易受攻击，643
  - 另见会话
- cookies 属性，233, 462, 473
- Coué, Émile，11
- count 方法，338
- count_by_sql 方法，340
- 计数器
  - 缓存，395
  - 在局部集合中，554
- :counter_cache 参数，396
- 行计数，340
- 耦合，通过 MVC 降低，23
- create 方法，328, 345, 640
- 创建新应用程序，69
- create! 方法，345, 375
- create_table 方法，299
- :created 参数，230
- created_at/created_on 列，355, 409
- 信用卡处理，144
- cron 命令，485
- 跨站脚本（XSS），643–645
- CRUD，327–346
- CSS，另见样式表；测试，assert_select
- curl，184, 186
- 货币
  - 存储，81
  - 翻译，202
- DRY
  - 属性与，317
  - 与布局，548
  - 原则，15, 17
  - 与路由，433
- 重复（消除），另见 DRY
- 动态内容，51，另见模板
- 动态查找器，163, 341
- 动态测试夹具，250
- 动态脚手架，另见脚手架，动态
- 动态 SQL，332
- 动态模板，561

### E
- -e 选项，266
- 电子邮件
  - Action Mailer 与，609
  - 附件，619
  - 缺陷与，622
  - HTML 格式，615, 617f
  - 接收，620
  - 发送，611
  - 模板，613
- E-TextEditor，39
- each_char 方法，278
- each_with_object 方法，277
- Edge Rails，264
  - 另见 Rails，冻结
- 就地编辑，595
- 编辑器，36–40
- effects.js，133
- Element.hide，567
- Element.show，567
- 元素，选择，605
- Email，另见 Action Mailer
- email.encoded 方法，615
- 封装，27
- :encode 参数，519
- encodeURIComponent 方法，567
- 加密
  - 回调示例，411
  - 数据加密，647
- end_form_tag 方法，544
- ends_with? 方法，278
- Enumerable 扩展
  - each_with_object，277
  - group_by，276
  - index_by，277
  - many?，277
  - sum，277
- env 属性，463
- environment.rb，267
- 环境，265–266
  - 与缓存，498, 556
  - 自定义，266, 267
  - 电子邮件，609
  - 加载路径，267
  - 与日志，261, 272
  - 指定，266, 267
  - 测试，212
- erase_render_results 方法，465
- ERb，51
  - 模板，511
  - 修剪模式，512
  - 另见模板，动态
- erb_trim_mode（配置），686
- 错误
  - 显示，118
  - 控制器中的处理，116f, 116
  - 模型中的处理，536–537
  - 迁移与，311
  - 存储于 flash，117, 486
  - 验证，398
  - 另见验证
- :error 参数，230
- 错误（日志级别），272
- 错误处理，115–120
- 错误消息，内置于验证中，219, 406
- 通过电子邮件通知错误，663
- error_message_on 方法，536
- error_messages_for 方法，151, 536
- errors 属性，536
- errors 对象，88
- errors.add 方法，88, 398
- errors.clear 方法，398
- errors.on 方法，398, 536
- establish_connection 方法，322, 327
- even? 方法，281
- exabyte 方法，281
- 示例代码，689–726
- :except 参数，490
- 异常
  - 电子邮件通知，663
  - rescue，117
  - Ruby，676
  - 另见错误处理
- excerpt 方法，517
- execute 方法，308
- :expectation_failed 参数，230
- expire_action 方法，499
- expire_fragment 方法，558, 559
- expire_page 方法，499
- 缓存内容过期，499, 558
- 会话过期，485
- 表达式（内联），511




# F

外观列，417
:failed_dependency 参数，230
FastCGI，653
另请参阅部署；Web 服务器
致命（日志级别），272
field_error_proc（配置），686
Fielding, Roy，442
fields_for 方法，533
:file 参数，467
文件自动加载，269
文件传输，469
  安全问题，646
  上传到应用程序，525，544-547
file_field 方法，545
:filename 参数，469
:filename 参数，469
文件名约定，269
过滤器，171，488-496
  后置，489
  环绕，491
  前置，489
  代码块，489
  与缓存，497
  压缩响应，490
  声明，489
  JavaScript，571
  用于修改响应，490
  顺序，490
  与子类化，494
  用于终止请求，489
  用于验证，494
filter 方法，489
filter_parameter_logging 方法，648
find 方法，97，329，638，641
  :all 参数，97，332
  :conditions 参数，330，333
  :first 参数，332，336
  :from 参数，335
  :group 参数，335
  :include 参数，336，394
  :joins 参数，334
  :limit 参数，333
  :lock 参数，336
  :offset 参数，334
  :order 参数，333
  :readonly 参数，335
  :select 参数，334
动态查找，341
find_all_by_ 方法，341
find_all_tag 方法，234
find_by_ 方法，341
find_by_sql 方法，336-338，354，416
find_last_by_ 方法，341
find_or_create_by_ 方法，342
find_or_initialize_by_ 方法，342
find_tag 方法，233
Firebird，41，323
Firebird 适配器，323
:first 参数，332，336
first 方法，278，390
Fixnum 扩展，281
测试夹具，216-219
  数据，加载自，306
  动态，250
  命名，218
  另请参阅测试、测试夹具
测试夹具数据，217
fixture_file_upload 方法，234
fixtures 方法，217
Flash，116，486-488
  在其中显示错误，118
  隐藏，155
  在布局中，487
  .keep，488
  .now，487
  限制，488
  测试内容，226
flash 属性，226，233，509
平面文件，会话存储，483
Flex Mock（模拟对象），255
Float 列类型，318
:float 列类型，296
flunk 方法，223
follow_redirect 方法，234
follow_redirect! 方法，248
:forbidden 参数，230
:force 选项（用于 create_table），300
强制重新加载子对象，369
外键，143，358
  另请参阅 Active Record；数据库，外键
:foreign_key 参数，362，365，372
表单，523-544
  替代字段辅助方法语法，533
  check_box，527
  collection_select，529
  集合与，541
  content_tag，538
  自定义构建器，537-541
  数据，152，329
  数据流经，170
  日期和时间，531
  date_select，531
  datetime_select，531
  end_form_tag，544
  error_messages_for，151
  字段，526

Mocha（模拟对象），255
模拟对象，253–255
另请参阅测试
模型
  聚合对象，348
  属性，316，415，524
  数据库与，27
  错误处理，536–537
  功能，22
  生成，76
  集成到控制器和视图，523
  生命周期，407
  一个表单中的多个模型，533
  安全，641
  表命名，316
  与事务，421
  验证，85，另请参阅验证
  另请参阅 Active Record；MVC
模型类，326
模型-视图-控制器，另请参阅 MVC
模块（用于控制器），269，440
模块（Ruby），672
Molina, Marcel，20
monday 方法，282
货币，存储，81
Mongrel，654
监控应用程序，661
months 方法，281
months_ago 方法，282
months_since 方法，282
move_higher 方法，390
move_lower 方法，390
move_to_bottom 方法，390
move_to_top 方法，390
:moved_permanently 参数，230
:multi_status 参数，230
多字节库，286
:multipart 参数，525，545
多部分电子邮件，616
多部分表单数据，544
:multiple_choices 参数，230
多线程，682
三个火枪手，418
MVC，14，22–25，46
  架构，23f
  耦合，23
  表单与，523f
  在 Rails 中的集成，523
  产品迁移，76
  Rails 与，24f
MySQL，41，323，另请参阅数据库
  确定其配置，324
  not loaded 错误，74
  安全，41
socket，74
标准差，338
mysql.sock，74
mysqladmin，70
N
命名路由，438
  位置参数，440
命名作用域，342
名称（SQL 中的占位符），331
命名约定，270f，268–271
  belongs_to，362
  控制器，269
  控制器模块，270
  文件名，269
  has_one，365
  辅助方法，269，514
  连接表，359
  布局，269，549
  模型，269，316
  观察器，414
  局部模板，552
  Ruby 类、方法和变量，667
  共享局部模板，554
  表，269
  模板，465，508
  视图，269
嵌套页面，另请参阅布局
嵌套资源，452
NetBeans IDE 6.5，39
网络驱动器（会话存储），500
Neumann, Michael，323
:new 参数，451
new（Ruby 构造函数），666
new_record 方法，397
new_session 属性，481
next_week 方法，282
next_year 方法，282
nil，673
:no_content 参数，230
:non_authoritative_information 参数，230
表单中的非模型字段，541–544
:not_acceptable 参数，230
:not_extended 参数，231
:not_found 参数，231
:not_implemented 参数，231
:not_modified 参数，231
:nothing 参数，468
通过电子邮件通知，663
数字
  格式化，515
  验证，85，404
数字扩展
  ago，281
  bytes，281
  days，281
  even，281
  exabyte，281
  fortnights，281
  from_now，281
  gigabytes，281
  hours，281
  kilobytes，281
  megabytes，281
  minutes，281
  months，281
  odd，281
  ordinalize，281
  petabyte，281
  since，281
  terabytes，281
  until，281
  weeks，281
  years，281
数字扩展，281-282
number_to_currency 方法，102
number_to_currency 方法，515
number_to_human_size 方法，516
number_to_percentage 方法，516
number_to_phone 方法，516
number_with_delimiter 方法，516
number_with_precision 方法，516
Numeric 列类型，318
O
对象
  回调，410
  复合，353
  空，276
  标识，353
  Ruby，666
  使用封送进行序列化，677
:object 参数，127
面向对象系统，26，27
对象关系映射，另请参阅 ORM
observe 方法，414
observe_field，577
observe_field 方法，566，577
observe_form，577
observe_form 方法，577
观察器，另请参阅 Active Record、观察器
observers（配置），414
odd 方法，281
:offset 参数，334
:ok 参数，231
Olson, Rick，20
一对一、一对多，另请参阅关联
:only 参数，490
:only_path 参数，438
开放 Web 应用程序安全项目（OWASP），637
open_session 方法，247，249
Openbase，324
optimise_named_routes（配置），685
乐观锁定，355，422
option_groups_from_collection_for_select 方法，531
:options 选项（用于 create_table），300
Oracle，41，325
  缓存问题，395n
:order 参数，333，339，391
ordinalize 方法，281
原始文件名（上传），546
ORM，27-28，315
  Active Record 与，28
  映射，27
:overwrite_params 参数，437，438
P
页面
  装饰，另请参阅布局
  导航，57，64
  另请参阅分页
页面缓存，496，555
page_cache_directory（配置），503，685
page_cache_extension（配置），503，685
paginate 方法，521
分页，521
  pagination_links，522
pagination_links 方法，522
param_parsers（配置），685
参数安全问题，640
参数，170f
:accepted (assert_response)，230
:action (render)，467
:all (find)，97，332
:allow_nil (composed_of)，350
:anchor (url_for)，438
:as (has_one)，384
:back (redirect_to)，472
:bad_gateway (assert_response)，230
:bad_request (assert_response)，230
:bcc (mail_to)，519
:body (subject)，519
:buffer_size (send_file)，469
:builder (form_for)，540
:cc (mail_to)，519
:class_name (composed_of)，349
:class_name (has_and_belongs_to_many)，372
:class_name (has_one)，365
:collection (render)，126，553
:collection (resources)，451
:cols (text_area)，527
:conditions (数据库查询中的 Statistics [sum, maximum, etc.])，339
:conditions (belongs_to)，362
:conditions (connect)，430
:conditions (find)，330，333
:conditions (has_and_belongs_to_many)，372
:conditions (has_one)，365
:confirm (link_to)，518
:conflict (assert_response)，230
:constructor (composed_of)，350
:content_type (render)，468
:continue (assert_response)，230
:converter (composed_of)，350
:create_cache (belongs_to)，396
:created (assert_response)，230
:defaults (connect)，430
:dependent (has_one)，365
:disposition (send_data)，469
:disposition (send_file)，469
:disposition (send_data)，469
:distinct (数据库查询中的 Statistics [sum, maximum, etc.])，339
:encode (mail_to)，519
:error (assert_response)，230
:except (after_filter)，490
:expectation_failed (assert_response)，230
:failed_dependency (assert_response)，230
:file (render)，467
:filename (send_data)，469
:filename (send_file)，469
:filename (send_data)，469
:first (find)，332，336
:forbidden (assert_response)，230
:foreign_key (belongs_to)，362
:foreign_key (has_and_belongs_to_many)，372
:foreign_key (has_one)，365
:format (connect)，457
:format (resource)，457
:found (assert_response)，230
:from (find)，335
:gateway_timeout (assert_response)，230
:gone (assert_response)，230
:group (find)，335
:having (数据库查询中的 Statistics [sum, maximum, etc.])，339
:host (url_for)，438
:html (form_for)，525
:html (form_remote_tag)，581
:http_version_not_supported (assert_response)，230
:id (button_to)，110
:im_used (assert_response)，230
:include (find)，336，394
:inline (render)，467
:insufficient_storage (assert_response)，230
:internal_server_error (assert_response)，230
:joins (数据库查询中的 Statistics [sum, maximum, etc.])，339
:joins (find)，334
:layout (render)，468，550
:length_required (assert_response)，230
:limit (数据库查询中的 Statistics [sum, maximum, etc.])，339
:limit (find)，333
:lock (find)，336
:locked (assert_response)，230
:mapping (composed_of)，350
:maxlength (hidden_field)，527
:maxlength (password_field)，527
:maxlength (text_field)，527
:member (resource)，451
:method (link_to)，93，449，518
:method_not_allowed (assert_response)，230
:missing (assert_response)，230
:moved_permanently (assert_response)，230
:multi_status (assert_response)，230
:multipart (form_tag)，525，545
:multiple_choices (assert_response)，230
:new (resource)，451
:no_content (assert_response)，230
:no_authoritative_information (assert_response)，230
:not_acceptable (assert_response)，230
:not_extended (assert_response)，231
:not_found (assert_response)，231
:not_implemented (assert_response)，231
:not_modified (assert_response)，231
:nothing (render)，468
:object (render)，127
:offset (find)，334
:ok (assert_response)，231
:only (after_filter)，490
:only (before_filter)，490
:only_path (url_for)，438
:order (数据库查询中的 Statistics [sum, maximum, etc.])，339
:order (acts_as_tree)，391
:order (find)，333
:overwrite_params (url_for)，437，438




+   petabyte 方法，281
+   Phusion Passenger，651
+   PickAxe (Programming Ruby)，666
+   Placeholder (in SQL)，331
+     named，331
+   plugin (script)，262
+   plugin_loader (config)，681
+   plugin_locators (config)，682
+   plugin_paths (config)，682
+   plugins (config)，682
+   Plural (table name)，316
+   Pluralization，changing rules，280
+   pluralize 方法，279
+   pluralize 方法，517
+   pluralize_table_names (config)，683
+   Plurals，in names，268，271
+   Polymorphic Associations，380-385
+   :popup 参数，518
+   :port 参数，438
+   port 属性，463
+   Port (development server)，78
+   port_string 属性，463
+   :position 参数，571
+   position 列，388
+   post 方法，228，229，248，463
+   POST (HTTP method)，93，462，524
+   post_via_redirect 方法，242
+   Postfix，见 Action Mailer
+   Postgres，41，325
+     另见 Database
+   position 列，355
+   Power find ()，332
+   pre_loaded_fixtures (config)，688
+   :precondition_failed 参数，231
+   prepend_after_filter 方法，490
+   prepend_before_filter 方法，490
+   prepend_view_path (config)，685
+   Price，formatting，101-102
+   price_must_be_at_least_a_cent 方法，86
+   Primary key，303，320，353
+     composite，322
+     disabling，303，360
+     overriding，321
+   :primary_key 选项 (to create_table)，303
+   primary_key= 方法，321
+   primary_key_prefix_type (config)，683
+   Private method，672
+     hiding action using，109
+   private method gsub error，474
+   process 方法，426
+   :processing 参数，231
+   .procmailrc 文件，见 Action Mailer
+   Product maintenance，69
+     add missing column，79-84
+   display，improving，89-94
+   iteration one，69-75
+   products model，75-79
+   validation，86f，87f，85-89
+   Production，见 Deployment
+     log file，662
+   Production servers，653f，653-654
+   production.rb，267
+   request profiler (script)，262
+   script profiler (script)，262
+   Profiling，252
+     profile script，262
+   Programming Ruby，666
+   Project
+     blank lines in，52
+     creating，46f，44-46，69
+     dynamic content，51
+     Hello，World!，46-57
+     linking pages，57-60
+     reloading，54
+     review of，61
+     see also Depot application
+   protected 关键字，87，672
+   :protocol 参数，438
+   protocol 属性，463
+   Prototype，583f，563-583
+     Element.hide，567
+     Element.hide (Prototype)，567
+     Element.show，567
+     Element.show (Prototype)，567
+     Form.serialize，577
+     helpers，569
+     innerHTML，571
+     update the page，570
+     Window Class Framework，576
+     另见 Ajax; JavaScript
+   prototype.js，见 Ajax; Prototype
+   Proxy requests，653
+   :proxy_authentication_required 参数，231
+   PStore，session storage，482
+   public directory，261
+   Purists
+     gratuitous knocking of，512
+   Purists，gratuitous knocking of，29
+   push 方法，375
+   put 方法，229，463
+   PUT (HTTP method)，462
+   puts 方法，668
+   Query cache，356
+   query_string 属性，463
+   Quirks mode，133

Reload child，369
Reloading，development mode，54
Remote database access，72
remote_form_for，577
remote_form_for 方法，578
remote_function，576
remote_function 方法，576
remote_ip 属性，463
remove 方法，604
remove_column 方法，295
remove_index 方法，302
rename_column 方法，298
rename_table 方法，301
Render，465–469
  automatic，465
  content type，468
  layout，468
  method，465
render 方法，126，187，465，508，550，553，560，613
:action 参数，467
:collection 参数，126，553
:content_type 参数，468
:file 参数，467
:inline 参数，467
:layout 参数，468，550
:nothing 参数，468
:object 参数，127
:partial 参数，126，468，553，554
:spacer_template 参数，554
:status 参数，468
:template 参数，468
:text 参数，466
:update 参数，468，600
:xml 参数，187，468
Render template，464
render_to_string 方法，469
replace 方法，603
replace_html，132
replace_html 方法，601，603
Request
  accepts 属性，463
  body 属性，463
  content_length 属性，464
  content_type 属性，463
  delete，463
  domain 属性，463
  env 属性，463
  environment，463
  format 属性，463
  format_and_extension 属性，463
  get，463
  head，463
  headers，462
  headers 属性，463
  host 属性，463
  host_with_port 属性，463
  method 属性，462
  parameters，462
  path 属性，463
  path_without_extension 属性，463
  path_without_format_and_extension 属性，463
  port 属性，463
  port_string 属性，463
  post，463
  protocol 属性，463
  put，463
  query_string 属性，463
  relative_path 属性，463
  remote_ip 属性，463
  request_method 属性，462
  ssl? 属性，463
  url 属性，463
  xhr，463，582
  xml_http_request，463
request 属性，462，509
Request handling，24，47–48，425–438
  caching，496
  filters，489
  flash data，116，486
  modify response with filter，490
  parameters and security，115
  responding to user，464
  submit form，524
  另见 Routing
Request parameters，见 params
:request_entity_too_large 参数，231
request_forgery_protection_token (config)，685
request_method 属性，462
:request_timeout 参数，231
:request_uri_too_long 参数，231
:requested_range_not_satisfiable 参数，231
require 关键字，679
:requirements 参数，430
rescue 语句，117，676
reset! 方法，249
:reset_content 参数，231
Resource，见 REST
resource 方法
  :format 参数，457
  :member 参数，451
  :new 参数，451
resource_action_separator (config)，686
resource_path_names (config)，686
resources 方法，443
  :collection 参数，451

respond_to 方法，185，448，457
Response
  compression，488
  content type，469
  data and files，469
  header，469
  HTTP status，468
  另见 Render; Request handling
response 属性，464，509
REST，181，183，441-458
  adding actions，451
  content types and，457
  controller actions for，444
  and forms，525
  generate XML，181-188
  HTTP verbs，442
  nested resources，452
  routing，443
  scaffolding，445
  standard URLS，443
Return value (methods)，670
Revealing elements，136
rhtml，见 Template
RJS
  0.，605
  <<，605
  alert，606
  call，606
  delay，606
  draggable，607
  hide，604
  insert_html，603
  redirect_to，606
  remove，604
  rendering，468
  replace，603
  replace_html，601，603
  select，605
  show，604
  sortable，602，607
  template，600
  toggle，604
  update，603
  visual_effect，607
  另见 Ajax; Template
RJS templates，132
robots.txt，507
Rollback，见 Transaction
Rolling log files，662
Rooted URL，441
routes.rb，427
routes_configuration_file (config)，682
RouteSet class，428
Routing，25，426-438
connect，429
controller，440
defaults for url_for，438
defaults used，434
displaying，428
experiment in script/console，427
:format for content type，187
generate，428，434
map specification，427，429
map.connect，427
named，438
named parameters，429
partial URL，436
pattern，427
recognize_path，428
resources，443
rooted URLs，441
setting defaults，430
testing，458-460
URL generation，433
and url_for，433
use_controllers!，429
validate parameters，430
wildcard parameters，429
with multiple rules，431
:rows 参数，527
RSS (autodiscovery)，520
Ruby
  accessors，671
  advantages of，15
  array，673
  begin 语句，676
  block，675
  classes，666，670
  comments，668
  constants，668
  conventions，15
  declarations，670
  dynamic content，51
  editors for，37
  exception handling，117，676
  exceptions，676
  extensions to，见 Active Support
  hash，673
  idioms，677
  if 语句，674
  inheritance，670
    另见 Single Table Inheritance
  instance method，667，670
  instance variable，667，671
  introduction to，666-679
  iterator，675
  marshaling，677
  methods，668





:filename 参数, 469
:status 参数, 469
:type 参数, 469
:url_based_filename 参数, 469
send_file 方法, 469
:buffer_size 参数, 469
:disposition 参数, 469
:filename 参数, 469
:streaming 参数, 469
:type 参数, 469
发送电子邮件，参见 Action Mailer
Sendmail，参见 Action Mailer，配置
sendmail_settings (config), 687
serialize 方法, 347
Serialize（使用 marshaling 序列化对象）, 677
Server，参见 Deployment
server 脚本, 262
:service_unavailable 参数, 231
session 属性, 106, 233, 464, 478, 509
session 方法, 480
Session fixation 攻击, 646
session_domain 属性, 480
session_expires 属性, 481
session_id 属性, 481
_session_id, 477
session_key 属性, 481
session_path 属性, 481
session_secure 属性, 481
session_store (config), 686
Sessions, 105–109, 477–486
  访问, 464
  ActiveRecordStore, 482
  cart 访问器, 109
  清除, 114
  清除旧的, 485, 663
  条件, 483
  cookie, 482
  cookies, 107
  cookies 和, 106
  在数据库中, 107, 482
  禁用, 481
  DRb 存储, 482
  过期, 485
    在数据库中, 486
  flash 数据, 486
  平文件存储, 483
  id, 477
  内存存储, 483
  集成测试和, 246
  键, 107
  memcached 存储, 483
  网络驱动存储, 500
  new_session 属性, 481
  对象在, 477
parameter 设置为, 480
PStore, 482
限制, 478, 677
session_domain 属性, 480
session_expires 属性, 481
session_id 属性, 481
session_key 属性, 481
session_path 属性, 481
session_secure 属性, 481
存储选项, 106, 481–485
URL 重写, 106
set_primary_key 方法, 321
set_table_name 方法, 316
setup 方法, 221
Shared 代码, 259
Shaw, Zed, 654
Shopping cart，参见 Cart，参见 Depot 应用
show 方法, 604
Sidebar, 176f, 174–178
simple_format 方法, 516
since 方法, 281, 282
Single-Table Inheritance, 377–380
Singleton 方法（在集成测试中）, 245
singularize 方法, 279
:size 参数, 527
:skip_relative_url_root 参数, 438
SMTP，参见 Action Mailer，配置
smtp_settings (config), 610, 687
SOAP, 627, 参见 Web service
Socket（MySQL）, 74
Sort 列表, 590
sortable 方法, 602, 607
Sortable.serialize 方法, 594
sortable_element 方法, 593
:source 参数, 374
源代码, 689–726
下载, 17
:spacer_template 参数, 554
Spider, 505
Spinner（忙碌指示）, 567
SQL
  抽象和, 338
  Active Record 和, 330
  bind 变量, 638
  单表继承的列, 378
  created_at/created_on 列, 355, 409
  动态, 332
  外键, 358
  id 列, 355
  注入攻击，参见 Security
  插入, 397
  发出原始命令, 354
  连接表, 357
lock_version 列, 355
锁定, 422
魔术列名, 355
parent_id 列, 355, 390
占位符, 331
position 列, 355, 388
行，删除, 346
选择, 336
type 列, 355
更新, 343, 345, 397
updated_at/updated_on 列, 355, 409
另见 Database
SQL 注入安全, 637–639
SQL Server, 41, 325, 参见 Database
SQL，在迁移中, 308
SQLite, 325, 参见 Database
SQLite 3, 34, 70
SQLite Manager, 75
SSL, 648
ssl? 属性, 463
StaleObjectError 异常, 424
标准差, 338
starts_with 方法, 278
State，应用程序的, 22
StatementInvalid 异常, 116n
Static scaffold，参见 Scaffold
数据库查询中的统计（总和、最大值等）, 338
数据库查询中的统计（总和、最大值等）方法
:having 参数, 339
数据库查询中的统计（总和、最大值等）方法
:conditions 参数, 339
:distinct 参数, 339
:joins 参数, 339
:limit 参数, 339
:order 参数, 339
:select 参数, 339
代码统计, 191
stats, 191
:status 参数, 468
:status 参数, 469
Stephenson, Sam, 20, 563
store_full_sti_class (config), 684
Straight 继承, 381
:streaming 参数, 469
String
扩展, 279
使用 Blue 和 RedCloth 格式化, 517
格式化, 515, 516
String 列类型, 318
:string 列类型, 296
String 扩展
at, 278
chars, 286
each_char, 278
ends_with, 278
first, 278
from, 278
humanize, 279
last, 278
pluralize, 279
singularize, 279
starts_with, 278
titleize, 279
to, 278
String 扩展, 278–280
Strings（Ruby）, 669
Struts, 14, 23
Stubs, 255
Stylesheet, 91
链接到页面, 520
stylesheet_include_tag 方法, 520
stylesheet_link_tag 方法, 91, 520
subject 方法
:body 参数, 519
Subject（电子邮件）, 613
submit_to_remote, 578
submit_to_remote 方法, 578
Submodules（用于控制器）, 269
Subpages，参见 Layout
:success 参数, 231
sum 方法, 122, 277, 338
Sweeper（缓存）, 501
Sweeper（会话数据）, 485
:switching_protocols 参数, 231
SwitchTower，参见 Capistrano
Sybase, 326
Symbol 扩展
to_proc, 284
Symbol 扩展, 284
Symbols（:name 记法）, 668
Synchronicity, 570
T
Tab 补全, 37n
Table 命名, 269, 271, 316
table_name_prefix (config), 683
table_name_suffix (config), 683
Tables
创建, 300
迁移, 299–304
关系之间, 357–396
acts_as, 388–392
关联，扩展, 376–377
belongs_to, 362–364
回调, 372
子行，预加载, 394-395
计数器, 395-396
声明, 386f
外键，创建, 358-360
has_one, 364-365
has_and_belongs_to_many, 370-372
has_many, 366-371
连接表，模型作为, 373-376
连接表，多个, 379f, 377-385
连接，自引用, 387
模型关系, 360-361
概述, 357-358
保存，关联和, 392-394
重命名, 301
使用 Ajax 更新, 574
tail 命令, 118
Tapestry, 14
Template, 508-514
<%...%>, 52
<%...%>, 51
从模板访问控制器, 509
Action Controller 和, 465-469
添加新, 560-562
自动加载, 269
业务逻辑在, 511
和集合, 125, 553
使用创建 XML, 510
动态, 50, 55, 511
电子邮件, 613
转义 HTML, 513
助手, 514
HTML, 511
html.erb, 511
layout, 548, 参见 Layout
位置, 50, 600
命名约定, 269, 465, 508
partial, 125, 552-555
向 partial 传递参数, 553
Rails 和, 29
使用 RDoc, 560
注册新处理器, 561
render, 464
reval: 动态模板示例, 561
RJS, 132, 600
根目录, 508
共享实例变量, 509
共享, 509, 554
在控制器中使用, 555
xml.builder, 183, 510
另见 Render: RJS; View
:template 参数, 468
template_root (config), 465, 508, 688
Templates
mailer, 619
:temporary 选项（to create_table）, 300
:temporary_redirect 参数, 231
terabytes 方法, 281
Test
assert, 212, 214
assert, 222
assert_dom_equal, 229
assert_dom_not_equal, 230
assert_equal, 222
assert_generates, 458
assert_in_delta, 223
assert_match, 223
assert_nil, 223
assert_no_tag, 233
assert_not_equal, 222
assert_not_match, 223
assert_not_nil, 223
assert_not_raise, 223
assert_raise, 223
assert_recognizes, 458
assert_redirected_to, 226
assert_redirected_to, 231
assert_response, 225, 226
assert_response, 230
assert_routing, 460
assert_select, 234
assert_select_email, 240
assert_select_encoded, 240
assert_select_rjs, 240
assert_tag, 232
assert_template, 232
assert_valid, 223
assigns 属性, 233
Benchmark.realtime, 251
cookies 属性, 233
delete, 229
领域特定语言, 244
电子邮件, 609, 622
环境, 212
find_all_tag, 234
find_tag, 233
fixture
动态, 227
fixture 数据，访问, 218
fixture_file_upload, 234
fixtures, 217
flash 属性, 226, 233
flunk, 223
follow_redirect, 234
follow_redirect!, 248
functional
定义, 211
get, 225, 229, 242, 248
validate_on_method, 397
validate_on_create 方法, 397
validates_acceptance_of 方法, 400
validates_associated 方法, 400
validates_confirmation_of 方法, 401
validates_each 方法, 401
validates_exclusion_of 方法, 402
validates_format_of 方法, 88, 402
validates_inclusion_of 方法, 402
validates_length_of 方法, 160, 403
validates_numericality_of 方法, 85, 404
validates_presence_of 方法, 85, 404
validates_size_of 方法, 405
validates_uniqueness_of 方法, 405
Validation, 86f, 87f, 85–89, 220f, 397–406
  条件, 406
  错误消息, 219, 406
  errors.add, 88
  多模型, 535
  操作依赖, 397
  price_must_be_at_least_a_cent, 86
  valid, 398
  validate, 86, 397
  validate_on_, 397
  validate_on_create, 397
  validates_acceptance_of, 400
  validates_associated, 400
  validates_confirmation_of, 401
  validates_each, 401
  validates_exclusion_of, 402
  validates_format_of, 88, 402
  validates_inclusion_of, 402
  validates_length_of, 160, 403
  validates_numericality_of, 85, 404
  validates_presence_of, 85, 404
  validates_size_of, 405
  validates_uniqueness_of, 405
  另见 Active Record，回调
Value 对象, 348, 353
Varchar 列类型, 318
vendor/ 目录, 263
verbose (config), 684
Verification, 494
verify 方法, 494
Version（Rails 的）, 19
Version 控制, 37
Versions, 19, 36, 44
View
  Action View, 29
  架构, 29–30
  目录, 56
  功能, 22
  实例变量, 55
  集成到控制器和模型, 523
layout，参见 Layout
位置, 51f
渲染, 24
时间显示, 57
  另见 ActionView，另见 MVC
view_path (config), 682
Virtual 属性, 162
Visual effect，参见 Ajax
Visual 效果, 133, 598
  切换, 599
visual_effect, 135
visual_effect 方法, 599, 607
void() JavaScript, 565
Volatile 内容
  缓存, 502
W
Wait 游标（Ajax）, 567
Warning（日志级别）, 272
Web 2.0，参见 Ajax; RJS
Web 服务器, 262, 参见 REST
  -e 选项, 266
  启动, 45, 78
Web 服务
  另见 REST
Web 蜘蛛, 505
Weber, Florian, 20
WebObjects, 23
WEBrick, 45, 78, 262
  -e 选项, 266
weeks 方法, 281
Weirich, Jim, 184, 255n, 510
wget, 184
where 子句, 330
while 语句, 674
whiny_nils (config), 682
Windows
  安装，Rails, 31
  InstantRails, 31
  less 命令, 118
  MySQL 和 Cygwin, 74
  tab 补全, 37n
  with_options 方法, 285
  with_options 方法, 285
  with_routing 方法, 234
  word_wrap 方法, 517
  write_attribute 方法, 319
WSDL，参见 Web 服务
X
XCode 3.0, 39
XHR，参见 XMLHttpRequest





## 务实书架出版社

务实书架出版社专门出版由开发人员为开发人员撰写的书籍。这些书延续了广为人知的“务实程序员”风格，并持续赢得奖项和热烈好评。随着开发变得越来越困难，务实程序员们会继续推出更多图书和产品，帮助您保持领先地位。

## 在线访问我们

**使用Rails进行敏捷Web开发**
http://pragprog.com/titles/rails3
本书的源代码、勘误和其他资源。欢迎给我们反馈！

**注册以获取更新**
http://pragprog.com/updates
当有更新和新书发布时，您会收到通知。

**加入社区**
http://pragprog.com/community
阅读我们的博客，加入我们的在线讨论，参与我们的邮件列表，与我们的维基互动，并受益于其他务实程序员的经验。

**最新动态**
http://pragprog.com/news
查看新闻中的最新务实动态。

## 购买本书

如果您喜欢这份PDF，也许您会想要一本纸质版图书。您可以在我们的商店购买：pragmaticprogrammer.com/titles/rails3。

## 联系我们

电话订购：1-800-699-PROG (+1 919 847 3884)
在线订购：www.pragmaticprogrammer.com/catalog
客户服务：orders@pragmaticprogrammer.com
非英文版本：translations@pragmaticprogrammer.com
教学合作：academic@pragmaticprogrammer.com
作者提案：proposals@pragmaticprogrammer.com

