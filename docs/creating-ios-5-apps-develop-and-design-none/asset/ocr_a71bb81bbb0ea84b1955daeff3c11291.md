# FETCH REQUESTS

Fetch requests are expensive. They start by accessing the data from the persistent store. Then they merge this data with the existing data in the managed object context. Most of the time, we want to reduce the total number of fetches. In general, this means combining groups of smaller fetches into a single larger fetch.

However, there are times when we want to quickly return a small subset of the data and then fill in the rest while the system is idle. We might do this, for example, when filling in a table view.

We can restrict the number of objects loaded into memory by setting either `setFetchLimit:` or `setFetchBatchSize:`. In both cases, the full fetch is calculated, and all the other objects are returned as faults. When calling `setFetchLimit:`, we can manually load in the remaining objects by calling `setFetchOffset:` and then setting the fetch limit to 0. A second fetch will then grab the remaining objects.

Setting the batch size, on the other hand, returns a proxy array that automatically faults new batches when needed.

# FAULTING

When a fault fires, it acts like a fetch request, except only a single object is returned. This becomes very expensive if we accidentally iterate over an array of faults, firing each one individually. Instead, we need to batch fault or pre-fetch our data to reduce the total number of trips to the persistent store (see "Persistent Stores" for more information).

Note that we can safely call the following methods on a fault without causing it to fire: `isEqual:`, `hash`, `superclass`, `class`, `self`, `zone`, `isProxy`, `isKindOfClass:`, `isMemberOfClass:`, `conformsToProtocol:`, `respondsToSelector:`, `description`, `managedObjectContext`, `entity`, `objectID`, `isInserted`, `isUpdated`, `isDeleted`, and `isFault`.

Among other things, this means we can freely store faults into collections. However, we must treat these collections carefully. It is easy to accidentally trigger faults when calling the collection's methods. Anything that calls `valueForKey:` on the collection's objects will trigger faults—most likely triggering all the faults in the entire array.