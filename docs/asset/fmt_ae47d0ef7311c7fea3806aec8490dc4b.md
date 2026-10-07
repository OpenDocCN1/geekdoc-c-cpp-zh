
puts "First 20 characters of /etc/passwd"

`IO.copy_stream(io, op, 20)`

`op.close`

puts File.readlines("extract")

:

First 20 characters of extract

```
# for_fd

`IO.new` 的别名。
```

`IO.foreach(portname, separator) {line} -> nil`

`IO.foreach(portname, limit) {options} -> nil`

`IO.foreach(portname, separator, limit) {options} -> nil`
```

### # foreach

对命名 IO port 中的每一行执行 block，行由 separator 分隔。如果 separator 为 nil，则整个文件作为单个字符串传递。如果 limit 参数存在且为正，则每次迭代返回最多 limit 个字符。如果 limit 参数为负，则将忽略查找 record separator，这提高了性能。
```

`IO.foreach("testfile") { |x| puts "#{x}" }`

This is line
```

用于将参数传递给底层 open 的可选 hash。它可以包含以下一个或多个：

| key | Value(s) |
|---|---|
| encoding | 字符串，"external" 或 "external:internal" |
| mode | 传递给 open 的模式字符串 |
| open_args | 传递给 open 的数组；如果存在则被忽略 |
```

`IO.foreach("testfile", nil, mode: "rb", encoding: "ascii-8bit") do |content|`

  puts content.encoding

end

`IO.foreach("testfile", nil, open_args: ["r:iso-8859-1"]) do |content|`

  puts content.encoding

end
```
ASCII-8BIT
ISO-8859-1

### # new(int, mode) -> IO

为给定的文件描述符和模式返回 IO 对象（流）。另见 `IO#fileno` 和 `for_fd`。
```

a = `IO.new(2, "w")` # '2' 是标准错误

`STDERR.puts "Hello"`

a.puts "World"
```

Hello
World

### # IO.open(args+) -> IO

`IO.open(args+) {io|block} -> obj`

`IO.open` 创建一个 IO 对象并将 args 传递给 initialize 方法。如果没有 block，直接返回对象。如果有 block，将 IO 对象传递给 block。当 block 退出（通过异常或终止），IO 对象将被关闭。如果 block，`IO.open` 返回 block 的值。粗略实现如下：
```ruby
class IO
  def open(*args)
    file = return_value = self.new(*args)
    begin
      return_value = yield(file)
    ensure
      file.close
    end if block_given?
    return_value
  end
end
```

注意，IO 的子类如 File 可以使用 open，尽管构造函数接受不同的参数。调用 `File.open(...)` 将调用 File 的构造函数而不是 IO 的。
```

`IO.open(1, "w") do |io|`

  io.puts "Writing to stdout"

end
```

Writing to stdout
```

`File.open("testfile", mode: "r", encoding: "utf-8") do |f|`

  puts f.read
```

This is line one
This is line two
This is line three
And so on...

### # pipe

`IO.pipe -> [read_file, write_file]`

创建一个管道端点（相互连接）并作为两个元素的数组返回它们。`write_file` 会自动设置为同步模式。并非所有平台都可用。

在示例中，两个进程关闭了它们没有使用的管道端。这并不是必须的。如果任何写入者仍然打开管道，则管道的读取将不会产生文件结束条件。对于父进程，如果不先执行 `a.close`，`rd.read` 将永远不会返回。
```

rd, wr = `IO.pipe`

if fork

  wr.close

  puts "Parent got: #{rd.read}"

  rd.close

  Process.wait

else

  rd.close

  puts "Sending message to parent"

  wr.write "Hi Dad"

  wr.close

end
```
Sending message to parent
Parent got: <Hi Dad>

### # popen

`IO.popen(cmd, mode="r") -> IO`
`IO.popen(cmd, mode="r") {io|block} -> obj`

运行指定的命令作为子进程；子进程的标准输入和输出将连接到返回的 IO 对象。参数 cmd 可以是字符串或在 Ruby 1.9 中是字符串数组。后者数组被用作新进程的 argv 参数，且不对子进程进行特殊处理。此外，如果数组以 hash 开头，则 hash 将用于设置子进程的环境变量。详情见见 `Kernel#spawn`。如果 cmd 是字符串，它将受到 shell 扩展。如果 cmd 以减号 (-) 开头且操作系统支持 fork(2)，则当前进程会被 fork。新对象的默认模式为 r，但 mode 可以设置为第 547 页表 27.7 中的任何模式。

