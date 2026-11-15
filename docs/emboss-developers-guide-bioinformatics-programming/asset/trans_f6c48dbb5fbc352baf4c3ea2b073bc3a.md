

if(!ajSeqoutOpenFilename(rndo, rnd))
    ajFatal("Failed to open file '%s'", rnd);
ajSeqoutSetFormatC(rndo, "fasta");
ajSeqoutWriteSet(rndo, seqfile);
ajSeqoutClose(rndo);
ajSeqoutDel(&rndo);

## 10.7.2.4 构建命令行

以下是构建命令行的代码。再次强调，命令行是按特定顺序构建的，以便将来更易于维护。

这里需要指出的是，EMBOSS 支持某些原始 HMMER 不支持的比对格式，而 HMMER 支持某些 EMBOSS 不支持（或在撰写本文时不支持）的格式。

如果用户指定的格式不受支持，则会引发异常并将格式设置为 Stockholm。将来，这可以替换为根据需要重新格式化输出文件的代码。

```
/* 3. Build hmmalign command line */
/* Command line is built in this order:
i. Application name.
ii. HMMER 'options' (in order they appear in ACD file)
iii.HMMER 'options' (that don't appear in ACD file)
iv. HMMER and new parameters.
*/
ajFmtPrintS(&cmd, "hmmalign ");

if(mapali)	ajFmtPrintAppS(&cmd, " -mapali %s ", ajFileGetNameC(mapali));

if(withali)	ajFmtPrintAppS(&cmd, " --withali %s ", ajFileGetNameC(withali));

if(m)	ajStrAppendC(&cmd, " -m ");

if(q)	ajStrAppendC(&cmd, " -q ");

/* Ensure output alignment is in user-specified format. */
fmtok=ajTrue;
ajStrAssignS(&fmt, ajAlignGetFormat(o));
/* fasta and a2m are identical formats. */

if(ajStrMatchC(fmt, "fasta"))	ajStrAssignC(&fmt, "A2M");
else if(ajStrMatchC(fmt, "a2m"))	ajStrAssignC(&fmt, "A2M");
else if(ajStrMatchC(fmt, "msf"))	ajStrAssignC(&fmt, "MSF");
else if(ajStrMatchC(fmt, "phylip"))	ajStrAssignC(&fmt, "PHYLIP");
/* hmmmer also supports stockholm, SELEX and Clustal output, EMBOSS does not.
** EMBOSS supports unknown/multiple/simple and srs output, hmmmer does not.
*/
else
fmtok = ajFalse;
if(!fmtok)
{
    /* This could be replaced with code to reformat the file. */
    ajWarn("Specified output alignment format ('o' ACD option) is "
           "not understood by HMMER. Using stockholm format instead.");
    ajStrAssignC(&fmt, "Stockholm");
}
```

## 10.7.2.5 调用应用程序

这展示了调用 hmmalign 应用程序的代码。同样，对 system() 的调用可能应该替换为对 exec() 的调用。可以看到，一个名为 rnd 的临时变量用于重写的序列输入文件的名称。必须使用 -inform 选项显式指定 FASTA 格式。

```
/* rnd is the name of the rewritten seqfile. MUST specify FASTA format explicitly. */
ajFmtPrintAppS(&cmd, " --inform FASTA --outformat %S -o %s %s %S",
               fmt,
               ajAlignGetFilename(o),
               ajFileGetNameC(hmnfile),
               rnd);

/* 4. Close ACD files */
ajFileClose(&hmnfile);
ajSeqsetDel(&seqfile);
ajFileClose(&mapali);
ajFileClose(&withali);
ajAlignDel(&o);

/* 5. Call hmmalign */
ajFmtPrint("\n%s\n\n", cmd);
system(ajStrGetPtr(cmd));

/* 6. Exit cleanly */
ajFmtPrintS(&tmp, "rm %s", rnd);
system(ajStrGetPtr(tmp));

ajStrDel(&cmd);
ajStrDel(&tmp);
ajStrDel(&fmt);
ajStrDel(&rnd);

embExit();

return 0;
}
```

## 10.8 减少命令行长度

在封装具有许多可能命令行限定符的应用程序时，可能会出现问题。MIRA 包就是一个例子，它大约有一百个限定符。对于这样的包，不能明智地采用构建包含所有可能限定符的命令行的方法；命令行可能对 shell 来说太长，而且肯定难以阅读和调试。

MIRA 封装器采用两种方法来避免命令行混乱。第一种是使用 ajAcdIsUserdefinedC 库函数。下面的代码片段演示了这一点：

```
...
AjPStr cl = NULL;
AjPStr squal = NULL;
...
if(ajAcdIsUserdefinedC("genome"))
{
    squal = ajAcdGetListSingle("genome");
    ajFmtPrintAppS(&cl, " -genome%S", squal);
    ajStrDel(&squal);
}
```

ajAcdIsUserdefinedC 函数调用检查用户是否针对命名的 ACD 限定符名称输入了任何内容，或者是否在命令行上为该限定符指定了值。如果其中任何一种情况为真，则上述代码从 ACD 检索值，并将限定符和值添加到命令行中。如果用户未提供值，则（正确）假设 MIRA 程序将使用默认值，因此命令行保持不变。

