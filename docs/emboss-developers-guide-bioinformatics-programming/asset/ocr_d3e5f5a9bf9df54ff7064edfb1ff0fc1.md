+   1. Add code to pick up application options from ACD file processing rather than processing them as in the original
+   2. Identify functions that read input from user and update the function calls
+   3. Replace the output functions with appropriate calls to the EMBOSS libraries (possibly).

You must identify any functions that read input from the user, then add code to pick up values from the ACD file instead of processing them as in the original. The output can be left in whatever format is produced by the original application. You might add code to use the output functions provided by the EMBOSS libraries.

Clearly it's necessary to carefully familiarise yourself with the third-party source code. It might be necessary to make edits across multiple files. This is the main disadvantage to porting software.

The remaining sections illustrate the approach taken for the port ohmmalign.

# 10.10 HMMER port

# 10.10.1 HMMER port: ohmmalign.acd

The ACD file is essentially the same as in the wrapper apart from a few changes resulting from differences in options between the two releases. One thing to point out is in the output section. In the port the alignment output is handled by an outfile ACD data item. The align datatype that the wrapper used wasn't available at the time.

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

# 10.10.2 HMMER port: ohmmalign.c

# 10.10.2.1 Heading code

This shows the top of the C source code. You can see straight away that there's an amalgamation of the original HMMER code and additions for EMBOSS. For example the EMBOSS interface is imported before the first include directive.

```
/******************************
* HMMER - Biological sequence analysis with profile HMMs
* Copyright (C) 1992-1998 Washington University School of Medicine
* All Rights Reserved
```