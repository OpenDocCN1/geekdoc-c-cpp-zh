```
```
            @"directory, %@",
            [error localizedDescription]];
    }
    sharedLocalURL = [documentDirectory
    URLByAppendingPathComponent:FileName];
    });
return sharedLocalURL;
}
```
```

This method calculates the URL for a locally stored data file; however, there’s a little bit of fancy footwork going on here. The dispatch_once() block is guaranteed to only run one time. This will calculate the local URL and assign it to the static sharedLocalURL variable. The next time through, our method will simply use the version previously stored in sharedLocalURL.

To calculate the directory, we call NSFileManager’s URLForDirectory:inDomain:appropriateForURL:create:error: method and request the URL for our application’s Document directory. We then calculate the sharedLocalURL by appending our filename to the end of our directory URL.

There’s no good reason why this request should fail. If it returns an error, we’ve almost certainly made a mistake somewhere in our code. Therefore, we simply throw an exception. This will help us find the mistake during development, making sure we fix it.

```
```
+ (NSURL*)cloudURL {
    static NSURL* sharedCloudURL;
    static dispatch_once_t onceToken;
    dispatch_once(&onceToken, ^{
        NSFileManager* fileManager =
            [NSFileManager defaultManager];
        NSURL* containerURL =
            [fileManager URLForUbiquityContainerIdentifier:nil];
        if (containerURL) {
```
```