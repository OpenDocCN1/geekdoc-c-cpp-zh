If the indexOfObjectPassingTest finds a match (meaning you returned YES from your block at least one occasion), it will return the lowest matching index from the set. Otherwise, if no match is found, it will return NSNotFound.

Here's a modified version of the lookup: method from our AddressBook class.

```
- (AddressCard *) lookup: (NSString *) theName {
    NSInteger result = [book indexOfObjectPassingTest:
        ^ (id obj, NSInteger idx, BOOL *stop) {
            if ([[obj] name] caseInsensitiveCompare:NSOrderedSame)
                *stop = YES; // found a match, one is enough
                return YES;
            } else {
                return NO; // keep looking
            }
        }];

// See if we found a match
if (result != NSNotFound) // there should only be one element
    return [book objectAtIndex: result];
} else {
    return nil;
}
```

If you were looking to find all the matching entries from the array, you could store each match inside an array inside the block and never