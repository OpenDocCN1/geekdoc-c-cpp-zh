```
// verify its contents

NSLog("%%@", [NSString
stringWithContentsOfFile: @"fileB"
    encoding: NSUTF8StringEncoding error:
]);
    return 0;
}
```

Contents of fileA before running [Program 16.8]

```
This is line 1 in the first file.
This is line 2 in the first file.
```

Contents of fileB before running [Program 16.8]

```
This is line 1 in the second file.
This is line 2 in the second file.
```

# Program 16.8. Output

```
Contents of fileB
This is line 1 in the second file.
This is line 2 in the second file.
This is line 1 in the first file.
This is line 2 in the first file.
```

You can see from the output that the contents of the first file were successfully appended to the end of the second file. Incrementally, seekToEndFile returns the current file offset after the seek is performed. We chose to ignore that value; you can use that information to obtain the size of a file in your program if you need it.