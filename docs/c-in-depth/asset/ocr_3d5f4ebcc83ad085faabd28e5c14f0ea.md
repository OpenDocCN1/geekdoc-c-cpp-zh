-ftell( )
-rewind( )

Before studying these functions it is necessary to understand the concept of file position pointer. File position pointer points to a particular byte in the file and all read and write operations on the file take place at this byte. This pointer automatically moves forward when a read or write operation takes place. To access the data randomly, we'll have to take control of this position pointer.

# 13.1 fseek ( )

This function is used for setting the file position pointer at the specified byte.

```
Declaration: int fseek( FILE *fp, long displacement, int origin );
```

Here fp is a file pointer, displacement is a long integer which can be positive or negative and it denotes the number of bytes which are skipped backward ( if negative ) or forward ( if positive ) from the position specified in the third argument. This argument is declared as long integer so that it is possible to move in large files.

The third argument named origin is the position relative to which the displacement takes place. It can take one of these three values.

| Constant | Value | Position |
|---|---|---|
| SEEK_SET | 0 | Beginning of file |
| SEEK_CURRENT | 1 | Current position |
| SEEK_END | 2 | End of file |

These three constants are defined in stdio.h so we can either use these names or their values.

Some examples of usage of fseek( ) function are-

+   1. `fseek ( p, 10L , 0 );`
+      Origin is 0, which means that displacement will be relative to beginning of file so position pointer is skipped 10 bytes forward from the beginning of the file. Since the second argument is a long integer, so L is attached with it.
+   2. `fseek ( p, 5L , 1 );`
+      Position pointer is skipped 5 bytes forward from the current position.
+   3. `fseek ( p, 8L , SEEK_SET );`
+      Position pointer is skipped 8 bytes forward from the beginning of file.
+   4. `fseek ( p , -5L , 1 );`
+      Position pointer is skipped 5 bytes backward from the current position.
+   5. `fseek ( p, 0L , 2 );`
+      Origin is 2 which represents end of file and displacement is 0 which means that 0 bytes are skipped from end of file. So after this statement position pointer will point to the end of file.
+   6. `fseek( p, -6L, SEEK_END );`
+      Position pointer is skipped 6 bytes backward from the end of file.
+   7. `fseek ( p, 0L , 0 );`
+      This means 0 bytes are skipped from the beginning of file. After this statement position pointer points to the beginning of file.