这种方法效果相当不错，但有一个缺点。如果用户输入了任何内容，ajAcdIsUserdefinedC 调用将返回真值；这包括输入 ACD 中给定限定符的默认值。最好是命令行中不包含不必要的指定的默认值。MIRA 封装器中其余代码（即第二种方法）所做的正是如此。研究这段代码是一个有用的练习。

由于 MIRA 允许用户可选地提供一个可以附加到命令行限定符的前缀，因此代码变得稍微复杂了一点。例如，限定符 -project 也可以指定为 -GE:project，因为它属于“GEneral”输入选项类。因此，封装器首先在静态数组中列出所有限定符及其前缀。然后，它将它们全部加载到 AjPTable 查找表中，作为 main() 中的第一项工作之一（代码很简单，因此此处未显示）

```
typedef struct MiraSPrefix
{
    const char* qname;
    const char* prefix;
} MiraOPrefix;
#define MiraPPrefix MiraOPrefix*

static MiraOPrefix miraprefix[] = {
    {"project", "GE:"},
    {"lj", "GE:"},
    {"fo", "GE:"},
    {"mxti", "GE:"},
    {"rns", "GE:"},
    {"eq", "GE:"},
    {"eqo", "GE:"},
    {"droeqe", "GE:"},
    {"uti", "GE:"},
    {"ess", "GE:"},
    {"ps", "GE:"},
    ...
    {NULL, NULL}
};
```

在解释了这一复杂性之后，现在可以描述封装器使用的策略了。封装器程序员浏览 ACD 文件，并为 C 代码将所有不同的数据类型分组。换句话说，封装器将把所有字符串数据类型作为一个代码部分来处理，然后是所有输入文件数据类型，等等。以字符串数据类型为例，封装器在另一个静态块中定义了这些内容。

```
typedef struct MiraSquals
{
    const char* qname;
    const char* mname;
    const char* def;
} MiraOQuals;
#define MiraPQuals MiraOQuals*

static MiraOQuals miraStrings[] =
{
    {"project", "project", "mira"},
    {"bsn", "bsn", ""},
    {"np", "np", "mira"},
    {"gapfda", "gap4da", "gap4da"},
    {"log", "log", "miralog"},
    {"co", "co", "mira_out.caf"},
    ...
    {NULL, NULL, NULL}
};
```

MiraSquals 结构体用于定义所有其他数据类型名称块以及字符串。对于每个定义块，变量 qname 是 ACD 中指定的限定符名称，变量 mname 是要在命令行上打印的名称（如您所见，对于 gapfda 它们不同），而 def 是 ACD 文件中指定的限定符的默认值。这就是该方法的微小缺点所在，即您必须在 ACD 文件和 C 代码中都指定默认值。您还显然应该确保它们匹配，尽管如果不匹配也不会造成太大危害——您只是会在命令行上看到一个意外的限定符。在这种情况下，优点大于缺点。接下来需要做的就是为每种数据类型编写一个简单的函数，并从 main() 中调用该函数。处理字符串的函数如下所示：

```
static void emira_dostrings (AjPStr *cl, AjPTable table)
{
    ajuint i;
    AjPStr squal = NULL;
    AjPStr prefix = NULL;
    AjPStr key = NULL;
    AjPStr value = NULL;

    prefix = ajStrNew();
    key = ajStrNew();

    i = 0;
    while(miraStrings[i].qname)
    {
        squal = ajAcdGetString(miraStrings[i].qname);
        ajStrAssignC(&key,miraStrings[i].qname);
        ajStrAssignC(&prefix,"");
        value = ajTableFetch(table, key);
        if(value)
            ajStrAssignS(&prefix,value);
        if(!ajStrMatchC(squal,miraStrings[i].def))
            ajFmtPrintAppS(cl, " -%Ss=%S",prefix,miraStrings[i].mname,squal);
            ajStrDel(&squal);
            ++i;
    }
    ajStrDel(&key);
    ajStrDel(&prefix);
    return;
}
```

代码按顺序查看定义的字符串静态表。首先，代码从 ACD 检索关联值。然后，它在限定符前缀表中查找任何关联的前缀值，并相应地设置变量（对于大多数包不需要这样做，因此代码可以简化）。然后，它将从 ACD 检索的值与静态定义块中给出的默认值进行比较，只有在两个值不匹配时才将限定符添加到命令行中。

这段代码的结果是一个整洁干净的命令行。该代码的另一个优点是，它避免了在封装器开头定义一长串难看的 `ajAcdGet*` 函数调用块。尽管您可能认为这种方法对于封装接口更简单的包来说有些过度设计，但它仍然值得考虑，因为生成的封装器更易于维护。

## 10.9 如何移植第三方应用程序

开发封装器时完成的大部分步骤在移植软件时也需要完成。仍然需要 ACD 文件。主要区别在于编写源代码。基本步骤相同：

- 1. 实现 C 源代码
- 2. 头文件文档
- 3. 空 main() 函数
- 4. 调用 embInitPV
- 5. 用于处理 ACD 数据项的变量
- 6. 调用 ajAcdGet* 以检索 ACD 值
- 7. 清理 ACD 变量的代码。

对于移植，需要考虑的事情要多得多。main() 函数需要重写以处理 ACD 文件处理，如下所示：

