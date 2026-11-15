
## 6.12.7.3 Alternative object construction and loading

### 6.12.7.3.1 Phylogenetic data input

Currently there are no functions for this.

### 6.12.7.3.2 Phylogenetic data output

Currently there are no functions for this.

### 6.12.8 Reading phylogenetic data from file

The functions for this are:

```
AjPPhyloDist* ajPhyloDistRead (const AjPStr filename, ajint size, AjBool missing);
AjPPhyloFreq ajPhyloFreqRead (const AjPStr filename, AjBool contchar, AjBool genedata, AjBool indiv);
AjPPhyloProp ajPhyloPropRead (const AjPStr filename, const AjPStr propchars, ajint len, ajint size);
AjPPhyloState* ajPhyloStateRead (const AjPStr filename, const AjPStr statechars);
AjPPhyloTree* ajPhyloTreeRead (const AjPStr filename, ajint size);
```

They are provided in case phylogenetic data needs to be processed outside the context of ACD file processing. See the online documentation for further information.

### 6.12.9 Getting elements of phylogenetic objects

Currently there is a single function for this. It returns the size of a properties object:

```
ajint ajPhyloPropGetSize (const AjPPhyloProp thys);
```

### 6.12.10 Debug functions

These report the elements of each object to the debug file. The functions are:

```
void ajPhyloDistTrace (const AjPPhyloDist thys);
void ajPhyloFreqTrace (const AjPPhyloFreq thys);
void ajPhyloPropTrace (const AjPPhyloProp thys);
void ajPhyloStateTrace (const AjPPhyloState thys);
void ajPhyloTreeTrace (const AjPPhyloTree thys);
```

## 6.13 Handling codon usage tables

### 6.13.1 Introduction

EMBOSS provides a codon usage table object that holds arrays describing codon usage in a nucleotide sequence.

Codon usage tables for input and output are usually defined in the ACD file, but they can be created directly if this is required. Functions are provided for reading and writing the data, getting and setting elements of the object, calculating properties of the codon usage table and for back translation. There are also some miscellaneous functions, mostly used for interconverting triplet base codes to codon indices.

Code that creates a codon usage table needs to first create an output object, then populate it with codon usage data from coding sequences, calculate statistics on codon frequencies and write to a file which uses the user-selected format.

### 6.13.2 AJAX library files

AJAX library files for handling codon usage tables are listed in the table below. Library file documentation, including a complete description of datatypes and functions, is available at: http://emboss.open-bio.org/rel/dev/libs/

| Library file documentation | Description |
|---|---|
| ajcod | Codon usage table handling |

ajcod.h/c. Defines the AjPCod object and functions for handling codon usage tables. It also contains static data structures and functions for handling them at a low level. You are unlikely to need these unless you plan to extend the core functionality of the library.

### 6.13.3 ACD datatypes

The ACD datatype for handling codon usage tables is:

- codon Codon usage table file

### 6.13.4 ACD data definition

A typical ACD definition for codon usage table input:

```
codon: infile
[
  parameter: "y"
]
```

A typical ACD definition for codon usage table output:

```
outcodon: outfile
[
  parameter: "Y"
]
```

### 6.13.4.1 Parameter name

All data definitions for codon usage table input and output should have an intuitive name: no standard names are currently defined.

### 6.13.4.2 Common attributes

Attributes that are typically specified are summarised below.

parameter: If a codon usage table is the primary input or output of an EMBOSS application it should be defined as a parameter by using parameter: "Y" (see Section A.4, 'Global attributes').

### 6.13.5 AJAX datatypes

For handling codon usage tables, including input codon usage tables defined in the ACD file, use:

- AjPCod Codon usage table object (for codon ACD datatype)

For handling output codon usage tables defined in the ACD file use:

- AjPOutfile General output file (for outcodon ACD datatype)

### 6.13.6 ACD file handling

Datatypes and functions for handling codon usage tables via the ACD file are shown below.

| | To read a codon usage table | To write a codon usage table |
|---|---|---|
| ACD datatype | codon | outcodon |
| AJAX datatype | AjPCod | AjPOutfile |
| To retrieve from ACD | ajAcdGetCodon | ajAcdGetOutcodon |

