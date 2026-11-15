
seqoutall: outseq
[
    parameter: "Y"
    features: "$(feature)"
]

In contrast, boolean: feature is a control definition which, if set by the user, will cause **seqret** to read sequence feature information, if available, from the input file.

boolean: firstonly is another control definition which, if set, will cause only a single sequence to be read:

```
boolean: feature
[
    information: "Use feature information"
]
boolean: firstonly
[
    information: "Read one sequence and stop"
]
```

In practice, many different ACD datatypes (Section A.2, 'Datatypes') are available. Programming these data definitions is covered in greater detail in Section 5.5, 'Programming with objects'.

## 9.1.4 Attributes

Each ACD definition has attributes which are name : value pairs. Attributes are of two basic types. _Global attributes_ are available for all datatypes whereas _datatype-specific attributes_ are available for individual or groups of related datatypes.

Consider the definitions for `feature` and `sequence`:

```
boolean: feature
[
    information: "Use feature information"
]
seqall: sequence
[
    parameter: "Y"
    type: "gapany"
    features: "$(feature)"
]
```

`parameter:` and `information:` are global attributes whereas `type:` and `features:` are datatype-specific.

`parameter:` "Y" defines a data definition to be a _parameter_ as opposed to some kind of _qualifier_. A value for a parameter can be given on the command line with or without a flag (parameter name) as described above. All parameters are required by the application and a value will be prompted for if one is not given on the command line.

parameter: "Y" is not given for the boolean definitions which means, in the absence of standard: "Y" or additional: "Y" attributes, that they will default to being an advanced qualifier. An advanced qualifier is never prompted for. Had standard: "Y" or additional: "Y" been defined, then the data definitions would be standard or additional qualifiers. More information on the behaviour of qualifiers and parameters is available (Section 4.1, 'Introduction to ACD file development').

information: gives a very succinct description of the data definition. The text is used in web forms and other GUIs. It is also the text used to prompt the user for a value at the command line. You'll notice information: is not defined for the sequence inputs and outputs. A default prompt is provided by EMBOSS for these datatypes. All boolean: datatypes have the default value of False which means that a default needn't be defined explicitly in the ACD file.

The type: attribute is specific to the sequence datatypes. type: "gapany" indicates that the input sequence can be of any type and may contain gap characters. In practice many different sequence types are supported (Section A.7, 'Sequence types').

The features: attribute is also sequence-specific. The attribute definition looks a little strange:

```
features: "$(feature)"
```

The $ syntax means 'retrieve the value of...', in this case 'retrieve the value of the feature ACD definition', such that the features: attribute of outseq is set to that value. In other words, the input sequence will include features if the user turned the feature advanced qualifier on by giving it on the command line, e.g. secret -feature. Whilst it is not strictly necessary to have features: "$(feature)" (the information is after all specified in boolean: feature) it makes the application source code a good deal cleaner.

In addition to global and datatype-specific attributes there are two other types of attribute that may appear in an ACD file. Calculated attributes receive a value once the ACD file has been processed and application input files have been read. Finally, there are datatype-specific command line qualifiers which are defined for single or groups of ACD datatypes and may be hard-coded as attributes within an ACD file. See Section A.4 ('Global attributes'), Section A.5 ('Datatype-specific attributes'), and Section A.6 ('Calculated attributes').

## 9.2 The C source code (secret.c)

The application C source code (see below) is very simple. Its basic functions are:

- Declare variables for holding values from the ACD file (AjP* type declarations)
- Process the ACD file and command line (embInit)
- Read the values (input and output sequence streams) from the ACD file into memory (prefix ajAcdGet family of functions)
- Iterate through the input sequences and load a sequence into memory (ajSeqallNext)
- Write the sequence out (ajSeqoutWriteSeq)
- Close the output file
- Exit cleanly (embExit).

The source code is shown below:

/*@source secret application
**
** Return a sequence
**
** @author Copyright (C) Peter Rice
** @@
**
** This program is free software; you can redistribute it and/or
** modify it under the terms of the GNU General Public License
** as published by the Free Software Foundation; either version 2
** of the License, or (at your option) any later version.
**
** This program is distributed in the hope that it will be useful,
** but WITHOUT ANY WARRANTY; without even the implied warranty of
** MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the
** GNU General Public License for more details.
**
** You should have received a copy of the GNU General Public License
** along with this program; if not, write to the Free Software
** Foundation, Inc., 59 Temple Place - Suite 330, Boston, MA 02111-1307, USA.
******************************************************************************/

#include "emboss.h"

/* @prog secret **************************************************************
**
** Reads and writes (returns) sequences
**
******************************************************************************/

int main(int argc, char **argv)
{
    AjPSeqall seqall;
    AjPSeqout seqout;
    AjPSeq seq = NULL;
    AjBool firstonly;

    embInit("secret", argc, argv);

    seqout = ajAcdGetSeqoutall("outseq");
    seqall = ajAcdGetSeqall("sequence");
    firstonly = ajAcdGetBoolean("firstonly");

    while(ajSeqallNext(seqall, &seq))
    {
        ajSeqoutWriteSeq(seqout, seq);
        if(firstonly)
            break;
    }

    ajSeqoutClose(seqout);

    embExit();

    return 0;
}
```

### 9.2.1 Variable declarations

The first block of code in `main()` declares variables for holding values from the ACD file:

```c
AjPSeqall seqall=NULL;
AjPSeqout seqout=NULL;
AjPSeq seq = NULL;
AjBool firstonly;
```

The variables beginning with `AjP` are all C pointers to EMBOSS objects (C data structures for the corresponding types). These include `AjPSeqall`, `AjPSeqout` and `AjPSeq`. Many EMBOSS objects, for both complex biological and other types, are defined in the AJAX and NUCLEUS programming libraries. `AjBool`, in contrast, is the EMBOSS datatype for a simple boolean variable. You'll notice that the pointer variables are initialised to `NULL`. It is good practice to always initialise pointers to `NULL` where they're first defined. For an explanation of why, and detailed information on programming with objects, see Section 5.3, 'Objects (C data structures)'.

`AjPSeq` is for single sequence input, `AjPSeqall` for multiple sequence input and `AjPSeqout` for single sequence output. For the **seqret** application `AjPSeqall seqall` is used for the input sequence stream, `AjPSeq seq` is used to hold the data for a single sequence from that stream and `AjPSeqout seqout` is used for the output sequence stream. `AjBool firstonly` is used to hold the value of the `firstonly` control attribute from the ACD file.

You'll notice that no variable is required for the `feature` data definition. The value for this option is set on the input sequence stream, within the ACD file itself, by the ACD code `features: "$(feature)"`. In other words whether feature information will or will not be included with the sequences is set within the ACD file and stored within the `seqall` object, therefore no additional variable is needed for it in the C code.

### 9.2.2 ACD file and command line processing

The code:

```c
embInit("secret", argc, argv);
```

is used to process the ACD file and command line. It handles all of the user input processing which is why it's called first. `embInit` reads in local database definitions, finds the right ACD file to use (the first argument is "secret" so it looks for `secret.acd` in the ACD directory), reads the ACD file and processes the command line using `argc` and `argv` from `main`.

By the time `embInit` returns, the input sequence stream (`sequence`) will be opened for reading and the first sequence read into memory, the boolean variables `feature` and `firstonly` will have received values (possibly the default) and an output file will be opened for `outseq`. Memory is allocated for these objects and is available for use by the program.

`embInit` handles prompting of the user for values that are not entered on the command line, including functionality such as reprompting the user for values that are out of range.
