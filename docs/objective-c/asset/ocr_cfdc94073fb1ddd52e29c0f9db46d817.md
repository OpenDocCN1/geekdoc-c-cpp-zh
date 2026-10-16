In this example, I’m only using a single descriptor, but you can also sort by multiple criteria by providing multiple descriptors. The parameter is an array, so you simply put them all into an NSArray and call the method.

The second of these methods -sortUsingFunction:context: It is for use when you need to perform your compare by using a function pointer. The function pointer that is passed as the argument to this method should be of the form NSInteger comparisonFunction (id obj1, id obj2, void *). Its first two arguments are the two objects being compared. Its third argument is the context information, which is passed unchanged from the additional parameter provided to the method. This technique is useful when you need to pass some kind of additional external information to the comparison. You would do this by passing it as the contextual information pointer. Listing 13.21 shows an example sorting an array using this technique.

# Listing 13.21

# Sorting an array using a function

```
NSUInteger sortByEmploymentDate(id employee1,
    id employee2,
    void *ctx)
{
    return [[employee1 employmentDate]
        compare:[employee2 employmentDate]];
}

NSMutableArray *employees = [...];

[employees sortUsingFunction:sortByEmploymentDate context:nil];
```

The third technique, using the method -sortUsingSelector: takes a selector object as a parameter. When used, the array iterates over all the elements of the array calling the given selector as a comparison method. The selector in question is expected to be implemented as an object method on the class of all of the elements of the array. It takes as an argument another element of the array and returns an NSComparisonResult specifying NSOrderedSame, NSOrderedAscending, or NSOrderedDescending, depending upon whether the receiver of the method and the past in object are equal, ordered ascending, were ordered descending relative to each other. Listing 13.22 shows the same employee array sort being done by using this technique. In this example, I’m showing the Employee class as well, to demonstrate how you might create the method that’s being called.