Your application code will call embInit to process the ACD file and command line (see Section 6.3, 'Handling ACD files'). All values from the ACD file are read into memory and files are opened as necessary. You have a handle on the files and memory through the ajAcdGet* family of functions which return pointers to appropriate objects.

### 6.13.6.1 Input codon usage table retrieval

To retrieve an input codon usage table an object pointer is declared and then initialised using ajAcdGetCodon:

```
AjPCod cod = NULL;
cod = ajAcdGetCodon("infile");
```

### 6.13.6.2 Output codon usage table retrieval

To retrieve an output codon usage table stream an object pointer is declared and initialised using ajAcdGetOutcodon:

```
AjPOutfile codout = NULL;
codout = ajAcdGetOutcodon("outfile");
```

### 6.13.6.3 Processing command line options and ACD attributes

Currently there are no functions for this.

### 6.13.6.4 Memory and file management

It is your responsibility to close any files and free up memory at the end of the program.

#### 6.13.6.4.1 Closing output codon usage table files

To close an output codon usage table use ajOutfileClose:

```
ajOutfileClose(&codout);
```

#### 6.13.6.4.2 Freeing memory

You must call the default destructor function (see below) on any objects returned by calls to ajAcdGetCodon or ajAcdGetOutcodon.

Additionally, you must call ajCodExit to clean up internal memory allocated for housekeeping of codon usage processing:

```
ajCodExit();
```

### 6.13.7 Codon usage table object memory management

#### 6.13.7.1 Default object construction

To use a codon usage table object that is not defined in the ACD file you must first instantiate the appropriate object pointer. The default construction function is:

```
AjPCod ajCodNew(void);
```

All constructors return the address of a new object. In the following code the pointer does not need to be initialised to NULL but it is good practice to do so:

```c
AjPCod cod = NULL;
cod = ajCodNew();
/* The object is instantiated and ready for use */
```

#### 6.13.7.2 Default object destruction

You must free the memory for an object when you are finished with it. The default destructor function is:

```c
void ajCodDel (AjPCod *pthys) ;
```

It is used as follows:

```c
AjPCod cod = NULL;
AjPOutfile codout = NULL;
cod = ajAcdGetCodon("infile");
codout = ajAcdGetOutcodon("outfile");
...
ajCodDel(&cod);
ajOutfileClose(&codout);
```

#### 6.13.7.3 Alternative object construction and loading

There are two alternative constructor functions. ajCodNewCodenum creates a codon usage object with the amino acid assignments taken from a standard genetic code. In contrast, ajCodNewCod will duplicate an existing codon object and return a pointer to the new object:

```c
AjPCod ajCodNewCodenum (ajint code) ;
AjPCod ajCodNewCod (const AjPCod thys) ;
```

### 6.13.8 Reading and writing codon usage tables

#### 6.13.8.1 Reading a codon usage table

To use a codon usage table created directly (i.e. not one defined in the ACD file) it's necessary to assign a codon index to it. ajCodRead will read codon usage data from a file

```
AjBool ajCodRead (AjPCod thys, const AjPStr fn, const AjPStr format);
```

Codon input and output formats are printed by the entrails utility using the ajCodPrintFormat function.

#### 6.13.8.2 Writing a codon usage table

There are two analogous functions for writing codon usage table information to file which differ in the type of file object (AjPFile and AjPOutfile) passed:

```
void ajCodWrite (AjPCod thys, AjPFile outf);
void ajCodWriteOut (const AjPCod thys, AjPOutfile outf);
```

Usually codon usage table output files (AjPOutfile) are loaded from ACD file processing (see above). Therefore ajCodWriteOut is called for such an AjPOutfile corresponding to an outcodon : ACD data definition:

```
AjPCod cod = NULL;
AjPOutfile codout = NULL;

cod = ajAcdGetCodon("infile");
codout = ajAcdGetOutcodon("outfile");

ajCodWriteOut(cod, codout);
```

Where ajCodWrite is used it's necessary to handle the creation of the output file manually. Use ajFileNewOutNameC (or other functions) for doing so:

```
AjPCod cod = NULL;
AjPFile codout = NULL;

/* Open a file called "OutputFileName" */
codout = ajFileNewOutNameC ("OutputFileName");

ajCodWrite(cod, codout);
```

### 6.13.9 Getting and setting elements

The following elements of a codon usage table may be retrieved or set:

- Name
- Release
- Description
- Division
