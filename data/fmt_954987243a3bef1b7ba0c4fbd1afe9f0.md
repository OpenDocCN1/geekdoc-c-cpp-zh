
## 本章回顾

在本章中，我解释了时间和计算的基础知识。这包括对纪元（epoch）更深入的理解、现代计时术的起源，以及关于时间的一些历史。随后，我深入研究了标准库模块 `time`，并解释并演示了与该模块相关的许多方法和属性。我开发了几个 Python 脚本，向你们展示了如何应用和解释时间处理的结果。

我提供了 NTP（网络时间协议）的概述，它赋予了我们与国家测量标准进行时间同步的能力。接下来，我详细介绍了 Python NTP 库 `ntplib` 的安装和设置。然后，我通过对该模块进行实验，建立了一个与基于网络的时间源接口的 NTP 客户端。我编写了一个脚本来比较并计算我的本地时钟与 NIST 服务器之间的差异。

## 总结问题

- 1. 回到第 3 章，我开发了一个程序，遍历文件系统、对文件进行哈希处理，并记录每个文件的修改、访问和创建（MAC）时间。使用 `time` 模块修改该程序，将 MAC 时间从本地时间转换为 GMT/UTC 值。
- 2. 扩展代码列表 6.1，从全球范围内选择五个额外的时间服务器，并设计一种方法来比较每个服务器报告的时间与你本地系统时钟的关系。同时，记录每个服务器的网络延迟值。注意，你应该执行多次运行并取平均值。
- 3. 在取证调查期间，还应该对哪些时间来源进行检查和或归一化？

## 额外资源

利用时间证明数字证据的完整性。Int Digital Evid 2002;1(1) 1–7。
Python 标准库，http://docs.python.org/2/library/time.html?highlight=#time。
《网络时间协议第 4 版：协议和算法规范》。http://tools.ietf.org/html/rfc5905。
《经度》（Longitude）. Longitude: the true story of a Lone Genius who solved the greatest scientific problem of his time. New York, NY: Walker & Co.; 1995.

# 在取证中使用自然语言工具 7

### 章节目录
什么是自然语言处理？.......................................................... 183
基于对话的系统 ........................................................................ 184
语料库 ................................................................................................... 184
安装自然语言工具包（NLTK）及相关库 ...... 185
使用语料库 ....................................................................... 185
实验使用 NLTK ..................................................................... 186
从网络创建语料库 ................................................ 193
NLTKQuery 应用 ..................................................................... 194
NLTKQuery.py .............................................................................. 195
_classNLTKQuery.py ................................................................... 196
_NLTKQuery.py ............................................................................ 198
NLTK 示例执行 ................................................................ 199
NLTK 执行追踪 ........................................................................ 199
本章回顾 ................................................................................ 202
总结问题 ............................................................................ 202
额外资源 ....................................................................... 203

## 什么是自然语言处理？

在开始之前，需要定义自然语言。1987 年，我在与伊利诺伊理工学院研究院（IITRI）的 James Cook 博士合作的一个研究项目中，阅读了《自然语言处理导论》。我的妻子 Janet 在 IITRI 与 Larry Jones 博士合作进行自然语言项目。他将自然语言作为决策引擎的一部分，可以更好地理解牛群的行为。书中引用我见过的对自然语言的最优定义，因此我在这里也与你们分享。

> “自然语言是人类从环境中学习并用于相互间交流的任何语言。无论交流的形式如何，自然语言都用于表达我们的知识和情感，并向他人及我们的周围环境做出反应。” [Harris]

Python 取证
© 2024 Elsevier Inc. 保留所有权利。

183

显然，就像所有好的定义都经受住了时间的考验。由于互联网直到 20 世纪 80 年代后期才形成可识别的形式，因此以数字形式表达情感和知识的概念并不包括 Facebook、Twitter、表情符号、博客、短信、性短信、BitStrips 甚至是基于互联网的电子邮件！然而，该定义无疑涵盖了这些最新形式的自然语言表达。从自然语言中提取含义（语义）比看起来要困难得多。

判断试图解释、理解并做出相应响应的自然语言系统的有效性，取决于图灵测试，该测试以艾兰·图灵及其 1950 年的论文《计算机器与智能》命名。在他的论文中，图灵提出了一个主动性的问题：“机器能思考吗？” [Turing]

## 基于对话的系统

基于对话的系统的目标是响应用户输入，这意味着我们无法区分是人类还是机器的响应。有些人可能对正在转向这种能力的系统很熟悉。例如，这里是我和 Sync 系统之间的对话：

