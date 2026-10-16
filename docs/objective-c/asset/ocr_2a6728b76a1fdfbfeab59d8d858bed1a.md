# Listing 5.17 (continued)

```
[candidates addObject:[NSNumber numberWithInteger:n]];
}
}
return self;
}

-(NSMutableArray *)filterArray:(NSArray *)inArray
withBlock:(BOOL (^)(id))block
{
NSMutableArray *result = [NSMutableArray array];
for(id item in inArray)
{
if(block(item))
[result addObject:item];
}
return result;
}

-(void)start
{
[self setStartedDate:[NSDate date]];

BOOL (^isPrime)(id) = ^(id number)
{
NSInteger value = [number integerValue];
for(NSInteger n = 2; n < value; n++)
if((value % n) == 0)
return NO;
return YES;
};

[self setPrimes:[self filterArray:candidates withBlock:isPrime]];

[self setEndedDate:[NSDate date]];
}

-(NSTimeInterval)elapsedTime
{
return [endedDate timeIntervalSinceDate:startedDate];
}

@end
```

First, you create your candidates array in your initializer.