如果给了 block，Ruby 将把命令作为连接到 Ruby 的子进程运行。管道的 Ruby 端将作为参数传递给 block。在这种情况下，`IO.popen` 返回 block 的值。

如果带有 cmd_string 为 "-" 的 block，block 将两个进程中运行：一次在父进程中，一次在子进程中。父进程将管道对象作为参数传递给 block，子版本的 block 为 nil，子的标准输入输出将通过管道与父进程连接。并非所有平台都可用。另见第 783 页的 Open3 库和第 568 页的 `Kernel#exec`。

```ruby
pipe = IO.open("uname")
p(pipe.readlines)
puts "Parent is #{Process.pid}"
IO.open("date") {|pipe| puts "#{Process.pid}" here, pipe=#{pipe} }
IO.open("-") {|pipe| STDERR.puts here, pipe=#{pipe}}
Parent 84543
Apr 13 13:26:27 2009
84543 is here, pipe=#IO:0x0a2fd0
84546 is here, pipe=
```

这是一个使用 Ruby 1.9 选项将标准错误和标准输出合并到一个字符串的示例。注意，缓冲确保了错误输出会在标准输出之前返回。
```ruby
pipe = IO.open(["bc", STDERR => STDOUT], "r+")
pipe.puts '1 + 3; bad_function()'
pipe.close_write
puts pipe.readlines
```

运行时错误 (func(main), ar=8): Function bad_function not defined.

### # read

#### 1.9

打开文件，可选地跳转到指定的偏移量，并返回字节长度（默认到文件尾）。`read` 确保在返回前关闭文件。

`options` 是一个可选的哈，用于传递参数给 `read` 使用的底层 `open`。详情请参阅 `IO.foreach`。
```ruby
IO.read("testfile") # = "This is line one\ntwo\nThis is line three\nAnd so on\n..."
IO.read("testfile", 20) # = "This is line one\nThis"
IO.read("testfile", 20, 10) # = "\oneThis is line "
```

### # readlines

#### 1.9

逐行读取由路径指定的文件，并将这些行作为数组返回。行之间由分隔符分隔。如果 `separator` 为 `nil`，则整个文件将作为单个字符串传递。如果存在 `limit` 参数，则迭代时最多返回该 `limit` 行。如果给出了 `limit` 参数且该值为负数，则会在寻找记录分隔符时进行编码，这会提高性能。`options` 是一个可选的哈，用于传递参数给 `read` 使用的底层 `open`。详情请参阅 `IO.foreach`。
```ruby
IO.readlines(pathname, {:length=>>(:offset)}, (:options)) -> array
IO.readlines(pathname, limit, (:options)) -> array
IO.readlines(pathname, separator, (:options)) -> array
```

```ruby
a = IO.readlines("testfile")
a[0] # = "This is line one\n"
```

### # IO.select(read_array ( , write_array ( , error_array ( , timeout ) )) → array or nil

请参阅第 576 页的 `Kernel#select`。

### # IO.sysopen(path, , mode ( , perm )) → int

打开给定路径，返回文件描述符（作为 Fixnum）。
```ruby
IO.sysopen("testfile") # => 4
```

### # IO.try_convert( obj ) → an_io or nil

如果 `obj` 不是 I/O 对象，尝试通过调用其 `:to_io` 方法对其进行转换。如果无法进行转换，则返回 `nil`。
```ruby
class SillyIOObject
  def :to_io
    STDOUT
  end
end
```

```ruby
IO.try_convert(SillyIOObject.new) # => #IO:<STDOUT>
IO.try_convert("Shemp") # => nil
```

### # io << obj → io

字符串输出—将 `obj` 写入 `io`。`obj` 将使用 `to_s` 转换为字符串。
```ruby
STDOUT << "Hello" << "world\n"
```

产生：
Hello world

### # io.binmode → io

将 `io` 置为二进制模式。二进制模式是在打开文件时在模式字符串中使用 "b" 修饰符。读取或写入包含无效二进制序列的文件时需要二进制模式。一旦流进入二进制模式，无法重置为非二进制模式。

### # io.binmode? → true or false

如果 `io` 处于二进制模式，则返回 `true`。
```ruby
f = File.open("/etc/passwd")
f.binmode? # => false
f = File.open("/etc/passwd", "rb-binary")
f.binmode? # => true
```

