

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

## 创建你自己的 Rails API 文档

你可以创建 Rails API 文档的本地合并版本。只需在命令提示符下输入以下命令（如果使用 InstantRails 或 Locomotive，请记住在 Rails 环境中启动命令窗口）：

```
rails_apps> rails dummy_app
rails_apps> cd dummy_app
dummy_app> rake rails:freeze:gems
dummy_app> rake doc:rails
```

最后一步需要一段时间。当它完成后，你将在从 doc/api 开始的目录树中拥有 Rails API 文档。我们建议将此文件夹移动到桌面，然后删除 dummy_app 树。

要查看 Rails API 文档，请用浏览器打开位置 doc/api/index.html。

## 桌面

我们不会告诉你在使用 Rails 时如何组织桌面，但我们会描述我们的做法。

大部分时间，我们都在编写代码、运行测试，并在浏览器中查看应用程序。因此，我们的主要开发桌面始终打开一个编辑器窗口和一个浏览器窗口。我们还想关注应用程序生成的日志，因此我们保持一个终端窗口打开。在其中，我们使用 tail -f 来滚动日志文件的内容，因为它在更新。我们通常以非常小的字体运行此窗口，以便占用更少的空间——如果我们看到有意思的内容闪过，我们会放大以进行调查。

我们还需要访问 Rails API 文档，我们在浏览器中查看它。在介绍中，我们谈到了使用 gem server⁵ 命令运行包含 Rails 文档的本地 Web 服务器。这很方便，但不幸的是，它将 Rails 文档分散在多个单独的文档树中。如果你在线，可以使用 http://api.rubyonrails.org 在一个地方查看所有 Rails 文档的合并视图。

## 3.7 Rails 和数据库

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

## 3.8 保持最新

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

## 3.9 Rails 和 ISP

如果你想在共享托管环境中将 Rails 应用程序上线，你需要找到一个精通 Ruby 的 ISP。寻找支持 Ruby、具有你需要的 Ruby 数据库驱动程序，并提供 Phusion Passenger 和/或

6. 较早版本的 gem 可能需要 --include-dependencies 选项。

## 第 4 章

## 即时满足

让我们编写一个简单的应用程序，以验证我们是否已在机器上稳妥地安装了 Rails。在此过程中，我们将一窥 Rails 应用程序的工作方式。

### 4.1 创建新应用程序

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

