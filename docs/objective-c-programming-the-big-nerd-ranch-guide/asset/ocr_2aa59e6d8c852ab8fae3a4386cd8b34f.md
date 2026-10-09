There is no property lifetime specifier called *mutableCopy*. If you wish for your setter to set the property to be a mutable copy of an object, you must implement the setter yourself so that it calls the *mutableCopy* method on the incoming object. For example, in *OwnedAppliance*, you might create a *setOwnerNames:* method:

```
- (void)setOwnerNames: (NSSet *)newNames
{
	ownerNames = [newNames mutableCopy];
}
```

# More about copying

Most Objective-C classes have no *copyWithZone:* method at all. Objective-C programmers make fewer copies than you might think.

Curiously, the *copy* and *mutableCopy* methods are defined in *NSObject* like this:

```
- (id)copy
{
	return [self copyWithZone:NULL];
}

- (id)mutableCopy
{
	return [self mutableCopyWithZone:NULL];
}
```

Thus, if you have some code like this:

```
Appliance *b = [[Appliance alloc] init];
Appliance *c = [b copy];
```

You will get an error like this:

```
-[Appliance copyWithZone:]: unrecognized selector sent to instance 0x100110130
```

# Advice on atomic vs. nonatomic

This is an introductory book on programming, and the *atomic/nonatomic* option relates to a relatively advanced topic known as multithreading. Here is what you need to know: the *nonatomic* option will make your setter method run a tiny bit faster. If you look at the headers for Apple’s UIKit, every property is marked as *nonatomic*. You should make your properties *nonatomic*, too.

(I give this advice to everyone. In every group, however, there is someone who knows just enough to be a pain. That person says, “But when I make my app multithreaded, I’ll need the protection that atomic setter methods get me.” And I *should* say, “I don’t think you will write multithreaded code anytime soon. And when you do, I don’t think atomic setter methods are going to help.” But what I really say is “OK, then you should leave your setters *atomic*.” Because you can’t tell someone something they aren’t ready to hear.)

In *Appliance.h*, make your accessors non-atomic:

```
@property (copy, **nonatomic**) NSStr ing *productName;
@property (**nonatomic**) int voltage;
```

Sadly, at this time, the default for properties is *atomic*, so you do have to make this change.