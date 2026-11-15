
| AJAX datatype | AjPFeattable | AjPFeattabOut |
| --- | --- | --- |
| To retrieve from ACD | ajAcdGetFeatures | ajAcdGetFeatout |

Your application code will call embInit to process the ACD file and command line (see Section 6.3, ‘Handling ACD files’). All values from the ACD file are read into memory and files are opened as necessary. You have a handle on the files and memory through the ajAcdGet* family of functions which return pointers to appropriate objects.

### 6.9.6.1 Input feature retrieval

To retrieve input features an object pointer is declared and then initialised using ajAcdGetFeatures:

```
AjPFeattable features=NULL;
features = ajAcdGetFeatures("features");
```

### 6.9.6.2 Output feature retrieval

To retrieve an output feature stream an object pointer is declared and initialised using ajAcdGetFeatout:

```
AjPFeattabOut outfeat=NULL;
outfeat = ajAcdGetFeatout("outfeat");
```

### 6.9.6.3 Processing command line options and ACD attributes

### 6.9.6.3.1 Setting the features range

The features input datatype has various inbuilt command line qualifiers including -fbegin and -fend which specify a start and end position for the features, and -freverse to reverse the orientation of nucleotide features.

When a feature table is read the feature values are held in the appropriate feature table object. Regardless of the range values you still get the entire table loaded into memory. The functions ajFeattableTrim or ajFeattableTrimOff are used to trim the features to the region defined by -fbegin and -fend:

```
AjFeattable ftable=NULL;
ftable = ajAcdGetFeatures("features");
ajFeattableTrim(ftable);
/* ajFeattableTrimOff(ftable,0,ajFeattableGetLen(ftable));*/
```

## 6.9 HANDLING FEATURES

When a sequence is read the feature values are held in a feature table in the appropriate sequence object. Regardless of the sequence range values you still get the entire sequence loaded into memory. The function ajSeqTrim (or ajSeqsetTrim for a AjPSeqset object) is used to trim the sequence and features to the region defined by -sbegin and -send:

```
AjPSeq seq=NULL;

seq = ajAcdGetSeq("sequence");

ajSeqTrim(seq);
```

### 6.9.6.4 Memory management

It is your responsibility to free up memory at the end of the program. You must call the default destructor function (see below) on any objects returned by calls to ajAcdGet*.

Additionally you must call embExit to clean up internal memory including that allocated for the housekeeping of feature tables:

```
embExit();
```

### 6.9.7 Memory management

### 6.9.7.1 Default object construction

To use a feature table object that is not defined in the ACD file you must first instantiate the appropriate object pointer. The default construction function is ajFeattableNew.
ajFeattableNew leaves the type of feature table uninitialised. It is set when a feature is added to the table. Type-specific functions ajFeattableNewDna and ajFeattableNewProt create feature tables for nucleotide and protein features respectively. Function ajFeattableNewSeq creates a feature table with the type and length matching a sequence object.

Feature table output objects are typically loaded from ACD file processing (see above). In the unlikely event you need to create one manually you can use the default constructor ajFeattabOutNew or functions ajFeattabOutNewCSF or ajFeattabOutNewSSF which use an existing output file and a specified type and sequence name.

To create a feature object (usually to be stored within a feature table), a similar set of functions is available. ajFeatNew creates a feature with all attributes including the type. ajFeatNewProt creates a feature with all attributes required by protein features (no strand or frame).
ajFeatNewII and ajFeatNewIIRev are generic constructors requiring only the start and end values. The feature type will default to a 'miscellaneous feature' or 'polypeptide region' value.
ajFeatNewFeat is a copy constructor making a feature object from an existing feature.

```
/* Constructor for feature which is added to table */
AjPFeature ajFeatNew (AjPFeattable thys,
                     const AjPStr source,
                     const AjPStr type,
                     ajint Start,
                     ajint End,
float score,
char strand,
ajint frame);
/* Constructor for protein feature */
AjPFeature ajFeatNewProt(AjPFeattable thys,
const AjPStr source,
const AjPStr type,
ajint Start, ajint End,
float score);
/* Simple constructor with only start and end positions */
AjPFeature ajFeatNewII (AjPFeattable thys,
ajint Start, ajint End);
/* Simple constructor, sets features to be on reverse strand */
AjPFeature ajFeatNewIIRev (AjPFeattable thys,
ajint Start, ajint End);
/* Copies a feature */
AjPFeature ajFeatNewFeat (const AjPFeature orig);
/* Feature Table Object Constructors */
AjPFeattable ajFeattableNew (const AjPStr name);
AjPFeattable ajFeattableNewDna (const AjPStr name);
AjPFeattable ajFeattableNewProt (const AjPStr name);
AjPFeattable ajFeattableNewSeq (const AjPSeq seq);
/* Output Feature Table Object constructors */
AjPFeattabOut ajFeattabOutNew (void);
AjPFeattabOut ajFeattabOutNewCSF (const char* fmt, const AjPStr name,
const char* type, AjPFile file);
AjPFeattabOut ajFeattabOutNewSSF (const AjPStr fmt, const AjPStr name,
const char* type, AjPFile file);
```

