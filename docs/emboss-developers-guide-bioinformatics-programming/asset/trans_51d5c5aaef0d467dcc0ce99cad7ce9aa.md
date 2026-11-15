

ajFmtPrintAppS(&cmd, " --swexit %f ", swexit);

if(verbosity)
    ajStrAppendC(&cmd, " --verbose ");

构建命令行的其余代码如下。唯一需要指出的是，**append** 选项始终被设置。这意味着输出应始终追加到指定输出文件中的内容。不过，EMBOSS 默认会清除其输出文件，因此要使此功能生效，hmmfile ACD 数据项的 append : 属性必须设置为 True：

```
/* ACD option only allows one selection */
option = ajStrGetCharFirst(weighting[0]);

if(option == 'B')
    ajStrAppendC(&cmd, " -wblosum ");
else if(option == 'G')
    ajStrAppendC(&cmd, " -wgsc ");
else if(option == 'K')
    ajStrAppendC(&cmd, " -wme ");
else if(option == 'W')
    ajStrAppendC(&cmd, " -wpb ");
else if(option == 'V')
    ajStrAppendC(&cmd, " -wvoronoi ");
else if(option == 'N')
    ajStrAppendC(&cmd, " -wnone ");

if(o)
    ajFmtPrintAppS(&cmd, " -o %s ", ajFileGetNameC(o));

if(cfile)
    ajFmtPrintAppS(&cmd, " -cfile %s ", ajFileGetNameC(cfile));

/* -A (append) always set but file will be wiped by EMBOSS first unless
** append: "Y" is set for "hmmfile" in the ACD file.
*/
ajStrAppendC(&cmd, " -A -F ");
ajFmtPrintAppS(&cmd, " %S %S", hmmfilename, ajSeqsetGetFilename(alignfile));
```

## 10.6.2.6 调用应用程序

下面的代码展示了使用刚刚构建的命令行调用 **hmmbuild** 应用程序的系统调用。请注意，此处使用了 `system()`，但如前所述，可能应将其替换为对 `exec()` 的调用。还有一些用于内存管理的清理代码，以确保应用程序可以干净地关闭：

```
/* 4. Close ACD files */
ajSeqsetDel(&alignfile);
ajFileClose(&prior);
ajFileClose(&null);
ajFileClose(&pam);
ajFileClose(&hmmfile);
ajFileClose(&o);
ajFileClose(&cfile);

/* 5. Call hmmbuild */
ajFmtPrint("\n%s\n", cmd);
system(ajStrGetPtr(cmd));
/* 6. Exit cleanly */
ajStrDel(&n);
ajStrDel(&cmd);
ajStrDel(&rnd1);
ajStrDel(&rnd2);
ajStrDel(&tmp);
ajStrDel(&fmt);
ajStrDel(&hmmfilename);

embExit();

return 0;
}
```

## 10.7 HMMER 包装器：hmmalign

我们现在将介绍另一个 HMMER 应用程序 hmmalign。其基本功能是读取 HMM 配置文件和一组序列，将序列与配置文件比对，并输出多序列比对。调用方式如下：

```
hmmalign [options] hmmfile seqfile outfile
```

序列集可以是未比对的，也可以是已比对的。如果已比对，则会忽略现有的比对，hmmalign 将按其意愿对其进行比对。

hmmalign 仅作基本介绍，因为之前关于 hmmbuild 的几乎所有内容都适用于所有其他 HMMER 应用程序。

-outfile 参数是 EMBOSS HMMER 中的新增参数。多序列比对始终写入 outfile，而不是写入 stdout。

与 hmmbuild 不同，用户可以为序列输入指定 USA。这是因为 HMMER 会忽略任何比对，因此包装器可以将文件视为未比对序列，并在必要时将其转换为 HMMER 可理解的格式。应用程序会对其输入序列数据制作临时本地副本。由用户确保运行目录中有足够的磁盘空间。

原始 HMMER 的一些选项不受支持。再次强调，-h 是多余的。-informat、-oneline 和 -outformat 是为用户指定输入序列文件和输出比对的格式而提供的。包装器中不需要这些选项。

几乎任何序列格式都会被理解，而比对格式可以在 ACD 文件中指定，或通过使用内置的 -aformat 命令行限定符来指定。

## 10.7.1 HMMER 包装器：hmmalign.acd

ACD 文件非常简单。它只包含输入和输出部分。

## 10.7.1.1 输入部分

此处显示了输入部分的摘录。请注意，HMM 文件使用 infile，而序列输入使用 seqset。如前所述，EMBOSS 通常支持的所有序列格式均受到完全支持。

