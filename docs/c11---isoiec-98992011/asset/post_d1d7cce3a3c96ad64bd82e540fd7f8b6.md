
At program startup, three text streams are predefined and de-not to be opened explicitly — standard input (for reading conventional input), standard output (for writing conventional output), and standard error (for writing diagnostic output). As initially opened, the standard error is not fully buffered; the standard input and output streams are fully buffered if and only if the stream can be determined not to refer to an interactive device.

Functions that operate additional (temporary) files require a file name, which is a string. The rules for composing valid file names are implementation-defined. Whether the same file can be simultaneously open multiple times is also implementation-defined.

Although both text and binary wide-oriented streams are conceptually sequences of wide characters, the external file associated with a wide-oriented stream is a sequence of multibyte characters, generalized as follows:

- Multibyte encodings within files may contain null bytes (unlike multibyte encodings for use internal to the program).
- A file name does not begin nor end in the initial shift state.<sup>268)

Moreover, the encodings used for multibyte characters may differ among files. Both the nature and choice of such encodings are implementation-defined.

The wide character input functions read multibyte characters from the stream and convert them to wide characters as if they were read by successive calls to the fgetwc function. Each conversion occurs as by a call to the mbtwc function, with the conversion described by the stream's own mbstate_t object. The input functions read characters from the stream as by successive calls to the fgetc function.

The wide character output functions convert wide characters to multibyte characters and write to the stream as if they were written by successive calls to the fputwc function. Each conversion occurs as by a call to the mbctomb function, with the conversion state described by the stream's mbstate_t object. The output functions write characters to the stream as by successive calls to the fputc function.

In some cases, some of the input/output functions also perform conversions between multibyte characters and wide characters. These conversions also occur as by calls to the mbtwc and wctomb functions.

An encoding error occurs if the character sequence presented to the underlying mbtwc function does not form a valid (generalized) multibyte character, or if the code passed to the underlying wctomb does not correspond to a valid (generalized) multibyte character. The wide character input/output functions and the byte input/output functions store the value of the macro EILSEQ in errno if and only if an encoding error occurs.

<sup>268 Setting the file position indicator to end-of-file, as fseek(file, 0, SEEK_END), has undefined behavior for a binary stream (because of trailing null characters) or for any stream with-dependent encoding that does not end in the initial shift state.</sup>

# Environmental limits

- 15 The value of FOPEN_MAX shall be at least enough for the three standard text streams.

Forward references: the exit function (7.22.4.4), the fgetc function (7.21.7.1), the fopen function (7.21.5.3), the fputc function (7.21.7.3), the setbuf function (7.21.5.5), the setvbuf function (7.21.5.6), the fgetwc function (7.29.3.1), the fputwc function (7.29.3.2), conversion state (7.29.6), the mbrtwc function (7.29.6.2), the weortomb function (7.29.6.3).

## 7.21.4 Operations on files

### 7.21.4. The remove function

#### Synopsis

```
#include <stdio.h>
int remove(const char *filename);
```

#### Description

- 2 The remove function causes the file name the string pointed to by filename to be no longer accessible by that name. A subsequent attempt to open that file using that name will fail, unless it is created. If the file is open, the behavior of the remove function is implementation-defined.

#### Returns

- 3 The remove function returns zero if the operation succeeds, nonzero if it fails.

### 7.21.4.2 The rename function

#### Synopsis

```
#include <stdio.h>
int rename(const char *old, const char *new);
```

#### Description

- 2 The rename function causes the file name the string pointed to by old to be henceforth known as the name given by the string pointed to new. The file named old is no longer accessible by that name. If a file named the string pointed to new exists prior to the call to the rename function, the behavior is implementation-defined.

#### Returns

- 3 The rename function returns zero if the operation succeeds, nonzero if it fails,<sup>269</sup> in which case if the file existed previously is still known by its original name.

### 7.21.4.3 The tmpfile function

#### Synopsis

```
#include <stdio.h>
FILE *tmpfile(void);
```

#### Description

- 2 The tmpfile function creates a temporary binary file that is different from any other existing file and will automatically be removed when it is closed or at program termination. If the program terminates abnormally, whether an open temporary file is removed is implementation-defined. The file is opened with "wb+" mode.

#### Recommended practice

- 3 It should be possible to open at least TMP_MAX temporary files during the lifetime of the program and there should be no limit on the number of files (FOPEN_MAX).

#### Returns

- 4 The tmpfile function returns a pointer to the stream that it created. If the file cannot be created, tmpfile function returns a null pointer.

**Forward references:** the fopen function (7.21.5.3).

### 7.21.4.4 The tmpnam function

#### Synopsis

```
#include <stdio.h>
char *tmpnam(char *s);
```

#### Description

- 2 The tmpnam function generates a string that is a valid file name and is not the same as an existing file.<sup>270</sup> Among the reasons the implementation may cause the rename function to fail that the file is open or that it is necessary to copy its contents to effectuate its renaming.

<sup>270 Files created using strings by the tmpnam function are temporary only in the sense that their names should not collide with those generated by naming rules.</sup>

- 3 The tmpnam function generates a different string each time it is called.

- 4 Calls to the tmpnam function with a null pointer may introduce data races with each other. The implementation shall behave as if no library function calls tmpnam function.

#### Returns

- 5 If no suitable string can be generated, the tmpnam function returns a null pointer. Otherwise, if the argument is a null pointer, the tmpnam function leaves its result in the internal static state and returns a pointer to that object (subsequent calls to the tmpnam function may modify the same object). If the argument is not a null pointer, it is assumed to point to an array of at least L_tmpnam chars; the tmpnam function writes its result in that array and returns the argument as its value

#### Environmental limits

- 6 The value of the macro TMP_MAX shall be at least 25.

## 7.21.5 File access functions

### 7.21.5.1 The fclose function

#### Synopsis

```
#include <stdio.h>
int fclose(FILE *stream);
```

#### Description

- 2 A successful call to the fclose function closes the stream pointed to by stream to be flushed and the associated file to be closed. Any unwritten buffered data for the stream are delivered to the host environment to be written to the file; any unused buffered data are discarded. Whether or not the call succeeds, the stream is dissociated from the file and any buffer by the setbuf or setvbuf function is dissociated from the stream (and deallocated if it was automatically allocated).

#### Returns

- 3 The fclose function returns zero if the stream was successfully closed, EOF if any errors were detected.
