

# 第二部分：MicroWorlds 游戏

## #15 Madlibs

我们将要做一个新项目，一个名为 Madlibs 的游戏。它将让我们再次练习处理变量。

在编写这个程序时，我们将遵循一组定义的步骤。步骤如下：

- 1. 确定目标。
- 2. “沙盒”获取必要的知识。
- 3. 编写伪代码，用英语描述我们想做的事情。
- 4. 编写代码。
- 5. 测试。
- 6. 重复一遍，即“增强”。

你可能以前玩过 Madlibs，但不是用电脑。首先，你写一个留有空白的故事。然后你采访某人，记录下蔬菜名称或你需要的任何内容，将交谈的对象作为随机单词生成器。然后你将这些词填入故事中。结果会是出奇的荒诞，你们两个都可以乐在其中。

为了完成这个项目，我们需要遵循我们的编程步骤！

## 1. 确定目标

在这一步中，你需要思考具体想让这个过程完成什么任务。总有一些决定需要做，现在就是做这些决定的时候。

我们将从用户那里获取单词，保存它们，然后将它们插入到在图形页面（Graphics Page）上打印的故事中。我们将利用变量的知识。我们要创建一个变量来捕捉用户输入的单词。然后我们将保留这些单词，直到使用它们为止。因此，需要的变量数量与故事中的空白数量相同。以下是我们的任务：

- 使用至少五个变量创建一个 madlib。
- 要求用户使用单词填充到变量中。
- 使用这五个变量在文本框中打印出一个故事。
- 创建一个名为 madlibs 的程序，该程序要与 Main 和 Start 程序协同工作。

## 2. 沙盒获取必要的知识

这一步是一个学习步骤。在这里，你查看你的代码，看看在编写代码之前是否有某些你需要学习的方面。如果是，你就写一些“沙盒”或“一次性”代码来教自己需要知道的知识。

我们需要知道如何接受用户输入的单词。这是一个示例。假设我们给变量命名为 `noun1`。打开一个新文件。在你的过程页面（Procedures Page）上，开始写一个名为 Madlistest 的新程序。然后添加一行代码创建一个变量 `noun1`：

```
to madlistest
-local "noun1"
```

这是我们创建的内容：

| | | | | | |
|---|---|---|---|---|
| | | ? | | |
| Mailbox with Unknown Contents Noun | | | |

现在我们输入这段代码：

```
question [What is your favorite animal?]
```

这个名为 `question` 的程序向用户提问并为答案提供空间。

```
make noun1 answer
```

`answer` 程序输出用户刚刚输入的任何内容。`make` 程序给变量 `noun1` 赋值 `answer` 的值。假设用户输入了“worm”。此时，变量 `noun1` 将包含“worm”。

| | | | | | |
|---|---|---|---|---|
| | | Worm Noun | | |
| Mailbox with New Contents | | | |

让我们看看发生了什么。你的初步程序看起来像这样：

```
to madlibstest
local "noun1"
question [Please type in an animal name.]
make "noun1" answer
show :noun1 ;这意味着显示 noun1 中的内容
end
```

进入命令中心（Command Center）并输入 `madlibstest` 来运行该程序。按照要求输入一个动物名称。电脑在屏幕底部显示了动物名称吗？按理说是应该是。

但让我们创建一个文本框并在其中打印我们的输出。这样我们就可以可以在不使用命令中心的情况下使用我们的游戏。如果我们把游戏发布到网上，就需要它。要创建一个文本框，点击带有 ABC 或单个 A 的图标。然后点击屏幕并调整文本框的大小，使其至少占屏幕的一半大。你可以点击文本框（然后在 MicroWorlds EX 中点击 edit）并告诉它不要显示框的名称。

要把内容打印到文本框中，我们使用 `print` 命令，而不是用于打印到命令中心的 `show` 命令。

现在我们需要在“帮助词汇表”（Help vocabulary）中检查 `print`。方法如下：

在 MicroWorlds 2.0 中，点击 Help，然后点击 Vocabulary。会弹出一个网页。在右上角，你可以选择 Basic（基础）或 Advanced（高级）。我们需要 Advanced，所以选择它。现在选择 Vocabulary 标签页。你的 Internet Explorer 可能会阻止此页面，因为它包含 ActiveX 编程，但它是你计算机本地的，所以点击弹出拦截器栏并允许内容。现在你已进入 Vocabulary 标签页，可以从左侧菜单选择主题来找到你需要的单词，或者可以点击字母表中显示的第一个字母。我们可以点击 P 并找到 `print`。MicroWorlds EX 和 2.0 告诉我们类似这样的信息：

```
print word-or-list
```

在当前文本框中打印一个单词或列表。文本后紧跟一个回车和换行符序列。参见“插入”（insert）部分。

示例：

假设页面上有一个包含某些文本的文本框：

```
print [The End]
```

建议的格式是 `print word-or-list`。单词在正前方有一个双引号 `"`。列表被包含在 `[方括号]` 中。因此，我们的输入需要其中之一，即双引号或方括号。在命令中心尝试这些：

- `print "hello"`
- `print [hello]`
- `print [[hello][Mom]]`

你能让它打印出 "Hello out there!" 吗？在翻页之前试一下。

我们的“Hello out there!”看起来像这样：

```
print [Hello out there!]
```

我们如何让它打印出变量中的内容呢？在过程页面上，让我们尝试这个：

```
to test
local :noun1
make "noun1" "me"
print [Hello :noun1]
```

在命令中心输入 `test` 并按回车。哎！它在框里打印了“Hello :noun1”！那不是我们想要的！我们想要 `noun1` 中的内容！

让我们看看名为 `sentence` 的程序。帮助文档关于 `sentence` 是这样说的：

```
sentence (se) word-or-list1 word-or-list2
(sentence word-or-list1 word-or-list2 word-or-list3...)
```

报告一个单词或列表。`sentence` 可以接受超过 2 个输入。注意包含单词的括号。参见格式：

```
sentence input1 input2
```

示例：

```
sentence "a"
```

```
sentence [a]
```

```
sentence "a" [b]
```

```
sentence "a" [b] [c]
```

现在，如果我们想一次性创建多个变量呢？我们至少至少五个变量。让我们猜一下 `local` 可能可以帮到我们。在帮助索引下查找 `local`。它写道：

```
local
local word-or-list
```

我们可以使用单个单词（带有双引号）或列表（带有方括号）作为 `local` 的输入。例如，我们可以说：

```
local "fred"
```

或者

```
local [fred sam bob]
```

