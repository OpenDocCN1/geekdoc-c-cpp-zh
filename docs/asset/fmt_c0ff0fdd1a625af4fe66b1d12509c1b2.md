
Perl 是许多事务的极佳工具，但与许多其他脚本语言一样，它限于其设计运行的环境。为了运行 Perl 脚本，我们需要在运行脚本的系统上有一个解释器，并且我们受到命令行界面所能做的事情的。对于这两个问题，在 Perl 脚本方面，我们可以稍微“作弊”来绕过它们。

### 编译 Perl 脚本

正如我们目前为止在书中讨论的，解释型编程语言在运行时运行时需要一个工具来处理脚本，即解释器。如果我们处于在想要运行脚本的机器上没有解释器的情况（这在渗透测试中并不罕见），我们就遇到了一些问题。幸运的是，这是我们在某些脚本语言（包括 Perl）中可以处理的。我们可以直接编译我们的脚本。

现在等一下，我们不是讨论过 Perl 是一种解释型语言，根据定义，它是不被编译的吗？是的，我们确实讨论过。在这样的情况下，我们可以完成的不是严格意义上的编译，但结果是相同的。有很多工具，包括来自 ActiveState 的 `PerlApp` 和来自 IndigoStar 的 `Perl2Exe`，它们本质上会将一个小 Perl 解释器副本、我们的脚本以及任何其他依赖模块封装起来，并为各种平台生成可执行的二进制文件。当我们无法控制或更改正在使用的系统上的环境时，这是一个非常实用的功能。

## Perl 中的图形用户界面

在大多数情况下，Perl 脚本被用于生成命令行驱动的应用程序。有时，我们可能需要创建一个带有图形用户界面 `GUI` 的工具。例如，如果我们正在处理一个技术上面临挑战的用户，或者我们需要为现有工具添加界面，GUI 可能正是我们需要的。

实际上，在 Perl 中我们可以访问此类功能的库其实非常少。我们可以利用 `Perl / Tk` 来访问 `Tk` 工具包，访问 GIMP 工具包 `GTK+` 的功能，或者其他任何一种工具。使用此类工具较方便的特性之一是我们可以生成 GUI 驱动的 Perl 工具，这些工具可以在多个平台之间使用，无需修改脚本的图形部分。

## Perl 基础

在本节中，我们将介绍 Perl 使用的一些基本结构，包括变量、如何运行 shell 命令、如何使用模块扩展 Perl、参数、控制语句、文件输入和输出以及正则表达式的使用。

#### Hello World

好了，我们开始 Perl 中的标准 Hello World 脚本：

```perl
#!/usr/bin/perl
print "hello world!\n";
```

在创建文件后，设置权限使其可执行，并通过发布如 `./helloworld.pl` 的命令运行脚本，我们应该能看到图 3.2 所示的输出。

![](img/42f332b2adf7dab7e681e5d6cdd2074c_123_0.png)

**图 3.2** Hello World 脚本和输出。

让我们这个非常简单的脚本。从 shebang 开始，正如我们在第一章“命令行脚本脚本简介”中讨论的那样。在这种情况下，我们通常可以在大多数 UNIX 类系统上找到位于 `/usr/bin/perl` 的 Perl 解释器。如果它不在，我们可以通过 `whereis perl` 找到它，或者手动检查其他常用目录，如 `/usr/local/bin`、`/bin` 或 `/opt/bin/`。如果所有尝试都失败且我们拥有系统的管理权限，我们可以通过发布类似 `find -name perl -print` 的命令来查找它。

#### 提示

