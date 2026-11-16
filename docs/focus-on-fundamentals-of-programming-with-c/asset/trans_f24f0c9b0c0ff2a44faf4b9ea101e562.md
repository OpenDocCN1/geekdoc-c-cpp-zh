

/*
Reads a compressed file created by compress() and writes a standard
ASCII file, one word per line.
*/
void expand(void) {
    char prev[MAX_CHAR], word[MAX_CHAR];
    int samechr;
    FILE *fpin, *fpOut;
    if ((fpin = fopen("compressedDictionary.txt", "r")) == NULL) {
        printf("file could not be opened for input.\n");
        exit(1);
    }
    if ((fpOut = fopen("newDictionary.txt", "w")) == NULL) {
        printf("file could not be opened for output.\n");
        exit(1);
    }
    while ((samechr = getWord(word, fpin)) >= 0) {
        strcpy(prev, word);
        fputs(prev, fpOut);
        fprintf(fpOut, "\n");
    }
    fclose(fpin);
    fclose(fpOut);
}
int getWord(char *w, FILE *fpin) {
    int c, count;
    while ((c = fgetc(fpin)) < 'a') {
        count = 0;
        if (c == EOF) {
            return -1;
        }
    }
    ungetc(c, fpin);
    while ((c = fgetc(fpin)) >= 'a') {
        w[count++] = c;
    }
    ungetc(c, fpin);
    w[count] = '\0';
    return count;
}

对包含 482,884 字节的 50,000 词典实现 compress() 会生成 185,339 字节的文件，压缩率为 61.62%。

## 字符串作业

1. 下列函数调用声称写入一个单个换行符，但有些是不正确的。找出哪些调用不起作用并解释原因。

- a) printf("%c", '\n');
- b) printf("%c", "\n");
- c) printf("%s", '\n');
- d) printf("%s", "\n");
- e) printf('\n');
- f) printf("\n");
- g) putchar('\n');
- h) putchar("\n");
- i) puts('\n');
- j) puts("\n");
- k) puts("");

2. 假设 p 已按如下方式声明：

```c
char *p = "abc";
```

下列哪些函数调用是合法的？显示每个合法调用产生的输出，并解释其他调用为何非法。

- a) putchar(p);
- b) putchar(*p);
- c) puts(p);
- d) puts(*p);

## 3. 假设 str 是一个字符数组。下列哪条语句与其他三条不等价？

- a) *str = '\0'; → 空字符串 → 替换 'se' 字符...
- b) str[0] = '\0'; → 空字符串
- c) strcpy(str, ""); → 空字符串
- d) strcat(str, ""); → 原字符串

## 4. 执行以下语句后，字符串 s1 的值将是多少？

```c
strcpy(s1, "computer");
strcpy(s2, "science");
if (strcmp(s1, s2) < 0)
    strcat(s1, s2);
else
    strcat(s2, s1);
s1[strlen(s1)-6] = '\0';
```

## 5. 下列函数声称创建字符串的完全副本。函数有什么问题？

```c
char *dup(char *p)
{
    char *q;
    strcpy(q, p);
    return q;
}
```

## 6. 下列程序打印什么？

```c
#include <stdio.h>
int main(void) {
    char s[] = "Hello";
    char *p;
    for (p = s; *p; p++)
        --*p;
    puts(s);
    return 0;
}
```

## 密码实验

这个简短作业的目的是让你练习使用字符和字符串。你将创建一个名为 `cipher.c` 的程序，通过将每个字母移动一定的位数来编码消息。因此，如果移位为 2，则 A 变为 C，B 变为 D，依此类推。如下所示：

![](img/7f36c52b5170b89b142dbb7b1ea4666b_366_0.png)

令人惊讶的是，你可以通过简单地对字符进行算术运算来实现这一点，但你应该向 C 保证结果是一个字符，使用强制类型转换。例如，如果一个字母包含值 'A'，那么 'A' + 2 给出整数结果 67，你可以通过说 `(char)(letter + 2)` 将其转换回字符，得到值 'C'。

不幸的是，`(char)('Z' + 2)` 不会给你字母 'B'（你可以从上面的图片中看出原因）。但如果你意识到已经越过 'Z'，你可以减去 26（结果为 'Z' + 2 - 26，或 'Z' - 24），这将给你 'B'。

这也意味着，如果你用移位 n 编码消息，你可以用另一个移位 26 - n 来解码。

