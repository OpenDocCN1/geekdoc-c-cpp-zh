

例如，给定偏移量为 1，程序应将此消息转换为：

国会不得制定关于确立宗教或禁止信教自由的法律；不得削弱言论自由或新闻自由；也不得剥夺人民和平集会以及向政府请愿以伸张冤情的权利。

转换为：

DPOHS FTTTI BMMNB LFOPM BXSFT QFDQU OHBOF TUBCM JTINF OUPGS
FMJHU POPSQ SPIJC JUJOH UIFGS FFFYF SDJTF UIFSF PGPSB CSJEH
JOHUI FGSFF EPNPG TQFFD IPSPG UIFQS FTTP SIFSJ HIUPG UIFQF
PQMFQ FBDFB CMZUP BTTFN CMFBO EUPQF UJUJP OUIFH PWFSO NFOUG
PSBSF ESFTT PGHSJ FWBOD FT

请记住，main() 函数应作为程序中的第一个函数出现。请确保为程序中使用的每个函数使用函数原型。

程序的输出应同时发送到终端窗口（您的屏幕）以及请求的 csis.txt 输出文件。请务必阅读关于 Capturing Program Output 的文档。您的全名和 Palomar ID 号必须作为注释出现在包含 main() 的源文件中。请务必将 csis.txt 输出文件包含在 zip 压缩包中。

## 文本格式实验

### 第一部分

本实验的第一部分是编写一个程序 `word.c`，从文件 `getty.txt` 中读取单词，并将每个单词单独显示在一行上。单词的定义是由空格、制表符或换行符分隔的任意字符序列。请注意，此单词定义将标点符号视为单词的一部分。

您可以使用以下 while 循环，它将从文件中读取下一个单词到单词缓冲区 `wbuf` 中，`wbuf` 在 `main()` 中声明为字符数组：

```c
while (!feof(fp)) {
    fscanf(fp, "%s", wbuf);
    ...
}
```

每个单词在 `wbuf` 参数中返回后，会被发送到输出函数 `output()`，该函数在单词前后各加上一个加号（`+`）并将 `wbuf` 的内容显示到标准输出：

```
+Four+
+score+
+and+
+seven+
+years+
+ago+
+our+
+fathers+
+brought+
+forth,+ <- Note that the comma is considered part of the word.
```

加号不应存储在 `wbuf` 中，而应在 `wbuf` 的内容输出前后立即输出。

本实验部分的输出文件应命名为 `csis1.txt`。

### 第二部分

本实验的第二部分是编写一个文本对齐程序 align.c。该程序尝试在一行中填充尽可能多的单词，一行长度为 62 个字符，且不拆分单个单词。

该程序将使用 word.c 中定义的 while 循环和字符数组 wbuf，以及在 main() 中声明为字符数组的行缓冲区 lbuf。这次，当从文件中读取每个单词到 wbuf 时，wbuf 和 lbuf 会被发送到 output()，其中 wbuf 被放入 lbuf，直到行缓冲区已满，此时将 lbuf 的全部内容发送到标准输出。

这是一个简单的算法：

```
While there are more words to be read from the file
    Read the next word into wbuf
    Send wbuf and lbuf to the output() function
    If EOF has been reached and there are words in lbuf that have not yet been output
        Output lbuf. End of program.
    Otherwise
        Determine if the word in wbuf will fit into lbuf, being careful to allow room for the blank separating words.
        If there is room in lbuf,
            copy the contents of wbuf into lbuf
        Otherwise
            Output the contents of lbuf
            Print a newline to begin the next line
            Clear lbuf
            Copy the contents of wbuf into lbuf
```

本实验部分的输出文件应命名为 csis2.txt。

### 注释

打开文件进行读写时，请务必进行错误检查。如果输入文件不存在或无法创建输出文件，程序应生成错误消息并退出。

请注意，我不希望您在程序中读取输入的“行”。这是因为输入的一行可能非常长。输入文件的形式没有限制。事实上，输入可能全是一行（非常长的一行），这很容易导致 wbuf 的大小溢出。虽然提供的输入文件中没有长行，但一个正确（且有用）的程序必须能够处理它们。因此，请使用我的 while 循环从输入文件中一次读取一个单词。

### 额外学分

为了获得额外学分，您需要将文本对齐程序转换为文本格式化程序 `format.c`。该程序将文本的单词输出到既左对齐又右对齐的行上。幸运的是，我们的程序模块化程度很高，这只需要添加一个新函数 `fmt()`，该函数在 `lbuf` 的单词之间插入额外空格以实现完全对齐。该函数应在将 `lbuf` 发送到标准输出之前立即调用。

您的每个程序都应在文件 `getty.txt` 上运行。

```
Four score and seven years ago our fathers brought forth, upon this continent, a new nation, conceived in liberty, and dedicated to the proposition that all men are created equal. Now we are engaged in a great civil war, testing whether that nation, or any nation, so conceived, and so dedicated, can long endure. We are met here on a great battlefield of that war. We have come to dedicate a portion of it as a final resting place for those who here gave their lives that that nation might live. It is altogether fitting and proper that we should do this. But in a larger sense we can not dedicate - we can not consecrate - we can not hallow this ground. The brave men, living and dead, who struggled here, have consecrated it far above our poor power to add or detract. The world will little note, nor long remember, what we say here, but can never forget what they did here. It is for us, the living, rather to be dedicated here to the unfinished work which they have, thus far, so nobly carried on. It is rather for us to be here dedicated to the great task remaining before us that from these honored dead we take increased devotion to that cause for which they here gave the last full measure of devotion - that we here highly resolve that these dead shall not have died in vain; that this nation shall have a new birth of freedom; and that this government of the people, by the people, for the people, shall not perish from the earth.
```

请记住，`main()` 函数应作为程序中的第一个函数出现。请确保为程序中使用的每个函数使用函数原型。

程序的输出应同时发送到终端窗口（您的屏幕）以及请求的 `csis1.txt` 和 `csis2.txt` 输出文件。请务必阅读关于 Capturing Program Output 的文档。您的全名和 Palomar ID 号必须作为注释出现在包含 `main()` 的源文件中。请务必将输出文件包含在 zip 压缩包中。

## 文本统计实验

本次作业的目的是让您练习使用文本和数据处理技术来计算文本文件的一些统计信息。作业还将让您有机会了解更多关于字符串和文件的知识，以及如何组织一个中等规模的程序。

构建一个程序 stats.c，以检查数据文件 getty.txt 中的字符和单词。您的程序应执行以下操作：

- 统计文本中的行数。

- 统计文本中的单词数。

- 计算文本中所有单词的平均长度。

- 显示文本中单词长度的直方图，即类似于以下的条形图：

```
1: 2 * *
2: 6 * * * * * *
3: 3 * * *
4: 8 * * * * * * * *
```

以指示文本中有 2 个单字母单词、6 个双字母单词、3 个三字母单词、8 个四字母单词，等等。

- 统计文本中的字符数（不包括空格和标点符号）。

- 显示一个表格，列出文本中每个字母的频率。

- 统计文本中的元音字母数，并输出每个元音字母的频率，占读取的元音字母总数的百分比。

请记住，main() 函数应作为程序中的第一个函数出现。请确保为程序中使用的每个函数使用函数原型。