我们中眼光敏锐的人看了图 3.1，我们注意到通常可以在 `/usr/bin/perl` 找到 Perl 解释器。在某些情况下，我们将文件命名为 `helloworld.pl`。在 Perl 中，无论修改内容还是简单读取，变量总是用 `$` 寻址，我们可以使用变量来存储和处理各种内容，而无需它们是特定类型，如字符串或整数。我们在这个脚本中使用了变量，还用了一些其他东西，让我们回过一下它们。我们在第一行使用了 shebang，像往常一样，以便我们使用正确的解释器。在第二行，我们打印出一个字符串来请求名称。下一行定义了我们的变量 `$name`，并等待来自标准输入 `<STDIN>` 的输入，`<STDIN>` 是我们在运行脚本时将输入的控制台。这将我们在控制台上输入的任何内容（直到我们按下 Enter 键）放入我们的变量中。还要注意到行末尾的注释，以井号 `#` 开头。这将防止在脚本运行时解释该行的剩余部分。

下一行利用了 `chop`，这是一个非常实用的 Perl 函数。当我们从 `<STDIN>` 获取输入时，我们通过按下 Enter 键对其编辑。由 Enter 代表的换行符（也称为 `\n`）也被输入到了我们的变量中，如果我们不删掉它，它将出现在最后一个输出语句中，这就是 `chop` 所作用的。虽然 `chop` 是专门针对换行符的，但我们也可以使用 `chop`，它将删除最后一个字符，无论它是什么。

我们可能注意到脚本的输出行以分号结束。在 Perl 中，除了少数例外，每个语句都需要以分号结束。我们在这里注意到的是“语句”而不是“行”。我们也可以在单行语句中省略分号，但我们通常倾向于加上它以保持一致。

#### 变量

Perl 当然还有许多我们可以用于存储事物的数据结构，其中最常见的是标量变量。Perl 中的变量总是用 `$` 寻址，无论修改内容还是简单读取，我们可以使用变量来存储和处理各种内容，而无需它们是特定类型，如字符串或整数。我们在这个简单的脚本中使用变量：

```perl
#!/usr/bin/perl
print "Hi. What is your name?\n";
$name = <STDIN>; # take in a name
chomp $name;
print "$name is a nice name\n";
```

我们在这里使用了变量，还用了一些其他东西，让我们过一下。我们在第一行使用了 shebang，像往常一样，以便我们使用正确的解释器。在第二行，我们打印出一个字符串来请求名称。下一行定义了我们的变量 `$name`，并等待来自标准输入 `<STDIN>` 的输入，`<STDIN>` 是我们在运行脚本时输入的控制台。这将我们在控制台上输入的任何内容（直到我们按下 Enter 键）放入我们的变量中。还要注意到行末尾的注释，以井号 `#` 开头。这将防止在脚本运行时解释该行的剩余部分。

下一行利用了 `chop`。当我们从 `<STDIN>` 获取输入时，我们通过按下 Enter 键对其编辑。由 Enter 代表的换行符（也称为 `\n`）也被输入到了我们的变量中，如果我们不删掉它，它将出现在最后一个输出语句中，这就是 `chop` 所作用的。虽然 `chop` 是专门针对换行符的，但我们也可以使用 `chop`，它将删除最后一个字符，无论它是什么。

#### Shell 命令

我们可以利用的另一个有趣且非常实用的工具是执行 shell 命令的能力，这与我们在第 1 章“命令行 shell 脚本简介”中使用 `bash` 脚本所完成的操作非常相似。我们将查看如何执行 shell 命令，还将查看如何使用 Perl 来操作文件的时间戳。

```perl
#!/usr/bin/perl
$file = "testfile";
touch $file;
$originaccessed = (stat($file)) [8];
$origodified = (stat($file)) [9];
print "original accessed = $originaccessed\n";
print "original modified = $origodified\n";
sleep(5);
touch $file;
$newaccessed = (stat($file)) [8];
$newmodified = (stat($file)) [9];
print "new accessed = $newaccessed\n";
print "new modified = $newmodified\n";
utime $originaccessed, $origodified, $file;
$finalaccessed = (stat($file)) [8];
$finalmodified = (stat($file)) [9];
print "final accessed = $finalaccessed\n";
print "final modified = $finalmodified\n";
```

