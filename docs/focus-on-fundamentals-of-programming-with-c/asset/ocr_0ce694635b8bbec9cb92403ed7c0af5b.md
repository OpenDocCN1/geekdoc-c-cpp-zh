# Text Files

A text file is a sequence of *characters* terminated by an *end-of-file marker*. The length of the file is not specified when the file is defined. The characters in the file are stored on a storage device other than the memory occupied by the program while the program is executing, such as a disk drive.

Note the emphasis on characters. That's all there is in a text file, just characters. Sprinkled among the characters may be newline characters, '\n', or tab '\t' characters. In addition, each data element in the file (words, numeric data) is usually (though not always) separated from the others by blanks.

The advantage of files is that they can exist independently of the program that creates or uses the data in the file. The size of the file is also not a limiting factor as we can increase the file size simply by adding a character to the end of the file.

# Accessing Text Files

A text file is accessed via a pointer to a structure that is defined in the standard header file `stdio.h` as `FILE`. This structure `FILE` contains members (fields) that describe the current state of the file.

C communicates with files using a data type called a *file pointer*. This type is defined within `stdio.h`, and is written as `FILE *`. A file pointer called `fp` is declared in a statement like:

```
FILE *fp;
```

Your program must first open a file before it can access it. This is done using the `fopen()` function, which returns the required file pointer. `fopen()` is declared as follows:

```
FILE *fopen(char *fileName, char *fileMode);
```

`fopen()` opens a file for I/O and returns a pointer to `FILE`. Both `fileName` and `fileMode` are strings. File names may be any valid file name that can exist under the operating system and can include path information: