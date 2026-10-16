```
buf = malloc(1024);
[bufData getBytes:buf length:1024];
}
}
return self;
}
```

# CAUTION

The -initWithCoder: method is specified as part of the NSCoding protocol. If the object you are inheriting from implements the NSCoding protocol, you should call [super initWithCoder:...] here instead of [super init]. In this case, the class inherits from NSObject, which does not implement that protocol. The same goes for the -encodeWithCoder method. It should also call -encodeWithCoder on the superclass if the superclass implements the NSCoding protocol.

Of special note, make sure you are retaining the objects you get back from NSCoder. They follow the same retain/release rules as you would use elsewhere. Your scalars and structs, however, do not need to be retained because they’re not objects.

# Using NSArchiver and NSUnarchiver

After your objects support the NSCoding protocol, you can archive them and unarchive them using NSCoders. The most common NSCoders are NSArchiver and NSKeyedArchiver, and the corresponding decoding classes, NSUnarchiver and NSKeyedUnarchiver. Again, NSArchiver is considered more of a legacy class, so I’ll focus here on NSKeyedArchiver.

To archive an object graph using NSKeyedArchiver, use the class method +archivedDataWithRootObject:, which will return an NSData with all the data from the root object on down archived within it. Alternatively, you can also use the factory method +archiveRootObject:toFile: to directly write that data to a file. Listing 18.5 shows this in action.

# Listing 18.5

# Writing data to disk

```
-(void)writeDataToPath:(NSString *)inPath
{
    [NSKeyedArchiver archiveRootObject:objects toFile:inPath];
}
```