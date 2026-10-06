
```objc
NSLog(@"Couldn't remove file todolist");
return 1;
```

The attributes dictionary enables you to specify, among other things, the permissions for a file you are creating or to obtain or change information for an existing file. For file creation, if you specify nil for this parameter, the default permissions are set for the file. The attributesOfItemAtPath:traverseLink: method returns a dictionary containing the specified file's attributes. The traverseLink: parameter is YES or NO for symbolic links. If the file is a symbolic link and YES is specified, the attributes of the linked-to file are returned; if NO is specified, the attributes of the link itself are returned.

For preexisting files, the attributes dictionary includes information such as the file's owner, its size, its creation date, and so on. Each attribute in the dictionary can be extracted on its key, all of which are defined in <Foundation/FileManager.h>. For example, NSFileSize is the key for a file's size.

Program 16.1 shows some basic operations with files. This example assumes you have a file called testfile in your current directory with the following three lines of text:

```
This is a test file with some data in it.
Here's another line of data.
And a third.
```

# Program 16.1

```objc
// Basic File operations
// Assumes the existence of a file called "testfile"
// in the current directory
#import <Foundation/Foundation.h>

int main (int argc, const char * argv[]) {
    @autoreleasepool {
        NSString *fName = @"testfile";
        NSFileManager *fm = [NSFileManager defaultManager];
        NSDictionary *attr;

        // Need to create an instance of the file manager
        fm = [NSFileManager defaultManager];

        // Let's make sure our test file exists
        if ([fm fileExistsAtPath:fName] == NO) {
            NSLog(@"File doesn't exist!");
            return 1;
        }

        //now lets make a copy
        if ([fm copyItemAtPath:fName toPath:@"newfile" error:NULL] == NO) {
            NSLog(@"File Copy failed!");
            return 2;
        }

        // Now let's test to see if the two files are equal
        if ([fm contentsEqualToPath:fName andPath:@"newfile"] == NO) {
            NSLog("Files are Not Equal!");
            return 3;
        }

        // Now lets rename the copy
        if ([fm moveItemAtPath: @"newfile" toPath: @"newfile2" error: NULL] == NO) {
            NSLog("File rename Failed!");
            return 4;
        }

        // get the size of the newfile
        if ((attr = [fm attributesOfItemAtPath:@"newfile2" error: NULL]) == nil) {
            NSLog("Couldn't get file attributes!");
            return 5;
        }

        NSLog("File size is %llu bytes",
            [attr objectForKey: NSFileSize] unsignedLongLongValue());

        // And finally, let's delete the original file
        if ([fm removeItemAtPath: fName error:NULL] == NO) {
            NSLog("file removal failed!");
            return 6;
        }

        NSLog("@All operations were successful");

        // Display the contents of the newly-created file
        NSLog(@"%%@", [NSString stringWithContentsFile:@"newfile2" encoding:NSUTF8StringEncoding error:NULL]);
    }
    return 0;
}
```

# Program 16.1. Output

File size is 84 bytes
All operations were successful!

This is a test file with some data in it.
Here's another line of data.
And a third.

The program first tests whether file exists. If it does, it makes a copy of it and then tests the two files for equality. Experienced UNIX users should note that you cannot move or copy a file into a directory by specifying the destination directory for the copyItemAtPath:pathTo:error: and moveItemAtPath:pathTo:error: methods; the filename within that directory must be explicitly specified.

# Note

You can create testfile with Xcode by selecting File.

The moveAtPath:toPath: method can be used to move a file from one directory to another. (It also be used to move directories.) If the two paths reference files in the same directory (as in our example), the effect is to simply rename the file. So, in Program 16.1, you use this method to rename the file newfile2.

As noted in Table 16.1, when performing copying, renaming, or moving operations, the destination file cannot already exist. If it does, the operation will fail.

The size of newfile2 is determined by using the attributesOfAtPath:error: method. To make sure a non-nil dictionary is returned and then use the NSDictionary method objectForKey: to get the file's size from the dictionary using the key NSFileSize. The integer value from the dictionary is then displayed.

The program uses removeAtPath:error: method to remove your original file testfile.

Finally, NSString's stringWithContentsOf:encoding: method is used to read the contents of the file newfile2 into a string object, which is then passed as an argument to NSLog to be displayed. The encoding argument specifies how the character data in the file is represented. The choices to use this argument are defined in the header file NSString. NSUTF8StringEncoding can be used to specify a file containing normal UTF-8 ASCII characters.

Each of the file operations is tested for success in Program 16.1. If any fails, an error is logged using NSLog, and the program exits by returning a nonzero exit status. Each nonzero value, by convention indicates program failure, is unique based on the type of error. If you write command-line tools, this is a useful technique because another program can test the return value, such as from within a shell script.

# Working with the NSData Class

When working with files, you frequently need to read data into a temporary storage area, often called a buffer. When collecting for subsequent output to a file, a storage area is often used. Foundation's NSData class provides an easy way to set up a buffer, read the contents of the file into it, or write the contents of a buffer out to a file. And just in case you're wondering, for a 32-bit application, an NSData buffer can store up to 2GB. For a 64-bit application, it can hold up to 8EB (exabytes) or 8 billion gigabytes of data!

As you would expect, you can define either mutable (NSData) or mutable (NSMutableData) storage areas. We introduce methods from this class in this chapter and in succeeding chapters as well.

Program 16.2 shows how easily you can read the contents of a file into a buffer in memory.

The program reads the contents of your file newfile2 and writes to a new file called newfile3. In a sense, it implements a file copy operation, although not in as straightforward fashion as the copyItemAtPath:toPath:error: method.

# Program 16.2

```objc
// Make a copy of a file
#import <Foundation/Foundation.h>

int main (int argc, char * argv[]) {
    @autoreleasepool {
        NSFileManager *fm;
        NSData *fileData;

        fm = [NSFileManager defaultManager];

        // Read the file newfile2
        fileData = [fm contentsAtPath:@"newfile2"];

        if (fileData == nil) {
            NSLog(@"File read failed!");
            return 1;
        }

        // Write the data to newfile3
        if ([fm createFileAtPath:@"newfile3" contents:fileData attributes:nil] == NO) {
            NSLog(@"Couldn't create the copy!");
            return 2;
        }

        NSLog(@"File copy was successful!");
    }
    return 0;
}
```

# Program 16.2. Output

File copy was successful!

The contentsAtPath: method simply takes a pathname and reads the contents of the specified file into a storage area that it creates, returning the storage area object as the result or nil if the read fails (for example, if the file does not exist or can't be read by you).

The createFileAtPath:contents:attributes: method creates a file with the specified attributes (or uses the default if nil is supplied for the attributes argument). The contents of the specified NSData object are then written to the file. In our example, this data area contains the contents of the previously read file.

# Working with Directories

Table 16.2 summarizes some of the methods provided by NSFileManager for working with directories. Many of these methods are the same as those for ordinary files, as listed in Table 16.1.

# Table 16.2. Common NSFileManager Directory Methods
