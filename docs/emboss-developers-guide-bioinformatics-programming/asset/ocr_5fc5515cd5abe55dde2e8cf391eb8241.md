```
/* Directory object. */
AjPFile ajFileNewOutNameDirS (const AjPStr name, const AjPDir dir);

/* Path. */
AjPFile ajFileNewOutNamePathS (const AjPStr name, const AjPStr path);
```

To open a named general output file for appending you can use:

```
AjPFile ajFileNewOutappendNameS (const AjPStr name);
```

# 6.14.8 Reading from file

Functions for reading lines from a general file have the prefix ajReadline. The file position before the read can be retained, newline characters can be trimmed from the line, and the line can be appended to a provided buffer:

```
/* Read a line from a file. */
AjBool ajReadline (AjPFile file, AjPStr* Pstr);

/* Read and retain file position before read. */
AjBool ajReadlinePos (AjPFile file, AjPStr* Pstr, ajlong* fpos);

/* Read and trim any trailing newline character. */
AjBool ajReadlineTrim (AjPFile file, AjPStr* Pstr);

/* Read, trim newline characters and retain file position before read. */
AjBool ajReadlineTrimPos (AjPFile file, AjPStr* Pstr, ajlong* fpos);

/* Read and append to buffer. */
AjBool ajReadlineAppend (AjPFile file, AjPStr* Pbuff);
```

To read a binary file call:

```
/* Binary read from a file using the C 'fread' function. */
AjBool ajReadbinBinary (AjPFile file, size_t count, size_t element_size,
void* buffer);

/* Read unsigned int */
AjBool ajReadbinUint (AjPFile file, ajuint* ret);

/* Read unsigned int bigendian and converts if needed. */
AjBool ajReadbinUintEndian (AjPFile file, ajuint* ret);
```

ajReadbinBinary will read count elements of size element_size from an input file. ajReadbinUint and ajReadbinUintEndian read an unsigned integer and convert from littleendian (the form used for binary data output, e.g. database index files) or bigendian respectively. Both functions use the C function fread.