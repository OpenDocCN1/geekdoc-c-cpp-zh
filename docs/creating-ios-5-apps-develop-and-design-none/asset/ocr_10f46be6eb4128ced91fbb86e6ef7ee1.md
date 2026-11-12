We also need to replace the init method with a new designated initializer:

```
```objective-c
#pragma mark - initialization
- (id)initWithFileURL:(NSURL *)url
{
    self = [super initWithFileURL:url];
    if (self) {
        _weightHistory = [[NSMutableArray alloc] init];
    }
    return self;
}
```
```

We're still overriding our superclass's designated initializer. The name has changed and it takes an argument—but since we just pass the argument on to the superclass, it doesn't affect our implementation. Also, we've deleted the code that initialized our _defaultUnits property. Other than that, everything's the same.

Now we just need to implement a few required features. Specifically, we need to override the UIDocument methods to save and load our data. We need to change our weightHistory accessors, letting us alert the superclass whenever a change is made. Finally, we need to deal with version conflicts whenever they arise.

# # SAVING AND LOADING THE DOCUMENT

The easiest way to save and load our UIDocument is to simply convert our model into an NSData instance. This isn't absolutely required. UIDocument has a number of methods we could override to more fully customize our saving and loading code—but we should try to use simple NSData or NSFileWrapper objects whenever possible.

Currently, our WeightHistory class has a single instance variable: our weightHistory mutable array. So how do we convert an array into an NSData object? A quick glance at the class references for NSMutableArray and NSData doesn't reveal any obvious methods for converting one into the other; however, NSMutableArray does adopt the NSCoding protocol. This means we can load and save our array using a keyed archiver—and keyed archivers can read and write to NSData objects (or directly to files, for that matter).