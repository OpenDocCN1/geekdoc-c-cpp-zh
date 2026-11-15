
The required directories are as follows:

- src
  The “applications directory” holding the application C source code. This should contain a Makefile.am file.

- emboss_acd
  The “ACD directory” holding the application ACD files. This should contain a Makefile.am file (see below).

- emboss_doc
  The “documentation directory”. This contains the following sub-directories: html : documentation in HTML format text : documentation in plain text format master : documentation in final format with include files There is a Makefile.am file in this directory and in the html and text sub-directories, all of which need editing when the new package is created. A semi-automated process (Appendix 8, Application documentation standards) is used to create the files of documentation in these directories.

- DOCS
  This was intended for peripheral documentation but is not currently used.

- m4
  This contains macro files used in the automake process. The files can be copied from another EMBASSY package.

Additionally, some packages may have the following directories:

- include
  Header files that are specific to the package.

- data
  Data files that are specific to the package.

The CVS directory only appears if the package has been committed to the CVS server.

The required files are as follows. If you omit any of these then the GNU software will complain when you come to bundle the EMBASSY package into a distribution file; the GNU software will then usually add a default file:

- README
  This is the package user guide and normally contains general comments about the package as a whole such as installation instructions, usage notes and so on. It should not normally contain documentation about individual applications. The README is not strictly required but is very highly recommended, especially where the package contains wrappers to third-party applications (see Section 10.2, ‘Wrappers and ports’) and there are differences between the original applications and the wrappers.

- COPYING
  Copyright or other information on usage restrictions. This might just be a reference to the README file where such information is given, or contain the GPL licence or something else.

- INSTALL
  Standard installation instructions for EMBASSY packages. This file can be copied from another EMBASSY package.

- NEWS
  Package version information. It is used in making a bundled distribution file (via make dist).

- AUTHORS
  Author contact details. Where an EMBASSY package contains wrapper applications, both the authors of the original software and the EMBASSY package should be mentioned.

| File | Description |
|---|---|
| ChangeLog | The log file of changes made to the package. It is helpful to provide one but not strictly necessary. |
| configure.in | The configure file that is processed using autoconf to produce a configure script (see Section 1.2, 'Installation of CVS (Developer's) Release'). It should be copied from another EMBASSY package but requires some simple customisation before it can be used (see Section 3.2.4.3, 'Editing the configure.in files'). |
| ltmain.sh | The libtool package front-end script. It can be copied from another EMBASSY package. |

Other files can be given. For example, HMMERNEW includes documentation for the original HMmer application.

## 3.2.4.2 Editing the Makefile.am files

The Makefile.am files used in EMBASSY are different from those used in the main EMBOSS package. When creating a new EMBASSY package, there are six Makefile.am files which must be edited, in each of the following directories:

- /packagename/
- /packagename/src
- /packagename/emboss_acd
- /packagename/emboss_doc
- /packagename/emboss_doc/html
- /packagename/emboss_doc/text

The required edits to these files should be obvious from inspecting the files below, which are for the myemboss package.

### /myemboss/Makefile.am

The file is shown below:

```
#
SUBDIRS = source emboss_acd emboss_doc

EXTRA_DIST = depcomp ltmain.sh install-sh config.sub config.guess

# tar to pick up the other directories
# then remove any CVS subdirectories

dist-hook:
	tar cBf - emboss_acd | ( cd $(distdir); tar xBf - ; cd emboss_acd; rm -rf CVS)
	tar cBf - emboss_doc | ( cd $(distdir); tar xBf - ; cd emboss_doc; rm -rf CVS; rm -rf master)
```

The SUBDIRS line must reference all top-level subdirectories in the package for which there are Makefile.am files.

The dist-hook entry must be edited accordingly.

### /myemboss/src/Makefile.am

The file is shown below:

```
## Process this file with automake to produce Makefile.in

EXTRA_DIST = Makefile.am

bin_PROGRAMS = myseq mytest

if LOCALLINK
INCLUDES = -I../include -I../../../nucleus -I../../../ajax -I../../../plplot
else
INCLUDES = -I../include -I${embprefix}/include -I${embprefix}/include/eplplot
endif

if ISSHARED
if ISAXIA64
if LOCALLINK
AM_CFLAGS = -Wl,-bdynamic -Wl,-brtl -L../../../plplot/.libs -L../../../ajax/.libs -L../../../nucleus/.libs -lnucleus -lajax -leplplot
else
AM_CFLAGS = -Wl,-bdynamic -Wl,-brtl -L${embprefix}/lib -lnucleus -lajax -leplplot
endif
else
AM_CFLAGS =
endif
endif

myseq_SOURCES = myseq.c
mytest_SOURCES = mytest.c

if LOCALLINK
LDADD = ../../../nucleus/libnucleus.la ../../../ajax/libajaxg.la ../../../ajax/libajax.la ../../../plplot/libeplplot.la $(XLIB)
else
LDADD = -L${embprefix}/lib -lnucleus -lajaxg -lajax -leplplot $(XLIB)
endif
```

