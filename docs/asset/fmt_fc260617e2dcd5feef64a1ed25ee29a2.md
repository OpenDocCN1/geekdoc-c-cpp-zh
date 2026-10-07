
# `File.exist?`

`File.exist?(filename)` → true or false

如果命名的文件或目录存在则返回 `true`。

```ruby
File.exist?("testfile") # true
```

# `File.exists?`

`File.exists?(filename)` → true or false

`File.exist?` 的同义词。

# `File.expand_path`

`File.expand_path(filename, dirstring)` → filename

将路径转换为绝对路径。相对路径从进程当前的目录引用，除非给出了 `dirstring`，则将其作为起始点。给路径可能以 `~` 开头，它扩展为进程所有者的 HOME（HOME 环境变量必须正确设置）。

```ruby
File.expand_path("~/bin") # => "/Users/dev/bin"
File.expand_path("../../x") # => "/tmp"
```

# `File.extname`

`File.extname(path)` → string

返回扩展名（路径中文件名点之后的部分）。

```ruby
File.extname("test.rb") # => ".rb"
File.extname("a/b/test.rb") # => ".rb"
File.extname("") # => ""
```

# `File.file?`

`File.file?(filename)` → true or false

返回命名的命名文件是否为普通文件（不是设备、目录、管道、套接字等）。

```ruby
File.file?("testfile") # true
File.file?(".") # false
```

# `File.fnmatch`

`File.fnmatch(glob_pattern, path, (flags))` → true or false

如果 `path` 匹配 `glob_pattern` 则返回 `true`。（从 Ruby 1.9 开始，`File.fnmatch` 是 `Dir.fnmatch` 的别名）。模式不是正则表达式；而是类似于 shell 通配符的规则。`glob_pattern` 可能会包含以下元字符：

- `*` 匹配文件或目录名中的一个或多个字符。
- `**` 匹配一个或多个字符，忽略名称边界。通常用于递归扫描子目录。
- `?` 匹配任意单个字符。
- `[charset]` 匹配给定字符集中的任何字符。字符范围写为 `from-to`。集合可以通过开头的脱字符 (`^`) 取反。
- `\` 转义下一个字符的特殊含义。

`flags` 是下一页列出的 `FNM___` 参数的按位或结果。另参见第 480 页的 `Dir.glob`。

```ruby
File.fnmatch('cat', 'cat') # true
File.fnmatch('cat', 'category') # false
File.fnmatch('c*', 'cat') # true
File.fnmatch('c?', 'cat') # false
File.fnmatch('c??', 'cat') # false
File.fnmatch('c*', 'cats') # true
File.fnmatch('c/*', 'a/b/c/t') # true
File.fnmatch('c*t', 'a/b/c/t') # true
File.fnmatch('c++t', 'cat') # true
```

## 表 27.3. 匹配模式常量

- `FNM_NOESCAPE`: 反斜杠在图表中不作为转义字符，模式中的反斜杠必须匹配文件名中的反斜杠。
- `FNM_FILENAME`: 文件名中的正斜杠被视为路径部分的分隔符，必须在模式中进行显式匹配。
- `FNM_DOTMATCH`: 如果未指定此项，包含开头点的文件名必须通过模式中的显式点来匹配。开头点是指文件名开头（或在指定 FNM_PATH 的情况下）跟在斜杠后的点。
- `FNM_CASEFOLD`: 文件名匹配忽略大小写

```ruby
File.match('*', '.profile') # => false
File.match('*', '.profile', File::FNM_DOTMATCH) # => true
File.match('*', 'dave/profile') # => true
File.match('*', 'dave/profile', File::FNM_DOTMATCH) # => true
File.match('*', 'dave/profile', File::FNM_FILENAME) # => false
File.match('*', 'dave/profile', File::FNM_FILENAME) # => false
STRICT = File::FNM_PATHNAME | File::FNM_DOTMATCH
File.match('*', 'dave/profile', STRICT) # => true
```

> `File.fnmatch?(glob, path, flags)` → (true 或 false)

# `File.fnmatch?`

`File#fnmatch` 的别名。

> `File.type(filename)` → filetype

# `File.type`

标识命名文件的类型。返回的字符串是 file、directory、characterSpecial、blockSpecial、lfo、link、socket 或 unknown（未知）中的其中之一。

