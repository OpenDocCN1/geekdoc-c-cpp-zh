To clear a feature table of all features call:

```
void ajFeattableClear (AjPFeattable thys);
```

To clear an output feature table of all features call:

```
void ajFeattabOutClear (AjPFeattabOut *thys);
```

# 6.9.8 Reading features

Features may be read directly, using feature table input objects (these are the functions used by ACD processing):

```
AjPFeattable ajFeattableNewRead (AjPFeattabIn ftin);
AjPFeattable ajFeattableNewReadUfo (AjPFeattabIn tabin,
const AjPStr Ufo);
```

ajFeattableNewReadUfo will parse a UFO, open an input file and read a feature table.
ajFeattableNewRead is a generic interface function for reading in features from a feature table input object.

# 6.9.9 Writing features

Features may be written directly, i.e. without using ACD processing (which uses either GFF3 format by default or the format defined by the environment variable
EMBOSS_OUTFEATFORMAT). Features may be written in any format defined in the data structure FeatOOutFormat defined in ajfeat.c:

```
AjBool ajFeatOutFormatDefault (AjPStr* pformat);
AjBool ajFeattableWriteUfo (AjPFeattabOut tabout, const AjPFeattable thys,
const AjPStr Ufo);
AjBool ajFeattableWrite (const AjPFeattable ft, AjPFeattabOut ftout);
```

ajFeatOutFormatDefault sets the default output format which is “gff” unless the
EMBOSS_OUTFEATFORMAT variable is defined or a format is passed in the pformat
parameter.

ajFeattableWriteUfo and ajFeattableWrite are equivalent to
ajFeattableNewRead and ajFeattableNewReadUfo but for writing.
ajFeattableWriteUfo will parse a UFO, open an output file and write a feature table to
it. ajFeattableWrite is a generic interface function for writing features to a file given the
file handle, class of map, data format of output and possibly other associated data.

The following functions write the feature table in the indicated format: