
```
:Hello.downcase # => hello
:"HELLO WORLD".downcase # => "hello world"
:"123ABC".downcase # => "123abc"
```

# empty?

`sym.empty` → true or false

- 1.9 如果 `sym` 的字符串表示为空，则返回 true。

```
:hello.empty? # => false
:""empty? # => true
```

# encoding

`sym.encoding` → enc

- 1.9 返回 `sym` 的编码。

```
# encoding: utf-8
:hello.encoding # <Encoding:ASCII>
:"dog".encoding # <Encoding:UTF-8>
```

# id2name

`sym.id2name` → string

返回 `sym` 的字符串表示。

```
:fred.id2name # => "fred"
:"99 balloons!".id2name # => "99 balloons!"
```

# inspect

`sym.inspect` → string

返回作为字面量的 `sym` 的字符串表示。

```
:fred.inspect # => fred
:"99 balloons!".inspect # => "99 balloons!"
```

# intern

`sym.intern` → sym

`Symbol#to_sym` 的别名。

# length

`sym.length` → int

- 1.9 返回字符串表示中的字符数量。

```
# encoding: utf-8
:dog.length # => 3
:dog.length # => 3
```

# match

`sym.match(regexp)` → int or nil

- 1.9 将符号转换为字符串并与 `regexp` 进行匹配。与 `String#match` 不同，它不支持块或 `regexp` 参数。

```
:hello.match(/(.)/) # => 2
:hello.match(/1/) => 2
```

# next

`sym.next` → symbol

- 1.9 `Symbol#succ` 的别名。

# size

`sym.size` → int

- 1.9 `Symbol#length` 的别名。

# slice

`sym.slice(int)` → string or nil

`sym.slice(range)` → string or nil

`sym.slice(string)` → string or nil

# succ

`sym.succ` → symbol

- 1.9 使用与 `String#succ` 相同的规则返回 `sym` 的后继。

```
:abcd.succ # => :abce
:1239.succ # => :THX
:"koala".succ # => :"alb"
:"9999".succ # => :AAA00
:"***".succ # => "***"
```

# swapcase

`sym.swapcase` → symbol

- 1.9 返回一个所有字符交换大小的符号。

```
:Hello.swapcase # => :hELLO
:"123abc".swapcase # => :"123abc"
```

# to_proc

`sym.to_proc` → proc

- 1.9 允许在预期块时使用符号。符号作为每个参数上调用的方法。更多信息见第37页。

```
?(ant).map(:reverse) # => ["tna", "eb", "tac"]
```

# to_s

`sym.to_s` → string

`Symbol#to_sym` 的别名。

# to_sym

`sym.to_sym` → sym

符号是类符号！

# upcase

`sym.uppercase` → symbol

- 1.9 返回一个所有字符都为大写的符号。

```
:Hello.uppercase # => :HELLO
:"123ABC".uppercase # => :"123ABC"
```

# Thread < Object

`Thread` 封装了执行线程的行为，包括主线程。参见第12章从第184页开始的教程。在随后的描述中，参数指的是符号，即带引号的字符串或 `Symbol`（如 `:name`）。

# 类方法

## abort_on_exception → true or false

返回“异常时中止”条件的状态。默认值为 false。当设置为 true 或 DEBUG 标志为 true 时（因为指定了命令行选项 `-d`），如果任何线程中出异常，所有线程将中止（进程将 `exit(0)`）。参见 `Thread.abort_exception`。

## abort_on_exception=

`abort_on_exception=` → true or false

当设置为 true 时，如果出异常，所有线程将中止。返回新状态。

```
abort_on_exception = true
t1 = Thread.new do
  puts "New thread"
  raise "Exception from thread"
end
sleep(1)
puts "not reached"
```

产生：

In thread

prog.rb:4:1 block in 'main': Exception from thread (RuntimeError)

# Thread.current → thread

## current

返回当前执行的线程。

`Thread.current` # => `<Thread:0x0ac684 run`

# Thread.exclusive { block } → obj

## exclusive 1.9

执行块并返回块是否返回。内部使用 `Mutex`，以便只有一个线程可以执行代码。一次一个 `Thread.exclusive` at a time。

# Thread.exit

