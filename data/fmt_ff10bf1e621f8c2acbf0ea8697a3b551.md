
`pages = %w(www.rubycentral.com slashdot.org www.google.com)`

`threads = []`

```ruby
for page_to_fetch in pages
  threads << Thread.new(page_to_fetch) do |url|
    h = Net::HTTP.new(url, 80)
    print "Fetching: #{url}\n"
    resp = h.get('/')
    print "Got #{url}: #{resp.message}\n"
  end
end
threads.each{|thr| thr.join }
```

产生输出：

```
Fetching: www.rubycentral.com
Fetching: slashdot.org
Fetching: www.google.com
Got www.google.com: OK
Got www.rubycentral.com: OK
Got slashdot.org: OK
```

让我们详细查看这段代码，因为其中发生着一些微妙的变化。

新线程是通过 `Thread.new` 调用创建的。它接收了一个块，该块包含了在新线程中运行的代码。在我们的案例中，该块使用 `net/http` 库从我们选定的每个站点获取第一个页面。清晰地追踪到这些抓取是并行进行的。

当我们创建线程时，我们将所需的 URL 作为参数传递。这个参数作为 `arg` 传递给块。我们为什么要这样做，而不是直接在块中使用变量 `page_to_fetch` 的值呢？

线程会共享线程启动时存在的所有全局、实例和局部变量。正如任何弟弟都能告诉你的一样，共享并不总是是好事。在这种情况下，所有线程将共享变量 `page_to_fetch`。第一个线程启动，`page_to_fetch` 被设置为 "rubycentral.com"。与此同时，创建线程的循环仍在运行。第二次时，`page_to_fetch` 被设置为 "slashdot.org"。如果第一个线程还未完成对 `page_to_fetch` 变量的处理，它将突然开始使用新值。这类 bug 很难追踪。

然而，在线程内部创建的局部变量对于线程来说是真正的局部的——每个线程都有自己的变量副本。在我们的案例中，变量将在线程创建时被设置，每个线程将拥有自己的页面详情副本。你可以通过 `Thread.new` 向块传递任意数量的参数。

这段代码还说明了如何做到。在循环内部，线程使用 `print` 来写入消息，而不是 `puts`。为什么？因为在后台，`puts` 将工作分成若干部分：它先写入参数，然后写入一个换行符。在这两者之间，线程可能会被调度，导致输出交错在一起。使用单个字符串调用 `print` 可以避免这种换行符带来的问题。

### 线程操作

我们的下载程序最后一行出现了另一个微妙之处。我们为什么要对创建的每个线程调用 `join` 呢？

当 Ruby 程序终止时，所有线程都会被杀死，无论它们的状态如何。你可以通过调用该线程的 `Thread#join` 方法来等待特定线程完成。调用的 `join` 会阻塞直到给定的线程完成。通过对每个请求线程执行 `join`，你可以确保在终止主程序之前所有请求都已完成。如果你不想永久阻塞，可以给 `join` 一个超时时间——如果超时在线程结束前过期，`join` 将返回 `nil`。`join` 的另一种变体方法 `Thread#value` 返回最后一次执行的语句的值。

除了 `join` 之外，还使用了其他方便的例程来操作线程。当前线程始终可以通过 `Thread.current` 访问。你可以使用 `Thread.list` 获取所有线程列表，它返回一个可运行或已停止的 `Thread` 对象列表。要确定特定线程的状态，可以使用 `Thread#status` 和 `Thread#?alive?`。

此外，你可以使用 `Thread#priority=` 调整线程的优先级。高优先级线程将在低优先级线程之前运行。稍后我们将讨论更多关于线程调度、启动和停止线程。

### 线程变量

线程通常可以访问创建时在作用范围内的任何变量。阻塞线程代码中的局部变量对线程是不可见的且不共享的。

