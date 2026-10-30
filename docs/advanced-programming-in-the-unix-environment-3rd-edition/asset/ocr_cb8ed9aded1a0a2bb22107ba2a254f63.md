text file and a binary file. Since the UNIX kernel doesn’t differentiate between these types of files, specifying the character b as part of the type has no effect.

With fdopen, the meanings of the type argument differ slightly. The descriptor has already been opened, so opening for writing does not truncate the file. (If the descriptor was created by the open function, for example, and the file already existed, the O_TRUNC flag would control whether the file was truncated. The fdopen function cannot simply truncate any file it opens for writing.) Also, the standard I/O append mode cannot create the file (since the file has to exist if a descriptor refers to it).

When a file is opened with a type of append, each write will take place at the then current end of file. If multiple processes open the same file with the standard I/O append mode, the data from each process will be correctly written to the file.

Versions of fopen from Berkeley before 4.4BSD and the simple version shown on page 177 of Kernighan and Ritchie [1988] do not handle the append mode correctly. These versions do an lseek to the end of file when the stream is opened. To correctly support the append mode when multiple processes are involved, the file must be opened with the O_APPEND flag, which we discussed in Section 3.3. Doing an lseek before each write won’t work either, as we discussed in Section 3.11.

When a file is opened for reading and writing (the plus sign in the type), two restrictions apply.

+   - Output cannot be directly followed by input without an intervening fflush, fseek, fsetpos, or rewind.
+   - Input cannot be directly followed by output without an intervening fseek, fsetpos, or rewind, or an input operation that encounters an end of file.

We can summarize the six ways to open a stream from Figure 5.2 in Figure 5.3.

| Restriction | r | w | a | r+ | w+ | a+ |
|---|---|---|---|---|---|---|
| file must already exist | • |  |  | • |  |  |
| previous contents of file discarded |  | • |  |  | • |  |
| stream can be read | • |  |  | • | • | • |
| stream can be written |  | • | • | • | • | • |
| stream can be written only at end |  |  | • |  |  | • |

Figure 5.3 Six ways to open a standard I/O stream

Note that if a new file is created by specifying a type of either w or a, we are not able to specify the file’s access permission bits, as we were able to do with the open function and the creat function in Chapter 3. POSIX.1 requires implementations to create the file with the following permissions bit set:

S_IRUSR | S_IWUSR | S_IRGRP | S_IWGRP | S_IROTH | S_IWOTH

Recall from Section 4.8, however, that we can restrict these permissions by adjusting our umask value.

By default, the stream that is opened is fully buffered, unless it refers to a terminal device, in which case it is line buffered. Once the stream is opened, but before we do