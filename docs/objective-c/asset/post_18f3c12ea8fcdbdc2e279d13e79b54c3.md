
If the coder does not allow keyed coding, the variables will be encoded in the order you feed them to the NSCoder. Thus, it's important that they also be unencoded in the same order, so your unarchiving code will need to know that order as well. For this reason, using a keyed archiver is usually preferable to a non-keyed one.

Keyed archiving is considered the more “modern” form of archiving. So if you do not need backwards compatibility with non-keyed archivers, you can safely implement this code to only encode using keys.

## NOTE

Be sure to state that you are implementing the NSCoding protocol as part of your interface declaration.

## Encoding basic types

Basic scalars like ints, floats, and structs can also be encoded using NSCoder by using the methods defined on it such as -encodeDouble:forKey:, -encodeInt:forKey:, and so on. If you extended the class from the last example to include some scalars and structures, you might change the -encodeWithCoder: method to look like Listing 18.2.

## Listing 18.2

```
@interface MyClass : NSObject <NSCoding>
{
    Foo *memberVariable;
    Bar *anotherVariable;
    NSArray *someMemberArray;
    NSRect aRect;
    int aNumber;
}

@end

@implementation MyClass

...

-(void)encodeWithCoder:(NSCoder *)inCoder
{
    if([inCoder allowsKeyedCoding])
    {
        [inCoder encodeObject:memberVariable forKey:@"memberVariable"];
        [inCoder encodeObject:anotherVariable forKey:@"anotherVariable"];
        [inCoder encodeObject:someMemberArray forKey:@"someMemberArray"];
```

## Listing 18.2 (continued)

```
[inCoder encodeRect:aRect forKey:@"aRect"];
[inCoder encodeInt:aNumber forKey:@"aNumber"];
}
else
{
[inCoder encodeObject:memberVariable];
[inCoder encodeObject:anotherVariable];
[inCoder encodeObject:someMemberArray];
[inCoder encodeRect:aRect];
[inCoder encodeInt:aNumber];
}
}
@end
```

NSCoder has a variety of these methods available. See the NSCoder documentation for more information.

## Working with object graphs

Because of the way the NSCoding protocol works, it’s expected that any given object will encode its member variables, and each of them will encode their member variables, and so on. So the nice thing about NSCoder is that you only really need to worry about encoding your own state. Assuming all your member variables also implement the NSCoding protocol, you can encode them “opaquely” and not have to think about what’s inside them.

That said, you might need to be concerned about circular references. NSCoder does not do any kind of circular reference checking, so if you have a circular reference in your code, it may cause issues for archiving. Another gotcha that can sometimes catch programmers unaware is the fact that only the data itself, and not the pointers and addresses of objects, are archived. Meaning, an archived object pointer, when unarchived, will be different from the original pointer. Therefore, when unarchiving things, you may need to manually reconnect your references in order to fully complete your object graph.

## Using other types of data

In cases where you have data that doesn’t neatly fit into one of the scalar types or into an object, you may need to encode that data using NSData boxing. To do this, you simply box your data into an NSData object, and then encode the NSData object using the NSCoder method -encodeDataObject:. An example of this is shown in Listing 18.3.

## Listing 18.3

## Encoding a malloc’ed memory block in your NSCoder

```
@interface MyClass : NSObject <NSCoding>
{
    Foo *memberVariable;
    Bar *anotherVariable;
    NSArray *someMemberArray;
    NSRect aRect;
    int aNumber;
    char *buf;
}

@end

@implementation MyClass

// buf might be allocated using malloc(1024) etc...
...

-(void)encodeWithCoder:(NSCoder *)inCoder
{
    if([inCoder allowsKeyedCoding])
    {
        [inCoder encodeObject:memberVariable forKey:@"memberVariable"];
        [inCoder encodeObject:anotherVariable forKey:@"anotherVariable"];
        [inCoder encodeObject:someMemberArray forKey:@"someMemberArray"];
        [inCoder encodeRect:aRect forKey:@"aRect"];
        [inCoder encodeInt:aNumber forKey:@"aNumber"];
        NSData *bufData = [NSData dataWithBytes:buf length:1024];
        [inCoder encodeObject:bufData forKey:@"someData"];
    }
    else
    {
        [inCoder encodeObject:memberVariable];
        [inCoder encodeObject:anotherVariable];
        [inCoder encodeObject:someMemberArray];
        [inCoder encodeRect:aRect];
        [inCoder encodeInt:aNumber];
        NSData *bufData = [NSData dataWithBytes:buf length:1024];
        [inCoder encodeDataObject:bufData];
    }
}

@end
```

