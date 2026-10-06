```
@autoreleasepool {
  Foo *myFool = [[Foo alloc]
  init];
  NSMutableData *dataArea;
  NSKeyedArchiver *archiver;
  AddressBook *myBook;
```

// Insert code from Program 19.7 to
create an Address Book
// in myFool containing four address
cards

```
[myFool setStrVal: @"This is the
string\];
[myFool setIntVal: 12345];
[myFool setFloatVal: 98.6];
```

// Set up a data area and connect it to
an NSKeyedArchiver dataArea = [NSMutableData data];

```
archiver = [[NSKeyedArchiver alloc]
initForWritingMutableData:
dataArea];
// Now we can begin to archive objects
[archiver encodeObject: myBook forKey:
@"mybook\];
[archiver encodeObject: myFool forKey:
@"myfool\];
[archiver finishEncoding];
```

// Write the archived data area to a file
if ([dataArea writeToFile: @"myArchive"
atomically: YES] == NO)

```
NSLog (@"Archiving failed!");
```