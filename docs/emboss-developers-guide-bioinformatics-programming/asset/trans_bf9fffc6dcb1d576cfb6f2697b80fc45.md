

- 1. 添加代码，从 ACD 文件处理中获取应用程序选项，而不是像原始代码那样处理它们
- 2. 识别从用户读取输入的函数，并更新函数调用
- 3. 将输出函数替换为对 EMBOSS 库的适当调用（如果可能）。

您必须识别任何从用户读取输入的函数，然后添加代码从 ACD 文件中获取值，而不是像原始代码那样处理它们。输出可以保留为原始应用程序生成的任何格式。您可以添加代码以使用 EMBOSS 库提供的输出函数。

显然，有必要仔细熟悉第三方源代码。可能需要在多个文件中进行编辑。这是移植软件的主要缺点。

其余部分说明了 ohmmalign 移植所采用的方法。

## 10.10 HMMER 移植

### 10.10.1 HMMER 移植：ohmmalign.acd

ACD 文件基本上与包装器中的相同，只是由于两个版本之间选项的差异而有一些更改。需要指出的一点是输出部分。在移植中，排列输出由 outfile ACD 数据项处理。包装器使用的 align 数据类型在当时不可用。

```
section: output
[
    information: "Output section"
    type: "page"
]

outfile: outfile
[
    parameter: "Y"
    knowntype: "hmmalign output"
]

endsection: output
```

### 10.10.2 HMMER 移植：ohmmalign.c

### 10.10.2.1 标题代码

这显示了 C 源代码的顶部。您可以立即看到，这里是原始 HMMER 代码和针对 EMBOSS 的添加的混合体。例如，EMBOSS 接口在第一个 include 指令之前导入。

```
/******************************
* HMMER - Biological sequence analysis with profile HMMs
* Copyright (C) 1992-1998 Washington University School of Medicine
* All Rights Reserved
*
* This source code is distributed under the terms of the
* GNU General Public License. See the files COPYING and LICENSE
* for details.
***********************************************************************/
/* hmmalign.c
* SRE, Thu Dec 18 16:05:29 1997 [St. Louis]
*
* main() for aligning a set of sequences to an HMM.
* RCS $Id: DevWrappingPorting.xml,v 1.30 2010/07/08 14:21:05 jonsourceforge Exp $
* Modified for EMBOSS by Alan Bleasby (ISMB 2001)
*/
#include "emboss.h"
#include <stdio.h>
#include <stdlib.h>

#include "structs.h"       /* data structures, macros, #define's */
#include "config.h"        /* compile-time configuration constants */
#include "funcs.h"         /* function declarations */
#include "globals.h"       /* alphabet global variables */
#include "squid.h"         /* general sequence analysis library */

#ifdef MEMDEBUG
#include "dbmalloc.h"
#endif

extern void emboss_rseqs(AjPSeqset seqset, char ***ret_rseqs,SQINFO **ret_sqinfo,int *ret_num);

static void include_alignment(char *seqfile, struct plan7_s *hmm, int do_mapped,
char ***rseq, char ***dsq, SQINFO
**sqinfo, struct p7trace_s ***tr, int *nseq);
```

### 10.10.2.2 main() 函数变量声明

此处显示了 main() 函数和变量声明。在尽可能保持原始代码不变的同时，有必要添加 AJAX 特定类型的变量来保存从 ACD 文件中检索的值。这些变量与之前一样设置为 NULL。

```
int main(int argc, char **argv)
{
const char *hmmfile;       /* file to read HMMs from */
HMMFILE *hmmfp;            /* opened hmmfile for reading */
const char *seqfile;       /* file to read target sequence from */
char **rseq;               /* raw, unaligned sequences */
SQINFO *sqinfo;            /* info associated with sequences */
char **dsq;                /* digitized raw sequences */
int nseq;                  /* number of sequences */
char **aseq;               /* aligned sequences */
AINFO ainfo;               /* alignment information */
float *wgt;                /* per-sequence weights */
int i;
struct plan7_s *hmm;       /* HMM to align to */
struct p7trace_s **tr;     /* traces for aligned sequences */
int be_quiet; /* TRUE to suppress verbose banner */
int matchonly; /* TRUE to show only match state syms */
const char *outfile; /* optional alignment output file */
FILE *ofp; /* handle on alignment output file */
AjPFile ajwithali; /* name of additional alignment file to align */
AjPFile ajmapali; /* name of additional alignment file to map */
AjBool ajmap = ajFalse;
AjPFile outf = NULL;
AjPStr outfname = NULL;
AjPFile inf = NULL;
AjPStr infname = NULL;
AjPSeqset seqset = NULL;
AjPStr ajseqfile = NULL;
char* mapali = NULL;
char* withali = NULL;
```

