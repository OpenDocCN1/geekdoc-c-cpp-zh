where offset is the number of bytes to seek from whence in the file pointed to by stream. Positive offsets seek forward, and negative offsets seek backward. The argument whence can be SEEK_SET, SEEK_CUR or SEEK_END (all defined in <stdio.h>), which indicate the location from which the seek begins:

+   - SEEK_SET indicates that the seek is measured from the *beginning* of the file.
+   - SEEK_CUR indicates that the seek is measured from the *current location* in the file.
+   - SEEK_END indicates that the seek is measured from the *end* of the file.

You should use only positive offsets with SEEK_SET and only negative ones with SEEK_END.

# ## 11.7.2 Error Checking

For simplicity, the programs in this chapter do *not* perform error checking. Industrial-strength programs should determine whether functions such as fscanf (Fig. 11.5, lines 34–35), fseek (lines 38–39) and fwrite (line 42) operate correctly by checking their return values. Function fscanf returns the number of data items successfully read or the value EOF if a problem occurs while reading data. Function fseek returns a nonzero value if the seek operation cannot be performed (e.g., attempting to seek to a position before the start of the file). Function fwrite returns the number of items it successfully output. If this number is less than the *third argument* in the function call, then a write error occurred.

# ### Self Check

+   1. (Fill-In) Function ______ sets the file position pointer to a specific byte position in the file.
+      Answer: fseek.
+   2. (Fill-In) The symbolic constant ______ indicates that the file position pointer should be positioned relative to the beginning of the file.
+      Answer: SEEK_SET.

# ## 11.8 Reading Data from a Random-Access File

Function fread reads a specified number of bytes from a file into memory. For example,

```
fread(&client, sizeof(struct clientData), 1, cfPtr);
```

reads the number of bytes determined by sizeof(struct clientData) from the file referenced by cfPtr, stores the data in client and returns the number of bytes read. It reads bytes from the location specified by the file position pointer.

Function fread can read several fixed-size array elements by providing a pointer to the array in which the elements will be stored and by indicating the number of elements to be read. The preceding statement reads one element. To read more than one, specify the number of elements as fread’s third argument. Function fread