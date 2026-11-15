```
/* Create a new prosite pattern object */
AjPPatComp ajPatCompNew (void);
```

All constructors return the address of a new object. The pointers do not need to be initialised to NULL but it is good practice to do so:

```
AjPPatlistRegex  expression = NULL;
AjPPatlistSeq    pattern = NULL;

expression = ajPatlistRegexNew();
pattern    = ajPatlistSeqNew();
/* The objects are instantiated and ready for use */
```

# 6.6.7.2 Default object destruction

You must free the memory for an object before the pointer is reused and also once you are finished with it. The default destructor functions are:

```
/* Delete a regular expression.  */
void ajPatlistRegexDel (AjPPatlistRegex* pthys);
/* Delete a pattern list object */
void ajPatlistSeqDel (AjPPatlistSeq* pthys);
```

```
/* Delete a pattern object */
void ajPatternSeqDel (AjPPatternSeq* pthys);
/* Delete a prosite pattern object */
void ajPatCompDel (AjPPatComp* pthys);
```

They are used as follows:

```
AjPPatlistSeq plist = NULL;
AjPPatlistRegex rlist = NULL;
AjPRegexp patexp = NULL;
AjPSeqall seqall = NULL;
AjPSeq seq = NULL;

plist = ajAcdGetPattern("pattern");
rlist = ajAcdGetRegexp("regexp");
seqall = ajAcdGetSeqall("sequence");
while(ajSeqallNext(seqall, &seq))
/* Do something */

ajPatlistSeqDel(&plist);
ajPatlistRegexDel(&rlist);
```