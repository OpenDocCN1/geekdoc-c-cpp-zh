with a `/` that represents the top of the file system, whereas relative paths start at the working directory of the program. Relative paths do not start with a `/.` In Objective-C programming, you'll find that we nearly always use absolute paths because we typically don't know what the working directory of the program is. (To find the the `/tmp` directory in Finder, use the **Go** > **Go to Folder** menu item.)

# # NSError

As you can imagine, all sorts of things can go wrong when you try to write a string to a file. For example, the user may not have write-access to the directory where the file would go. Or the directory may not exist at all. Or the filesystem may be full. For situations like these, when an operation may be impossible to complete, the method needs a way to return a description of what went wrong in addition to the boolean value for success or failure.

Recall from Chapter 9 that when you need a function to return something in addition to its return value, you can pass **by-reference**. You pass the function (or method) a reference to a variable where it can directly store or manipulate a value. The reference is the memory address for that variable.

For error handling, many methods take an **NSError** pointer by reference. Add error handling to the example above:

```
```objective-c
#import <Foundation/Foundation.h>

int main (int argc, const char * argv[])    {
    @autoreleasepool {

        NSMutableString *str = [[NSMutableString alloc] init];
        for (int i = 0; i < 10; i++) {
            [str appendString:@"Aaron is cool!\n"];
        }

        // Declare a pointer to an NSError object, but don't instantiate it.
        // The NSError instance will only be created if there is, in fact, an error.
        NSError *error = nil;

        // Pass the NSError pointer by reference to the NSStr ing method
        BOOL success = [str  writeToFile:@"/tmp/cool.txt"
                              atomically:YES
                                 encoding:NSUTF8StringEncoding
                                    error:&error];

        // Test the returned BOOL, and query the NSError if the write failed
        if (success) {
            NSLog(@"done writing /tmp/cool.txt");
        } else {
            NSLog(@"writing /tmp/cool.txt failed: %@", [error localizedDescription]);
        }

    }
    return 0;
}```
```

Build and run it. Now change the code to pass the write method a file path that doesn't exist, like `@/too/darned/bad.txt`. You should get a friendly error message.

Notice that you declare a pointer to an instance of **NSError** in this code, but you don't create, or *instantiate*, an **NSError** object to assign to that pointer.