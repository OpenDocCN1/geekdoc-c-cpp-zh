append, the current file position is set to the first null byte in the buffer. If the buffer contains no null bytes, then the current position is set to one byte past the end of the buffer. When a stream is not opened for append, the current position is set to the beginning of the buffer. Because the append mode determines the end of the data by the first null byte, memory streams aren't well suited for storing binary data (which might contain null bytes before the end of the data).

Second, if the buf argument is a null pointer, it makes no sense to open the stream for only reading or only writing. Because the buffer is allocated by fmemopen in this case, there is no way to find the buffer's address, so to open the stream only for writing means we could never read what we've written. Similarly, to open the stream only for reading means we can only read the contents of a buffer into which we can never write.

Third, a null byte is written at the current position in the stream whenever we increase the amount of data in the stream's buffer and call fclose, fflush, fseek, fseeko, or fsetpos.

# Example

It's instructive to look at how writes to a memory stream operate on a buffer we provide. Figure 5.15 shows a sample program that seeds the buffer with a known pattern to see how writes to the stream behave.

```
#include "apue.h"

#define BSZ 48

int
main()
{
    FILE *fp;
    char buf[BSZ];

    memset(buf, 'a', BSZ-2);
    buf[BSZ-2] = '\0';
    buf[BSZ-1] = 'X';
    if ((fp = fmemopen(buf, BSZ, "w+")) == NULL)
        err_sys("fmemopen failed");
    printf("initial buffer contents: %s\n", buf);
    fprintf(fp, "hello, world");
    printf("before flush: %s\n", buf);
    fflush(fp);
    printf("after fflush: %s\n", buf);
    printf("len of string in buf = %ld\n", (long)strlen(buf));

    memset(buf, 'b', BSZ-2);
    buf[BSZ-2] = '\0';
    buf[BSZ-1] = 'X';
    fprintf(fp, "hello, world");
    fseek(fp, 0, SEEK_SET);
    printf("after fseek: %s\n", buf);
    printf("len of string in buf = %ld\n", (long)strlen(buf));
```