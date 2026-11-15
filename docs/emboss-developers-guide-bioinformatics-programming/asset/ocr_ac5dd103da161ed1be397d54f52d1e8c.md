# 6.6.6.1.1 regexp

```
AjPPatlistRegexp patterns=NULL;
patterns = ajAcdGetRegexp("patterns");
```

# 6.6.6.1.2 pattern

```
AjPPatlistSeq seqpatterns=NULL;
seqpatterns = ajAcdGetPattern("seqpatterns");
```

# 6.6.6.2 Alternative ACD retrieval functions

In cases where just a single regular expression is required ajAcdGetRegexpSingle is used to return a single AjPRegexp object:

```
AjPRegexp ajAcdGetRegexpSingle (const char *token);
```

It is used as follows:

```
AjPRegexp regexp=NULL;
regexp = ajAcdGetRegexpSingle("patterns");
```

The memory for any other patterns or regular expressions is automatically cleared by a final call to embExit.

# 6.6.6.3 Processing command line options and ACD attributes

Currently there are no functions for this.

# 6.6.6.4 Memory management

It is your responsibility to close any files and free up memory at the end of the program. You must call the default destructor function (see below) on any objects returned by calls to ajAcdGetRegexp or ajAcdGetPattern.

# 6.6.7 Pattern object memory management

# 6.6.7.1 Default object construction

To use a pattern object that is not defined in the ACD file you must first instantiate the appropriate object pointer. The default constructor functions are:

```
/* Create a new regular expression. */
AjPPatlistRegexp ajPatlistRegexpNew (void);

/* Create a new sequence pattern */
AjPPatlistSeq ajPatlistSeqNew (void);
```