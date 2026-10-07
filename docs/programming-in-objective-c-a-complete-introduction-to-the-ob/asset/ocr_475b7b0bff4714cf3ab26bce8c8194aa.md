# Table 15.9 Common NSSetMethods

| Method | Description |
| --- | --- |
| +(id) setWithObjects:obj1,obj2,..., nil | Creates a new set from the list of objects |
| -(id) anyObject | Returns any object from the set |
| -(id) initWithObjects:obj1,obj2,..., nil | Initializes a newly allocated set with a list of objects |
| -(NSInteger) count | Returns the number of members in the set |
| -(BOOL) containsObject:obj | Determines whether the set contains obj |
| -(BOOL) member:obj | Determines whether the set contains obj (using the isEqual:method) |
| -(NSEnumerator) objectEnumerator | Returns an NSEnumerator for all the objects in the set |
| -(BOOL) isSubsetOf:nset | Determines whether every member of the receiver is present in nset |
| -(BOOL) intersectsSet:nset | Determines whether at least one member of the receiver appears in nset |
| -(BOOL) isEqualTo:nset | Determines whether the two sets are equal |

# Table 15.10 Common NSUTableSet Methods

| Method | Description |
| --- | --- |
| +(id) setWithCapacity:size | Creates a new set with an initial capacity size members |
| -(id) initWithCapacity:size | Sets the initial capacity of a newly allocated set to size members |
| -(void) addObject:obj | Adds obj to the set |
| -(void) removeObject:obj | Removes obj from the set |
| -(void) removeObjects | Removes all members of the receiver |
| -(void) unionSet:nset | Adds each member of nset to the receiver |
| -(void) minusSet:nset | Removes all members of nset from the receiver |
| -(void) intersectSet:nset | Removes all members from the receiver that are not also in nset |

# NSIndexSet

Let’s take a look at another type of set: the NSSet.This class is used to store ordered indexes into some other data structure, typically an array. You can use this class, for example, to efficiently generate a list of index numbers from an array of objects, where each object satisfies some criteria that you specify.You’ll want to note that there is no mutable version of the NSIndexSet class.