### # io.bytes → enumerator

返回一个迭代 `io` 中字节（而非字符）的迭代器，并将每个字节返回为整数。另参阅 `IO#getbyte`。

### # ruby 3.1.4 ◀ 553
```ruby
file = File.open("testfile")
enum = file.bytes
enum.first(10) # => [84, 104, 105, 115, 32, 102, 115, 32, 108, 105]
```

### # chars

#### 1.9
```ruby
io.chars → enumerator
```

```ruby
file = File.open("testfile")
enum = file.chars
enum.first(7) # => ["T", "h", "i", "s", "", "i", "s"]
```

### # close

关闭 `io` 并将任何写入操作刷新到操作系统。该流无法进行任何后续操作；如果尝试操作，将抛出 `IOError`。当 I/O 流被垃圾回收器回收时会自动关闭。

### # close_on_exec?

#### 1.9
```ruby
io.close_on_exec? → true or false
```

返回 `io` 的 close exec 状态。如果不可用则报错。

### # close_on_exec=

#### 1.9
```ruby
io.close_on_exec= → true or false → nil
```

设置 `io` 的 close exec 标记。如果不可用则报错。带有此标记的 I/O 对象将在调用 `exec(2)` 后关闭。

### # close_read
```ruby
io.close_read → nil
```

关闭双工流的读端（即包含读写端的管道）。如果流不是双工，则抛出 `IOError`。
```ruby
f = IO.open("/bin/sh", "+")
f.close_read
f.readlines
```

产生：
```
prog.rb:3:in `readlines': not opened for reading (IOError)
from /tmp/prog.rb:3:in `<main>'
```

### # close_write
```ruby
io.close_write → nil
```

关闭双工流的写端（即包含读写端的管道）。如果流不是双工，则抛出 `IOError`。
```ruby
f = IO.open("/bin/sh", "+")
f.close_read
f.readlines
```

产生：
```
prog.rb:3:in `readlines': not opened for reading (IOError)
from /tmp/prog.rb:3:in `<main>'
```

### # flush

将 `io` 中的任何缓冲数据刷新到底层的操作系统（注意这仅是 Ruby 内部缓冲；操作系统也可能缓冲数据）。
`STDOUT.print "no newline"`
`STDOUT.flush`

`io.flush -> io`

产生：
no newline

### # fsync

立即将所有缓冲区数据写入 io。如果底层系统不支持 `fsync(2)`，则返回 `nil`。注意 `fsync` 与 `IO#sync` 不同。后者确保数据从 Ruby 缓冲区中刷新，但不保证底层操作系统已将其写入磁盘。

### # getbyte

`io.getbyte → fixnum or nil`

+ 1.9

从 IO 返回 8 位的字节（而非编码后的字符），或者在文件末尾返回 `nil`。另见 `IO#bytes`。
```
file = File.open("testfile")
file.getbyte => 84
file.getbyte => 104
```

### # getc

`io.getc → string or nil`

+ 1.9

从 io 获取下一个字符。如果在文件末尾调用，则返回 `nil`。
```
f = File.new("testfile")
f.getc => "\n"
f.getc => "h"
```

### # gets

`io.gets(separator=$) → string or nil`
`io.gets(limit) → string or nil`
`io.gets(limit) → string or nil`

+ 1.9

从 I/O 流中读取下一“行”；行由 separator 分隔。separator 为 `nil` 时会读取整个条目，长度为 0 的 separator 则每次读取一个输入字符（或者在输入中的两个或多个换行符会分隔段落）。如果 separator 不为 `nil`，则将整行作为单个字符串传递。如果 `limit` 参数存在且为正数，则每次迭代最多返回 `limit` 个字符。如果只给出了 `limit` 参数且该参数为负数，则在查找正确分隔符时将忽略编码，从而提高性能。读取的行将返回并赋值给 `$`（对 `$` 的设置被认为是不优雅的——未来可能会移除）。如果在文件末尾调用，则返回 `nil`。
```
file = File.new("testfile")
file.gets => "This is line one\n"
$.gets => "This is line one\n"
file.gets(10) => "*This is li"
file.gets("line") => "ne two\nThis is line"
file.gets("line", 4) => "thr"
```

### # internal_encoding

`io.internal_encoding → encoding`

+ 1.9

返回表示此 IO 对象内部编码的编码对象。
```
