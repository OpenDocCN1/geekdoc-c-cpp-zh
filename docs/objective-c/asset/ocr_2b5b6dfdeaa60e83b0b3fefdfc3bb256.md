This causes each element of the array to receive a call to -updatePosition: with the parameter gameState.

# Sorting and Filtering

NSArray and NSMutableArray benefit from a plethora of sorting and filtering capabilities. NSArray, because of its immutability, has methods that allow you to retrieve a copy of the array, sorted or filtered, whereas NSMutableArray allows you to also sort the array in place. For the purposes of discussion here, I focus primarily on NSMutableArray, but you should know that you can access any of the non-mutating methods through NSArray as well.

Sorting an array can be done with the methods -sortUsingDescriptors:, -sortUsingFunction:context:, or my personal favorite, -sortUsingSelector:, each of which takes a different type of sorting object as an argument to use for performing the sort.

The first of these, -sortUsingDescriptors: takes an instance of NSSortDescriptor as an argument. To create one of these, you specify the key path of the property upon which you want to sort the objects, whether this sort will be ascending or descending, and finally, if you choose, a selector which will be called using the property as arguments to do the comparison. If no selector is provided, the default is to use the standard -compare: selector.

In other words, take for example if you have an array of Employee objects, and you wanted to sort them based on employment date. The property that you would actually be sorting by in this case would be the employment date property, and you could perform this sort by using something like the code shown in Listing 13.20.

# Listing 13.20

# Sorting an array of employees using -sortUsingDescriptors:

```
NSMutableArray *employees = [...];

NSSortDescriptor *descr =
[NSSortDescriptor sortDescriptorWithKey:@"employmentDate"
    ascending:YES];

NSArray *descriptors = [NSArray arrayWithObject:descr];

[employees sortUsingDescriptors:descriptors];
```