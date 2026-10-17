
```ruby
require 'ripper'
# 此类处理解析器事件，提取
# 注释并附加到类定义上
class BabyDoc < Ripper::Filter
  def initialize()
    super
    reset_state
  end

  def on_default(event, token, output)
    reset_state
    output
  end

  def on_sp(token, output) end
  alias n_on_sp

  def on_comment(comment, output)
    @comment << comment.sub(/^\s*=\s*/, "")
    output
  end

  def on_kw(name, output)
    @expecting_class_name = (name == 'class')
    output
  end

  def on_const(name, output)
    if @expecting_class_name
      output << "#{name}:\n"
      output << @comment
    end
    reset_state
    output
  end

  private
    def reset_state
      @comment = ""
      @expecting_class_name = false
    end
end

BabyDoc.new(File.read(__FILE__)).parse(STDOUT).
```

输出：

`BabyDoc`
此类处理解析器事件，提取
注释并附加到类定义上

# RSS

## RSS Feed 的生成与解析

Rich (or RDF) Site Summary, Really Simple Syndicate——随你挑选其一即可。RSS 是互联网上传播新闻的首选协议。RSS 库支持创建和解析符合 RSS 0.9、RSS 1.0 和 RSS 2.0 的流。

- 读取并总结来自 `http://ruby-lang.org` 的最新故事：

```ruby
require 'rss/2.0'
require 'open-uri'
open('http://ruby-lang.org/feeds/news.rss') do |http|
  response = http.read
  result = RSS::Parser.parse(response, false)
  puts "Channel: " + result.title
  result.items.each_with_index do |item, i|
    puts "#{i}.#{item.title}" if i < 3
  end
end
```

输出：
Channel: Ruby News
1. MountainWest RubyConf Schedule
2. Ruby 1.9.1 released
3. Server maintenance

- 生成 RSS 信息：

```ruby
require 'rss/0.9'
rss = RSS::New("0.9")
chan = RSS::Channel.new
chan.title = "The Daily Dave"
chan.description = "Dave's Feed"
chan.language = "en-US"
chan.link = "http://pragave.pragprog.com"
rss.channel = chan
image = RSS::Channel::Image.new
image.url = "http://pragprog.com/pragave.gif"
image.title = "Pragave"
image.link = chan.link
chan.image = image
3.times do |i|
  item = RSS::Channel::Item.new
  item.title = "My News Number #{i}"
  item.link = "http://pragave.pragprog.com"
  item.description = "This is a story about #{i}"
end
rss.to_s
```

# Shellwords 使用 POSIX 语义操作 Shell 行

该模块作为 shell 命令行的字符串表示，根据 POSIX 语义将其拆分为单词标记（tokens）。同时也允许你从单个单词创建正确转义的 shell 行。

- 双引号或单引号之间的空格被视为单词的一部分。
- 双引号可以使用可以使用反斜杠进行转义。
- 否则，由空白字符分隔的标记被视为单词。

![](img/44b0533e8e4c9d6926ebd13a65acab0d_808_0.png)

```ruby
require 'shellwords'
include Shellwords
```

```
line = %(Code Ruby Be Happy!)
shellwords(line)      => ["Code", "Ruby", "Be", "Happy!"]
line = %{'Code Ruby 'Be Happy!'}
shellwords(line)      => ["Code Ruby", "Be Happy!"]
line = %q(Code\ Ruby "Be Happy")
shellwords(line)      => ["Code Ruby", "Be Happy!"]
```

`shelljoin("Code Ruby", "Be Happy")`      => Code Ruby Be Happy

此外，该库分别为 `Class` 和 `CArray` 添加了 `shellssplit` 和 `shelljoin` 方法：

![](img/44b0533e8e4c9d6926ebd13a65acab0d_808_1.png)

```ruby
require 'shellwords'
include Shellwords
```

```
%{Code\ Ruby Be Happy!}.shellssplit      => ["Code Ruby", "Be", "Happy!"]
["Code Ruby", "Be Happy"].shelljoin      => Code Ruby Be Happy
```

# Singleton (单例)

