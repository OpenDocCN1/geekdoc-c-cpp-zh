```
valid: "Positive integer"
expected: "14"
]

integer: gapextend [
additional: "Y"
information: "Gap length penalty"
default: "4"
minimum: "0"
valid: "Positive integer"
expected: "4 for any sequence"

]
... lines omitted
```

# 2.4.3 Editing the C source file

The main() function for matcher is shown below. The application includes several functions and macros that are not shown:

```
#include "emboss.h"
/* @prog matcher **********************************************************
**
** Finds the best local alignments between two sequences
**
***********************************************************************/

int main(int argc, char **argv)
{
    AjPStr aa0str = 0;
    AjPStr aalstr = 0;
    const char *s1;
    const char *s2;
    ajint gdelval;
    ajint ggapval;
    ajint i;
    ajint K;

    AjPAlign align = NULL;

    embInit("matcher", argc, argv);

    .seq = ajAcdGetSeq("asequence");
    ajSeqTrim(seq);
    seq2 = ajAcdGetSeq("bsequence");
    ajSeqTrim(seq2);
    matrix = ajAcdGetMatrix("datafile");
    K = ajAcdGetInt("alternatives");
    gdelval = ajAcdGetInt("gapopen");
    ggapval = ajAcdGetInt("gapextend");
    align = ajAcdGetAlign("outfile");

    /*
    create sequence indices. i.e. A->0, B->1 ... Z->25 etc.
    This is done so that ajBasecodeToInt has only to be done once for
    each residue in the sequence
```