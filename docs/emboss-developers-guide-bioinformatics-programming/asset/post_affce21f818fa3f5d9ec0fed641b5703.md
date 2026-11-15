
## 1.2.1 Downloading via CVS

To download via CVS you must have cvs installed on your system. It is there if an application is listed after typing:

```
which cvs
```

You must also use the secure shell SSH for the file transfer. Depending on your shell, type one of the following:

```
setenv CVS_RSH ssh
declare -x CVS_RSH=ssh
export CVS_RSH=ssh
```

To checkout the EMBOSS source code tree, go to the directory where you want the top-level EMBOSS directory created. For example to create EMBOSS in /home/auser/src/ you'd type:

```
cd /home/auser/src
```

To checkout EMBOSS you must first log on to the open-bio.org CVS server by typing:

```
cvs -d :pserver:cvs@cvs.open-bio.org:/home/repository/emboss login
```

You will be prompted for a password which is cvs. You are now logged on to the CVS server. Checkout (download) EMBOSS by typing:

```
cvs -d :pserver:cvs@cvs.open-bio.org:/home/repository/emboss checkout
emboss
```

This will take some time as it's downloading several megabytes of source code and data from the USA. Once the download is complete, terminate your CVS session with:

```
cvs -d :pserver:cvs@cvs.open-bio.org:/home/repository/emboss logout
```

Here is a typical CVS session:

```
% declare -x CVS_RSH=ssh
% cvs -d :pserver:cvs@cvs.open-bio.org:/home/repository/emboss login
Logging in to :pserver:cvs@cvs.open-bio.org:2401/home/repository/emboss
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

## 1.2.2 Keeping up to date with CVS

Once you’ve downloaded the CVS version of EMBOSS, you should keep up to date with the latest changes. To do this, move to the directory which you wish to update (or the root emboss directory to update everything) and type:

```
cvs -d :pserver:cvs@cvs.open-bio.org:/home/repository/emboss update
```

Bear in mind that if you have edited any files then those edits will be merged with the version downloaded via CVS. If you wish to conserve your edits in their original form, you should copy the edited files to a safe place first.

## 1.2.3 Configuration

You must first build the script and other files used to configure the package. From the second-level EMBOSS directory (e.g. /home/auser/emboss/emboss) type:

```
aclocal -I m4
autoconf
automake -a
```

aclocal is part of the automake package. These commands build the “configure” script (./configure) from the file configure.in (in the EMBOSS distribution) and various other files needed for installation. Specifically:

- aclocal creates aclocal.m4 containing m4 macros used by the auto* tools.
- autoconf reads configure.in and creates the “configure” script.
- automake reads Makefile.am and creates Makefile.in

**Tip**

If you experience any errors at that stage it is possible that your GNU configuration tools are out of date, if so then update them. It is also possible that your version of libtool is more recent than that used in the current EMBOSS CVS; you can check that by looking at the version number in the ltmain.sh file at the top source level of the checked-out tree. If your installed version of libtool is newer then you may have to type autoreconf -fi and then retype the previous GNU configuration tool commands. autoreconf is part of the autoconf package.

Running the resulting ./configure will

- Check whether your system has the necessary functionality and libraries to compile EMBOSS.
- Read Makefile.in and generate platform-specific Makefiles (used later).
- Configure your system. For example, the installation path and various system variables are set and files are flagged to compile (or not).

**Note**

./configure is controlled by command line arguments and by environment variables. Command line arguments are generally used to switch on features autoconf was unable to detect. Environment variables are generally used to set build information such as compiler options.

If you intend to compile using make install (see below) you must specify an installation area for the executables and supporting files. It is good practice to specify these even if you intend to compile with a plain make. To do this, type:

```
./configure --prefix=/home/auser/emboss
```

Further, if you are using the gcc compiler it's a good idea to turn warnings on. You can do this while setting the installation areas:

```
./configure --prefix=/home/auser/emboss --enable-warnings
```

You can also turn on more strict developer warnings by typing:

```
./configure --prefix=/home/auser/emboss --enable-warnings --enable-devwarnings
```

### Important

Note that the warnings switches, such as `--enable-warnings`, are for `gcc` compilers only. There is a further configuration switch, `--enable-devextrawarnings`, which turns on some rather pedantic warnings which are nonetheless useful in some rare circumstances. As that switch can produce compilation noise it is not recommended to specify it in general use.

### Caution

To support the Portable Network Graphics (PNG) format, EMBOSS requires the `libgd`, `libpng` and `libz` libraries. On many Linux systems, most support libraries are installed under the directories `/usr/` and `/lib`. For example, `/lib`, `/usr/lib`, `/usr/X11R6/lib`, etc. Whereas Linux distributions include RPMs for these libraries, other operating systems do not.

If you are installing these libraries and include files in somewhere other than `/usr` then you must specify their location when configuring. Assuming you have installed them under `/usr/local` (e.g. `/usr/local/lib` and `/usr/local/include`) you would add the following switch to the configuration command line:

```
--with-pngdriver=/usr/local
```

For more information on the configurability of the build type:

```
./configure --help
```

## 1.2.4 Compilation

To compile EMBOSS, type:

```
make
```

This will, by using the Makefiles, compile all the source files into executable binaries within your chosen checked-out location e.g.:

```
/home/auser/emboss/emboss/emboss
```

Alternatively, compiling with:

```
make install
```

will install the binaries and supporting files into bin, lib and share subdirectories of the directory you specified using --prefix on the configure line. In the example above, this is the top-level EMBOSS directory level from the CVS checkout, e.g.:

```
/home/auser/emboss
```

Had you not specified --prefix=/home/auser/emboss they'd be installed to /usr/local by default (that isn't recommended).

> **Tip**
> If you want EMBOSS installed in somewhere other than /usr/local then use the --prefix option of GNU configure to specify the EMBOSS installation directory. This is the recommended method of installation as EMBOSS has hundreds of files which might otherwise obscure other software, particularly under /usr/local/bin.

To compile and reinstall EMBOSS on subsequent occasions, use the following commands:

```
make clean
./configure
make
make install
```

Though extremely rare, there are circumstances where you may have to type rm config.cache (on very old installations) or rm -rf autom4te.cache before doing the above. Those occasions generally happen when trying to update a rather old existing version of EMBOSS.

### 1.2.4.1 Static and dynamic compilation

> **Note**
> A static library (statically linked library) is a library called by an application in which links to external functions and variables are resolved at compile-time by a linker. Static libraries are either compiled into object files and merged with the application during building/linking into a single executable, or are loaded at run-time and are accessible to the executable.
> 
> A dynamic library (dynamically linked library) in contrast implements dynamic linking, where libraries remain in separate files on disk and are not copied into the executable or library at compile-time. Instead a loader is used to access the library at load or run-time.
> 
> Executables created using static libraries are larger than executables linked to dynamic libraries, because static libraries include the code for the library function(s) within the executable. Static libraries, however, can be useful for debugging purposes and sometimes result in faster executables than when using dynamic libraries.
