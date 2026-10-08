# ### NSArray

The NSArray class is handy for storing a group of objects in one place.

To demonstrate, here's one way you might create and populate an array with NSString objects:

```
```
NSArray *theArray;
NSString *name1;
NSString *name2;
NSString *name3;
NSString *name4;

//assign values to the four names
name1 = @"Maria";
name2 = @"Mercedes";
name3 = @"Leopold";
name4 = @"Frederick";

//create and populate the array
theArray = [NSArray arrayWithObjects:name1, name2,
                                     name3, name4, nil];
```
```

Note the arrayWithObjects method lets you create an NSArray by listing the objects in that array. The last object must always be nil to indicate the end of the array.

If you want to find out how many items were in that array, use the count method:

```
```
int i = [theArray count];
```
```

You can then use the size of the array to retrieve the objects within that array, based on the index. This code snippet displays each item in the array that you just created:

```
```
NSLog(@"object1 = %@",[theArray objectAtIndex:0]);
NSLog(@"object2 = %@",[theArray objectAtIndex:1]);
NSLog(@"object3 = %@",[theArray objectAtIndex:2]);
NSLog(@"object4 = %@",[theArray objectAtIndex:3]);
```
```

![](bbox=[0.13, 0.78, 0.2, 0.87])

Don’t forget that the index is always zero-based.