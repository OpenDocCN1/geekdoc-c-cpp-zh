
### 6.14.8.1 Buffered files

Functions with the prefix ajBuffRead read a line from a buffered file. The line that's read can be appended to a string and the file position before the read can be retained:

```c
/* Read a line from a buffered file. */
AjBool ajBuffReadLine (AjPFilebuff file, AjPStr* Pstr);

/* Read a line and note the file position. */
AjBool ajBuffReadLinePos (AjPFilebuff file, AjPStr* Pstr, ajlong* fpos);

/* Read a line and optionally append to a Pstore buffer */
AjBool ajBuffReadLinePosStore (AjPFilebuff buff, AjPStr* Pdest, ajlong* Ppos,
                               AjBool dostore, AjPStr *Pstore);
```

### 6.14.9 Writing to files

### 6.14.9.1 General files

There are two functions from ajfmt.c/h for writing to files. The most widely used is ajFmtPrintF which writes to an AJAX file object. Alternative functions write to a C FILE or to standard output:

```c
/* Format and emit the "..." arguments according to fmt; writes to a file object */
void ajFmtPrintF (AjPFile file,
                  const char *fmt, ...);

/* Format and emit the "..." arguments according to fmt; writes to C FILE stream: */
void ajFmtPrintFp (FILE *stream,
                   const char *fmt, ...);

/* Format and emit the "..." arguments according to fmt; writes to stdout */
void ajFmtPrint (const char *fmt, ...);
```

### 6.14.9.2 Binary files

Functions for writing to a binary file have the prefix ajWritebin. A single byte, a C-type string (char *) or a string object can be written to a field of defined size (len), or a numeric values can be written with the correct byte orientation:

```c
/* Writes a single byte in a defined field. */
ajint ajWritebinByte (AjPFile file, char chr);
ajint ajWritebinChar (AjPFile file, const char* txt, ajint len);
ajint ajWritebinStr (AjPFile file, const AjPStr str, ajint len);

/* Writes a 2-byte integer. */
ajint ajWritebinInt2 (AjPFile file, ajlong i);

/* Writes a 4-byte integer. */
ajint ajWritebinInt4 (AjPFile file, ajlong i);
```

```c
/* Writes a 8-byte integer. */
ajint ajWritebinInt8 (AjPFile file, ajlong i);
```

### 6.14.9.3 Buffered files

In some cases it is necessary to write to a buffered file that is otherwise being used for input. Three functions are provided to write lines to a buffered file for input. These are used internally, for example when reading binary sequence formats.

```c
/* Writes a C-type string to the buffer */
void ajFilebuffLoadC (AjPFilebuff file, const char* txt);

/* Writes a string object to the buffer */
void ajFilebuffLoadS (AjPFilebuff file, const AjPStr str);

/* Writes all lines from a file into the buffer. */
void ajFilebuffLoadAll (AjPFilebuff file);
```

### 6.14.10 Manipulating files

Three functions are provided to set the properties of a file object:

```c
/* Close current file and open next one. */
AjBool ajFileReopenNext (AjPFile* Pfile);

/* Reopens a file with a new name. */
FILE* ajFileReopenName (AjPFile* Pfile, const AjPStr name);

/* Sets the current position in an open file. */
ajint ajFileSeek (AjPFile* Pfile, ajlong offset, ajint from);
```

For a file object that includes a list of input files, ajFileReopenNext will close the current input file and open the next one. ajTrue is returned on success or ajFalse otherwise. ajFileReopenName calls the C function freopen to close the current file and open a file with a new name. ajFileSeek is, essentially, a wrapper to the C function fseek and sets the current position in an open file. In cases where end-of-file was reached and this function is used to move back somewhere in the file, then the end-of-file flag in the file object is reset.

Functions for setting the properties of buffered file objects have the prefix ajFilebuffSet and include:

```c
/* Sets file to be buffered. */
AjBool ajFilebuffSetBuffered (AjPFilebuff* Pfile);

/* Sets file to be unbuffered. */
AjBool ajFilebuffSetUnbuffered (AjPFilebuff* Pfile);

/* Sets next read to start at first buffered line. */
AjBool ajFilebuffReset (AjPFilebuff* Pfile);
```

```c
/* Sets next read position and resets file position. */
AjBool ajFilebuffResetPos (AjPFilebuff* Pfile);

/* Resets the pointer and current record and optionally clears Pstore buffer */
void ajFilebuffResetStore (AjPFilebuff buff, AjBool dostore, AjPStr *Pstore);

/* Deletes processed lines from a file buffer. */
AjBool ajFilebuffClear (AjPFilebuff* Pfile, ajint n);

/* Clears processed records and removes extra record(s) from the Pstore buffer */
AjBool ajFilebuffClearStore (AjPFilebuff buff, ajint lines, const AjPStr lastline,
    AjBool dostore, AjPStr *Pstore);
```

