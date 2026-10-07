output. On an iOS device, your program runs in what is known as a sandbox, where it has-restricted access to files. If you run this program on such a device, you'll see that the current directory is listed as /. That's the root folder for the application running in its sandbox and not the root of the entire iOS device's file system.

After renaming the directory, the program makes that new directory the current using the `changeCurrentDirectoryPath:` method. The current directory path is displayed to verify that the change was successful.

# Enumerating the Contents of a Directory

Sometimes you need to get a list of the contents of a directory. This enumeration process can be accomplished using either the `enumeratorAtPath:error:` method. In the former case, each file in the specified directory is enumerated one at a time, and by default, if one of those is a directory, its contents are also recursively enumerated. During this process you can dynamically prevent recursion by sending a `skipDescendants` message to an enumeration object so that its contents will not be enumerated.

In the case of `contentsAtPathPath:error:`, the contents of the specified directory are enumerated, and the file list is returned in an array by the method. If any of the files contained in a directory is itself a directory, its contents are not recursively enumerated by this method.

Program 16.4 shows how you can use this method in your programs.

Program 16.4

```
// Enumerate the contents of a directory
#import <Foundation/Foundation.h>
int main (int argc, char *argv[])\{
    NSAutoreleasePool *pool = [[NSAutoreleasePool alloc] init];
    NSString *path;
    NSFileManager *fm;
    NSEnumerator *dirEnum;
    NSArray *dirArray;

    // Need to create an instance of the file manager
    fm = [NSFileManager defaultManager];
\    // Get current working directory path
    path = [fm currentDirectoryPath];


}
```