this in operation, in a trivial case. This will
be rejected by old Objective-C++ compilers.
You can use this to check whether your target
supports the unified exception model.

# Managing Memory with
Exceptions

```
id pool = [NSAutoreleasePool new];
id array = [NSArray new];
@try
{
    throw(array);
}@catch (id e)
{
    NSLog("Caught exception %@", e);
    e = [e retain];
    [pool drain];
    [e autorelease];
    pool = nil;
    @throw;
}inally
{
    [array release];
    [pool drain];
}
```

From: releaseexcept.m

Exception handling makes memory management
a bit more difficult. If you create a new object
in a method and then release it at the end, you
must take into account the fact that exceptions