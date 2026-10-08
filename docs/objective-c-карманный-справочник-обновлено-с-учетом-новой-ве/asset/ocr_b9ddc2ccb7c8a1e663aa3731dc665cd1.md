the class by other threads.\¹

**Note:** The Apple documentation recommends using @synchronized(self) in the +sharedInstance method for creating singletons. That approach is both significantly slower and requires more code than the approach proposed in this section, so it has little to recommend it.

You don’t need to override +allocWithZone: in a singleton, but it provides a little bit extra run-time checking if you do. The sample code will throw an exception if you try to allocate a new instance of the class after the singleton instance has been created.

Note the tests in both the +allocWithZone: and +initialize methods. These are needed for subclassing. You don’t want to throw an exception if someone creates a subclass of your singleton object. Subclassing singletons is quite tricky, so you may skip this extra test if you don’t want to support it.

# Delegation

Objective-C doesn’t support multiple inheritance. This is not a huge limitation, because it’s very hard to use multiple inheritance

> ¹There is a long-standing bug in the GCC runtime that prevents this from working correctly, but it’s fixed in the GNUStep runtime.