- 我：我饿了。
- Sync：好的，你想在哪里搜索？沿途路线还是城市里？
- 我：附近。
- Sync：你想按名称还是类别搜索？
- 我：按类别。
- Sync：好的，什么类别？
- 我：意大利菜。
- Sync：好的，请从屏幕上选择，例如第一行。
- Sync：Ross's Restaurant。你想打电话还是设置为目的地？
- 我：打电话。
- Sync：正在拨打 Rossi's Restaurant...

虽然有用，但它显然不符合图灵标准，因为我知道我在和机器而不是人类说话。然而，Sync 将语音转换为文本，并以及时的方式做出响应，结果系统达到了我想去的地方。

## 语料库

执行自然语言处理（NLP）的关键元素之一是语料库。语料库是与特定类型相关的大量语言样本。例如，位于 http://www.gutenberg.org/ 的[古登堡项目](gutenberg) 包含了超过 4 万本电子格式的书。

在本章中创建意义示例的挑战之一是建立语料库。然后我需要演示如何使用语料库创建这些示例，这些示例将作为科学领域 NLP 应用开发的催化剂。请记住，取决于你计划用于 NLP 应用，可能需要多个类型。

## 安装自然语言工具包及相关库

与第三方库和模块一样，支持 Windows、Linux 和 Mac 的安装。自然语言工具包（NLTK）是免费的，可以从 nltk.org 在线获取。安装 NLTK 需要使用 Numpy 和 PyYAML 安装其他依赖库。图 7.1 显示了 nltk.org 的安装页面，提供了易于遵循的指令。完成安装后，你可以通过你喜欢的 Python Shell 输入以下内容来验证安装：

Import NLTK

## 使用语料库

处理语料库的第一步要么加载 NLTK 包含的现有语料库，要么从本地文件或互联网创建自己的语料库。完成后，你可以对语料库执行各种强大的操作，

![](img/77956026d6b06352c72ae6ac437ce8ab_196_0.png)

图 7.1

nltk.org 安装地址。

# 第 7 章 法医鉴定中的自然语言工具

| 方法 | 说明 |
| --- | --- |
| raw() | 提取语料库的原始内容。该方法返回类型：Python "str" |
| word_tokenize() | 去除空格和标点符号，并创建单个标记（基本上是单词）的列表。该方法返回类型：Python "list" |
| collocations() | 词在文中频繁出现，并为调查人员提供有用信息。此外，一旦检测到，可以使用它们来寻找单词出现之间的关联。这是通过计算词的频率及其与其他词的连接实现的。collocation 方法在单个方法中完成所有这些操作 |
| concordance() | 该方法提供了生成特定单词每次出现及其上下文的能力（例如，该词在特定句子是如何使用的） |
| findall(search) | 该方法可用于语料库文本进行简单甚至是正则表达式搜索 |
| index(word) | 该方法提供所给单词首次出现的索引 |
| similar(word) | 注意，这不是同义词，而是该方法提供相似性，简单来说，是识别与指定词出现在相同“上下文”中的其他词 |
| vocab() | 对提交的文本生成全面的词汇列表 |

如果没有像 NLTK 这样的工具集的帮助，这些操作将变得既复杂又耗时。表 7.1 展示了可以在语料库上执行的一些关键操作，我将在本章节后的代码中演示这些操作。

## NLTK 实验

在本节中，我将调用表 7.1 中的方法并创建一个简单的程序，先创建一个文本语料库，然后用这些方法检查该语料库。首先，介绍一下我要创建的语料库背景。在这里，Jack Walraven 维护着网站 http://simpson.walraven.org/。Jack 整理了 O.J. Simpson 审判的记录。对于这次实验，我下载了 1995 年 1 月的审判记录（你可以下载任意数量的文本摘录）。1995 年诉讼存储了九个审判文本文件，它们代表 1 月 11-13 日、23-26 日、30 日和 31 日的记录。我在我的 Windows 系统上创建了一个目录 c:\simpson\ 来存放每个单独的文件。我的目标是使用这些文件创建一个包含所有文件的新文本语料库。说明这是如何运作的最佳方法是带你浏览一些处理每个方面的示例代码。我对代码进行了了注释，以确保你理解该过程的每一步。

## NLTK 实验

第一部分导入了实验所需的模块。最重要的是新安装的 NLTK 模块

```python
from __future__ import division

import nltk
```

接下来，我将从 NLTK 模块中导入 `PlaintextCorpusReader`。该方法将允许我读取并最终创建一个我可以处理的文本语料库。

```python
from nltk.corpus import PlaintextCorpusReader
```

