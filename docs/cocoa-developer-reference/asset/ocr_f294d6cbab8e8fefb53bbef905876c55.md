```
```objective-c
NSEntityDescription *albumEntity
= [NSEntityDescription entityForName:@"Album"
inManagedObjectContext:managedObjectContext];
NSFetchRequest *theRequest = [[NSFetchRequest alloc] init];
[theRequest setEntity:albumEntity];
NSPredicate *thePredicate =
[NSPredicate predicateWithFormat:@"Artist == %@", aString];

[theRequest setPredicate:thePredicate];
```
```

But this doesn’t work. The Artist key is a relationship, and the regex search code can’t follow to-many relationship links.

A workaround is to create a list of album keys and values in a separate array, and search the array for the Artist key. Instead of specifying a predicate, you request a list of all albums, and then search the returned array.

Counterintuitively, this solves the problem, with only minor extra complications. The code for a full solution follows. The search is packed into a refreshList: method that can be called when the application should refresh the list of filtered albums.

```
```objective-c
- (void) refreshList: (id) sender {
    NSEntityDescription *albumEntity =
    [NSEntityDescription entityForName:@"Album"
    inManagedObjectContext:managedObjectContext];
    NSFetchRequest *theRequest = [[NSFetchRequest alloc] init];
    [theRequest setEntity:albumEntity];
    searchReturnArray = [NSMutableArray arrayWithCapacity:50];
    tempArray =
    [managedObjectContext executeFetchRequest:theRequest
    error:nil];
    [tempArray enumerateObjectsUsingBlock:^(id obj,
    NSUInteger idx, BOOL *stop) {
        NSString *albumName = [obj valueForKey:@"Name"];
        NSString *artistName =
        [[obj valueForKey:@"Artist"] valueForKey:@"Name"];
        if ([artistName isEqual:selectedName.stringValue])
            [self.searchReturnArray insertObject:
            [NSDictionary dictionaryWithObject: albumName
            forKey:@"FileName"] atIndex: 0];
    }];
    self.searchReturnArray = searchReturnArray;
    NSLog(@" %@", searchReturnArray);
}
```
```