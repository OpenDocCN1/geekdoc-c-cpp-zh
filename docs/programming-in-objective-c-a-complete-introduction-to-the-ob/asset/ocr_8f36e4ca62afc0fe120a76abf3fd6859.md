# Chapter 16 Working with Files

method to the buffer and test for equality with zero to see whether any data remains to be read from the file.

If you open a file for updating, the file offset is set to the beginning of the file.You can change that offset by seeking within a file and then perform your read or write operations on the file. So, to seek to the 10th byte in a file where handle is databaseHandle, you can write the following message expression:

```
[databaseHandle seekToFileOffset: 10];
```

Relative positioning is done by obtaining the current file offset and adding to subtracting from it. So, to skip over the next 128 bytes in the file, then write the following:

```
[databaseHandle offsetFile + 128];
```

And to move back to the end of five integers in the file, write with this:

```
[databaseHandle offsetFile] - 5 * sizeof (int);
```

Program 16.8 appends the contents of one file to another. It does this by opening the second file for writing, seeking to the end of the file, and then writing the contents of the first file to the second.

# Program 16.8

// Append the file "fileA" to the end of "fileB"

```
#import <Foundation/Foundation.h>
int main (int argc, char *argv[]) {
    NSAutoreleasePool *pool = [NSAutoreleasePool alloc];
    NSFileHandle *inFile, *outFile;
    NSData *buffer;

    // Open the fileA for reading
    inFile = [NSFileHandle fileHandleForReadingPath:@"fileA"];

    if (inFile == nil) {
        NSLog("@Open of fileA for reading failed");
        return 1;
    }

    // Open the fileB for updating
    outFile = [NSFileHandle fileHandleForWritingPath:@"fileB"];
    if (outFile == nil) {
        NSLog("@Open of fileB for writing failed");
        return 2;
    }

    // Seek to the end of outFile
```