单例模式确保在程序的生命周期内，只能为特定类创建一个实例（参阅设计模式 [GHOV95]）。

`singleton` 库使得这种实现变得简单。将需要成为单例的每个类混合 `Singleton` 模块，该类的 `new` 方法将变为私有。取而代之，该类的用户调用 `instance` 方法，该方法会返回该类的单例实例。

在示例中，`MyClass` 的两个实例是同一个对象：

```ruby
require 'singleton'
class MyClass
  attr_accessor :data
  include Singleton
end
a = MyClass.instance # => #MyClass:0x128d4c
b = MyClass.instance # => #MyClass:0x128d4c
a.data = 123          # => 123
b.data               # => 123
```

# Socket (套接字)

`socket` 扩展定义了九类用于访问底层系统的 socket 级通信。这些类都是 `IO` 类的（间接）类，这意味着 `IO` 的方法可以用于 socket 连接。

socket 类的层次结构反映了网络编程的现实，因此有些令人困惑。`Basic` 类包含了所有基于 socket 连接传输的通用方法。它被细分为特定协议的实现：`IPSocket`、`UNIXSocket`（用于域接字）以及（间接的）`TCPSocket`、`UDPSocket`。

`BasicSocket` 也被 `Socket` 子类，`Socket` 是一种更通用的面向接口的网络。虽然像 `TCPSocket` 这样的类是特定协议的，但 `Socket` 对象无论什么协议都可以使用。

`TCPSocket`、`SOCKSocket` 和 `UNIXSocket` 都是面向连接的。每个类都有一个 `connection.xxxx.SocketServer` 类，该类实现了连接的服务器端。

socket 库是你永远不会直接使用的东西。如果你确实使用了它们，就需要了解细节。出于这个原因，我们在第 878 页的附录 A 中包含了涵盖 socket 库的参考章节。

以下代码显示了一个 UDP 服务器和客户端。更多示例请参阅附录 A：

- `BasicSocket`
  - `IPSocket`
    - `TCPSocket`
      - `SOCKSocket`
        - `TCPServer`
    - `UDPSocket`
  - `Socket`
  - `UNIXSocket`
    - `UNIXServer`

```ruby
# 简单日志器打印在 UDP 端口 12121 接收到的消息
require 'socket'
socket = UDSocket.new
socket.bind('127.0.0.1', 12121)
loop do
  msg, sender = socket.recvfrom(100)
  host = sender[3]
  puts "#{Time.now} '#{msg}'"
  STDOUT.flush
end
```

```ruby
# 测试日志器
require 'socket'
log = UDSocket.new
log.connect('127.0.0.1', 12121)
log.print("Up and Running!")
# process ... process ..
log.print "Done!"
```

产生输出：
2009-04-13 13:27:15 -0500: 127.0.0.1 'Up and Running!'
2009-04-13 13:27:15 -0500: 127.0.0.1 'Done!'

# StringIO

在某些方面，字符串和文件之间的区别是人为的：文件内容基本上是一个存储在磁盘上而不是内存中的字符串。`StringIO` 库统一了这两个概念，使字符串的行为得像 IO 对象一样。如果一个字符串被封装在 `StringIO` 对象中，就可以像打开的文件一样对其进行读写。这让你让测试变得更容易。它还允许将字符串传递给这些对象和方法。

## 视为 IO 对象

对字符串进行读写：

```ruby
require 'stringio'
sio = StringIO.new("hello")
puts sio.read
sio.puts("world")
puts sio.string
```

## StringIO 作为测试：

```ruby
require 'stringio'
require 'minitest/autorun'
class TestStringIO < Minitest::Test
  def test_read_write
    s = StringIO.new("hello")
    assert_equal "hello", s.read
  end
end
```

# Tempfile

`Tempfile` 类创建托管的临时文件。虽然它们的行为与任何其他 IO 对象相同，但临时文件在 Ruby 程序终止时会自动删除。一旦创建了 `Tempfile` 对象，底层文件可能会被连续打开和关闭多次。