The names of all the applications must be given on the bin_PROGRAMS entry, which may span multiple lines if these are delimited by a backslash character. A reference to the C source code file of each application is given towards the bottom of the file, for example
myseq_SOURCES = myseq.c.

### /myemboss/emboss_acd/Makefile.am

```
EXTRA_DIST = Makefile.am

pkgdata_DATA = myseq.acd mytest.acd

pkgdatadir=${prefix}/share/EMBOSS/acd
```

The name of all the application ACD files must be given following the pkgdata_DATA entry, which may span multiple lines.

### /myemboss/emboss_doc/Makefile.am

```
SUBDIRS = html text
```

The file does not typically require editing.

### /myemboss/emboss_doc/html/Makefile.am

```
pkgdata_DATA = index.html \
myseq.html

pkgdatadir=${prefix}/share/EMBOSS/doc/html/embassy/myseq
```

All the application documentation files (Chapter 8, Application documentation standards) in HTML format must be listed in the pkgdata_DATA entry, which may span multiple lines. Any other documentation files that are automatically generated are listed here also. The line beginning with pkgdatadir= must be changed so that it gives the correct package name.

### /myemboss/emboss_doc/text/Makefile.am

The file is shown below:

```
pkgdata_DATA = myseq.txt

pkgdatadir=${prefix}/share/EMBOSS/doc/programs/text
```

This is essentially the same as /myemboss/emboss_doc/html/Makefile.am but references the documentation in plain text format.

## 3.2.4.3 Editing the configure.in files

Two lines only need to be edited here:

- The AC_INIT line must be changed so that it references one (any) application C source code file in the package.
- The AM_INIT_AUTOMAKE line should give the package name and version number.

Once the application ACD files and C source code are written and integrated, compilation is as for any other EMBASSY package (see Section 3.2.1, ‘Using myemboss for application development’).

## 3.2.5 Adding new functions and datatypes

Any new functions and datatypes added to AJAX or NUCLEUS should be properly documented (Section D.1, ‘Code documentation standards’) if they are to be incorporated into the EMBOSS distribution. To compile the new code, type:

```
make
```

from the AJAX or NUCLEUS directory as appropriate. Of course, you will need to recompile any statically linked applications to use the changes. Alternatively, recompile the whole package by typing make from the second-level EMBOSS directory, e.g.:

```
/home/auser/emboss/emboss/
```

## 3.2.6 Adding new library files

If you have added entirely new library files then these must be integrated into AJAX or NUCLEUS by editing the Makefile.am in the AJAX or NUCLEUS directory as appropriate.

An excerpt of the AJAX Makefile.am file:

```
## Process this file with automake to produce Makefile.in

if ISCYGWIN
lib_LTLIBRARIES = libajax.la
else
lib_LTLIBRARIES = libajax.la libajaxg.la
endif

if ISSHARED
if ISAIA64
if NEEDAJAX
AM_CFLAGS = -Wl,-G -L../plplot/.libs -L.libs -lajax -leplplot -lm
else
AM_CFLAGS = -Wl,-G -L../plplot/.libs -L.libs -leplplot -lm
endif
else
AM_CFLAGS =
endif
endif

if ISCYGWIN
AM_LDFLAGS = -no-undefined -Wl,--add-stdcall-alias -Wl,--export-all-symbols -Wl,--enable-auto-import -L../plplot -leplplot
endif

## PCRE stuff (version 4.3)

POSIX_MALLOC_THRESHOLD = @POSIX_MALLOC_THRESHOLD@
PCRELIBVERSION = @PCRE_LIB_VERSION@
PCREPOSIXLIBVERSION = @PCRE_POSIXLIB_VERSION@

INCLUDES = -DAJAX_FIXED_ROOT=$(AJAX_FIXED_ROOT) -DPREFIX=\"$(prefix)\" -I$(top_srcdir)/plplot $(POSIX_MALLOC_THRESHOLD)
#LDFLAGS = -no-undefined
LIBS =

AJAXSRC = ajacd.c ajalign.c ajarr.c ajassert.c \
ajbase.c \
ajcall.c ajcod.c \
ajdan.c ajdmx.c ajdom.c ajdomain.c ajexcept.c \
ajfeat.c ajfile.c ajfmt.c ajgraphxml.c ajindex.c ajjava.c ajlist.c \
ajmath.c ajmatrices.c ajmem.c ajmess.c ajnam.c ajnexus.c \
ajpat.c ajpdb.c ajpdbio.c ajphylo.c \
ajrange.c ajreg.c ajreport.c \
ajseq.c ajseqabi.c ajseqdb.c ajseqread.c ajseqtype.c ajseqwrite.c \
ajsort.c ajstr.c ajsys.c \
ajtable.c ajtime.c ajtranslate.c ajtree.c ajutil.c ajvector.c \
pcre.c pcre_study.c pcreposix.c

AJAXGSRC = ajgraph.c ajhist.c

include_HEADERS = ajax.h ajarch.h ajdefine.h \
ajacd.h ajalign.h ajarr.h ajassert.h \
```