但如果你需要可以被其他线程（包括主线程）访问的线程变量该怎么办？`Thread` 类提供了一个特殊机制，允许按名称创建和访问线程局部变量。你只需要将线程对象看作一个 `Hash`，使用 `[]` 写入写入元素，并使用 `[]` 读取它们。在接后的示例中，每个线程都将变量 `count` 的值记录在键为 `mycount` 的线程局部变量中。这段代码中存在竞态条件，但我们还没有讨论过同步，所以我们暂且忽略它。

> 竞态条件发生在两个或多个代码段（或硬件）访问资源时，结果取决于它们访问的顺序。在示例示例中，可能一个线程将 `mycount` 变量的值设置为 `count`，但在它有机会增加 `count` 之前，该线程被调度，另一个线程使用了相同的 `count` 值。这些问题通过同步对共享资源（如 `count` 变量）的访问来解决。

产生：

`7, 0, 8, 6, 5, 4, 1, 9, 3, 2, count = 10`

主线程等待子线程完成，然后打印每个线程捕获的 `count` 值。为了增加趣味，让每个线程在记录值之前等待随机的时间。

### 线程与异常

如果线程抛出一个未处理的异常会发生什么？这取决于 `abort_exception` 标志的设置（见第705页和705页文档）以及调试标志位。如果 `abort_exception` 为假且未启用调试标志位（默认情况），未处理的异常将直接杀死所有线程。事实上，你仍然看到其他线程的追踪。`samples_7.rb`

```ruby
threads = []
4.times do |number|
  threads << Thread.new(number) do |i|
    raise "Boom!" if i == 2
    print "#{i}\n"
  end
end
sleep 1
```

你通常不会使用 `sleep` 来等待线程终止。相反，你会使用 `join` 方法。如果你 join 一个发生了异常的线程，该异常将在调用 join 的线程中抛出。`samples_8.rb`

```ruby
threads = []
4.times do |number|
  threads << Thread.new(number) do |i|
    raise "Boom!" if i == 2
    print "#{i}\n"
  end
end
threads.each do |t|
  begin
    t.join
  rescue RuntimeError => e
    puts "Failed: #{e.message}"
  end
end
```

产生：

```
0
1
3
Failed: Boom!
```

然而，将 `abort_exception` 设置为 true 或使用 -d，未处理的异常会杀死所有线程。一旦线程2 死亡，就不会产生更多输出。

```ruby
Thread.abort_exception = true
threads = []
4.times do |number|
  threads << Thread.new(number) do |i|
    raise "Boom!" if i == 2
    print "#{i}"
  end
end
threads.each {|t| t.join}
```

产生：

```
0
1
3
prog.rb:5:in `block' in `<main>`: Boom! (RuntimeError)
```

### 互斥锁

让我们先来看一个简单的竞态条件（race condition）示例——两个线程更新同一个共享变量：

```ruby
def inc(n)
  n + 1
end
sum = 0
threads = (1..10).map do
  Thread.new do
    10_000.times do
      sum = inc(sum)
    end
  end
end
threads.each(&:join)
sum
```

产生：
`17335`

有 10 个线程，每个线程对共享变量 `sum` 递了 10000 次。然而，当它们都完成时，`sum` 的最终值远少于 100,000。显然我们存在竞态条件。

幸运的是，这很容易修复。我们可以使用内置的 `Mutex` 来同步区域——即一次只允许一个线程进入的代码区域。

`mutex` 就像那个卫生间通行证。你创建一个 `mutex` 来控制对资源的访问，并在你想使用该资源时锁定它。如果没有人锁定它，你的线程就会继续运行。如果其他人已经锁定了那个特定的 `mutex`，你的线程就会挂起，直到他们解锁。

```ruby
def inc(n)
    n + 1
end
sum = 0
mutex = Mutex.new
threads = (1..10).map do
    Thread.new do
        10_000.times do
            mutex.lock
            sum = inc(sum) # 请一次处理一个
            mutex.unlock
        end
    end
end
threads.each(&:join)
p sum
```

产生：
`100000`

这种模式非常常见，因此 `Mutex` 类提供了 `Mutex#synchronize`，它会锁定 `mutex`，运行块中的代码，然后解锁 `mutex`。这还确保了即使在锁定期间抛出异常，`mutex` 也会被解锁。