`Tempfile` 并没有直接继承自 `IO`。相反，它将调用委托给 `File` 对象。从程序员的角度来看，除了不寻常的 `new`、`open` 和 `close` 语义外，`Tempfile` 对象的行为就像是一个 IO 对象。

如果你在创建临时文件时没有指定用于存放它们的目录，则将使用 `tmpdir` 库来查找依赖于系统的位置。

另参见：`tmpdir` (第 822 页)

```ruby
require 'tempfile'
tf = Tempfile.new('afile')
tf.path # => "/var/folders/.../-Temp/afile202090413-86464-iwdzcf-0"
tf.puts("Cosi Fan Tutte")
tf.open
tf.gets # => "Cosi Fan Tutte\n"
tf.close(true)
```

# Test::Unit

`Test::Unit` 是一个基于原始 SUnit Smalltalk 框架的单元测试框架。它提供了一个结构，可以在其中组织、选择和运行单元测试。测试可以从命令行运行，也可以使用多个基于 GUI 的界面之一运行。

第 198 页的第 13 章包含了关于 `Test::Unit` 的教程。

我们可以有一个简单的播放列表类，用于选择和检索歌曲：

```ruby
require 'code/testunit/song.rb'
require 'forwardable'
class Playlist
  extend Forwardable
  def_delegators(:list, <<, :add_song)
  def_delegators(:list, :size, :empty?)
  def initialize
    @list = []
  end
  def find(title)
    @list.find{|song| song.title == title}
  end
```

我们可以编写测试来测试这个类。`Test::Unit` 框架足够智能，在没有提供主程序的情况下，会自动运行测试类中的测试。

```ruby
require 'test/unit'
require 'code/testunit/playlist.rb'
class TestPlaylist < Test::Unit::TestCase
  def test_adding
    pl = Playlist.new
    assert_empty(pl)
    assert_nil(pl.find("My Way
```

产生：

Loaded state /tmp/prog

Started

Finished in 0.002641 seconds.

1 tests, 7 assertions, 0 failures, 0 errors, 0 skips

线程库添加了一些支持线程的实用函数和类。其中大部分内容已被 `Monitor` 类取代，但线程库仍然包含了两个非常有用的类：`Queue` 和 `SizedQueue`。它们都实现了一个线程安全的队列，可以在多个线程之间在生产者和消费者之间传递对象。`SizedQueue` 对象限制了其容量；任何尝试向达到容量的队列添加对象的生产者将被阻塞，直到消费者移除了一个对象。

- 下面的示例由 Robert Kellner 提供。它包含三个消费者从一个无限制队列中获取对象。这些对象由两个生产者产生，每个生产者添加三次。

```ruby
require 'thread'
queue = Queue.new
consumers = (1..3).map do |i|
  Thread.new("consumer #{i}") do |name|
    begin
      obj = queue.dequeue
      print "#{name}: consumed #{obj.inspect}\n"
    end until obj == :END_OF_WORK
  end
end
producers = (1..2).map do |i|
  Thread.new("producer #{i}") do |name|
    3.times do |j|
      queue.enqueue("Item #{j} from #{name}")
    end
  end
end
producers.each(&:join)
consumers.size.times { queue.enqueue(:END_OF_WORK) }
consumers.each(&:join)
```

consumer 1: consumed "Item 0 from producer 2"
consumer 1: consumed "Item 0 from producer 1"
consumer 2: consumed "Item 1 from producer 2"
consumer 1: consumed "Item 1 from producer 1"
consumer 2: consumed "Item 2 from producer 2"
consumer 3: consumed "Item 2 from producer 1"
consumer 2: consumed :END_OF_WORK
consumer 3: consumed :END_OF_WORK
consumer 1: consumed :END_OF_WORK

# ThreadsWait

`ThreadsWait` 处理一组线程对象的终止。它提供了方法允许你检查任何线程的终止情况，并等待所有线程终止。下面的示例启动了许多线程，它们在等待稍短的时间后终止。使用 `ThreadsWait`，我们可以在这些线程终止时（单独或作为一个组）捕获它们。![](img/44b0533e8e4c9d26ebd13a65ab0d_817_0.png)
