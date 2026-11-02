# ### 11.3.1 Pointer to a FILE

Now let’s examine this program. Line 7 states that `cfPtr` is a *pointer to a FILE structure*. A C program administers each file with a separate FILE structure. Each open file must have a separately declared pointer of type `FILE` that’s used to refer to the file. You need not know the specifics of the FILE structure to use files, but you can study the declaration in `stdio.h` if you like. We’ll soon see precisely how the FILE structure leads *indirectly* to the operating system’s file control block (FCB) for a file.

# ### 11.3.2 Using fopen to Open the File

Line 10 names the file—"clients.txt"—to be used by the program and establishes a “line of communication” with the file. The file pointer `cfPtr` is assigned a *pointer to the FILE structure* of the file opened with `fopen`. Function `fopen` takes two arguments:

+   - a filename (which can include path information leading to the file’s location) and
+   - a file open mode.

The file open mode `"w"` indicates that the file is to be opened for writing. If a file *does not exist* and it’s opened for writing, `fopen` *creates the file*. If an existing file is opened for writing, the contents of the file are *discarded without warning*. In the program, the `if` statement is used to determine if the file pointer `cfPtr` is `NULL` (i.e., the file is not opened because it does not exist or whether the user does not have permission to open the file). If it’s `NULL`, the program prints an error message and terminates. Otherwise, the program processes the input and writes it to the file.

> **Common Programming Error 11.1**
> 
> *Opening an existing file for writing ("w") when, in fact, the user wants to preserve the file, discards the contents of the file without warning.*

> **Common Programming Error 11.2**
> 
> *Forgetting to open a file before attempting to reference it in a program is a logic error.*

# ### 11.3.3 Using feof to Check for the End-of-File Indicator

The program prompts the user to enter the various fields for each record or to enter *end-of-file* when data entry is complete. Figure 11.3 lists the key combinations for entering end-of-file for various computer systems.

| Operating system | Key combination |
|---|---|
| Linux/Mac OS X/UNIX | `<Ctrl> d` |
| Windows | `<Ctrl> z` then press *Enter* |

**Fig. 11.3**  |  End-of-file key combinations for various popular operating systems.