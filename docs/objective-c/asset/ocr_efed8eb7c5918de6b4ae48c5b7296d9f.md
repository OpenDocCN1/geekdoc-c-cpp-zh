# Listing 18.2 (continued)

```
[inCoder encodeRect:aRect forKey:@"aRect"];
[inCoder encodeInt:aNumber forKey:@"aNumber"]
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

# Working with object graphs

Because of the way the NSCoding protocol works, it’s expected that any given object will encode its member variables, and each of them will encode their member variables, and so on. So the nice thing about NSCoder is that you only really need to worry about encoding your own state. Assuming all your member variables also implement the NSCoding protocol, you can encode them “opaquely” and not have to think about what’s inside them.

That said, you might need to be concerned about circular references. NSCoder does not do any kind of circular reference checking, so if you have a circular reference in your code, it may cause issues for archiving. Another gotcha that can sometimes catch programmers unaware is the fact that only the data itself, and not the pointers and addresses of objects, are archived. Meaning, an archived object pointer, when unarchived, will be different from the original pointer. Therefore, when unarchiving things, you may need to manually reconnect your references in order to fully complete your object graph.

# Using other types of data

In cases where you have data that doesn’t neatly fit into one of the scalar types or into an object, you may need to encode that data using NSData boxing. To do this, you simply box your data into an NSData object, and then encode the NSData object using the NSCoder method -encodeDataObject:. An example of this is shown in Listing 18.3.