The parameters to ajFeatNew are as follows:

- thys Pointer to the feature table to which the new feature is added
- source Analysis basis for feature
- type Type of feature (e.g. exon)
- Start Start position of the feature
- End End position of the feature
- score Analysis score for the feature
- strand Strand of the feature
- frame Frame of the feature

All constructors return the address of a new object.

### 6.9.7.2 Default object destruction

You must free the memory for an object once you are finished with it. The functions are:

```
void ajFeatDel (AjPFeature *pthis);
void ajFeattableDel (AjPFeattable *pthis);
void ajFeattabOutDel (AjPFeattabOut* pthis);
```

### Example

In the example below, a feature table and individual features are built manually using the default constructor functions. The features are written out to a feature table retrieved from ACD processing:

```
AjPFeattable feattable;
AjPStr name = NULL;
AjPStr source = NULL;
AjPStr type = NULL;
char strand = '+';
ajint frame = 0;
AjPFeature feature = NULL;
AjPFeattabOut output = NULL;
ajint i;
float score = 0.0;
embInit("demofeatures", argc, argv);

output = ajAcdGetFeatout("outfeat");

ajStrAssignC(&name,"seq1");

feattable = ajFeattableNew(name);

ajStrAssignC(&source,"demofeature");
score = 1.0;

for(i=1;i<11;i++)
{
    if(i & 1)
        ajStrAssignC(&type,"CDS");
    else
        ajStrAssignC(&type,"misc_feature");
    feature = ajFeatNew(feattable, source, type, i, i+10, score, strand,
                        frame);
}

ajFeattableWrite(output, feattable);

ajStrDel(&source);
ajStrDel(&name);
ajStrDel(&type);
ajFeattableDel(&feattable);
ajFeattabOutDel(&output);
```

### 6.9.7.4 Alternative object construction and loading

### 6.9.7.4.1 Single feature

There are a variety of alternative ways to create a feature object. The start and end position of the features may be specified:

```
AjPFeature ajFeatNewII (AjPFeattable thys, ajint Start, ajint End);
AjPFeature ajFeatNewIIRev (AjPFeattable thys, ajint Start, ajint End);
```

```
AjPFeature ajFeatNewProt (AjPFeattable thys,
 const AjPStr source, const AjPStr type,
 ajint Start, ajint End, float score);
```

ajFeatNewIIRev sets features to be on the reverse strand whereas ajFeatNewProt is for protein features.

For cases where a copy of a feature is required that can be safely changed and/or deleted you can use ajFeatNewFeat:

```
AjPFeature ajFeatNewFeat (const AjPFeature orig);
```

### 6.9.7.4.2 Feature table

There are a variety of alternative ways to create a feature table object, either by name or from an existing sequence object:

```
/* DNA feature table
 */
AjPFeattable ajFeattableNewDna (const AjPStr name);

/* Protein feature table */
AjPFeattable ajFeattableNewProt (const AjPStr name);

/* From existing sequence; type is determined by the sequence type. */
AjPFeattable ajFeattableNewSeq (const AjPSeq seq);
```

For cases where a copy of a feature table is required that can be safely changed and/or deleted you can use:

```
/* Copy whole feature table */
AjPFeattable ajFeattableNewFtable (const AjPFeattable orig);

/* Copy limited number of features */
AjPFeattable ajFeattableNewFtableLimit (const AjPFeattable orig, ajint limit);
```

A feature table may be retrieved from a sequence object using these functions (defined in ajseq.c):

```
AjPFeattable ajSeqGetFeatCopy (const AjPSeq thys);
const AjPFeattable ajSeqGetFeat (const AjPSeq thys);
```

### 6.9.7.4.3 Editing a feature table

To add a new feature (AjPFeature) to a feature table (AjPFeattable) call:

```
void ajFeattableAdd (AjPFeattable thys, AjPFeature feature);
```
