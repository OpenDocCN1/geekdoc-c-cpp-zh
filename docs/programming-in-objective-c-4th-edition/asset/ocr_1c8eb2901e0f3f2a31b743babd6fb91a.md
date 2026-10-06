```
{
  book = [theBook mutableCopy];
}

-(void) sort
{
  [book sortUsingSelector:@selector(compareNames)]];
}

// Alternate sort using blocks

-(void) sort2
{
  [book sortUsingComparator:
    ^(id obj1, id obj2) {
      return [[obj1 name] compare: [obj name]];
    }];
}

-(void) addCard:(AddressCard *) theCard
{
  [book addObject:theCard];
}

-(void) removeCard:(AddressCard *) theCard
{
  [book removeObjectIdenticalTo:theCard];
}

-(int) entries
{
  return [book count];
}

-(void) list
```