
## 数据压缩 - 高级

数据压缩是减少存储或传输数据所需位数的技术。压缩可以是 *无损* 或 *有损*。无损和有损压缩是描述在文件解压缩或数据传输接收时，是否可以恢复所有原始数据的术语。

使用无损压缩时，文件解压缩后，原始文件中的每一位数据都保留下来。所有信息都完全恢复。这通常是文本或电子表格文件的首选技术，因为丢失单词或财务数据可能会造成问题。图形交换格式（GIF）是 Web 上使用的一种提供无损压缩的图像格式。其他无损压缩算法包括：

- TIFF
- Zip
- RAR
- FLAC
- LZW
- 霍夫曼编码
- PNG
- 莫尔斯电码

另一方面，有损压缩通过永久删除某些信息（尤其是冗余信息）来减小文件大小。当文件解压缩时，只剩下部分原始信息（尽管用户可能不会注意到）。有损压缩通常用于视频和音频，其中一定量的信息丢失大多数用户不会察觉。JPEG 图像文件常用于网页上的照片和其他复杂静态图像，是一种有损压缩图像。使用 JPEG 压缩时，创建者可以决定引入多少损失，并在文件大小和图像质量之间做出权衡。其他有损压缩算法包括：

- MP3
- JPG
- DivX

## 字典压缩

通过检查字典中连续数据项之间的关系，可以推导出一种高效的编码方案，以实现高水平的数据压缩。该压缩技术利用了这样一个事实：字典中的单词按字母顺序排列，往往与相邻条目以相同的字母开头。压缩算法的工作原理如下：压缩字典中的每个单词都以一个数字开头，该数字表示应从字典中的前一个单词复制多少个字符。单词的其余字母紧随数字之后。

例如，如果原始字典仅包含五个单词：

```
can<LF>
canal<LF>
cancel<LF>
cancer<LF>
candid<LF>
```

它将被压缩为：

```
0can<LF>
3al<LF>
3cel<LF>
5r<LF>
3did<LF>
```

在字典的编码版本中，只出现那些在前一个单词中未连续出现的字母。每个单词末尾前面的数字表示相同的字符数量。解码要求按顺序读取，以便前一个单词再次可用。待解压缩单词前面的计数提供了要保留的首字符数量，然后将未编码的字符连接起来。

在前面的示例中，原始字典包含 31 个字符，压缩版本包含 22 个字符，节省了 29% 的空间。通过减少每行末尾的换行符 <LF> 数量，可以实现更多压缩。这可以通过将单词输出到一行，直到达到预定义的右边距来实现：

```
0can3al3cel5r3did<LF>
```

压缩后的字典现在包含 18 个字符，节省了 42% 的空间。然而，在实际中，实际字典中的条目在词典学意义上比本示例中的条目更接近，节省的空间也更大。使用更大的字典时，压缩比超过 50%。

这种字典压缩方案的一个局限性是，要从字典中解压缩一个单词，你必须知道前一个单词是什么，而前一个单词的解压缩又依赖于再前一个单词，以此类推。然而，在实际中，字典访问并不仅限于从头开始的串行搜索，因为以新字母开头的第一个单词不会从其前驱复制任何字母。因此，当文件中有 26 个单词（从以 `a` 开头的单词到以 `z` 开头的单词各一个）时，字典可以被相当快速地搜索。指针方案可以扩展为一个索引，指向每个两字母对（`aa`、`ab`，一直到 `zy`、`zz`）的开头，这样查找给定单词时需要读取的字典内容会更少。

下面的函数 `compress()` 在按字母顺序排列的 ASCII 文本文件上执行此压缩算法，每行一个单词。字典必须全部小写。0 到 9 的数字范围在 ASCII 序列中扩展，冒号（`:`）解释为 10，分号（`;`）解释为 11，以此类推。

互补函数 `expand()` 执行逆操作。它从由 `compress()` 压缩的文件生成一个 ASCII 文本文件，每行一个单词。

