
Before you use `feof`, be aware that a function doesn't encounter end-of-file when the file position indicator has reached the end of the stream. It's only when the function *tries* to read beyond the end that it knows that EOF has occurred and then returns accordingly. Ignorance of this concept has led to the proliferation of erroneous code that uses `feof` as a control expression in a loop. Figure 15.2 shows alternative forms of usage of `feof`. The first is totally wrong while the second one is acceptable if we assume that no errors would occur.

|  |  |
| :--- | :--- |
| **Declarations:** `FILE *fp = fopen("foo", "r");` `char buf[80];` | |
| `while (!feof(fp)) {`<br>`    fgets(buf, 80, fp);`<br>`    fputs(buf, stdout);`<br>`}` | `while (1) {`<br>`    fgets(buf, 80, fp);`<br>`    if (feof(fp))`<br>`        break;`<br>`    fputs(buf, stdout);`<br>`}` |
| Incorrect Usage | Acceptable Usage |

**FIGURE 15.2** Using `feof` in a Loop

To understand why the code on the left is erroneous, consider that the last line of `foo` has been read and printed. At this stage, `fgets` has not encountered EOF yet because it doesn't know whether further data is forthcoming. When the control expression is tested, `!feof(fp)` is still true, so the body of the loop is executed. This time, `fgets` encounters EOF (which would impact the next iteration), but `fputs` still goes ahead and prints the previous line. This means that the last line is printed twice.

The EOF and error indicators remain set until a third function—`clearerr`—clears both indicators. This function also uses the file pointer as argument but it returns nothing (`void`). None of the three functions sets the variable `errno`, so you can't use `errno` and `perror` to handle EOF and file I/O errors.

## 15.12 TEXT AND BINARY FILES

So far, we have been reading and writing *text* files as opposed to *binary* ones. The popular distinction that is made between them is that text files contain data in character form while binary files contain binary data. This view is unacceptable because all data are eventually read and written in binary form. Though no formal definition of a text file exists to this day, we must adopt one that is consistent with its usage. A text file generally has these features:

- It contains *readable* and *printable* data that are organized as a set of *lines* delimited by the newline character appropriate to the machine.
- Some characters like newline and EOF (like *Ctrl-z*) are treated differently by a program. You are aware of the newline conversions that take place when these files experience a change of environment.
- Text characters are drawn from the ones available on the keyboard. They have the ASCII values between 0 and 127 (7-bit ASCII), though all characters in this range are not printable.
- A number is represented as a string comprising digit characters and a decimal point. For instance, the number 123 is saved as the characters '1', '2' and '3' in a text file.

None of the preceding observations apply to binary files. A binary file can contain any character in the entire ASCII range (0 to 255). The newline or EOF character has no special significance in a binary file. Even though strings are accorded the same treatment by both file types, a binary file saves numbers in binary form. The number 123 can be stored in one byte, but a program may specify a short or int, in which case two or four bytes may be allocated.

Number crunching becomes very efficient when numbers are handled directly in binary form. The overheads of conversion from text to binary and vice versa can be quite significant, the reason why databases always store numeric data in binary form.

This review of the two file types will help us handle the `fread` and `fwrite` functions that are meant to be used with binary files.

## 15.13 fread AND fwrite: READING AND WRITING BINARY FILES

The previous file I/O functions handled data in units of characters (`fgetc`/`fputc`), lines (`fgets`/`fputs`) or matched items (`fscanf`/`fprintf`). The fourth and final category comprising the `fread` and `fwrite` functions handle data in more versatile ways:

- Numeric data are read and written in binary form.
- The amount of data to be transferred can be specified in larger units—an array, structure or an array of structures.

Each read or write operation transfers one or more records of equal length. Because of this equality, binary files can be updated by “seeking” to a specific record using the `fseek` function. We haven’t updated a record so far, but we’ll do it this time using `fread` and `fwrite`.

### 15.13.1 The fread Function

|  |  |
| :--- | :--- |
| **Prototype:** | `size_t fread(void *p, size_t size, size_t num, FILE *stream);` |
| **Return value:** | Number of items successfully read even when EOF or error is encountered. |

The `fread` function takes four arguments. It reads *num* units of data of *size* characters each from *stream*, and saves the data in the variable *p*, whose pointer is specified as the first argument. Because *p* can be a variable of any type, a generic (void) pointer is specified. *size_t* represents an integer type which is typedef’d to one of the primitive data types during compilation.

`fread` is meant for handling user-defined and derived data types, but it’s a good idea to get started with a primitive data type. For reading a single integer, *num* must be specified as 1 and *size* as the size of an int:

```
int i;
fread(&i, sizeof(int), 1, fp);
```

*`fp` returned by `fopen`*

This call reads one unit of four bytes in binary form and saves it in the variable `i`. A string is read in the following manner:

```
char stg[10];
fread(stg, sizeof(char), 10, fp);
```

`fread` reads 10 characters from the stream, or rather, 10 units of one char where the unit size is specified as the second argument. What makes `fread` different from its peers is that a single call can read a set of integers into an array:

```
short arr[5];
fread(arr, sizeof(short), 5, fp);    // Reads five numbers to array arr
```

Like the members of the “scanf” family, `fread` returns the number of items successfully read even if the function terminates with an error. `fread` can also read multiple data items in one call provided they form members of a structure. We’ll be demonstrating this feature shortly.

### 15.13.2 The fwrite Function

|  |  |
| :--- | :--- |
| **Prototype:** | `size_t fwrite(void *p, size_t size, size_t num, FILE *stream);` |
| **Return value:** | Number of items successfully written even when error is encountered. |

`fread` and `fwrite` have identical prototypes; they differ only in the direction of data transfer. `fwrite` writes *num* units of data of *size* characters each from the variable *p* to the file associated with *stream*. This is how you save an entire array to a file:

```
short arr[5] = {100, 200, 300, 400, 500};
fwrite(arr, sizeof(short), 5, fp);
```

This is where using the binary mode can result in significant savings. The preceding `fwrite` function writes 10 bytes to disk. If these five numbers were saved in a text file, they would have taken up 15 bytes of disk space (plus one or two for the newline character).

### 15.13.3 fread_fwrite.c: Using the Primitive and Derived Data Types

Program 15.11 uses `fwrite` to write three data items—an integer, string and array of type short—to the file `foobar`, which is opened in binary mode (`"w+b"`). The items are originally stored in variables having the “out” suffix. They are read back using `fread` into a separate set of variables having the “in” suffix. Note that the contents of the five-element arrays, `s_in` and `s_out`, are transferred using a single invocation each of `fwrite` and `fread`.

```
/* fread_fwrite.c: Uses fwrite to write three types of data items
                to a file and then reads them back with fread. */
#include <stdio.h>
#include <stdlib.h>
#define SIZE 15
```
