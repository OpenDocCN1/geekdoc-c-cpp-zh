![](bbox=[0.16, 0.08, 0.76, 0.44])

Figure 4.2: The Core Data stack

The NSSortDescriptor takes two parameters as part of its -init: a key and a BOOL denoting whether the sort is ascending or descending. We can have as many NSSortDescriptor objects as we want as part of the sort, and therefore they are placed within an NSArray prior to the sort being performed.

Adding an NSSortDescriptor is especially useful on Cocoa Touch because the NSFetchedResultsController will continue to keep its results sorted without any intervention on our part. The NSFetchedResultsController is discussed in more depth in Chapter 10, Core Data and iPhone, on page 184.

# ## 4.4 NSManagedObjectContext

Next to NSManagedObject, NSManagedObjectContext is the one object in the Core Data stack that we access the most. The NSManagedObjectContext is the object we access when we want to save to disk, when we want to read data into memory, and when we want to create new objects. As