that the entire object hierarchy be loaded into memory, and that is something we generally cannot afford on a Cocoa Touch device. Therefore, unless there is a very solid design reason to use another store format, SQLite should be used.

# 10.2  Memory Management

One of the most important differences we need to keep in mind while working with Core Data on the iPhone is the management of memory. Depending on which Cocoa Touch device is targeted, we could have as little as 20MB of memory to work with. This is drastically different from the modern desktop that measures memory in gigabytes! Therefore, Core Data, to be a good citizen on this much smaller device, must handle memory differently.

The best way to handle memory management is to let someone else do it. Fortunately, Apple has stepped up to the plate and done most of the heavy lifting for us. As we will discuss in depth in Section 10.3, _Using the NSFetchedResultsController_, on page 194, the new class, NSFetchedResultsController, does a lot of the memory management work for us as long as we play by its rules. These rules break down into two separate sections.

# Grab Only What You Need

Because we have such a small amount of memory to work with, it is very important that we keep only the entities that we absolutely need for that view. What this means is that if we are working in a view (or a _page_, as some refer to a single screen of information), then we should be retaining only the entities that are needed for that view. In the case of a view that is a table, then that becomes a bit trickier. But fortunately, the NSFetchedResultsController helps us solve that problem as well.

# Handling Data Changes

The second rule of working with Core Data on the iPhone has to do with the notification of changes to the data entities. On the desktop our view elements are bound directly to the data entities, and when an entity changes, all the view elements associated with that entity are automatically updated through KVO, as discussed in Chapter 3, _Core Data and Bindings_, on page 34. However, on a CocoaTouch device, those bindings do not currently exist, and updates to visual elements need to be coded.