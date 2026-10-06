method, meaning you won't have to make the change to the AddressCard class.

More than 50 methods are available for working with array objects. Tables 15.4 and 15.5 list some commonly used methods for working with immutable and mutable arrays, respectively. Because NSMutableArray is a subclass of NSArray, the former inherits the methods of the latter.

# ## Table 15.4. Common NSArray Methods

| Method | Description |
| --- | --- |
| +(id) arrayWithObjects: obj1, obj2, ... nil | Creates a new array with obj1, obj2, ...as its elements |
| - (BOOL) containsObject: obj | Determines whether the array contains obj (uses isEqual:method) |
| - (NSInteger) count | Indicates the number of elements in the array |
| - (NSInteger) indexOfToObject: obj | Specifies the index number of the first element that contains obj (uses isEqual:method) |
| - (NSInteger) indexOfOfPassingTest:(BOOL)(id obj, NSInteger idx, BOOL *stop) block | Passes each obj (with index idx) into the block, which should return YES if obj passes the test, NO if it doesn't. Set variable pointed to by stop to YES to ending processing. |
| (id) lastObject | Returns the last object in the array |
| (id) objectAtIndex:i | Indicates the object stored in element i |
| - (void) makeObjectsPerformSelector:(SEL) selector | Sends the message indicated by selector to every element of the array |
| - (void) enumerateObjectsUsingBlock:(void)(id obj, NSInteger idx, BOOL *stop) block | Execute block for each element in the array, passing in the array object obj, and its index idx. Processing continues until all elements have been enumerated or the variable pointed to by stop is set to YES |
| -(NSArray *) sortedArrayUsingSelector:(SEL) selector | Sorts the array according to the comparison method specified by selector |
| -(NSArray *) sortedArrayUsingComparator:(NSComparator) block | Sorts the array according to the comparison performed by the block |
| -(BOOL) writeToFile:path atomically:(BOOL) flag | Writes the array to the specified file, creating a temporary file if flag is YES |