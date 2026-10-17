# # CHAPTER 14 File IO

At comment #3, you have exited the `while` loop and for good measure call the `tell()` function once again. The pointer has now advanced to the end of the file, so the position the `tell()` function reports marks the character position of the character that corresponds to the end of `Struthiomimus`. To close the file stream, you call the `close()` function. The single argument you provide to the function consists of the file handle.

In the lines trailing comment #4, you call the `print()` function and print the summary data. The `$LengthOfFile` identifier provides information taken directly from the `tell()` function, while the `$TotalWordLength` identifier represents the results of your calculations. Given the equality of the two values, as Figure 14.9 shows, you can conclude that the combined lengths of the lines (or dinosaur names) account for the total length of the file. Such is the work of the `tell()` function.

# ## Figure 14.9

As the pointer advances, the `tell()` function allows you to know word lengths.

![](bbox=[0.417, 0.361, 0.793, 0.603])

# # The seek() and getc() Functions

You use the `seek()` function to position a pointer in a file. The function takes the following form:

```
```
Seek(file_handle, offset, [beginning | point_within | end])
```
```

This function requires three arguments. The first argument is the file handle. The second argument provides the position in the file at which you want to locate the pointer (the offset). The third parameter proves a little more complicated that the first two. It allows three values. It designates what you want to assign as the initial position of your seek activities. The settings for the third parameter are as follows:

+   * 0 indicates that you want to start at the beginning of the file.

+   * 1 indicates that you want to start at the current position (a point within the file).