### 10.10.2.3 ACD 文件处理

这显示了从 ACD 检索值的代码。为此需要一些管家变量。mapali 和 withali 是 C 类型字符串（char *），用于保存 EMBOSS 输入文件的名称。名称通过调用 ajFileGetNameS 检索。然后关闭文件，使其准备好供 HMMER 使用。其他 HMMER 输入和输出文件也做了类似的操作：

```
/**********************************************************************/
* Parse command line
**********************************************************************/
matchonly = FALSE;
outfile = NULL;
be_quiet = FALSE;
withali = NULL;
mapali = NULL;

embInitP("ohmmalign",argc,argv,"HMMER");

ajmatch = ajAcdGetBoolean("matchonly");

if(ajmatch)
    matchonly=TRUE;
else
    matchonly=FALSE;

ajmapali = ajAcdGetInfile("mapalifile");

if (ajmapali)
    mapali = ajCharNewS(ajFileGetNameS(ajmapali));

ajFileClose(&ajmapali);
ajwithali = ajAcdGetInfile("withalifile");

if (ajwithali)
    withali = ajCharNewS(ajFileGetNameS(ajwithali));

ajFileClose(&ajwithali);

be_quiet=TRUE;

outf = ajAcdGetOutfile("outfile");
outfname = ajStrNewC((char *)ajFileGetNameC(outf));

if(*ajStrGetPtr(outfname)>31)
    ajFileClose(&outf);
outfile = ajStrGetPtr(outfname);

inf = ajAcdGetInfile("hmmfile");
infname = ajStrNewC((char *)ajFileGetNameC(inf));
ajFileClose(&inf);
hmmfile = ajStrGetPtr(infname);

seqset = ajAcdGetSeqset("sequences");
ajseqfile = ajStrNewC(ajStrGetPtr(seqset->Filename));
seqfile = ajStrGetPtr(ajseqfile);
```

### 10.10.2.4 处理输入数据

此处是管理数据输入的代码。您可以看到，用于保存 ACD 值的管家变量被传递到 HMMER 函数中。这里需要指出的唯一一点是，异常处理是通过调用 EMBOSS 函数 ajFatal 来处理的。显然，在编写移植时，有必要通读原始源代码：

```
/**********************************************************************
* Open HMM file (might be in HMMERDB or current directory).
* Read a single HMM from it.
*
* Currently hmmalign disallows the J state and
* only allows one domain per sequence. To preserve
* the S/W entry information, the J state is explicitly
* disallowed, rather than calling a Plan7*Config() function.
* this is a workaround in 2.1 for the 2.0.x "yo!" bug.
**********************************************************************/
if ((hmmfp = HMMFileOpen(hmmfile, "HMMERDB")) == NULL)
    ajFatal("Failed to open HMM file %s\n", hmmfile);

if (!HMMFileRead(hmmfp, &hmm))
    ajFatal("Failed to read any HMMs from %s\n", hmmfile);

HMMFileClose(hmmfp);

if (hmm == NULL)
    ajFatal("HMM file %s corrupt or in incorrect format? Parse failed", hmmfile);

hmm->xt[XTE] [MOVE] = 1.;    /* only 1 domain/sequence ("global" alignment)
/*hmm->xt[XTE] [LOOP] = 0.; */
P7Logoddssify(hmm, TRUE);

/* do we have the map we might need? */
if (mapali != NULL && ! (hmm->flags & PLAN7_MAP))
    ajFatal("HMMER: HMM file %s has no map; you can't use -mapali.", hmmfile);

/**********************************************************************
* Open sequence file in current directory.
* Read all seqs from it.
**********************************************************************/

