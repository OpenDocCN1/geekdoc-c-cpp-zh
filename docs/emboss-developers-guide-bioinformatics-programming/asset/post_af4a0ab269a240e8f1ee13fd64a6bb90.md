
```
ajbase.h ajcall.h ajcod.h \
ajdan.h ajdmx.h ajdom.h ajdomain.h ajexcept.h \
ajfeat.h ajfeatdata.h ajfile.h ajfmt.h \
ajgraph.h ajgraphxml.h ajgraphstruct.h ajhist.h ajindex.h ajjava.h ajlist.h \
ajmath.h ajmatrices.h ajmem.h ajmess.h ajnam.h ajnexus.h \
ajpat.h ajpdb.h ajpdbio.h ajphylo.h \
ajrange.h ajreg.h ajreport.h \
ajseq.h ajseqabi.h ajseqdata.h ajseqdb.h ajseqread.h ajseqtype.h ajseqwrite.h \
ajsort.h ajstr.h ajsys.h \
ajtable.h ajtime.h ajtranslate.h ajtree.h ajutil.h ajvector.h \
pcre.h pcre_chartables.c pcre_config.h pcre_get.c pcre_printint.c \
pcre_internal.h pcreposix.h
```

```
if ISCYGWIN
libajax_la_SOURCES = $(AJAXSRC) $(AJAXGSRC)
libajax_la_LDFLAGS = -version-info 5:0:0
else
libajax_la_SOURCES = $(AJAXSRC)
libajax_la_LDFLAGS = -version-info 5:0:0
libajaxg_la_SOURCES = $(AJAXGSRC)
libajaxg_la_LDFLAGS = -version-info 5:0:0
endif
```

## The NUCLEUS Makefile.am file:

```
## Process this file with automake to produce Makefile.in
lib_LTLIBRARIES = libnucleus.la
if ISSHARED
if ISAIXIA64
AM_CFLAGS = -Wl,-G -lm -L../ajax/.libs -lajax
else
AM_CFLAGS =
endif
endif
if ISCYGWIN
AM_LDFLAGS = -no-undefined -Wl,--add-stdcall-alias -Wl,
--export-all-symbols -Wl,--enable-auto-import -L../plplot -L../ajax -leplplot -
lajax
endif
INCLUDES = -I$(top_srcdir)/plplot $(X_CFLAGS) -I$(srcdir)/ -I$(top_srcdir)/ajax
LIBS =
NUCLSRC = embaln.c embcom.c embcons.c \
embdata.c embdbi.c embdmx.c embdomain.c \
embest.c embexit.c embgroup.c \
embiep.c embindex.c embinit.c \
embmat.c embmisc.c embmol.c \
embnmer.c embpat.c embpatlist.c embprop.c embpdb.c \
embread.c embsig.c \
embshow.c embword.c
libnucleus_la_SOURCES = $(NUCLSRC)
```

## 3.2 INTEGRATION AND COMPILATION

```
libnucleus_la_LDFLAGS = -version-info 5:0:0

include_HEADERS = emboss.h \
  embaln.h embcom.h embcons.h \
  embdata.h embdbi.h embdmx.h embdomain.h \
  embest.h embexit.h embgroup.h \
  embiep.h embindex.h embinit.h \
  embmat.h embmisc.h embmol.h \
  embnmer.h embpat.h embpatlist.h embprop.h embpdb.h \
  embread.h embsig.h \
  embshow.h embword.h
```

You must also add any new header files to ajax.h and/or emboss.h. ajax.h looks like this:

```
#ifdef __cplusplus
extern "C"
{
#endif

/*
**
** AJAX master include file
**
*/

#ifndef ajax_h
#define ajax_h

#include <stdio.h>

#include "ajarch.h"

#include <stdarg.h>
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
/*#include <malloc.h>*/

#include "ajassert.h"
#include "ajdefine.h"
#include "ajstr.h"
#include "ajtime.h"
#include "ajfile.h"
#include "ajlist.h"

#include "ajtable.h"
#include "ajnexus.h"
#include "ajfeat.h"
#include "ajseq.h"
#include "ajseqdata.h"
#include "ajseqtype.h"
#include "ajarr.h"
#include "ajseqread.h"
#include "ajseqwrite.h"
#include "ajindex.h"
#include "ajseqdb.h"
#include "ajseqabi.h"
#include "ajreport.h"
#include "ajfmt.h"
#include "ajmatrices.h"
#include "ajalign.h"

#include "ajrange.h"
#include "ajcod.h"
#include "ajmath.h"

...
... Entries omitted for brevity
...

#endif

#ifdef __cplusplus
}
#endif
```

