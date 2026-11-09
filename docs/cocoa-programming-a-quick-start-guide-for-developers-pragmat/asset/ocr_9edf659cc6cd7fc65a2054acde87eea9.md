changes to an NSDictionary because it is immutable. Instead, you have to use the NSMutableDictionary. This is the subclass of NSDictionary that allows such changes.

By now you have probably found it frustrating that the Apple documentation for a class doesn’t at least list all of the methods that are available for objects of a particular type. The documentation contains in-depth descriptions of methods defined for that class but doesn’t show you the methods that are inherited from superclasses. You have to follow the documentation up the tree to find that a particular method is defined several levels up (often in a class you would never have thought to look at).⁴

This general inconvenience can sometimes be a benefit. For example, if you look at the documentation for NSMutableDictionary, you can quickly see how it differs from NSDictionary. Only the additional methods are listed. There are methods for creating a mutable dictionary that allow you to specify the initial capacity of the dictionary.⁵ There are additional methods for adding entries to and removing entries from a mutable dictionary. In every other way, an NSMutableDictionary is just an NSDictionary, so all of those methods in the superclass are available to us in the NSMutableDictionary as well.

So, let’s play with the NSMutableDictionary a bit. First declare an instance variable named runningApps in CurrentApp.h.

Download Dictionaries/HelloApplication16/CurrentApp.h

```
```objc
#import <Cocoa/Cocoa.h>
#import "ActivityMonitorDelegate.h"

@interface CurrentApp : NSObject {
    NSObject <ActivityMonitorDelegate> *delegate;
    NSString *name;
    NSDictionary *delegateMethods;
    NSMutableDictionary *runningApps;
}
@property IBOutlet NSObject <ActivityMonitorDelegate> *delegate;
@property(copy) NSString *name;
@end
```
```

4. You can always press Escape after typing the name of your target and a space to see all of the methods available to you. Use this in conjunction with Quick Help to quickly understand what each method does.
5. As the dictionary grows, more memory will be allocated to it as needed.