## Decoding objects

The other side of the NSCoding protocol is used to decode objects that have been encoded. There’s a special initializer provided specifically for this purpose called `-initWithCoder:`, it is the only initializer that requires that you **not** call the designated initializer when you use it. An implementation of this method for decoding our example is shown in Listing 18.4.

## Listing 18.4

## An example of -initWithCoder:

```
- (id)initWithCoder:(NSCoder *)inCoder
{
    if((self = [super init]))
    {
        if([inCoder allowsKeyedCoding])
        {
            memberVariable =
                [[inCoder decodeObjectForKey:@"memberVariable"]
                    retain];
            anotherVariable =
                [[inCoder decodeObjectForKey:@"anotherVariable"]
                    retain];
            someMemberArray =
                [[inCoder decodeObjectForKey:@"someMemberArray"]
                    retain];
            memberVariable =
                [[inCoder decodeObjectForKey:@"memberVariable"]
                    retain];
            aRect = [inCoder decodeRectForKey:@"aRect"];
            aNumber = [inCoder decodeIntForKey:@"aNumber"];
            NSData *bufData = [[inCoder decodeObjectForKey:@"someData"]
                retain];
            buf = malloc(1024);
            [bufData getBytes:buf length:1024];
        }
        else
        {
            memberVariable = [[inCoder decodeObject] retain];
            anotherVariable = [[inCoder decodeObject] retain];
            someMemberArray = [[inCoder decodeObject] retain];
            memberVariable = [[inCoder decodeObject] retain];

            aRect = [inCoder decodeRectForKey:@"aRect"];
            aNumber = [inCoder decodeIntForKey:@"aNumber"];
            NSData *bufData = [inCoder decodeDataObject];
```

```
buf = malloc(1024);
[bufData getBytes:buf length:1024];
}
}
return self;
}
```

## CAUTION

The -initWithCoder: method is specified as part of the NSCoding protocol. If the object you are inheriting from implements the NSCoding protocol, you should call [super initWithCoder:...] here instead of [super init]. In this case, the class inherits from NSObject, which does not implement that protocol. The same goes for the -encodeWithCoder method. It should also call -encodeWithCoder on the superclass if the superclass implements the NSCoding protocol.

Of special note, make sure you are retaining the objects you get back from NSCoder. They follow the same retain/release rules as you would use elsewhere. Your scalars and structs, however, do not need to be retained because they’re not objects.

## Using NSArchiver and NSUnarchiver

After your objects support the NSCoding protocol, you can archive them and unarchive them using NSCoders. The most common NSCoders are NSArchiver and NSKeyedArchiver, and the corresponding decoding classes, NSUnarchiver and NSKeyedUnarchiver. Again, NSArchiver is considered more of a legacy class, so I’ll focus here on NSKeyedArchiver.

To archive an object graph using NSKeyedArchiver, use the class method +archivedDataWithRootObject:, which will return an NSData with all the data from the root object on down archived within it. Alternatively, you can also use the factory method +archiveRootObject:toFile: to directly write that data to a file. Listing 18.5 shows this in action.

## Listing 18.5

## Writing data to disk

```
-(void)writeDataToPath:(NSString *)inPath
{
    [NSKeyedArchiver archiveRootObject:objects toFile:inPath];
}
```
