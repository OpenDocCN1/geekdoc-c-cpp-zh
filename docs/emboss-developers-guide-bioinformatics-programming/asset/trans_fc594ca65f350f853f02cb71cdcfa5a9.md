

## 10.10.2.5 干净退出

然后有大量未显示的本机代码。最后，程序必须通过调用 embExit() 来退出：

```
if (outfile != NULL && (ofp = fopen(outfile, "w")) != NULL)
{
WriteSELEX(ofp, aseq, &ainfo, 50);
printf("Alignment saved in file %s\n", outfile);
fclose(ofp);
}
else
WriteSELEX(stdout, aseq, &ainfo, 50);

/********************************************************************
* Cleanup and exit
********************************************************************/
for (i = 0; i < nseq; i++)
{
P7FreeTrace(tr[i]);
FreeSequence(rseq[i], &(sQinfo[i]));
free(dsq[i]);
}

FreeAlignment(aseq, &ainfo);
FreePlan7(hmm);
free(sQinfo);
free(rseq);
free(dsq);
free(wgt);
free(tr);

SqdClean();

ajStrDel(&outfname);
ajStrDel(&infname);
ajStrDel(&ajseqfile);

#ifdef MEMDEBUG
current_size = malloc_inuse(&histid2);
if (current_size != orig_size) malloc_list(2, histid1, histid2);
else fprintf(stderr, "[No memory leaks.]\n");
#endif
```

```
embExit();
return 0;
}
```

## 10.11 总结

将第三方应用程序集成到 EMBOSS 中需要大量工作，无论应用程序是被包装还是移植。不过，这项工作非常值得，因为在分发方面（软件将触达更多用户）以及在某些情况下，培训、支持和维护成本会降低。此外，任何集成的软件都可以使用 EMBOSS 的内置功能，例如对常见序列格式的支持，并将集成到众多可用的 EMBOSS 接口中。这些接口包括图形用户界面、工作流软件和 Web 服务。

完全移植的软件提供最大的灵活性，但这伴随着相对较高的维护成本。尽管如此，当代码将被 EMBOSS 本质上采纳时，这是首选路径。通过使用临时文件，包装器中也可以实现或多或少相同的灵活性，尽管这种方法有缺点和潜在的复杂性。例如，需要用于相互转换文件格式的代码。

## 附录 A ACD 语法参考

### A.1 ACD 语法简介

#### A.1.1 一般语法

Ajax 命令定义（ACD）语言专为编写 EMBOSS 应用程序的 ACD 文件而设计。ACD 语法允许对应用程序的参数及其命令行界面进行非常灵活的描述。它可以指定命令行或其他界面（例如网页）上可以出现的所有内容。

ACD 文件是纯 ASCII 文本文件，*必须*具有 .acd 扩展名。通常它们与应用程序同名，但这不是强制性的。

##### A.1.1.1 空白字符

在解析 ACD 文件时，整个文件内容实际上被视为一个字符串，并被解析为由 *空格* 字符分隔的标记。各个标记之间需要一个空格：多余的空白字符将被忽略。

##### A.1.1.2 注释

可以添加注释行，注释行以 “#” 开头，并持续到行尾。

### A.1.2 ACD 定义

ACD 文件包含一个 *应用程序定义* 和每个参数的 *数据定义*。先给出应用程序定义，然后是数据定义。数据定义组织成各个部分（第 A.1.6 节，‘ACD 文件部分’）。

应用程序和数据定义具有以下一般形式：一个文本标记，后跟冒号 ‘:’（或 ‘=’）和一个空格，然后是第二个标记。定义体紧随其后，由一个或多个属性组成，这些属性由强制的一对方括号 [ ] 分隔，可以跨多行。每个属性都是一个 *名称*: *值* 对，属性值放在引号（“ ”）中：

或者：

```
token: token
{
    Attribute1Name: "Attribute1Value"
    Attribute2Name: "Attribute2Value"
}
```

或：

```
token=token
[
    Attribute1Name: "Attribute1Value"
    Attribute2Name: "Attribute2Value"
]
```

第一个标记要么是 application:（用于应用程序定义），要么是数据定义的 AJAX 数据类型（例如 sequence）。第二个标记要么是应用程序的名称（例如 secret），要么是参数的名称（例如 asequence）。

应用程序定义：

```
application: ApplicationName
{
    ApplicationAttribute1Name: "ApplicationAttribute1Value"
    ApplicationAttribute2Name: "ApplicationAttribute2Value"
}
```

数据定义：