```
application: ehmmalign
[
# EMBOSS wrapper to hmmalign from Sean Eddy's HMMER package
# v.2.3.2
    documentation: "Align sequences to an HMM profile"
    groups: "HMM"
    gui: "yes"
    batch: "yes"
    cpu: "medium"
    embassy: "hmmernew"
]

section: input
[
    information: "Input section"
    type: "page"
]

infile: hmmfile
[
    parameter: "Y"
    information: "HMM file"
    knowntype: "hmm file"
    help: "File containing a HMM profile"
]

seqset: seqfile
[
    parameter: "Y"
    type: "gapstopprotein"
    help: "File containing a (set of) sequence(s)"
    aligned: "N"
]

...
endsection: input
```

## 10.7.1.2 输出部分

此处显示了输出部分。唯一需要指出的是，输出文件由 align 数据项处理，且比对格式由 aformat : 属性设置：

```
section: output
[
    information: "Output section"
    type: "page"
]

align: o
[
    parameter: "y"
    help: "Multiple sequence alignment output file."
    aformat: "fasta"
]

boolean: m
[
    additional: "Y"
    default: "N"
    information: "Only show match state alignment symbols."
]

boolean: q
[
    additional: "Y"
    default: "N"
    information: "Suppress all output except the alignment."
]
endsection: output
```

## 10.7.2 HMMER 包装器：ehmmalign.c

## 10.7.2.1 文档标题

此处显示了 C 源代码的开头。文档与 hmmbuild 的完全相同。

```
/* @source ehmmalign application
**
** EMBOSS wrapper to hmmalign from Sean Eddy's HMMER package v.2.3.2
** Align sequences to an HMM profile.
**
** @author Copyright (C) Jon Ison
** @@
**
** This program is free software; you can redistribute it and/or
** modify it under the terms of the GNU General Public License
** as published by the Free Software Foundation; either version 2
** of the License, or (at your option) any later version.
**
** This program is distributed in the hope that it will be useful,
** but WITHOUT ANY WARRANTY; without even the implied warranty of
** MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the
** GNU General Public License for more details.
**
** You should have received a copy of the GNU General Public License
** along with this program; if not, write to the Free Software
** Foundation, Inc., 59 Temple Place - Suite 330, Boston, MA 02111-1307, USA.
********************************************************************************/
#include "emboss.h"

/* @prog ehmmalign *********************************************************************************
**
** EMBOSS wrapper to hmmalign from Sean Eddy's HMMER package v.2.3.2
** Align sequences to an HMM profile.
**
******************************************************************************************/
```

## 10.7.2.2 main() 函数、清理和 ACD 文件处理

此处显示了 main() 函数、变量声明、处理 ACD 文件的代码以及一些清理代码。

```
int main(int argc, char **argv)
{
	/* ACD data item variables */
	AjPFile hmmfile = NULL;
	AjPSeqset seqfile = NULL;
	AjPFile mapali = NULL;
	AjPFile withali = NULL;
	AjPAlign o = NULL;
	AjBool m = ajFalse;
	AjBool q = ajFalse;

	/* Housekeeping variables */
	AjPStr cmd = NULL;
	AjPStr tmp = NULL;
	AjPStr fmt = NULL;
	AjBool fmtok = ajFalse;
	AjPStr rnd = NULL;
	AjPSeqout rndo = NULL;

	/* ACD file processing */
	embInitP("ehmmalign",argc,argv,"HMMERNEW");

	hmmfile = ajAcdGetInfile("hmmfile");
	seqfile = ajAcdGetSeqset("seqfile");
	mapali = ajAcdGetInfile("mapali");
	withali = ajAcdGetInfile("withali");
	o = ajAcdGetAlign("o");
	m = ajAcdGetBoolean("m");
	q = ajAcdGetBoolean("q");

	/* MAIN APPLICATION CODE */
	/* 1. Housekeeping */
	cmd = ajStrNew();
	tmp = ajStrNew();
	fmt = ajStrNew();
	rnd = ajStrNew();
```

## 10.7.2.3 文件格式处理

此处显示了将输入文件重新格式化为 HMMER 适用格式（即 FASTA）所需的代码。必须这样做，因为 hmmalign 仅在输入时理解 FASTA 格式，而且序列可能是通过 USA 指定的，需要将其转换为序列文件。

使用 ajFilenameSetTempname 设置可用的随机文件名，然后使用 ajSeqoutOpenFilename 以该文件名初始化 seqout 对象。

通过 ajSeqoutSetFormatS 设置输出格式。使用 ajSeqoutWriteSeq 写入序列。最后，使用 ajSeqoutClose 关闭文件并删除 seqout 对象：

```
/* 2. Re-write seqfile to a temporary file in a format (FASTA) HMMER can understand.
   We cannot just pass the name of seqfile to HMMER as the name provided might be
   a USA which HMMER would not understand. */
rnd = ajStrNew();
ajFilenameSetTempname(&rnd);
rndo = ajSeqoutNew();
```

