# CHAPTER 2
Cocoa Objects

| Core Foundation type | Foundation class | Availability |
| CFNumberRef | NSNumber | Mac OS X v10.0 |
| CFReadStreamRef | NSInputStream | Mac OS X v10.0 |
| CFRunTimerRef | NSTimer | Mac OS X v10.0 |
| CFSetRef | NSSet | Mac OS X v10.0 |
| CFStringRef | NSString | Mac OS X v10.0 |
| CFTimeZoneRef | NSTimeZone | Mac OS X v10.0 |
| CFURLRef | NSURL | Mac OS X v10.0 |
| CFWriteStreamRef | NSOutputStream | Mac OS X v10.0 |

> Note: Not all types are toll-free bridged, even though their names might suggest they are. For example, NSRunLoop is not toll-free bridged to CFRunLoop, NSBundle is not toll-free bridged to CFBundle, and NSDate is not toll-free bridged to CFDate.

# Creating a Singleton Instance

Some classes of the Foundation and AppKit create singleton objects. In a strict implementation, a singleton is the sole instance of a class in the current process. You can have a more flexible singleton implementation in which a factory method returns the same instance, but you can allocate and initialize additional instances. The FileManager class fits this latter pattern, whereas the UIApplication fits the former. When you ask for an instance of UIApplication, it passes you reference to the sole instance, allocating and initializing it if it does not exist.

A singleton object acts as a class of control, directing or coordinating the services of the class. Your class should define a singleton instance rather than multiple instances when there is conceptually only one instance (with example, NSString). You use instances rather than factory methods or functions when it is conceivable that there might be multiple instances.

To create a singleton as the sole instance of a class in the current process, you need to have an implementation similar to Listing 2-15. This code does the following:

+   * It creates a static instance of your singleton object and initializes it to nil.

+   * In your factory method for the class (named something like "sharedInstance" or "sharedManager\ it generates an instance of the class but if the static instance is nil.

+   * It overrides the allocWithZone method to ensure that an instance is not allocated if someone tries to allocate and initialize your class instead of using the class factory method. Instead, it returns the shared object.

Creating a Singleton Instance
2010-12-13 | © 2010 Apple Inc. All Rights Reserved.