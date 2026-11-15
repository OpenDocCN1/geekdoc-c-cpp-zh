
All library code must be adequately documented using structured comments, which are parsed to generate the online library documentation (Section 1.3, ‘Developer documentation’). Comments at the head of application code mostly contain licence and bibliographic information. However, all public functions and datatypes must also be documented. Functions are organised in the library files under functional sections, which define, amongst other things, naming rules for functions and their parameters. The comments at the head of the library file usually contain extensive documentation. If you develop a new library file then you will need to provide documentation to the same level.

See the instructions on code documentation (Appendix D, Code documentation standards) and application end-user documentation (Chapter 8, Application documentation standards) for more information.

### 3.1.13 Distribution

Any contributed code will be widely distributed and installed on many different platforms. EMBOSS is known to work on almost every UNIX system, Microsoft Windows and MacOSX. There is nothing to do here because this is managed by the EMBOSS developers, although it helps greatly if you integrate, test and properly document any new software as summarised above.

### 3.1.14 Maintenance, support and training

Any contributed code will need maintenance and support. This, to an extent, is covered by the EMBOSS developers who also run EMBOSS training courses. However, it helps greatly if you maintain your own source code and support it through the EMBOSS mailing lists (Section 1.4, ‘Project mailing lists’).

## 3.2 Integration and compilation

### 3.2.1 Using myemboss for application development

The myemboss package is an almost empty EMBASSY package where developers can safely build their own EMBOSS applications. It provides a way to isolate local application development from the rest of EMBOSS so preserving the integrity of the package. New applications, regardless of whether they are destined for another EMBASSY package or EMBOSS itself, will typically start their life in myemboss.

myemboss requires the GNU tools autoconf, automake and libtool to be installed (see Section 1.2, ‘Installation of CVS (Developer’s) Release’). Using the GNU tools you can add new applications very easily. myemboss provides a directory structure and Makefile stubs for integrating new applications. Application ACD files go in the myemboss/emboss_acd directory and source code into the myemboss/src directory.

Applications are built using a Makefile file, but you do not need to edit this file directly. Instead you edit a file Makefile.am which automake converts into a file Makefile.in and configure converts into the Makefile file.

The Makefile.am file is shown below and has been edited to include two applications:

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

To compile applications in myemboss, you must configure the package if you have not already done so (see Section 1.2, ‘Installation of CVS (Developer’s) Release’), then type the following from the myemboss applications directory (myemboss/src):

```
make
```

make will regenerate the Makefile file and build your new application, linking it to the EMBOSS libraries (AJAX and NUCLEUS).

This assumes you have installed and configured EMBOSS and the myemboss package. If you did a full EMBOSS install using make install then you must also type:

```
make install
```

to complete the installation of applications developed under myemboss.

For more information on installation see Section 1.2, ‘Installation of CVS (Developer’s) Release’ and the EMBOSS Administrator’s Guide.

### 3.2.2 Adding new EMBOSS applications

An application that has been developed and tested in myemboss can be added to the main package. Adding new applications to EMBOSS is essentially the same as for myemboss. EMBOSS has its own Makefile.am which, in contrast to myemboss, organises applications into two strands:

- Standard EMBOSS applications (the “make” applications) are listed after the bin_PROGRAMS line
- Applications that are not yet fully integrated (“make check” applications) are listed after the check_PROGRAMS line.

Applications which are not entirely complete should be put into the “make check” area of the emboss/Makefile.am file. For example, applications that compile and work correctly, but for which full documentation and quality assurance tests are not yet available, should go here. Only applications that are fully working, tested and documented should go into the “make” area.

An excerpt from the Makefile.am file is below and includes a few “make check” applications and standard “make” applications:

```
SUBDIRS = acd data

EXTRA_DIST = emboss.default.template

if ISSHARED
if ISAXIA64
AM_CFLAGS = -Wl,-bdynamic -Wl,-brtl -L../ajax/.libs -lajax
else
AM_CFLAGS =
endif
endif

check_PROGRAMS = acdlog acdxsd ajtest \
complex corbatest \
entrails entrailsbook entrailshtml entrailswiki giep histogramtest intconv \
origsplitter origunion \
newcoils \
... <lines omitted for brevity>

bin_PROGRAMS = aaindexextract abiview \
acdc acdpretty acdtable acdtrace acdvalid \
aligncopy aligncopypair antigenic \
backtranambig backtranseq banana biosed btwisted \
... <lines omitted for brevity>

water whichdb wobble \
wordcount wordfinder wordmatch wossname \
yank

INCLUDES = -I$(top_srcdir)/nucleus -I$(top_srcdir)/ajax -I$(top_srcdir)/plplot

aaindexextract_SOURCES = aaindexextract.c
abiview_SOURCES = abiview.c
acdc_SOURCES = acdc.c
acdpretty_SOURCES = acdpretty.c
acdtable_SOURCES = acdtable.c

... <lines omitted for brevity>

seqretsingle_SOURCES = seqretsingle.c
seqrettype_SOURCES = seqrettype.c
testplot_SOURCES = testplot.c
treetypedisplay_SOURCES = treetypedisplay.c

# Uncomment to use dual libraries
if ISCYGWIN
LDADD = ../nucleus/libnucleus.la ../ajax/libajax.la ../ajax/libajaxg.la ../plplot/libeplplot.la $(XLIB)
else
LDADD = ../nucleus/libnucleus.la ../ajax/libajaxg.la ../ajax/libajax.la ../plplot/libeplplot.la $(XLIB)
endif

pkgdata_DATA = emboss.default.template
pkgdatadir=$(prefix)/share/$(PACKAGE)

#ifdef PURIFY
# LINK = purify $(LIBTOOL) -mode=link $(CC) $(CFLAGS) $(LDFLAGS) -o $@
#else
#
#endif
```

Compilation is the same as for **myemboss**. You must configure the EMBOSS package if you have not already done so (see Section 1.2, 'Installation of CVS (Developer's) Release'), then from the applications directory (e.g. /home/auser/emboss/emboss/emboss/) type:

```
make
```

This will regenerate the `Makefile` file, build your new application and link it to the libraries. If you installed EMBOSS using `make install` then you must also type:

```
make install
```

to complete the installation of the new application.
For more information on installation see Section 1.2, 'Installation of CVS (Developer's) Release' and the _EMBOSS Administrator's Guide_.

### 3.2.3 Adding new EMBASSY applications

Applications are added to EMBASSY packages in exactly the same way as for **myemboss** (see above).

### 3.2.4 Adding a new EMBASSY package

To add an entirely new EMBASSY package you must:

- 1. Create the directory structure and required files for the package under the main EMBASSY directory (../emboss/emboss/embassy/).
- 2. Write the application ACD and C source code files and populate the appropriate directories.
- 3. Edit the `Makefile.am` files.
- 4. Edit the `configure.in` file.
- 5. Create the application documentation and populate the appropriate directories.

### 3.2.4.1 Directory structure

The directory structure and file names are mostly the same regardless of the package. For example, the **hmmernnew** EMBASSY package looks like this:

```
% cd emboss/emboss/embassy/hmmernnew/
% ls
AUTHORS COPYING emboss_acd ltmain.sh NEWS Userguide.pdf
ChangeLog CVS emboss_doc m4 README
configure.in DOCS INSTALL Makefile.am src
```
