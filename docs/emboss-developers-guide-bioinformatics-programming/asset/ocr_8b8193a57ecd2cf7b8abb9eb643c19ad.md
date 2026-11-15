The file does not typically require editing.

/myemboss/emboss_doc/html/Makefile.am.

```
pkgdata_DATA = index.html \
myseq.html

pkgdatadir=$ (prefix) /share/EMBOSS/doc/html/embassy/myseq
```

All the application documentation files (Chapter 8, Application documentation standards) in HTML format must be listed in the pkgdata_DATA entry, which may span multiple lines. Any other documentation files that are automatically generated are listed here also. The line beginning with pkgdatadir= must be changed so that it gives the correct package name.

/myemboss/emboss_doc/text/Makefile.am. The file is shown below:

```
pkgdata_DATA = myseq.txt

pkgdatadir=$ (prefix) /share/EMBOSS/doc/programs/text
```

This is essentially the same as /myemboss/emboss_doc/html/Makefile.am but references the documentation in plain text format.

# 3.2.4.3 Editing the configure.in files

Two lines only need to be edited here:

+   - The AC_INIT line must be changed so that it references one (any) application C source code file in the package.

+   - The AM_INIT_AUTOMAKE line should give the package name and version number.

Once the application ACD files and C source code are written and integrated, compilation is as for any other EMBASSY package (see Section 3.2.1, ‘Using myemboss for application development’).

# 3.2.5 Adding new functions and datatypes

Any new functions and datatypes added to AJAX or NUCLEUS should be properly documented (Section D.1, ‘Code documentation standards’) if they are to be incorporated into the EMBOSS distribution. To compile the new code, type:

```
make
```

from the AJAX or NUCLEUS directory as appropriate. Of course, you will need to recompile any statically linked applications to use the changes. Alternatively, recompile the whole package by typing make from the second-level EMBOSS directory, e.g.:

```
/home/auser/emboss/emboss/
```