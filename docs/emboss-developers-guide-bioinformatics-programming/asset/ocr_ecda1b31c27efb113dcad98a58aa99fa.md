# outproperties

```
AjPOutfile outfile=NULL;
outfile = ajAcdGetOutproperties("outpropertiesfile");
```

# outtree

```
AjPOutfile outfile=NULL;
outfile = ajAcdGetOuttree("outtreefile");
```

# 6.12.6.1.3 Alternative ACD retrieval functions

There are functions to retrieve a single (the first) state or tree object from file:

```
AjPPhyloState ajAcdGetDiscretestatesSingle (const char *token);
AjPPhyloTree ajAcdGetTreeSingle (const char *token);
```

Where these are used, it is still necessary to call the appropriate destructor function (see below) to ensure that the array of state or tree objects allocated during ACD file processing is freed.

# 6.12.6.2 Processing command line options and ACD attributes

Currently there are no functions for this.

# 6.12.6.3 Memory and file management

It is your responsibility to close any files and free up memory at the end of the program.

# 6.12.6.3.1 Closing output phylogenetic data files

To close an output phylogenetic data stream call ajOutfileClose with the address of the output file:

```
ajOutfileClose(&outfile);
```

# 6.12.6.3.2 Freeing memory

You must call the appropriate destructor function (see below) on any phylogenetic data objects returned by calls to ajAcdGet*.

Additionally, you must call ajPhyloExit to free up any internal memory allocated internally for housekeeping:

```
void ajPhyloExit (void);
```

# 6.12.7 Phylogenetic object memory management

# 6.12.7.1 Default object construction

To use a phylogenetic data object that is not defined in the ACD file you must first instantiate the appropriate object pointer. The default constructor functions are: