send it an initialization message, you get an instance of one of the two private subclasses.

```
@implementation IntPair
-( (Pair*)initWithInt:(int)a int:(int)b {
    first = a;
    second = b;
    return self;
}
-(NSString*)description {
    return [NSString stringWithFormat:@"%d, %d",
	first, second];];
}
-(float)firstFloat { return (float)first; }
-(float)secondFloat { return (float)second; }
-(int)firstInt { return first; }
-(int)secondInt { return second; }
@end
```

Each of these concrete subclasses is quite simple. They both declare two instance variables: ints in one, floats in the other. They each provide a single initializer, which is called only from the superclass, and then they override the methods. This example doesn't provide any useful methods in the superclass. In a real implementation, you might see methods for comparison or arithmetic implemented in the superclass, in terms of the four methods that are shown here. Alternatively, they might be provided in a separate category.