

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

## Comparing Session Storage Options

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

## Session Expiry and Cleanup

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

## 22.3 Flash: Communicating Between Actions

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

