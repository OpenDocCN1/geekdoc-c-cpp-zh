```
NSMutableArray *hotel = [[NSMutableArray alloc] init];

// Lobby on the ground floor
[hotel addObject:lobby];

// Pool on the second
[hotel addObject:pool];

// The third floor has not been built out
[hotel addObject:[NSNull null]];

// Bedrooms on fourth floor
[hotel addObject:bedrooms];
```

# Challenge

Explore the reference pages for **NSArray**, **NSMutableArray**, **NSDictionary**, and **NSMutableDictionary**. You will use these classes every day.