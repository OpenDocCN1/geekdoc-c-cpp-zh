```
[NSFetchRequest fetchRequestWithEntityName:
    [WeightEntry entityName]];
// Set the batch size.
[fetchRequest setFetchBatchSize:20];
```

Here, we create a fetch request for our weight entry. By default, this fetch request will return all the weight entries in our Core Data store. Unfortunately, this could cause performance issues—especially when our application attempts to load a large number of entries all at once.

To solve this, we set the batch size. The batch size determines the number of objects that the fetch request will return in each batch. In our case, it will return the first 20 entries as objects and will return the rest as faults. If we try to access one of the faulted entries, the fetch request will fill in a new batch of 20 objects, including the fault. This provides a nice compromise between performance and memory usage. We don't need to load unnecessary objects into memory, but we also minimize the number of faults triggered while scrolling through the history.

```
// Set up sort descriptor.
NSSortDescriptor *sortDescriptor =
    [[NSSortDescriptor alloc] initWithKey:@"date" ascending:NO];
NSArray *sortDescriptors =
    [[NSArray alloc] initWithObjects:sortDescriptor, nil];
[fetchRequest setSortDescriptors:sortDescriptors];
```

This section adds a sort descriptor to the fetch request. First, we create our sort descriptor. This will sort our weight entry objects in descending order based on their date property. We then place this descriptor in an array of sort descriptors and assign it to our fetch request.

Our code only uses a single sort descriptor, but we could assign more than one. Their order of precedence is determined by their order in the array. The first descriptor will perform the initial sort. Any objects that are still equal are then sorted by the second descriptor. Objects that are still tied are passed to the third descriptor, and so forth.