我们从 shebang 行开始。然后我们设置一个变量 `$file`，并将字符串 `testfile` 放入其中。这将是脚本要处理的文件名。在第二行中，我们使用了反引号，就像我们在第 1 章“命令行 shell 脚本简介”中使用 `bash` 时做的那样。在这种情况下，我们的反引号中包含了 Linux 命令 `touch`，它将更新我们存储在 `$file` 中的文件名的时间戳，并且如果该文件尚不存在，它还将创建该文件。

接下来，我们将为文件中已存在的时间戳创建一个副本。我们将使用 Perl 内置的 `stat` 命令。`stat` 命令将向我们返回关于文件的某些信息，包括我们感兴趣的时间戳。我们可以像处理数组一样处理 `stat` 命令，以便访问我们感兴趣的特定位。在这里我们将使用类似 `stat` 的用法，例如 `(stat($file) [8])`，以便访问第 8 个元素，即文件的访问时间。我们同样想访问第 9 个元素以获取修改时间。对于这些每一个项目，我们分别将 `stat` 的结果输入到我们的变量 `$origaccessed` 和 `$origodified` 中。然后我们回出这两个变量的内容，以显示文件的初始时间戳。

#### Note

`stat` 返回的时间戳是以自纪元（epoch）以来秒为单位返回给我们的。这相当于“自 1970 年 1 月 1 日 00:00:00 UTC 以来经过的秒数”。[4] 我们将在本节后面讨论更多如何将这些转换为人类可读的时间。

在记录并回出初始时间戳后，我们使用 `sleep` 命令等待 5 秒，并执行 `touch` 命令再次更新我们文件的时间戳。我们使用 `sleep` 命令是为了在脚本的后续部分中看到时间戳之间略大的差异。

接下来，我们进入另一个循环，使用 `stat` 从文件中检索新更新的时间戳，将它们记录到变量中，并再次显示出来。我们会看到时间戳发生了细微变化，这在很大程度上是因为我们使用了 `sleep` 来导致短暂的延迟。

由于我们有文件原始时间戳的记录，我们可以利用 `utime` 命令将文件更改的时间戳重置为原始值。`utime` 命令非常容易使用，我们可以直接将在 `$origaccessed` 和 `$origmodified` 中记录的原始时间戳数据输入到 `utime` 中。简单来说，我们通过包含代码 `utime, $origaccessed, $origmodified, $file` 来使用 `utime`。接下来我们再次进行一次获取并显示结果的时间戳，如图 3.3 所示。

```
root@mostdefinitelykali:~/Desktop# ./timestamp.pl
original timestamps
accessed = Mon Nov 16 15:16:58 2015
modified = Mon Nov 16 15:16:58 2015
modified timestamps
accessed = Mon Nov 16 15:17:03 2015
modified = Mon Nov 16 15:17:03 2015
final timestamps
accessed = Mon Nov 16 15:16:58 2015
modified = Mon Nov 16 15:16:58 2015
root@mostdefinitelykali:~/Desktop# 
```

## 图 3.3 时间戳脚本输出。

我们可以做几件事来让这个脚本更好。我们可以对时间戳进行一些处理，使其更容易理解，并使用函数，这样我们就不不断重复获取和打印文件时间戳的代码。

```perl
#!/usr/bin/perl
$file = "testfile"
`touch $file`
print "original timestamps\n";
($originaccessed, $origodified) = (stat($file)) [8], (stat($file)) [9];
print "accessed = " . localtime($originaccessed) . "\n";
print "modified = " . localtime($origodified) . "\n";
sleep(5);
`touch $file`
print "modified timestamps\n";
($newaccessed, $newmodified) = (stat($file)) [8], (stat($file)) [9];
print "accessed = " . localtime($newaccessed) . "\n";
print "modified = " . localtime($newmodified) . "\n";
utime $originaccessed, $origodified, $file;
print "final timestamps\n";
($finalaccessed, $finalmodified) = (stat($file)) [8], (stat($file)) [9];
print "accessed = " . localtime($finalaccessed) . "\n";
print "modified = " . localtime($finalmodified) . "\n";
```