```ruby
File.type("testfile") # => "file"
File.type("/dev/tty") # => "characterSpecial"
system("mkfifo wibble") # => true
File.type("wibble") # => "fifo"
```

> `File.grpwned?(filename)` → true 或 false

# `File.grpwned?`

返回进程的有效组 ID 是否与命名文件的 ID 相同。在 Windows 上返回 false。

```ruby
File.grpwned("/etc/passwd") # => false
```

> `File.identical?`

# `File.identical?`

`File.identical?(name1, name2)` → true 或 false

1.9 仅当 `name1` 和 `name2` 指向同一个文件时才返回 true。两个内容相同的独立文件不被视为相同。

```ruby
File.identical?("testfile", "./../testfile") # => true
File.symlink("testfile", "wibble")
File.identical?("testfile", "wibble") # => true
File.link("testfile", "wibble") # => true
File.identical?("testfile", "wibble") # => true
File.identical?("testfile", "wibble") # => true
File.identical?("testfile", "wibble") # => true
```

# `File.join`

`File.join(string string)+` -> filename

返回一个使用 `File::SEPARATOR` 连接字符串而形成的新字符串。各种分隔符列在下一页的表 27.4 中。

```ruby
File.join("usr", "mail", "gumpy") # => "usr/mail/gumpy"
```

# `File.lchmod`

`File.lchmod(permission, (filename)+` -> 0

等同于 `File.chmod` 但不跟随符号链接（因此它将更改与链接关联的权限，而不是它所引用的文件）。通常不可。

# `File.lchown`

`File.lchown(owner, group, (filename)+` -> 0

等同于 `File.chown` 但不跟随符号链接（因此它将更改与链接关联的所有者，而不是它所引用的文件）。通常不可。

# `File.link`

`File.link(oldname, newname)` -> 0

使用硬链接为现有文件创建一个新名称。如果 `newname` 已经存在，则不会覆盖它（在这种情况下会抛出 `SystemCallError` 的子类）。并非所有平台均可用。

```ruby
File.link("testfile", "testfile.2") # => 0
f = File.open("testfile.2")
# => "This is one line\n"
f.gets
File.delete("testfile.2")
```

# `File.lstat`

`File.stat(filename)` -> stat

返回作为 `File::Stat` 类型对象的文件状态。与 `IO#stat` 相同（见第 56 页），但不跟随符号链接。返回链接本身。

```ruby
File.symlink("testfile", "link2test") # => 0
File.stat("testfile").size # => 66
File.stat("link2test").size # => 8
File.stat("link2test").size # => 66
```

# `File.mtime`

`File.mtime(filename)` -> time

返回包含命名文件修改时间的 `Time` 对象。

```ruby
File.mtime("testfile") # => 2009-04-13 12:45:10-0500
File.mtime("/tmp") # => 2009-04-13 13:16:08-0500
```

## 表 24. 路径分隔符常量（平台特定）

