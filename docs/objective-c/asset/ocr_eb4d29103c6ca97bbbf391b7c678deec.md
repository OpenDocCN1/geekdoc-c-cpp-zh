-remove<VariableName>: for removing objects, and -intersect<VariableName>: for removing a group of objects from the set.

Listing 6.13 shows an example implementation of these methods using an NSSet to actually implement the relationship.

# Listing 6.13

# Implementing mutable accessors for an unordered one-to-many relationship

```
// adding...
-(void)addBarsObject:(Bar *)inBar;
{
    [bars addObject:inBar];
}

// OR...
-(void)addBars:(NSSet *)inBars;
{
    [bars unionSet:inBars];
}

// removing
-(void)removeBarsObject:(Bar *)inBar;
{
    [bars removeObject:inBar];
}

// OR...
-(void)removeBars:(NSSet *)inBars;
{
    [bars minusSet:inBars];
}

// intersect
-(void)intersectBars:(NSSet *)inBars;
{
    return [bars intersectSet:inBars];
}
```