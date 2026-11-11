# Setting the Entity

The one thing that we must do as part of every NSFetchRequest is define what entity we want returned from the fetch. We do this by passing the appropriate NSEntityDescription to the NSFetchRequest. For example, if we wanted to retrieve recipe entities, we would construct the NSFetchRequest as follows:

```
NSManagedObjectContext *moc = [self managedObjectContext];
NSFetchRequest *request = [[NSFetchRequest alloc] init];
[request setEntity:[NSEntityDescription entityForName:@"Recipe"
                  inManagedObjectContext:moc]];
```

In this example code, we are constructing a new NSFetchRequest and calling -setEntity: on it. We are using the class method -entityForName:inManagedObjectContext: on the NSEntityDescription class to get the appropriate instance of NSEntityDescription back for the setter.

# Executing a Fetch Request

Once we have constructed our NSFetchRequest, we need to execute it against the NSManagedObjectContext to get back the results. Like a result set when accessing a database, an executed NSFetchRequest will return an NSArray of entities that match our search criteria. Since it is possible that a search will fail, the execution of an NSFetchRequest accepts a pointer to an NSError to describe any problems that resulted from the execution. For example, if we wanted to execute the fetch from the previous example, we could use the following code:

```
NSManagedObjectContext *moc = [self managedObjectContext];
NSFetchRequest *request = [[NSFetchRequest alloc] init];
[request setEntity:[NSEntityDescription entityForName:@"Recipe"
                  inManagedObjectContext:moc]];

NSError *error = nil;
NSArray *results = [moc executeFetchRequest:request error:&error];
if (error) {
    [NSApp presentError:error];
    return;
}
```

In this example, we are calling -executeFetchRequest:error: on the NSManagedObjectContext, passing in the NSFetchRequest and a pointer to a local NSError. If the fetch failed with an error, then the pointer will be directed to an instance of NSError that describes the problem, and the NSArray will be assigned to nil. In that situation, we ask the NSApplication to present the error for us and return. If there is no error, then we can