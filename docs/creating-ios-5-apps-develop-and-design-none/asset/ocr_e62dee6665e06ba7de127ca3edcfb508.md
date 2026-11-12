```
```objective-c
- (void)explorePath:(NSString*)path {
    // Access singleton file manager.
    NSFileManager* fileManager = [NSFileManager defaultManager];
    BOOL isDirectory;
    // If the file doesn't exist, display an error
    // message and return.
    if (![fileManager fileExistsAtPath:path
                                        isDirectory:&isDirectory]) {
        NSLog(@"%@ does not exist", path);
        return;
    }
    // If it's not a directory, print out some information
    // about it.
    if (!isDirectory) {
        NSString* fileName = [path lastPathComponent];
        NSMutableString* permissions =
            [[NSMutableString alloc] init];
        if ([fileManager isReadableFileAtPath:path]) {
            [permissions appendString:@"readable "];
        }
        if ([fileManager isWritableFileAtPath:path]) {
            [permissions appendString:@"writable "];
        }
        if ([fileManager isExecutableFileAtPath:path]) {
            [permissions appendString:@"executable "];
        }
        if ([fileManager isDeletableFileAtPath:path]) {
            [permissions appendString:@"deletable"];
```
```