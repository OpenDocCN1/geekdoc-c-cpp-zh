Click Build & Run. Remove an application. Quit that application, and restart it; this time it’s not added to the table view. Cool.

We haven’t made a lot of changes, but now we have everything working while HelloApplication is running. Next we will add persistence so that we don’t have to remove the same applications the next time we run HelloApplication.

# 17.2  Where to Put Application Support

Let’s save the names of the removed applications to disk every time one is added and retrieve the contents of the file when we instantiate BanishedApps. In this section, we’ll work with a property list that we create from the NSMutableArray. This technique is great when you are working with a single collection that contains a small amount of data consisting of strings and numbers.

You store your application support files in a folder named for your application or company inside ~/Library/Application Support. The ~ is shorthand for your home directory. We’ll use the function NSSearchPathForDirectoriesInDomains() to get the path to your application support directory like this:

```
NSSearchPathForDirectoriesInDomains(NSApplicationSupportDirectory,
                                NSUserDomainMask, YES)
```

The first parameter is a constant indicating we want the application support directory. The second parameter is filled by a constant that indicates we want to use the user’s Library directory as opposed to the system’s. The third parameter is a boolean we’ve set to YES so that ~ is expanded to the full path to the user directory. This call will result in an array containing the path we want as its only member. We’ll pull this value out of the array as a string and append the string /HelloApplication to get our full path to where we’ll be storing our application data.

We’ll do our work in BanishedApps.m. It’s pretty ugly-looking code, but it is essentially boilerplate that you’ll use to locate your application support files.

Download Persistence/HelloApplication38/BanishedApps.m

```
- (void) setSupportFile {
    NSFileManager *fileManager = [NSFileManager defaultManager];
    NSString *appSupport =
        [NSSearchPathForDirectoriesInDomains(
            NSApplicationSupportDirectory,
            NSUserDomainMask, YES)
        objectAtIndex:0];
```