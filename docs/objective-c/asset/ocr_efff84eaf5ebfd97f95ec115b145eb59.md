# Listing 5.4

# Declaring a function which takes a block parameter

```
void useCodeBlock(NSComparisonResult (^theBlock)(NSString *value));
```

Inside the body of the function that utilizes a block, you call the block by treating its variable just like a normal function name. In other words, you simply use the variable just as if it were a function, passing the parameters that the block requires inside parentheses, and storing the return result however, you need to use the assignment operator.

Listing 5.5 shows the same function that we declared earlier, but shows how it might use the block that was passed to it.

# Listing 5.5

# A function which uses a block

```
void useCodeBlock(NSComparisonResult (^theBlock)(NSString *value))
{
    if(NSOrderedSame == theBlock(@"foo"))
        doSomethingIfSame();
    else
        doSomethingElse();
}
```

When passing a block parameter as an argument to an object or class method (versus an argument to a function) the syntax is slightly different. Listing 5.6 shows an example of how you do that.

# Listing 5.6

# Passing a block to an object method

```
-(NSMutableArray *)filterArray:(NSArray *)inArray
                    withBlock:(BOOL (^)(NSUInteger))block
{
    NSMutableArray *result = [NSMutableArray array];
```