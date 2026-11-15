# 6.6.9 Getting elements of objects

Applications work at the level of lists of patterns and regular expressions. For these,
functions are available to return the number of items in the list, and to return the next
item.

```
/* Gets next available pattern from list. */
AjBool ajPatlistSeqGetNext (AjPPatlistSeq thys,
                            AjPPatternSeq* pattern);

/* Gets number of patterns from list. */
ajuint ajPatlistSeqGetSize (const AjPPatlistSeq plist);

/* Gets number of patterns from list. */
ajuint ajPatlistRegexGetSize (const AjPPatlistRegex plist);

/* Gets next available pattern from list. */
AjBool ajPatlistRegexGetNext (AjPPatlistRegex thys,
                              AjPPatternRegex* pattern);
```

There are further functions to return elements of each item retrieved from a list:

```
/* Returns the name of the pattern. */
const AjPStr ajPatternSeqGetName (const AjPPatternSeq thys);

/* Returns pattern in string format. */
const AjPStr ajPatternSeqGetPattern (const AjPPatternSeq thys);

/* Returns void pointer to compiled pattern. */
AjPPatComp ajPatternSeqGetCompiled (const AjPPatternSeq thys);

/* Returns true if the pattern is for a protein sequence. */
AjBool ajPatternSeqGetProtein (const AjPPatternSeq thys);

/* Returns the mismatch of the pattern. */
ajuint ajPatternSeqGetMismatch (const AjPPatternSeq thys);

/* Returns the name of the pattern */
const AjPStr ajPatternRegexGetName (const AjPPatternRegex thys);

/* Returns pattern in string format. */
const AjPStr ajPatternRegexGetPattern (const AjPPatternRegex thys);

/* Returns void pointer to compiled pattern. */
AjPRegexp ajPatternRegexGetCompiled (const AjPPatternRegex thys);

/* Returns the type of the pattern. */
ajuint ajPatternRegexGetType (const AjPPatternRegex thys);
```

# 6.6.10 Setting elements of objects

There are no elements that should be set within the pattern list objects.