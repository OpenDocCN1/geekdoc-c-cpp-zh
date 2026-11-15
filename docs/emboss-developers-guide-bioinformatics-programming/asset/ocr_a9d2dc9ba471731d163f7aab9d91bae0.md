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

# 6.9.7.4.2 Feature table

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

For cases where a copy of a feature table is required that can be safely changed and or deleted you can use:

```
/* Copy whole feature table */
AjPFeattable ajFeattableNewFtable (const AjPFeattable orig`;

/* Copy limited number of features */
AjPFeattable ajFeattableNewFtableLimit (const AjPFeattable orig, ajint limit`;
```

A feature table may be retrieved from a sequence object using these functions (defined in ajseq.c):

```
AjPFeattable ajSeqGetFeatCopy (const AjPSeq thys);
const AjPFeattable ajSeqGetFeat (const AjPSeq thys);
```

# 6.9.7.4.3 Editing a feature table

To add a new feature (AjPFeature) to a feature table (AjPFeattable) call:

```
void ajFeattableAdd (AjPFeattable thys, AjPFeature feature);
```