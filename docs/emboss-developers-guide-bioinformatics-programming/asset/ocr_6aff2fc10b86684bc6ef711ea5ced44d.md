> **Caution**
> 
> Note that `ajFeatGetType` returns a copy of the pointer to the type (key) of the specified feature object. The key is still owned by the feature and should not to be destroyed.

# ## 6.9.12 Retrieving elements of a feature table object

The elements of a feature table object may be retrieved be using the following:

```
/* Returns the feature table start position, or 1 if no start has been set.*/
ajint ajFeattableGetBegin (const AjPFeattable thys);

/* Returns the features table end position, or the
feature table length if no end has been set.*/
ajint ajFeattableGetEnd (const AjPFeattable thys);

/* Returns the name of a feature table object. */
const AjPStr ajFeattableGetName (const AjPFeattable thys);
const char* ajFeattableGetTypeC (const AjPFeattable thys);
const AjPStr ajFeattableGetTypeS (const AjPFeattable thys);

/* Returns the sequence length of a feature table */
ajint ajFeattableGetLen (const AjPFeattable thys);

/* Returns the number of features */
ajint ajFeattableGetSize (const AjPFeattable thys);
```

> **Caution**
> 
> `ajFeattableGetName`, `ajFeattableGetTypeC` and `ajFeattableGetTypeS` return a copy of the pointer to the name or type (key). This is still owned by the feature table and so should not to be destroyed.

# ## 6.9.13 Setting elements of a feature object

The elements (indicated in comments) of a feature object may be set using the following:

```
/* Description */
void ajFeatSetDesc (AjPFeature thys, const AjPStr desc);

/* Append to description */
void ajFeatSetDescApp (AjPFeature thys, const AjPStr desc);

/* Score */
void ajFeatSetScore (AjPFeature thys, float score);

/* Strand */
void ajFeatSetStrand (AjPFeature thys, AjBool rev);
```