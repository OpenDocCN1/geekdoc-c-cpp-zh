```
```objective-c
- (id)initWithNibName:(NSString *)nibName bundle:(NSBundle *)nibBundle{
    if (self = [super initWithNibName:nibName bundle:nibBundle]) {
        self.finishedApps = [[NSMutableArray alloc] init];
        self.runningApps = [NSMutableArray arrayWithCapacity:20];
        for (NSRunningApplication *app in
             [[NSWorkspace sharedWorkspace] runningApplications]) {
            if (![self.finishedApps containsObject:app]) {
                [self.runningApps addObject:app];
            }
        }
    }
    return self;
}
```
```

Click Build & Run. Applications you remove should not appear in your table view even if you quit and relaunch either HelloApplication or the applications you remove.

# 17.5 Saving an Archive to Disk

You’ll normally use plists to persist relatively small amounts of application data (often configuration related). But what if you want to store large amounts of data or if you want to persist an object tree? For the most part, you’ll want to use the techniques I’ll describe in Chapter 22, Core Data, on page 350. There are, however, in-between times when you need to write your data as an archive.

There are essentially two levels to saving an object graph to disk. At the top level, you need to create an archive of all the objects that need to be saved and later retrieved. These actions are handled by methods in instances of the NSKeyedArchiver and NSKeyedUnarchiver classes. You pass in the object at the root of the tree, and each object will be asked to encode or decode itself.

At this object level, each object is responsible for knowing what part of its state needs to be persisted using the encodeWithCoder: method. Loading the data from disk is the inverse operation and uses each object’s initWithCoder: method.

I’m not going to have you build a new application to illustrate this concept. For the most part, you should either be able to use the plist