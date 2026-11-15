# Sequence set

A sequence set can be created using ajSeqsetGetFromUsa in the same way as ajSeqGetFromUsa:

```
AjPSeq seqset = NULL;
AjPStr usa = NULL;
seqset = ajSeqsetNew(); /* Create sequence object */

usa = ajStrNewC("swiss:hba_*"); /* "swiss:hba_*" is a valid USA */

if(!ajSeqsetGetFromUsa(usa, 1, &seqset))
/* Do something to handle the failure */;
else
/* Sequence set was loaded successfully .. do something with it */;

ajSeqsetDel(&seqset);
```

# Sequence stream

A sequence input stream is created from a USA using ajSeqallFile, which in contrast to the previous two functions returns a pointer to the new object.

```
AjPSeq eqall = NULL;
AjPStr usa = NULL;

usa = ajStrNewC("swiss:hba_*"); /* "swiss:hba_*" is a valid USA *.

if(!(seqall=ajSeqallFile(usa)))
/* Do something to handle the failure */;
else
/* Sequence input stream was opened successfully .. do something with it * ;

ajSeqallDel(&seqall);
```

# Sequence output

ajSeqoutClearUsa creates (if necessary) or resets a sequence output object using a new USA:

```
AjPSeqout seqout = NULL;
AjPStr usa = NULL;

usa = ajStrNewC("asis:ALVLLYNITEF"); /* "asis:ALVLLYNITEF" is a valid USA *,

seqout = ajSeqoutNew();
ajSeqoutClearUsa (&seqout, usa);

ajSeqoutDel(&seqout);
```

The code would work equally well if the call to the constructor function was omitted.