- `ALT_SEPARATOR`: 备用路径分隔符（Windows 上为 `\`，否则如此）。
- `PATH_SEPARATOR`: 搜索路径中分隔符的分隔符（例如 `/`）。
- `SEPARATOR`: 路径分隔符（例如 `/`）。

## 表 27.5 打开常量

- `File::APPEND`: 以追加模式打开。
- `File::CREAT`: 如果文件不存在则创建它。
- `File::EXCL`: 如果文件存在则失败。
- `File::NOCTTY`: 不使其成为控制终端。
- `File::NONBLOCK`: 非阻塞模式打开。
- `File::RDONLY`: 仅读打开。
- `File::RDWR`: 读写打开。
- `File::TRUNC`: 打开时截断文件为零。
- `File::WRONLY`: 仅写打开。

# `File.socket?`

`File.socket?(filename)` → true 或 false

如果命名文件是 socket 则返回 true；否则返回 false（如果操作系统不支持）。

# `File.split`

`File.split?(filename)` → array

将给定字符串拆分为数组。

# `File.stat`

`File.stat(filename)` → stat

返回命名文件的 `File::Stat` 对象（见第 518 页）。

```ruby
stat = File.stat("testfile")
stat.mtime => 2009-04-13 12:45:10-0500
stat.ftype => "file"
```

# `File.pipe?`

`File.pipe?(filename)` → true 或 false

如果操作系统支持管道且命名文件是管道则返回 true；否则返回 false。

```ruby
File.pipe?("testfile") # => false
```

# `File.readable?`

`File.readable?(filename)` → true 或 false

如果文件对有效用户 ID 可读则返回 true。

```ruby
File.readable?("testfile") # => true
```

# `File.readable_real?`

`File.readable_real?(filename)` → true 或 false

如果命名文件对真实用户 ID 可读则返回 true。

```ruby
File.readable_real?("testfile") # => true
```

# `File.readlink`

`File.readlink(filename)` → string

以字符串形式返回符号链接。并非所有平台均可用。

```ruby
File.symlink("testfile", "link2test") # => 0
File.readlink("link2test") # => "testfile"
```

# `File.rename`

`File.rename(oldname, newname)` → 0

将文件或目录重命名为新名称。如果无法重命名则抛出 `SystemCallError`。

```ruby
File.rename("afile.bak") # => 0
```

# `File.setgid?`

`File.setgid?(filename)` → true 或 false

如果命名文件的设置组 ID 权限已设置则返回 true；如果未设置或操作系统不支持。

```ruby
File.setgid?("/usr/bin/lpc") # => false
```

# `File.setuid?`

`File.setuid?(filename)` → true 或 false

如果命名文件的设置用户 ID 权限已设置则返回 true；如果未设置或操作系统不支持。

```ruby
File.setuid?("/bin/su") # => false
```

# `File.size`

`File.size(filename)` → integer

以字节为单位的文件大小。

```ruby
File.size("testfile") # => 66
```

# `File.size?`

`File.size?(filename)` → integer 或 nil

如果命名文件长度为零返回 nil；否则返回大小。可以用作测试中的条件。

```ruby
File.size?("testfile") # => 66
File.size?("/dev/zero") # => nil
```

# `File.truncate`

`File.truncate(filename, int)` → 0

将文件名截断至至多 `int` 字节。并非在所有平台上都可用。

```ruby
f = File.new("out", "w")
f.write("1234567890")     # => 10
f.close                      # => nil
File.truncate("out", 5)     # => 0
File.size("out")               # => 5
```

# `File.umask`

`File.umask(int)` → int

返回进程的当前 umask。如果提供了可选参数，则将 umask 设置为该值并返回之前的值。Umask 值会从默认权限中排除；umask 为 0222 将使文件对所有人只读。参见第 506 页关于权限的讨论。

```ruby
File.umask(0006)   # => 18
File.umask()                # => 6
```

# `File.unlink`

`File.unlink(filename)` → int

`File.delete` 的同义词。也是 `Dir.rmdir`。

```ruby
File.open("testrm", "w")   # => nil
File.unlink("testrm")          # => 1
```

# `File.utime`

`File.utime(atime, mtime, , filename)` → int

更改多个文件的访问时间和修改时间。时间必须是 `Class` 类的实例或表示自 epoch 以来秒数的整数。返回已处理的文件数。并非在所有平台上都可用。

```ruby
File.utime(0, 0, "testfile")      # => nil
File.utime("testfile")             # => 1969-12-31 18:00:00 -0600
File.utime(0, Time.now, "testfile")  # => 1
File.utime("testfile")             # => 2009-04-13 13:26:23 -0500
```

# `File.world_readable?`

`File.world_readable?(filename)` → int

- 1.9

如果文件名可被读取，则返回一个表示文件名权限位数的整数。否则返回 nil。位位的含义取决于平台；在 Unix 系统上，请使用 `stat(2)`。

```ruby
File.world_readable?("/etc/passwd") # => 420
File.world_readable?("/etc/passwd").to_s(8) # => "644"
```

# `File.world_writable?`

`File.world_writable?(filename)` → int

- 1.9

如果文件名可被他人写入，则返回一个表示文件名权限位数的整数。否则返回 nil。位位的含义取决于平台；在 Unix 系统上，请使用 `stat(2)`。

```ruby
File.world_writable?("/etc/passwd") # => nil
File.world_writable?("/tmp") # => 511
File.world_writable?("/tmp").to_s(8) # => "777"
```