```
Datatype: ParameterName
{
    DataAttribute1Name: "DataAttribute1Value"
    DataAttribute2Name: "DataAttribute2Value"
}
```

应用程序标记以及数据类型和属性名称的标记可以缩写，直到不再产生歧义为止。不过，不推荐这种缩写，因为它们往往会使 ACD 文件更难以阅读。

属性值通常用双引号括起来，但这仅对包含空白字符的值（通常是字符串）是强制性的。

### A.1.2.1 应用程序定义

应用程序定义必须是文件中的第一个定义：

```
application: ApplicationName
{
    ApplicationAttribute1Name: "ApplicationAttribute1Value"
    ApplicationAttribute2Name: "ApplicationAttribute2Value"
}
```

应用程序名称是任意的，但通常与 ACD 文件名相同。应用程序 C 源代码中用于将其与 ACD 文件关联的是 ACD 文件名（如果不同，则不是 ApplicationName）。这样，可以为单个应用程序 C 源代码文件开发多个 ACD 文件（因此也有多个命令行界面）。

有关可用应用程序属性的完整描述，请参见第 A.3 节 ‘应用程序属性’。

### A.1.2.2 数据定义

所有应用程序参数都必须有数据定义。数据定义紧随应用程序定义之后，并且必须放在适当的文件部分中（第 A.1.6 节，‘ACD 文件部分’）：

```
Datatype: ParameterName
{
    DataAttribute1Name: "DataAttribute1Value"
    DataAttribute2Name: "DataAttribute2Value"
}
```

Datatype 必须是有效的 ACD 数据类型（参见第 A.2 节，‘数据类型’）。

ParameterName 是参数的名称。它是一个必须符合某些约定的字符串（第 A.1 节，‘ACD 语法简介’）。此名称用于从命令行和 C 源代码中引用数据定义（参见第 6.3 节，‘处理 ACD 文件’）。

有关可用属性的完整描述，请参见：第 A.4 节 (‘全局属性’)、第 A.5 节 (‘特定于数据类型的属性’) 和第 A.6 节 (‘计算属性’)。

### A.1.3 参数命名约定

#### A.1.3.1 一般约定

参数和限定符名称：

- 不得包含空白字符
- 通常不应为单个字符
- 应尽可能是有意义的单词，并指示选项的功能
- 不区分大小写。

#### A.1.3.2 特定于数据类型的约定

参数名称的一些约定适用于单个数据类型。在 ACD 文件中指定多个同一数据类型的实例时，可以将字符 a、b 等追加到标志：asequence、bsequence 等。这在表中通过参数名称中的星号表示，例如 *sequence。

| 数据类型 | 名称 | 用途 |
|---|---|---|
| sequence | sequence, *sequence | 主要输入序列，通常是必需的 |
| seqall | sequence, *sequence, seqall | 主要输入序列数据库，通常是必需的 |

### A.1 ACD 语法简介

| 参数 | 类型/名称 | 描述 |
| :--- | :--- | :--- |
| seqset | sequence, *sequence, sequences | 主要输入序列，通常是必需的 |
| seqsetall | sequence, *sequence, sequences | 主要输入序列，通常是必需的 |
| seqout, seqoutset, seqoutall | outseq, *outseq, *outfile | 主要输出序列，通常是必需的，通常应默认为主要输入序列名称，扩展名默认为输出序列格式的名称 |
| outfile | outfile, *file | 主要输出非序列结果文件，通常是必需的。文件扩展名应允许默认为应用程序名称。outfile 应用于第一个输出文件。outfile 或 *file 可用于第二个及后续输出文件 |
| report | outfile, *file | 报告输出文件。outfile 应用于第一个报告文件。outfile 或 *file 可用于第二个及后续报告文件 |
| align | outfile, *file | 比对输出文件。outfile 应用于第一个输出比对。outfile 或 *file 可用于第二个及后续输出比对 |
| infile | infile, *file | 主要输入非序列文件 |
| infile | data | 主要辅助输入数据文件，通常是可选的 |
| infile | patterns | 用于在序列中搜索的模式文件 |
| integer | minlen | 要查找的序列特征的最小长度 |
| integer | maxlen | 要查找的序列特征的最大长度 |
| integer | wordsize | 用于哈希表等的字长。通常最小值 = 2（蛋白质），4（DNA） |
| integer | window | 用于计算点图、特征等的窗口长度 |
| integer | shift | 每次迭代中窗口移动的量 |
| boolean | consensus | 是否应输出共识序列的标志 |
| float | gap | 间隙罚分 |