## exit

终止当前运行的线程并调度另一个线程运行。如果此线程已被标记为杀死，`exit` 返回 `Thread`。如果这是主线程或最后一个线程，`exit` 将退出进程。

# Thread.fork { block } → thread

## fork

`Thread.start` 的别名。

# kill

导致给定线程退出（参见 `Thread.exit`）。

```
count = 0
a = Thread.new loop { count += 1 }
sleep(0.1) # => 0
Thread.kill(a) # => Thread:0x0a3764 aborting
count # => 96799
# 给它时间...
sleep 0.01
a.alive? => false
```

# Thread.kill( thread )

`Thread.list` → array

## list

返回所有运行或停止线程的 `Thread` 对象数组。

```
Thread.new { sleep(200) }
Thread.new { 100000.times {|i| i * i }
Thread.new { Thread.stop }
Thread.list.each {|thr| p thr }
```

产生：

`#Thread:0x00ac684 run`

`#Thread:0x0a3b8 sleep`

`#Thread:0x0a370 run`

`#Thread:0x0a398 sleep`

## main

`Thread.main` → thread

返回进程的主线程。

`Thread.main` # => `<Thread:0x00ac684>`

## new

`..new( |arg ) { |args| block }` → thread

创建并运行新线程以执行块中给出的指令。传递给 `Thread.new` 的任何参数都会传递给块。

```
x = Thread.new { sleep 0.1; print "x"; print "y"; print "z" }

a = Thread.new { print "a"; Thread.pass; print "b" }; sleep 0.2; print "c" }

x.join; a.join # 等线程完成
```

产生：

`abxyzc`

# pass

`Thread.pass`

调用线程调度器将执行权传递给另一个线程。

```
a = Thread.new { print "a"; Thread.pass; print "b" }
b = Thread.new { print "x"; Thread.pass; print "y" }
a.join; b.join
```

产生：

`abxy`

# start

`Thread.start( args*) { args|block } -> thread`

基本上与 `Thread.new` 相同。然而，如果 `Thread` 被子类化，在该子类中调用 `start` 将不会调用子类的 `initialize` 方法。

# stop

`Thread.stop`

停止当前线程的执行，将其置于“睡眠”状态，并调度另一个线程的执行。将“critical”条件重置为 false。

```
a = Thread.new { print "a"; Thread.stop; print "c" }
Thread.pass
print "b"
a.run
a.join
```

输出：

- a

- b

- c

# Instance methods

### []

`thr[ symbol ] -> obj or nil`

属性引用—返回线程局部变量的值，可以使用符号或字符串名称。如果指定的变量不存在，返回 nil。

```
a = Thread.current["name"] = "A"; Thread.stop 

b = Thread.new { Thread.current["name"] = "B"; Thread.stop }

c = Thread.new { Thread.current["name"] = "C"; Thread.stop }

Thread.list.each { |x| puts "#{x.inspect}: #{x[:name]}" }
```

输出：

```
#Thread:0x0ac0684 run-
#Thread:0x00a2acc run-
#Thread:0x00a27c run-
#Thread:0x00a2cb0 run-
```

### []=

`thr[ symbol ] = obj`

属性赋值—设置或创建线程局部变量的值，可以使用符号或字符串。另见 `Thread#[]`.

# abort_on_exception

`thr.abort_on_exception -> true or false`

返回 `thr` 的线程局部“发生异常时中止”条件的状态。默认为 false。另见 `Thread.abort_on_exception`。

# abort_on_exception=

`thr.abort_on_exception= true or false -> true or false`

当设置为 true 时，如果在 `thr` 中抛出异常，将导致所有线程（包括主程序）中止。进程将有效退出(0)。

# alive?

`thr.alive? -> true or false`

如果 `thr` 正在运行或睡眠，则返回 true。

```
thr = Thread.new { }
thr.join               # => #Thread:0x0a49acad dead
thr.current.alive? # => true
thr.alive?           # => false
```

# exit

`thr.exit -> thr or nil`

终止 `thr` 并调度另一个线程运行。如果该线程已被标记为杀死，则 `exit` 返回该 `Thread`。如果这是主线程或最后一个线程，它将退出进程。

# group

