
## 10.10.2.5 Exiting cleanly

There's then lots of native code which isn't shown. Finally the program must exit with a call to embExit():

```
if (outfile != NULL && (ofp = fopen(outfile, "w")) != NULL)
{
WriteSELEX(ofp, aseq, &ainfo, 50);
printf("Alignment saved in file %s\n", outfile);
fclose(ofp);
}
else
WriteSELEX(stdout, aseq, &ainfo, 50);

/********************************************************************
* Cleanup and exit
********************************************************************/
for (i = 0; i < nseq; i++)
{
P7FreeTrace(tr[i]);
FreeSequence(rseq[i], &(sQinfo[i]));
free(dsq[i]);
}

FreeAlignment(aseq, &ainfo);
FreePlan7(hmm);
free(sQinfo);
free(rseq);
free(dsq);
free(wgt);
free(tr);

SqdClean();

ajStrDel(&outfname);
ajStrDel(&infname);
ajStrDel(&ajseqfile);

#ifdef MEMDEBUG
current_size = malloc_inuse(&histid2);
if (current_size != orig_size) malloc_list(2, histid1, histid2);
else fprintf(stderr, "[No memory leaks.]\n");
#endif
```

```
embExit();
return 0;
}
```

## 10.11 Summary

To incorporate third-party applications into EMBOSS takes significant work, regardless of whether an application is wrapped or ported. This work is very worthwhile though because of benefits in terms of distribution (the software will reach more users) and, in some cases, because of lowered costs of training, support and maintenance. Moreover, any incorporated software can make use of inbuilt EMBOSS functionality such as support for common sequence formats and will be integrated into the many available EMBOSS interfaces. These include graphical user interfaces, workflow software and web services.

Fully ported software provides the most flexibility but this comes at a high relative maintenance cost. Nonetheless, this is the preferred route where the code is to be essentially adopted by EMBOSS. More or less the same flexibility can be achieved in a wrapper by the use of temporary files, although there are drawbacks and potential complications to this. For example, code for interconverting file formats is needed.

## Appendix A ACD syntax reference

### A.1 Introduction to ACD syntax

#### A.1.1 General syntax

The Ajax Command Definition (ACD) language was designed for writing ACD files for EMBOSS applications. The ACD syntax allows for very flexible descriptions of an application's parameters and its command line interface. It can specify everything that can appear on the command line or in another interface such as a web page.

ACD files are plain ASCII text files and *must* have the extension .acd. Typically they have the same name as the application, but this is not mandatory.

##### A.1.1.1 Whitespace

During ACD file parsing, the entire file contents are effectively treated as a single string which is parsed into tokens delimited by *space* characters. A single space between individual tokens is required: extraneous whitespaces are ignored.

##### A.1.1.2 Comments

Comment lines can be added and begin with “#” and continue to the end of the line.

### A.1.2 ACD definitions

An ACD file contains a single *application definition* and a *data definition* for each parameter. The application definition is given first, followed by the data definitions. Data definitions are organised into sections (Section A.1.6, ‘ACD file sections’).

Application and data definitions have the following general form: a single text token followed by a colon ‘:’ (or ‘=’) and a whitespace, followed by a second token. The definition body follows, which is one or more attributes delimited by a mandatory pair of square brackets [ ], which can span multiple lines. Each attribute is a *name*: *value* pair with the attribute value given between quotes (“ ”):

Either:

```
token: token
{
    Attribute1Name: "Attribute1Value"
    Attribute2Name: "Attribute2Value"
}
```

Or:

```
token=token
[
    Attribute1Name: "Attribute1Value"
    Attribute2Name: "Attribute2Value"
]
```

The first token is either application: (for the application definition) or an AJAX datatype (e.g. sequence) for data definitions. The second token is either the name of the application (e.g. secret) or the name of parameter (e.g. asequence).

Application definition:

```
application: ApplicationName
{
    ApplicationAttribute1Name: "ApplicationAttribute1Value"
    ApplicationAttribute2Name: "ApplicationAttribute2Value"
}
```

Data definition:

```
Datatype: ParameterName
{
    DataAttribute1Name: "DataAttribute1Value"
    DataAttribute2Name: "DataAttribute2Value"
}
```

