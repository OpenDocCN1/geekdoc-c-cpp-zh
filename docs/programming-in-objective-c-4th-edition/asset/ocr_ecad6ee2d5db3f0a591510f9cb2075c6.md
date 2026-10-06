You can create testfile with XCode by selecting File

The moveAtPath:toPath: method can be used to move a file from one directory to another. (It also be used to move directories.) If the two paths reference files in the same directory (as in our example), the effect is to simply rename the file. So, in Program 16.1, you use this method to rename the file newfile2.

As noted in Table 16.1, when performing copying, renaming, or moving operations, the destination file cannot already exist. If it does, the operation will fail.

The size of newfile2 is determined by using the attributesOfAtPath:error: method. To make sure a non-nil dictionary is returned and then use the NSDictionary method objectForKey: to get the file's size from the dictionary using the key NSFileSize. The integer value from the dictionary is then displayed.

The program uses removeAtPath:error: method to remove your original file testfile.

Finally, NSString's stringWithContentsOf:encoding: method is used to read the contents of the file newfile2 into a string object, which is then passed as an argument to NSLog to be displayed. The