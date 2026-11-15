# After editing

```
bin_PROGRAMS = aaindexextract abiview acdc antigenic \
...
garnier geecee getorf helixturnhelix helloworld hmoment \
...
```

# Important

When editing Makefile.am, the line continuation characters ('\\') must be explicitly added to break the entries over more than one line.

Secondly, you must add your application source file to the SOURCES section. The line to add has the following general syntax:

```
ApplicationName_SOURCES = ApplicationName.c
```

where ApplicationName is the name of the application. This line should be added in alphabetic order. So, the appearance of the file would be as follows.

# Before editing

```
...
geecee_SOURCES = geecee.c
getorf_SOURCES = getorf.c
helixturnhelix_SOURCES = helixturnhelix.c
hmoment_SOURCES = hmoment.c
iep_SOURCES = iep.c
infoalign_SOURCES = infoalign.c
...
```

# After editing

```
...
geecee_SOURCES = geecee.c
getorf_SOURCES = getorf.c
helixturnhelix_SOURCES = helixturnhelix.c
helloworld_SOURCES = helloworld.c
hmoment_SOURCES = hmoment.c
iep_SOURCES = iep.c
infoalign_SOURCES = infoalign.c
```

The Makefile.am in the ACD directory contains information about each ACD file. All that needs to be done for this file is to add the name of the new ACD file. Again, it is usual to do this alphabetically. Here's what the file for the main EMBOSS package looks like: