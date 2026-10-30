```
#include <stdio.h>
long ftell(FILE *fp);
							Returns: current file position indicator if OK, -1L on error
int fseek(FILE *fp, long offset, int whence);
											Returns: 0 if OK, -1 on error
void rewind(FILE *fp);
```

For a binary file, a file’s position indicator is measured in bytes from the beginning of the file. The value returned by ftell for a binary file is this byte position. To position a binary file using fseek, we must specify a byte offset and indicate how that offset is interpreted. The values for whence are the same as for the lseek function from Section 3.6: SEEK_SET means from the beginning of the file, SEEK_CUR means from the current file position, and SEEK_END means from the end of file. ISO C doesn’t require an implementation to support the SEEK_END specification for a binary file, as some systems require a binary file to be padded at the end with zeros to make the file size a multiple of some magic number. Under the UNIX System, however, SEEK_END is supported for binary files.

For text files, the file’s current position may not be measurable as a simple byte offset. Again, this is mainly under non-UNIX systems that might store text files in a different format. To position a text file, whence has to be SEEK_SET, and only two values for offset are allowed: 0—meaning rewind the file to its beginning—or a value that was returned by ftell for that file. A stream can also be set to the beginning of the file with the rewind function.

The ftello function is the same as ftell, and the fseeko function is the same as fseek, except that the type of the offset is off_t instead of long.

```
#include <stdio.h>
off_t ftello(FILE *fp);
						Returns: current file position indicator if OK, (off_t)-1 on error
int fseeko(FILE *fp, off_t offset, int whence);
										Returns: 0 if OK, -1 on error
```

Recall the discussion of the off_t data type in Section 3.6. Implementations can define the off_t type to be larger than 32 bits.

As we mentioned earlier, the fgetpos and fsetpos functions were introduced by the ISO C standard.

```
#include <stdio.h>
int fgetpos(FILE *restrict fp, fpos_t *restrict pos);
int fsetpos(FILE *fp, const fpos_t *pos);
										Both return: 0 if OK, nonzero on error
```