The application token and tokens for the datatype and attribute names can be can be abbreviated up to the point where they are not ambiguous. Such abbreviations are not recommended however because they tend to make the ACD file more difficult to read.

Attribute values are normally enclosed in double quotes, although this is only mandatory for values (typically strings) which include whitespace.

### A.1.2.1 Application definition

The application definition must be the first definition in the file:

```
application: ApplicationName
{
    ApplicationAttribute1Name: "ApplicationAttribute1Value"
    ApplicationAttribute2Name: "ApplicationAttribute2Value"
}
```

The application name is arbitrary but is typically the same as that used for the ACD file name. It is the ACD file name (not ApplicationName, if different) that's used from within the application C source code to associate it with an ACD file. This allows multiple ACD files (and therefore command line interfaces) to be developed for a single file of application C source code.

For complete description of the available application attributes see Section A.3, 'Application attributes'.

### A.1.2.2 Data definition

All application parameters must have a data definition. Data definitions follow the application definition and must be placed in an appropriate file section (Section A.1.6, ‘ACD file sections’):

```
Datatype: ParameterName
{
    DataAttribute1Name: "DataAttribute1Value"
    DataAttribute2Name: "DataAttribute2Value"
}
```

Datatype must be a valid ACD datatype (see Section A.2, ‘Datatypes’).

ParameterName is the name of the parameter. It is a string that must conform to certain conventions (Section A.1, ‘Introduction to ACD syntax’). This name is used to refer to the data definition from the command line and from within the C source code (see Section 6.3, ‘Handling ACD files’).

For a complete description of the available attributes see: Section A.4 (‘Global attributes’), Section A.5 (‘Datatype-specific attributes’) and Section A.6 (‘Calculated attributes’).

### A.1.3 Parameter naming conventions

#### A.1.3.1 General conventions

Parameter and qualifier names:

- Must not contain whitespace characters
- Should not normally be single characters
- Should be meaningful words and indicate the function of the option so far as possible
- Are not case-sensitive.

#### A.1.3.2 Datatype-specific conventions

Some conventions for parameter names apply to individual datatypes. Where more than one instance of a datatype is specified in an ACD file, then the character a, b, etc. can be appended to the flag: asequence, bsequence, etc. This is indicated in the table by an asterisk in the parameter name, for example *sequence.

| Datatype | Name | Usage |
|---|---|---|
| sequence | sequence, *sequence | Primary input sequence, generally required |
| seqall | sequence, *sequence, seqall | Primary input sequence database, generally required |

### A.1 Introduction to ACD syntax

| Parameter | Type/Name | Description |
| :--- | :--- | :--- |
| seqset | sequence, *sequence, sequences | Primary input sequences, generally required |
| seqsetall | sequence, *sequence, sequences | Primary input sequences, generally required |
| seqout, seqoutset, seqoutall | outseq, *outseq, *outfile | Primary output sequence, generally required, generally should default to the primary input sequence name, extension defaults to the name of the output sequence format |
| outfile | outfile, *file | Primary output non-sequence results file, generally required. The file extension should be allowed to default to the application name. outfile should be used for the first output file. outfile or *file is acceptable for the second and subsequent output files |
| report | outfile, *file | Report output file. outfile should be used for the first report file. outfile or *file is acceptable for the second and subsequent report files |
| align | outfile, *file | Alignment output file. outfile should be used for the first output alignment. outfile or *file is acceptable for the second and subsequent output alignments |
| infile | infile, *file | Primary input non-sequence file |
| infile | data | Primary auxiliary input data file, generally optional |
| infile | patterns | File of patterns to search for in sequence |
| integer | minlen | Minimal length of sequence feature to be found |
| integer | maxlen | Maximum length of sequence feature to be found |
| integer | wordsize | Word size for hash tables, etc. Generally minimum value = 2 for protein, 4 for DNA |
| integer | window | Window length for calculating dotplots, features, etc. |
| integer | shift | Amount by which window is shifted in each iteration |
| boolean | consensus | Flag for whether consensus sequence should be output |
| float | gap | Gap penalty |
