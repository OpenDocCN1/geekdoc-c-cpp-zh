
ajStrDel(&cstring);
ajStrDel(&dstring);

embExit();
return 0;
}

## 2.5.3 Compilation and testing

To compile your program give the following command from the myemboss directory:

```
make
```

And, if you are using myemboss as part of a fully installed EMBOSS system, install it using:

```
make install
```

## 2.5.4 Adding functionality

The EMBOSS string handling library is very extensive. You can inspect ajstr.h and ajstr.c to get a feel for what's available. The functions are organised into sections for convenience and these include assignment, combination, cut, substitution, query, element retrieval, formatting, comparison, and so on. Just a few functions from these categories are shown below:

```
/** A string "assignment" function to copy a string to a string. */
AjBool ajStrAssignS(AjPStr* Pstr, const AjPStr str);

/** A string "combination" function which appends a strings */
AjBool ajStrAppendS(AjPStr* Pstr, const AjPStr str);

/** A string "combination" function which inserts a text string into a
string at a specified position. */
AjBool ajStrInsertS (AjPStr* pthis, ajint pos, const AjPStr str);

/** A string "cut" function which removes a substring from a string. */
AjBool ajStrCutRange(AjPStr* Pstr, ajint pos1, ajint pos2);

/** A string "cut" function which removes the end from a string
reducing it to a defined length. */
AjBool ajStrTruncateLen(AjPStr* Pstr, size_t len);

/** A string "substitution" function which reverses the order of characters
in a string. */
AjBool ajStrReverse(AjPStr* Pstr);
```

/* A string "query" function which counts occurrences of a character in a string. */
ajint ajStrCalcCountK(const AjPStr str, char chr);

/* A string "element retrieval" function which returns a single
character at a given position from a string. */
char ajStrGetCharPos(const AjPStr str, ajint pos);

/* A string "formatting" function which converts a string to upper case. */
AjBool ajStrFmtUpper(AjPStr* Pstr);
/* A string "comparison" function which is a simple test for matching
two strings. */
AjBool ajStrMatchS (const AjPStr this, const AjPStr str);

/* A string "comparison" to test for matching the start of a string against a
given prefix string. */
AjBool ajStrPrefixS(const AjPStr str, const AjPStr str2);

/* A string "comparison" function to find the first occurrence in a string of a
second string. */
ajint ajStrFindS (const AjPStr str, const AjPStr str2);

Many of the functions return AjBool. This might indicate whether the function was reallocated, was successful or not, whether a test was true or not and so on. You should refer to the documentation in ajstr.c for the exact meaning.

AjPStr* Pstr indicates a string argument that is (or might be) modified by the function. const in front of an argument indicates a variable with a constant value. So here, const AjPStr str indicates a string argument that is used but not modified by the function; the pointer cannot be reallocated by the function.

Here are a few examples to illustrate how some of the string functions are called. First, ajStrAssignS is used to assign an existing string to a new string. The function should follow construction of newstr. newstr is modified which is why the address of newstr is required:

```
ajStrAssignS(&newstr, astr);
```

Here ajStrFmtUpper is used to convert a string to upper-case. Again, the address of the string is required:

```
ajStrFmtUpper(&astring);
```

Here two strings are compared and some action taken if they are identical:

```
if(ajStrMatchS(astr, bstring))
{ /* Do something */ }
```

## 2.5.4.1 String memory management

It is good practice to explicitly construct (allocate memory for) each string before it is used, and destroy it (free memory) for the string once you are finished with it. A default constructor

## 2 YOUR FIRST EMBOSS APPLICATION

function (ajStrNew) and destructor function (ajStrDel) are provided for this purpose.
Their use is shown below:

```c
/* newstr is NULL, no memory is allocated */
AjPStr newstr=NULL;

/* newstr now points to a string object in memory and is ready for use by
our program */
newstr = ajStrNew();

/* memory for the string object is freed. The program can terminate without
potentially leaking memory. */
ajStrDel(&newstr);
```

You do not need to call the constructor function for ACD variables because memory is
allocated for these by the call to embInitP. There is risk of memory error if you do. In the
following rather contrived and bugged code the call to ajAcdGetString will overwrite the
pointer to memory allocated and returned by the (unnecessary) call to ajStrNewC:

