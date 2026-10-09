# Chapter 21 Collection Classes

```
[employees removeObjectAtIndex:5];

NSLog(@"allAssets: %@", allAssets);

NSPredicate *predicate = [NSPredicate predicateWithFormat:
                         @"holder.valueOfAssets > 70"];
NSArray *toBeReclaimed = [allAssets filteredArrayUsingPredicate:predicate];
NSLog(@"toBeReclaimed: %@", toBeReclaimed);
toBeReclaimed = nil;

NSLog(@"Giving up ownership of arrays");

allAssets = nil;
employees = nil;
}
return 0;
}
```

Build and run the program. You should see a list of assets:

```
toBeReclaimed: (
  "<Laptop 1: $17, assigned to <Employee 6: $119 in assets>>",
  "<Laptop 3: $51, assigned to <Employee 5: $136 in assets>>",
  "<Laptop 5: $85, assigned to <Employee 5: $136 in assets>>",
  "<Laptop 6: $102, assigned to <Employee 6: $119 in assets>>",
  "<Laptop 8: $136, assigned to <Employee 9: $136 in assets>>",
  "<Laptop 9: $153, assigned to <Employee 1: $153 in assets>>"
)
```

The format string used to create the predicate can be very complex. If you do a lot of filtering of collections, be sure to read *Apple’s Predicate Programming Guide*.

# NSSet/NSMutableSet

A set is a collection that has no sense of order, and a particular object can only appear in a set once. Sets are primarily useful for asking the question “Is it in there?” For example, you might have a set of URLs that are not child-appropriate. Before displaying any web page to a child, you would want to do a quick check to see if the URL is in the set. Sets do this incredibly quickly.

An employee’s assets have no inherent order, and an asset should never appear twice in the same employee’s assets collection. Change your program to use an `NSMutableSet` instead of an `NSMutableArray` for the assets relationship.