你的程序应该首先调用一个函数 `processFile()`，它从文件（`congress.txt`）中读取消息到一个非常大的字符数组中。该函数应将所有字母转换为大写字符。你可以丢弃输入字符串中的所有标点符号、数字、空格以及其他任何内容。

你的程序然后应接受移位量作为函数 `cipher()` 的输入。输入参数应为 13，尽管为了测试目的，你可以简化事情，使用移位 1。你的函数应通过移位正确的数量来编码每个字母，并将编码后的字母放入以空字符结尾的字符数组中。

最后，你应该创建一个函数 `outputCode()`，它以每块五个字母、每行十块的形式输出最终编码的消息。最后一行可能少于五块，最后一块可能少于五个字母。

例如，给定移位 1，程序应将此消息：

Congress shall make no law respecting an establishment of religion, or prohibiting the free exercise thereof; or abridging the freedom of speech, or of the press; or the right of the people peaceably to assemble, and to petition the government for a redress of grievances.

转换为：

```
DPOHS FTTTI BMMNB LFOPM BXSFT QFDUJ OHBOF TUBCM JTINF OUPGS
FMJHJ POPSQ SPIJC JUJOH UIFGS FFFYY SDJTF UIFSF PGPSB CSJEH
JOHUI FGSFT EPNPG TQFFD IPSPG UIFQS FTPS UIFSJ HIUPG UIFQF
PQMFQ FBDBF CMZUP BTTFN CMFBO EUQPF UJUJP OUIFH PWPSO NFOUG
PSBSF ESFTT PGHSJ FWBOD FT
```

你的程序输出应发送到终端窗口（你的屏幕）以及请求的 `csis.txt` 输出文件。务必阅读关于捕获程序输出的文档。你的全名和 Palomar ID 号必须作为注释出现在包含 `main()` 的源文件中。务必将 `csis.txt` 输出文件包含在 zip 存档中。

## 文本格式实验

### 第一部分

第一部分是编写一个程序 `word.c`，它从文件 `getty.txt` 中读取单词，并将每个单词单独显示在一行上。单词定义为由空格、制表符或换行符分隔的任何字符序列。注意，此单词定义将标点符号视为单词的一部分。

你可以使用以下 while 循环，它将从文件中读取下一个单词到单词缓冲区 `wbuf`，该缓冲区在 main() 中声明为字符数组：

```c
while (!feof(fp)) {
    fscanf(fp, "%s", wbuf);
    ...
}
```

当每个单词在 wbuf 参数中返回时，它随后被发送到输出函数 `output()`，该函数在单词前后各加一个加号（+）将 wbuf 的内容显示到标准输出：

```
+Four+
+score+
+and+
+seven+
+years+
+ago+
+four+
+fathers+
+brought+
+forth,+    <- 注意，逗号被视为单词的一部分。
```

加号不应存储在 wbuf 中，而应在 wbuf 的内容输出前后立即输出。

你这部分实验的输出文件应命名为 `csis1.txt`。

### 第二部分

第二部分是编写一个文本对齐程序 `align.c`。这是一个尝试在一行中填充最大数量单词的程序，一行长度为 62 个字符，且不拆分单个单词。

该程序将使用 word.c 中定义的 while 循环和字符数组 `wbuf`，以及在 main() 中也声明为字符数组的行缓冲区 `lbuf`。这次，当每个单词从文件读入 `wbuf` 时，`wbuf` 和 `lbuf` 被发送到 `output()`，其中 `wbuf` 被放入 `lbuf`，直到行缓冲区满，此时将 `lbuf` 的全部内容发送到标准输出。

这是一个简单的算法：

```
While there are more words to be read from the file
    Read the next word into wbuf
    Send wbuf and lbuf into the output() function
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

你这部分实验的输出文件应命名为 `csis2.txt`。

### 注释

务必在打开文件进行读取和写入时进行错误检查。如果输入文件不存在或无法创建输出文件，你的程序应生成错误消息并退出。

注意，我不希望你在程序中读取输入的“行”。这是因为输入行可能非常长。对输入文件的格式没有限制。事实上，输入可能全是一行（非常长），这很容易溢出 `wbuf` 的大小。虽然提供的输入文件中没有长行，但一个正确（且有用）的程序必须能够处理它们。因此，使用我的 while 循环一次从输入文件中读取一个单词。

