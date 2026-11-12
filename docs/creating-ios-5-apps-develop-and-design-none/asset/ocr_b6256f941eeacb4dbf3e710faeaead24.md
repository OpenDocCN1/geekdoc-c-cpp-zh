Let’s start by creating the GraphStats class. This class will process an array of weightEntries and calculate some simple statistics about the collection. These include: starting date, ending date, duration, minimum weight, maximum weight, and weight span. GraphStats will also provide a block-based method for iterating over all the WeightEntries in the collection.

Create a new NSObject subclass in the Views group. Name it GraphStats. Then open GraphStats.h and make the following changes:

```
    #import <Foundation/Foundation.h>

    @class WeightEntry;

    @interface GraphStats : NSObject

    @property (strong, nonatomic, readonly) NSDate* startingDate;
    @property (strong, nonatomic, readonly) NSDate* endingDate;
    @property (assign, nonatomic, readonly) NSTimeInterval duration;
    @property (assign, nonatomic, readonly) CGFloat minWeight;
    @property (assign, nonatomic, readonly) CGFloat maxWeight;
    @property (assign, nonatomic, readonly) CGFloat weightSpan;

    - (id)initWithWeightEntryArray:(NSArray*)weightEntries;
    - (void)processWeightEntryUsingBlock:(void (^)(WeightEntry*)) block;

    @end
```

The GraphStats class acts as a wrapper around an array of WeightEntry objects. We start by adding a forward declaration for the WeightEntry class. Then we add six readonly properties. These give us access to our calculated values, like the starting date of the array or the maximum weight value. Next, we declare our designated initializer. Not surprisingly, it consumes an array of WeightEntry objects.

We will create GraphStats as a non-mutable class. We pass in our WeightEntry array when we first instantiate the object, and the weights cannot change over the object’s lifetime. If you need to add or remove a weight, you must create an entirely new GraphStats object. This greatly simplifies our code. For example, we can bulk-calculate all the property values during our initialization step, and we never need to change them.