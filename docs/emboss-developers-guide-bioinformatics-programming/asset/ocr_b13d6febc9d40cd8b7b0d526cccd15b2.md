```
CVS password:
% cvs -d :pserver:cvs@cvs.open-bio.org:/home/repository/emboss checkout emboss
cvs checkout: Updating emboss
cvs checkout: Updating emboss/emboss
U emboss/emboss/AUTHORS
U emboss/emboss/COMPAT
U emboss/emboss/COPYING
U emboss/emboss/ChangeLog
.
... screen output truncated
.
%
% cvs -d :pserver:cvs@cvs.open-bio.org:/home/repository/emboss logout
Logging out of :pserver:cvs@cvs.open-bio.org:2401/home/repository/emboss
%
% ls
emboss
```

# 1.2.2 Keeping up to date with CVS

Once you’ve downloaded the CVS version of EMBOSS, you should keep up to date with the latest changes. To do this, move to the directory which you wish to update (or the root emboss directory to update everything) and type:

```
cvs -d :pserver:cvs@cvs.open-bio.org:/home/repository/emboss update
```

Bear in mind that if you have edited any files then those edits will be merged with the version downloaded via CVS. If you wish to conserve your edits in their original form, you should copy the edited files to a safe place first.

# 1.2.3 Configuration

You must first build the script and other files used to configure the package. From the second-level EMBOSS directory (e.g. /home/auser/emboss/emboss) type:

```
aclocal -I m4
autoconf
automake -a
```

aclocal is part of the automake package. These commands build the “configure” script (./configure) from the file configure.in (in the EMBOSS distribution) and various other files needed for installation. Specifically:

+   * aclocal creates aclocal.m4 containing m4 macros used by the auto* tools.
+   * autoconf reads configure.in and creates the “configure” script.
+   * automake reads Makefile.am and creates Makefile.in