```c
/* This code is bugged */
AjPStr astring=NULL;

/* allocates memory for all ACD data items */
embInitP("stringplay", argc, argv, "myemboss");

/* newstr now points to a string object in memory */
astring = ajStrNewC("Hello");

/* this call will break the handle to the memory allocated by ajStrNewC */
astring = ajAcdGetString("astring");
```

The correct code is:

```c
AjPStr astring=NULL;

/* allocates memory for all ACD data items */
embInitP("stringplay", argc, argv, "myemboss");

/* Get a string value from ACD */
astring = ajAcdGetString("astring");

/* memory for the string object is freed. The program can terminate without
potentially leaking memory. */
ajStrDel(&astring);
```

A string object was created by embInitP and must be freed once you are done with it. That is
what the call ajStrDel(&astring); is for.

## Software development under EMBOSS

### 3.1 EMBOSS programming

#### 3.1.1 Introduction

Software development and maintenance under EMBOSS is made easy. EMBOSS has powerful inbuilt functionality which any native application can make use of with little or no additional coding, saving you a great deal of effort. It includes extensive C programming libraries for extending the core functionality and developing new applications. Well-defined processes are in place for key aspects such as quality assurance testing, installation, maintenance and support. General aspects are handled by the EMBOSS developers, leaving you to support the parts specific to your own software.

#### 3.1.2 Inbuilt functionality

Major inbuilt areas of functionality include:

- Support for biological datatypes
- Support for common file formats
- Simple database configuration
- Command line handling
- Command line qualifiers
- Sequence and sequence feature specification.

#### 3.1.2.1 Support for biological datatypes

EMBOSS supports a variety of standard and biological datatypes (Section 4.3, 'Data definition'). Datatypes for application inputs and outputs are defined in the AJAX command definition (ACD) files. Datatype attributes allow an input or output to be specified in greater detail, for example by setting a default value or by defining the permitted type of an input sequence. Calculated attributes, such as the length of an input sequence, are available once the data have been read

during ACD file processing but before the application proper starts, allowing for further fine control in the ACD file.

#### 3.1.2.2 Support for common file formats

EMBOSS supports a wide range of file formats for input and output. Biological sequences can be read and written using all common formats. EMBOSS detects the format of an input sequence automatically, but this can be specified for efficiency. Many other formats for sequence features, alignments, data files and so on are handled automatically. Any application you write will support these formats automatically too. Furthermore, when new input and output data formats are added to EMBOSS, your applications will automatically be able to use them; no application code needs to change. For information on supported file formats, see the _EMBOSS User's Guide_.

#### 3.1.2.3 Simple database configuration

Database configuration is simple and flexible. A variety of databases (which can include remote data servers) and diverse access methods are supported. New databases and access methods are easily added. For more information see the _EMBOSS Administrator's Guide_.

#### 3.1.2.4 Command line handling

Your application will use the EMBOSS command line which is consistent across the applications. The ACD file defines the datatype and permissible values for all application options. The ACD file and all input at the command line is validated at startup, before the application proper starts. Command line behaviour, for example the production of a sensible prompt and reprompting for values that are out of range, is handled automatically.

#### 3.1.2.5 Command line qualifiers

EMBOSS includes various command line qualifiers which are not (typically) set in an ACD file. These include _global qualifiers_ and various _datatype-specific qualifiers_. Global qualifiers are available to all applications and control general application behaviour. Datatype-specific qualifiers are used to specify particular inputs and outputs, for instance sequences, in more detail.

#### 3.1.2.6 Sequence and sequence feature specification

Sequences are referenced on the command line by their Uniform Sequence Address (USA) which is a powerful and flexible specification for defining the location and format of sequence data. Similarly, sequence features are defined using a Uniform Feature Object (UFO). Any application you write will automatically support USAs and UFOs. For more information see the _EMBOSS User's Guide_.

#### 3.1.3 Basic steps to development

There's more to software than just coding, especially when developing for EMBOSS which is widely distributed and deployed in production environments. All code that is to be integrated into the package must be tested, documented and managed throughout its lifetime. Regardless of whether you intend to develop the libraries or new applications, many of the steps are the same:
