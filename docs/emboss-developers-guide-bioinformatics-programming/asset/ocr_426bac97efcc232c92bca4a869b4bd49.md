# Before editing

```
pkgdata_DATA = codes.english \
    aaindexextract.acd abiview.acd ajbad.acd ajfeatest.acd ajtest.acd \
...
    garnier.acd geecee.acd getorf.acd helixturnhelix.acd hmoment.acd \
    histogrammtest.acd iep.acd infoalign.acd infoseq.acd isochore.acd \
    lindna.acd listor.acd \
    marscan.acd maskfeat.acd maskseq.acd \
    matcher.acd
```

# After editing

```
pkgdata_DATA = codes.english \
    aaindexextract.acd abiview.acd ajbad.acd ajfeatest.acd ajtest.acd \
...
    garnier.acd geecee.acd getorf.acd helixturnhelix.acd helloworld.acd \
    hmoment.acd histogrammtest.acd iep.acd infoalign.acd infoseq.acd \
    isochore.acd lindna.acd listor.acd \
    marscan.acd maskfeat.acd maskseq.acd \
    matcher.acd
```

Again, line continuation characters ('\\') must be added explicitly.

# 2.2.6 Compilation

You compile the application by typing one of the following from the executables directory
(.../myemboss/source):

```
make helloworld
make
```

The latter option may be slower as it will sometimes (when library changes are made) have to
compile everything.

The GNU tools will recognise whether the Makefile.am files have been edited and
reconstruct the Makefile files when a make command is given. It is bad practice to edit the
Makefile files themselves.

Here's the example for helloworld compiled in the main EMBOSS package:

```
% pwd
/home/auser/emboss/emboss/emboss/
% make helloworld
/bin/sh ../libtool --tag=CC --mode=link gcc -O2 -Wall -fno-strict-aliasing -o
helloworld helloworld.o
../nucleus/libnucleus.la ../ajax/libajaxg.la ../ajax/libajax.la ../plplot/
libplplot.la -
L/usr/X11R6/lib
-lX11 -lm -lgd -lpng -lz -lm
gcc -O2 -Wall -fno-strict-aliasing -o .libs/helloworld helloworld.o
../nucleus/.libs/libnucleus.so
../ajax/.libs/libajaxg.so ../ajax/.libs/libajax.so ../plplot/.libs/libplplot.so-
L/usr/X11R6/lib -lX11
```