### 1.9

`thr.group -> thread_group`

返回拥有 `thr` 的 `ThreadGroup`，或 nil。

```
thread = Thread.new { sleep 99 } [#Thread:0x0ac684 run]
thread.current.list # => [#Thread:0x0a3764 run]
new_group = ThreadGroup.new
thread.current.list   # => [#Thread:0x0ac684 run]
new_group.add(thread)  # => [#Thread:0x0ac684 run]
thread.current.list # => [#Thread:0x0a3764 run]
thread.current.list # => [#Thread:0x0ac684 run]
```

# join

### 1.9

`thr.join(limit ) -> thr`

调用将挂起执行并运行 `thr`。在 `thr` 退出或经过 `limit` 秒之前，不会返回。如果 `limit` 过期，将返回 nil；否则返回 `thr`。

程序退出时，任何被连接的线程都将被杀死。如果它们之前抛出了异常且没有设置 `abort_on_exception` 和 DEBUG 标志（因此异常未被处理），则将在退出时处理。

```
a = Thread.new { print "a"; sleep(10); print "b" }
x = Thread.new { print "y"; Thread.pass; print "z" }
x.join # 等待 a 完成，a 将杀死。
```

输出：

```
axyz
```

示例说明了 `limit` 参数。

```
y = Thread.new { sleep 0.1; print "tick..." }
y.join(0.25)
puts "Gave waiting..."
```

输出：

```
tick...
Gave waiting...
```

# keys

`thr.keys -> array`

返回线程局部变量（符号）的名称数组。

```
thr = Thread.new do
Thread.current[:cat] = 'meow'
Thread.current["dog"] = 'woof'
end
thr.join => #Thread:0x0a44e dead
thr.keys => [:cat, :dog]
```

# key?

`thr.key?(:symbol) -> true or false`

如果给定的字符串或符号作为线程局部变量存在，则返回 true。

```
me = Thread.current
[:oliver] = "a"
me.key?(:oliver) => true
me.key?(:stanley) => false
```

# kill

`thr.kill`

`Thread#exit` 的同义词。

# priority

`thr.priority -> int`

返回 `thr` 的优先级。默认为零；高优先级线程将在低优先级线程之前运行。

```
Thread.current.priority => 0
```

# priority=

设置 `thr` 的优先级。高优先级线程将在低优先级线程之前运行。如果你发现多个线程需要完成工作，你正在执行某些操作。

```
count_high = 0
Thread.new do
Thread.current.priority = 1
loop { count_high += 1 }
end
Thread.current.priority = -1
loop { count_low += 1 }
```

```
sleep 1
count_high => 7
count_low => 6
```

# raise

`thr.raise(exception, message)`

为 `thr` 抛出异常。调用者不需要等待。

```
abort_on_exception = true
a = Thread.new { sleep(2) }
a.raise("Gotcha")
```

输出：

```
prog.rb:2 in 'sleep': Gotcha (RuntimeError)
from /tmp/prog.rb:2 in `<main>`
```

# run

`thr.run -> thr`

唤醒 `thr`，使其符合调度。如果不在关键区域，则会调用调度器。

```
a = Thread.new { puts "a" }; Thread.stop; puts "c"
Thread.pass
puts "Got here"
```

```
a.run
a.join
```

输出：

```
a
b
c
```

# safe_level

`thr.safe_level -> int`

返回 `thr` 的安全级别。在运行不安全代码时，设置线程局部安全级别有帮助。

```
thr = Thread.new { $SAFE = 3; sleep }
Thread.current.safe_level => 0
```

# status

`thr.status -> string, false or nil`

返回 `thr` 的状态：如果 `thr` 睡眠或等待 I/O，返回 sleep；如果 `thr` 正在执行，返回 run；如果 `thr` 正在中止，返回 aborting；如果 `thr` 正常终止，返回 false；如果 `thr` 因异常终止，则返回 nil。

```
a = Thread.new { raise("die") }
b = Thread.new { Thread.stop }
c = Thread.new { Thread.exit }
a.status => nil
b.status => "sleep"
c.status => false
Thread.current.status => "run"
```

# stop?

如果 `thr` 死亡或睡眠，返回 true。
