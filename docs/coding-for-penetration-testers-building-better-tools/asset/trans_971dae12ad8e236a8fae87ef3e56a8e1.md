
我们首先从常用的 shebang 行、模块导入开始，并将我们要搜索的站点和文件类型分别赋值给变量 $site 和 $filetype。我们还像在之前的脚本中一样，组装了 Google 的搜索 URL，并将其存放在 $searchurl 中。

接下来，我们创建一个 `WWW::Mechanize` 的新实例并将其赋值给 $mech 作为句柄。我们还设置了用户代理（user agent）字符串，然后使用该对象检索搜索 URL。

一旦获得结果页面，我们就可以筛选链接。`WWW::Mechanize` 模块让我们更精确地处理这种搜索。我们首先解析结果页面中的所有链接，然后通过正则表达式（regex）检查这些链接是否符合之前指定的类型类型，并将结果存放在 @links 中。

一旦获取了所需的链接，我们就设置一个循环来遍历每个元素。在循环内部，我们获取链接的绝对 URL，这样我们就不依赖于任何间接链接，并将其存放在 $url 中。然后，我们多次通过 `split` 函数来从 Google 复杂的 URL 中提取出我们关心的实际 URL，并在最后检查 $url 是否为空，如果为空则跳出本次循环迭代。接着，我们进行快速替换以将文件名与其路径分离，然后输出一行内容以指示我们正在下载哪个文件。最后，我们使用 `get` 方法和 `content_file` 下载我们需要的特定文件，并以 $filename 中的值命名。我们继续遍历 @links 数组，直到处理完所有元素。

我们以与之前版本相同的方式调用此脚本：`/mechanize.pl syngress.com ppt`。这应该会带回几个文件，脚本的输出应该类似于图 8.3 所示。

```
root@mostdefinitelynotkali: ~/Desktop$ ./mechanize.pl syngress.com ppt
downloading http://booksite.syngress.com/9781579494250/content/Video/HPTF/PPT/Module4.ppt to module4.ppt
downloading http://booksite.syngress.com/9781579494250/content/Video/HIPT/PPT/Module02_01.ppt to Module02_01.ppt
downloading http://booksite.syngress.com/9781579494250/content/Video/HIPT/PPT/Module02_02.ppt to Module02_02.ppt
downloading http://booksite.syngress.com/9781579494250/content/Video/HPTF/PPT/Module7.ppt to module7.ppt
downloading http://booksite.syngress.com/9781579494250/content/Video/HPTF/PPT/module2.ppt to module2.ppt
downloading http://booksite.syngress.com/9781579494250/content/Video/HPTF/PPT/module3.ppt to module3.ppt
downloading http://booksite.syngress.com/9781579494250/content/Video/HIPT/PPT/Module5.ppt to module5.ppt
downloading http://booksite.syngress.com/9781579494250/content/Video/HPTF/PPT/module05.ppt to Module05.ppt
downloading http://booksite.syngress.com/9781579494250/content/Video/HPTF/PPT/module6.ppt to module6.ppt
root@mostdefinitelynotkali:~/Desktop#
```

# 图 8.3 Mechanize.pl 输出。

这比我们在前面的章节中写的要精简一些，我们可以利用它来构建在“处理元数据”章节中将组合的工具。这段代码确实存在一些问题，其中一些我们本章稍后会讨论。

## 处理元数据

正如我们在本章开头讨论的，元数据可以为我们提供在渗透测试过程中可能用到的各种有趣信息。我们可能会找到名称、用户名、路径、网络信息以及各种有趣的片段。我们知道信息可能存在那里，但我们如何找到它，又如何从我们拥有的文件中提取出来呢？

## 寻找元数据

在某种程度上，我们可能通过利用创建或存在于我们处理的文件之应用程序来找到元数据。例如，如果在较新版本的 Word 中打开 Microsoft Word 文档，并选择“文件 | 信息 | 检查问题”，这将弹出“文档检查器”，允许我们看到 Word 认为存在的哪些元数据，并允许我们删除大部分此类数据。

像 Word 和 Adobe Acrobat 这样的工具在最新版本中显示此类数据的效果较好，但对于我们手头的每个工具或文件并不总是如此。搜寻此类数据的老牌工具是 `strings` 实用程序。

为了快速演示使用 `strings` 可以做什么，让我们来看一个我们可能无法从中获取太多信息的文件，即几乎是任何二进制格式的文件。在这种情况下，`strings` 工具本身提供了一个极佳的例子。在 Kali 上，`strings` 位于 `/usr/bin/strings`。如果我们运行它，会得到一堆快速滚过的混乱数据，其中一些是人类可读的数据，另一些不是。然而，如果我们运行 `strings /usr/bin/strings`，我们将得到来自该文件所有可读字符串的漂亮列表，如图 8.4 所示。

```
root@mostdefinitelynotkali: ~/Desktop
bfd_get_error
root@mostdefinitelynotkali:~/Desktop strings /usr/bin/strings
/lib64/ld-linux-x86-64.so.2
ifa
libbfd-2.25-system.so
ITM_registerTMCloneTable
_gmon_start
Jv_RegisterClasses
ITM_registerTMCloneTable
bfd_check_format
vexit
bfd_target_vector
bfd_target_list
bfd_malloc
_sch_listable
malloc_loc_set_program_name
bfd_close
bfd_close
bfd_set_default
bfd_set_format
bfd_list
```

# 图 8.4 Strings 输出。

我们可以通过一点点脚本来使用 `strings`：

```bash
#!/bin/bash
find . -name *.ppt | (
  while read file; do
    echo -e "********************$file\n********************" >> stringsreport.txt;
    strings $file >> stringsreport.txt;
  done)
```

所以我们在执行目录下快速 `find` 搜索 `.ppt` 文件，并将结果传递给 `while` 循环。在循环内部，我们向报告输出一行内容以区分不同的文件，然后对文件运行 `strings`。我们可以对这个想法进行一些尝试并扩展我们的脚本以添加其他功能。我们可以让它递归目录，以便获取子目录。我们可以让它根据命令行参数搜索文件类型，而不是硬编码文件类型。

## 文档元数据

当我们搜索文档元数据时，可以结合在本章讨论过的多种资源来帮助工作。我们可以结合使用 Google（或类似的搜索引擎）、正则表达式和文本搜索，将文档输入我们的搜索过程。

使用我们在本章早些讨论的 Google 高级操作符，我们可以搜索特定的文档类型。例如，如果我们只想在特定域名中查找特定文档类型，可以使用 `filetype:` 高级操作符从目标域名下载这些文档。这为我们提供了一个极佳的起点，以及可能一组值得梳理的文档。

从这里开始，我们可能使用一些正则表达式来过滤特定类型或模式的数据。这可能是使用我们在第3章“Perl 简介”中讨论过的正则表达式的好地方。特别是寻找电子邮件地址、文件系统路径、网络路径和其他类似信息可能会有用。我们可能会通过这种方式发现具有价值的信息，如信用卡号或社会安全号码，但在我们从公共网站、FTP 服务器等处爬取的文档中，这种情况并不常见。尽管如此，尝试一下总是无害的，而且通过自动化过程这样做通常不需要太大成本。

最后，我们可以使用类似 `strings` 的工具进行常规搜索，并直接导出给定文档中找到的所有文本字符串。这可能会产生大量的垃圾信息，并产生令我们惊讶的结果。我们完全可以记录下