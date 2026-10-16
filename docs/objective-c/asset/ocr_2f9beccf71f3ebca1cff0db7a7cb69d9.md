You may find a liberating simplicity in having the release coupled so closely to the allocation of the object. You are less likely to forget to do it later when using this pattern. Additionally, writing your code in this way enables you to think of Objective-C a bit more like a memory managed language, such as Python or Ruby. You can imagine that all of your variables that you are working with inside of this particular stack frame will always go out of scope and be deallocated. You only have to actually think about a particular object or variable when you want to keep it around outside of this particular stack frame.

The Cocoa and Cocoa Touch frameworks provide you with additional tools to help you follow this pattern, as well. Specifically, many of the foundation objects, such as NSString, NSArray, and NSDictionary, include factory methods that return autoreleased versions of the objects they create. By using these, instead of the alloc/init patterned constructors, you barely have to think about memory management at all.

Listing 4.8 shows an example of using these sorts of factory methods and compares them to the traditional pattern.

# Listing 4.8

# Using factory methods versus the traditional allocation pattern

```
-(void)usingFactories;
{
    NSMutableArray *array = [NSMutableArray array]; // nice, simple,
    autoreleased.

    NSMutableArray *array2 = [[NSMutableArray alloc] init];
    // do stuff with array and array 2...

    // need to release this one.
    [array2 release];

    // [array release]; no need to release this,
    // it's already autoreleased
    // if you release it here, it will cause a crash
}
```

Because you are essentially leaving it up to the runtime to delete the objects that you create, you are giving up a certain amount of control over when those objects will be deleted. In an