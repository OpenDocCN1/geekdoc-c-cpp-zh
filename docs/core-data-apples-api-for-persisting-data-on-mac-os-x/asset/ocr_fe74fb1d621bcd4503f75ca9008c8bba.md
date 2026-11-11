The resulting protocol is as follows:

Download DistributedCDServer/PPDistributedProtocol.h

```
```objective-c
#define kDomainName @"local."
#define kServiceName @"_pragProgExample._tcp"

@protocol PPDistributedProtocol

- (oneway void)ping;

- (byref NSManagedObject*)createObject;
- (byref NSManagedObject*)createChildForObject:(byref NSManagedObject*)parent;
- (oneway void)deleteObject:(byref NSManagedObject*)object;
- (byref NSArray*)allObjects;
- (byref NSArray*)objectsOfName:(bycopy NSString*)name
    withPredicate:(bycopy NSPredicate*)predicate;

@end
```
```

When we are working with distributed objects, we need to define how nonscalar attributes are handled.<sup>1</sup> In our protocol, we are passing most of the objects byref, which means that an NSDistantObject is created on the receiver as a proxy to the object that is residing on the server. This is different from bycopy, which will make a copy of the object on the receiving end. One of the interesting differences between these is that KVO works across a distributed object when it is passed byref. This will be demonstrated as we build the application.

# ### Broadcasting the Service

Distributed objects work by using good old Unix sockets. Fortunately, these are wrapped with NSSocketPort for us so that we do not need to use the raw C functions and all the complexity that entails. To use sockets, we need to know the address and port of the socket to talk to. This can be entered by the user, which is a suboptimal experience, or we can discover it using Bonjour. To use Bonjour, we need to set up a broadcast on the server for the client to discover.

Download DistributedCDServer/AppDelegate.m

```
```objective-c
- (void)startBroadcasting
{
    receiveSocket = [[NSSocketPort alloc] init];
    int receivePort = [self portFromSocket:receiveSocket];

    myConnection = [[NSConnection alloc] initWithReceivePort:receiveSocket
        sendPort:nil];
}
```
```

1. These are discussed in depth in Apple's documentation.