```
// compress.c

/*
Reads an alphabetized file (one word per line) and writes a compressed
version of the file. Words in the output file are preceded by a count
of characters identical to the previous word plus an offset of 48
(ASCII '0'), and these identical characters are omitted. Multiple words
are output on each line until column MAX_COL is reached. At this point,
the current word is made the last on the line by printing '\n'.
*/

void compress(void) {
    char prev[MAX_CHAR], word[MAX_CHAR], buf[MAX_CHAR];
    char *s, *t;
    int chrccount, linelen = 0;
    FILE *fpin, *fpout;

    fopen_s(&fpin, "dictionary.txt", "r");
    if (fpin == NULL) {
        printf("File could not be opened for input.\n");
        exit(1);
    }

    fopen_s(&fpout, "compressedDictionary.txt", "w");
    if (fpout == NULL) {
        printf("File could not be opened for output.\n");
        exit(1);
    }

    prev[0] = '\0';
    while (fgets(word, MAX_CHAR, fpin)) {
        if (strchr(word, '\n')) {
            word[strlen(word)-2] = '\0';
        }

        s = word;
        t = prev;
        chrccount = 0;
        while (*t != '\0' && (*s++ == *t++)) {
            ++chrccount;
        }

        buf[0] = chrccount + '0';
        buf[1] = '\0';
        strcat(buf, word[chrccount]);
        fputs(buf, fpout);
        linelen += 1 + strlen(&word[chrccount]);
        if (linelen >= MAX_COL) {
            linelen = 0;
            fputs("\n", fpout);
        }
        strcpy(prev, word);
    }

    fclose(fpin);
    fclose(fpout);
}
```

## // expand.c

> /*
> 读取由 compress() 创建的压缩文件并写入标准
> ASCII 文件，每行一个单词。
> */

```
void expand(void) {
    char prev[MAX_CHAR], word[MAX_CHAR];
    int samechr;
    FILE *fpIn, *fpOut;

    fopen_s(&fpIn, "compressedDictionary.txt", "r");
    if (fpIn == NULL) {
        printf("File could not be opened for input.\n");
        exit(1);
    }

    fopen_s(&fpOut, "newDictionary.txt", "w");
    if (fpOut == NULL) {
        printf("File could not be opened for output.\n");
        exit(1);
    }

    prev[0] = '\0';
    while ((samechr = getWord(word, fpIn)) >= 0) {
        strcpy(prev + samechr, word);
        fputs(prev, fpOut);
        fputs("\n", fpOut);
    }
    fclose(fpIn);
    fclose(fpOut);
}
```

```
int getWord(char *t, FILE *fpIn) {
    int c, count;

    while ((c = fgetc(fpIn)) < 'a') {
        count = c - '0';
        if (c == EOF) {
            return (-1);
        }
    }
    ungetc(c, fpIn);
    while ((c = fgetc(fpIn)) >= 'a') {
        *t++ = c;
    }
    ungetc(c, fpIn);
    *t++ = '\0';
    return(count);
}
```

在包含 482,884 字节的 50,000 单词字典上实现 compress() 会生成一个 185,339 字节的文件，压缩比为 61.62%。

## 字符串作业

- 下面的函数调用应该写入一个换行符，但有些是不正确的。找出哪些调用不起作用并解释原因。

  - a) `printf("%c", '\n');`
  - b) `printf("%c", "\n");`
  - c) `printf("%s", '\n');`
  - d) `printf("%s", "\n");`
  - e) `printf('\n');`
  - f) `printf("\n");`
  - g) `putchar('\n');`
  - h) `putchar("\n");`
  - i) `puts('\n');`
  - j) `puts("\n");`
  - k) `puts("");`

- 假设 `p` 已按以下方式声明：

  ```
  char *p = "abc";
  ```

  以下哪些函数调用是合法的？显示每个合法调用产生的输出，并解释其他调用为何非法。

  - a) `putchar(p);`
  - b) `putchar(*p);`
  - c) `puts(p);`
  - d) `puts(*p);`