Buffering of file input can be turned on and off by calling ajFilebuffSetBuffered and ajFilebuffSetUnbuffered respectively (buffering for an AjPFilebuff object is on by default). Functions with the prefix ajFilebuffReset set the next read position to the start of the first buffered line. ajFilebuffResetPos also resets the current file position to the last known read as a precaution in cases where this might have been changed by some other function. ajFilebuffResetStore also clears the caller's record of processed lines, using the same control parameter as ajBuffReadLinePosStore. ajFilebuffClear and ajFilebuffClearStore will delete the buffered lines processed so far. ajFilebuffClearStore will also clear the caller's record of processed lines, using the same control parameter as ajBuffReadLinePosStore.

### 6.14.11 Querying properties of files

### 6.14.11.1 Basic properties

The file name, C-type file pointer (FILE *) and file length of a file object are available by calling:

```c
/* File name. */
AjPStr ajFileGetNameS (const AjPFile file);

/* File name. */
const char* ajFileGetNameC (const AjPFile file);

/* C file pointer. */
FILE* ajFileGetFileptr (const AjPFile file);
```

These functions (and other *Get* functions below) return elements (or values calculated from them) of the object itself, therefore care must be taken not to inadvertently change the object in cases where a pointer is returned.

Functions with the prefix ajFileIs check whether a file is a certain type or if the object satisfies some other property:

```c
/* File is stderr. */
AjBool ajFileIsStderr (const AjPFile file);

/* File is stdin. */
AjBool ajFileIsStdin (const AjPFile file);

/* File is stdout. */
AjBool ajFileIsStdout (const AjPFile file);

/* File is set for appending. */
AjBool ajFileIsAppend (const AjPFile file);

/* File position is at end-of-file. */
AjBool ajFileIsEof (const AjPFile file);
```

These functions (and *Is* functions for other datatype below) return ajTrue if the condition is met.

### 6.14.11.2 Output files

The file object, C-type file pointer (FILE *) from the file object and format are available for retrieval from an output file object:

```c
/* File object. */
AjPFile ajOutfileGetFile (const AjPOutfile file);

/* Output format. */
AjPStr ajOutfileGetFormat (const AjPOutfile file);

/* C file pointer. */
FILE* ajOutfileGetFileptr (const AjPOutfile file);
```

### 6.14.11.3 Buffered files

The file object, C-type file pointer (FILE *) from the file object and standard record buffer size are available for retrieval from a buffered file object:

```c
/* File object */
AjPFile ajFilebuffGetFile (const AjPFilebuff file);

/* C file pointer from file object */
FILE* ajFilebuffGetFileptr (const AjPFilebuff file);
```

A buffered file can be tested for whether it is empty, buffered, whether end-of-file has been reached or whether the file is exhausted (end-of-file is reached and the buffer is empty):

```c
/* File buffer is empty. */
AjBool ajFilebuffIsEmpty (const AjPFilebuff file);

/* Input file is buffered. */
AjBool ajFilebuffIsBuffered (const AjPFilebuff file);

/* File is exhausted (EOF is reached and buffer is empty). */
AjBool ajFilebuffIsExhausted (const AjPFilebuff file);

/* EOF is reached. */
AjBool ajFilebuffIsEof (const AjPFilebuff file);
```

### 6.14.11.4 Directories

The directory name and file extension of files for reading are available for a directory object:

```c
AjPStr ajDirGetPath (const AjPDir Pdir);
AjPStr ajDirGetExt (const AjPDir Pdir);
AjPStr ajDirGetPrefix (const AjPDir Pdir);
```

The directory object can be used to generate a list of full path names of files in the directory and matching any specified prefix and extension:

```c
ajint ajFilelistAddDirectory (AjPList list, const AjPDir dir);
```

### 6.14.12 Querying and manipulating file and directory names

It's possible to check a string representing a filename includes a path by calling ajFilenameHasPath, which returns ajTrue if the property is satisfied. Functions with the prefix ajFilenameTest test a filename:

```c
/* Checks for path. */
AjBool ajFilenameHasPath (const AjPStr name);
```

There are various functions to test a filename (with or without a path specification) against wildcards defining filenames to include or exclude. Filenames may be included or excluded by default. The inclusion wildcard is used to select files, and the exclusion wildcard is then used to exclude selected files again:

```c
/* Tests a filename. Default is to exclude */
AjBool ajFilenameTestExclude(const AjPStr filename,
const AjPStr exclude,
const AjPStr include);

/* Tests a full path file name. Default is to exclude. */
AjBool ajFilenameTestExcludePath(const AjPStr filename,
const AjPStr exclude,
const AjPStr include);

/* Tests a file name. Default is to include. */
AjBool ajFilenameTestInclude(const AjPStr filename,
const AjPStr exclude,
const AjPStr include);

/* Tests a full path file name. Default is to include. */
AjBool ajFilenameTestIncludePath(const AjPStr filename,
const AjPStr exclude,
const AjPStr include);
```

There are functions to check whether a named file exists and is in a specified mode (read, write or executable):