我首先需要指定包含在语料库中的文件位置。我已将这些文件放在 c:\simpson\。9 个文件中的每一个存储在那里，每个都是一个文本文档。

```python
rootOfCorpus = "c:\simpson\"
```

现在，我将使用 `PlaintextCorpusReader` 收集变量 `rootOfCorpus` 中指定目录下的所有文件。我将通过第二个参数 `*` 来指定文件。如果你有包含多种文件类型的目录，且只想包含文本文档，可以指定 `.txt`。结果将是一个名为 `newCorpus` 的 NLTK 对象。

```python
newCorpus = PlaintextCorpusReader(rootOfCorpus, '*')

print type(newCorpus)
```

`type(newCorpus)` 产生 `newCorpus` 的类型输出：

```python
<class 'nltk.corpus.reader.plaintext.CorpusReader'>
```

我还可以使用 `fields()` 方法打印组成新语料库的每个文件的标识。

```python
print newCorpus.fields()
```

```python
['Trial-January-11.txt', 'Trial-January-12.txt', 'Trial-January-13.txt', 'Trial-January-23.txt', 'Trial-January-24.txt', 'Trial-January-25.txt', 'Trial-January-26.txt', 'Trial-January-30.txt', 'Trial-January-31.txt']
```

我还可以使用 `abspath()` 方法确定新语料库中单个文档的绝对路径。

```python
print newCorpus.abspath('c:\simpson\Trial-January-11.txt'),
FileSystemPointer('c:\simpson\Trial-January-12.txt'),
FileSystemPointer('c:\simpson\Trial-January-13.txt'),
FileSystemPointer('c:\simpson\Trial-January-23.txt'),
FileSystemPointer('c:\simpson\Trial-January-24.txt'),
FileSystemPointer('c:\simpson\Trial-January-25.txt'),
FileSystemPointer('c:\simpson\Trial-January-26.txt'),
FileSystemPointer('c:\simpson\Trial-January-30.txt'),
FileSystemPointer('c:\simpson\Trial-January-31.txt'))
```

现在我可以利用 `newCorpus` 对象提取 `rootOfCorpus` 中包含的原始文本。我可以确定审判文件的长度或大小。

```python
rawText = newCorpus.raw()

print len(rawText)
```

这产生了输出：

```
20824
```

现在我可以应用 `nltk.Text` 的内容来理解和解释语料库。我首先对语料库的 `rawText` 进行分词。这产生了标记（许多单词，但也包含数字和字符序列）。

```python
tokens = nltk.tokenize(rawText)
```

分词创建了一个标准的 Python 列表，现在可以处理标准语言对象。例如，可以使用 `len(tokens)` 来确定从文本中提取的标记数量。

```python
print len(tokens)
```

这产生了该语料库的结果：由于现在是一个简单的列表，我可以显示部分内容。例如，我打印分词返回的前 100 个标记。

```python
print tokens[:100]
```

```python
['LOS', 'ANGELLES', 'CALIFORNIA', '.', 'WEDNESDAY', '.', 'JANUARY', '.', '11', '.', 'DEPARTMENT', '.', '103', '.', 'HON.', '.', 'LANCE', '.', 'ITO', '.', 'JUDGE', '.', 'APPEARANCES', ',', 'APPEARANCES', ',', 'HERETOFORE', ',', 'NOTED', ',', 'DEPUTY', '.', 'DISTRICT', '.', 'ATTORNEY', '.', 'HANK', '.', 'ALSO', '.', 'SOJOURN', '.', 'MS.', '.', 'PAMELA', '.', 'WITHEY', '.', 'ATTORNEY-AT-LAW', '.', 'JANET', '.', 'MOXHAM', '.', 'CSR', '.', '4855', '.', 'OFFICIAL', '.', 'REPORTER', '.', 'CHRISTINE', 'M.', '.', 'OLSON', '.', 'CSR', '.', '2378', '.', 'OFFICIAL', '.', 'REPORTER', '.', ')', 'THE', 'FOLLOWING', 'PROCEEDINGS', 'WERE', 'HELD', 'IN', 'OPEN', 'OUT', 'OF', 'THE', 'PRESENCE', 'OF', 'THE', 'JURY', 'COURT', 'ALL', 'RIGHT', 'THE', 'SIMPSON']
```

接下来，我想创建一个可以应用 NLTK 文本方法的文本。通过使用 `Text` 方法对分词过程提取的标记创建 NLTK 对象 `textSimpson`。

```python
textSimpson = nltk.Text(tokens)

print type(textSimpson)
```

如预期的，对象类型是 `nltk.text.Text`

```
<class nltk.text.Text>
```