```ruby
def inc(n)
    n + 1
end
sum = 0
mutex = Mutex.new
threads = (1..10).map do
    Thread.new do
        10_000.times do
            mutex.synchronize {
                sum = inc(sum) # 请一次处理一个
            }
        end
    end
end
threads.each(&:join)
p sum
```

产生：
`100000`

有时你希望在 `mutex` 处于未锁定状态时获取其锁，但如果它已处于锁定状态，你并不希望挂起当前线程。`Mutex#try_lock` 方法正是此设计的，如果可以获取锁就获取，但如果锁已被占用则返回 `false`。

```ruby
rate_mutex = Mutex.new
exchange_rates = ExchangeRates.new
exchange_rates.update_from_online_feed
Thread.new do
  loop
    sleep 3600
    rate_mutex.synchronize do
      exchange_rates.update_from_online_feed
    end
  end
end
loop do
  print "输入货币代码和金额:"
  line = gets
  if rate_mutex.try_lock
    begin
      puts exchange_rates.convert(line)
    ensure
      rate_mutex.unlock
    end
  else
    puts "抱歉，汇率正在更新。请一分钟后再试"
  end
end
```

### 运行进程

```ruby
rate_mutex = Mutex.new
exchange_rates = ExchangeRates.new
exchange_rates.update_from_online_feed
Thread.new do
  loop
    sleep 3600
    rate_mutex.synchronize do
      exchange_rates.update_from_online_feed
    end
  end
end
loop do
  print "输入货币代码和金额:"
  line = gets
  if rate_mutex.try_lock
    begin
      puts exchange_rates.convert(line)
    ensure
      rate_mutex.unlock
    end
  else
    puts "抱歉，汇率正在更新。请一分钟后再试"
  end
end
```

### 队列与条件变量

本章中的大多数示例使用了 `mutex`。但很多时候我们需要创建多个进程。`Queue` 类是线程之间传递数据的一种线程安全方式。它是同步生产者和消费者的有用方法。

条件变量（condition variable）是一种机制，允许线程等待直到另一个线程满足某个特定条件。这通常与 `mutex` 配合使用。

### 产生新进程

在 Ruby 中产生进程的最简单方法是使用 `system` 方法。它执行命令并在命令成功时返回 `true`，否则返回 `false`。你也可以使用反引号（backticks）来捕获命令的输出：

```ruby
result = `ls`
puts result
```

`spawn` 方法是启动进程的另一种方法，但它返回进程的 PID，而不是等待它完成。

```ruby
pid = spawn("ls")
Process.wait(pid)
```

`Open3` 模块允许你运行命令并与其输入、输出和错误流交互。

```ruby
require 'open3'
stdout, stderr, status = Open3.capture3("ls")
puts stdout
```

除了打开方法外，某些平台还支持 `Kernel.fork` 和 `Kernel.exec`。许多 IO 方法以及 `Kernel.open` 的命名规范在将文件名的第一个字符设为 `/` 时，也会创建子进程（详情请参见第 546 页的 `IO` 类介绍）。注意，你不能使用 `File.new` 创建管道；它是用于文件的。

### 独立子进程

```ruby
exec('sort testfile > output.txt') if fork.nil?
# sort 现在正在子进程中运行
### 在主程序中继续处理
# ...
# 然后等待 sort 完成
Process.wait
```

调用 `Kernel.fork` 在父进程中返回一个进程 ID，而在子进程中，子进程将执行 `Kernel.exec` 并运行 `sort`。随后，我们发出 `Process.wait`，等待 `sort` 完成（返回其进程 ID）。

```ruby
trap('CHLD') do
  pid = Process.wait
  puts "Child #{pid} terminated"
end
fork { exec('sort testfile > output.txt') }
# 执行其他事情...
```

`processes:`  
`Child 83170: terminated`

有关关于使用和控制外部程序的更多信息，请参阅 `Kernel.open`、`IO.open` 的文档以及第 641 页的 `Process` 模块章节。

### 块与子进程