emboss.h looks like this:

```
#ifndef emboss_h
#define emboss_h

#include "ajax.h"
#include "ajgraph.h"
#include "embaln.h"
#include "embcom.h"
#include "embcons.h"
#include "embdbi.h"

...
... Entries omitted for brevity
...

#ifdef WIN32
#define VERSION "5.0.0"
#endif

#endif
```

## 3.3 Debugging

Bugs are problems with code that cause it to crash or operate in an unexpected way. They arise through erroneous use of syntax (which is not always caught by compilers) and errors in the code logic. This section gives some practical hints for debugging EMBOSS code.

### 3.3.1 Direct debugging

Very broadly, debugging proceeds in four stages, where bugs are fixed that:

- 1. Prevent the program from compiling
- 2. Cause the program to crash
- 3. Cause the program to operate incorrectly
- 4. Manifest under extensive test conditions.

With experience, most bugs are obvious from visual inspection of the code. It is highly recommended that, *before* you compile your code, you read then reread it until you’re satisfied it should work as expected. Be scrupulous when writing the code itself. Avoid the temptation to code too quickly; the extra time spent avoiding errors in the first place will be very well rewarded later.

> **Tip**
>
> A simple and powerful debugging method is to use `ajFmtPrint` and `fflush(stdout)` statements to report values of key variables at different stages of execution, allowing you to trace and identify problems. `ajFmtPrint` is used to print variables, and `fflush` is called immediately afterwards to flush the output buffer. This is important as the output buffer might have content at the point of the crash, which will only be printed to screen by calling `fflush(stdout)`. Most bugs are easily squashed using this method.

When writing your code, there will be many stages where you know in advance what value (s) a variable should (or should not) have, particularly when checking a function’s arguments or return values. For instance, the value of a pointer used by a function should in most cases not be `NULL`. At all such places, at least in early versions of the code, code should be added to trap errors and raise appropriate warnings, alerting you to potential bugs before they manifest.

AJAX functions in `ajmess.h` provide various levels of error handling. Each of the following format and output an exception message (provided as a string):

| Function | Description |
|----------|-------------|
| ajUser | Report an informative message |
| ajWarn | Report a warning message |
| ajErr | Report an error message |
| ajExit | Report a message then exit |
| ajDie | Report a message then crash (kill) the application |
| ajDebug | Report a general debugging message to the file `programname.dbg` if the switch `-debug` was given on the command line |

Messages go to `stdout` or `stderr` (in both cases usually the screen) or, in the case of `ajDebug`, to the file `programname.dbg`.

> **Important**
>
> The EMBOSS code makes extensive use of `ajDebug` so that bugs reported by users can easily be traced. The typical way therefore to debug applications is to produce a debug trace using `-debug`.

In practice, much of the error-trapping code can, for purposes of speed, be commented out or removed once extensive testing of the code is complete. This is especially true for library function code where speed is paramount.

For the vast majority of applications, ajDebug and the other functions above will suffice. In special circumstances, however, you might need to write your own exception handling functions. An AJAX library file ajmess is provided for this (see Section 6.23, ‘Handling exception messages’).

### 3.3.2 AJAX debugging functions

Most AJAX library files include functions for debugging the code in that library file. These usually call ajDebug. Typically functions are provided to report on the internal state of data structures defined in that library file. In some cases special debugging files are provided. For example, there is a “debug” output sequence format used when debugging sequence output, and a “trace feature table” used when debugging report formats.

For more information, see the library documentation for AJAX and NUCLEUS. See also the programming guides (Section 3.1, ‘EMBOSS programming’) for individual library files.

### 3.3.3 Controlling debugging behaviour

The default behaviour of EMBOSS is not to report debugging information generated by calls to ajDebug. The global command line qualifier -debug can be used to turn debugging on for any EMBOSS application. For example, if you think you have found a bug when the following command is issued:

```
secret sequence.seq
```

then debugging can be turned on as follows:

```
secret sequence.seq -debug
```

This will create a debug file called secret.dbg. Debugging could be explicitly turned off by prepending the qualifier with no:

```
secret sequence.seq -nodebug
```

but there’s normally no need to do this as the default is false (no debugging) anyway. It could however be useful if debugging was turned on by default in the EMBOSS configuration files or by an environment variable. Debugging can be globally switched on using the EMBOSS environment variable:

```
EMBOSS_DEBUG
```
