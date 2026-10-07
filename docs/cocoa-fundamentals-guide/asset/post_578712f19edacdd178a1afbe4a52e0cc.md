
## CHAPTER 3
## Adding Behavior to Cocoa Program

The convention for naming instance variables is to make them a lowercase string containing no punctuation marks or special characters. If the name contains multiple words, run them together, but make the first letter of the second and succeeding word uppercase. For example:

```objc
NSString *name
UIColor *backgroundColor;
SRange currentRange;
```

When the tag IBOutlet precedes the declarations of instance variables, it identifies an outlet (presumably) a connection anchored in a nib. The tag also enables Interface Builder and Xcode to synchronize their activities. When outlets are unarchived from an Interface Builder nib, the connections are automatically reestablished. ([Communicating with Objects](page 175)) discusses outlets in more detail.

Instance variables can hold more than an object's attribute, values of the client. Instance variables can hold private data that is used as the basis for task performed by the object; a backing store or a cache examples. (If data is not private, but is to be shared among instances of a class, use global variables instead of instance variables.)

When you add instance variables to a subclass, follow these guidelines:

- Add only instance variables that are absolutely necessary. The more instance variables you add, the more instance size grows. And the more instances of your class that are created, the more of concern this becomes. If it is possible, capture a critical value from existing instance variables rather than add another instance variable to hold that value.
- Again, for economy represent the instance data of the class efficiently. For example, if you want to specify a number of flags as instance variables, use a bit field instead of series of Booleans. Be aware, that there are archiving complications with bit fields). If you might use an NSDictionary object to consolidate a number of related attributes as key-value pairs; if you do this, make sure that the keys are adequately documented.
- Give the proper scope to your instance variables. Never scope a variable as @public as this violates the principle of encapsulation. Use @protected for instance variables if you know which are the likely subclasses of your class (such as the classes of your application) and you require efficient access of data. Otherwise, @private is a reasonable choice for high degree of implementation hiding. This implementation hiding is especially important for classes used by a framework and by applications; it permits the modification of the class implementation without needing to reclaim all clients.
- Make sure there are declared property accessor methods for instance variables that are essential attributes or relationships of your class. Accessor methods and declared properties encapsulation by enabling the values of instance variables to be set and retrieved. ([Storing and Accessing Properties](page 123)) for more information on this subject.
- If you indent your subclass to be public—that is, you anticipate that other subclass it—pad the end of the instance variable list with a reserved field, typically used as id. This reserved field helps to ensure binary compatibility, at any time in the future, you need to add another instance variable to the class. See ([When the Class Is Public (Mac OS X)](page 132)) for more information on preparing public classes.

### Basic Subclass Design

## Entry and Exit Points

The Cocoa framework sends messages to an object at various points in the object's life. Almost all objects (including classes, which are really objects themselves) receive messages at the beginning of their runtime life and just before their destruction. The methods invoked by these messages (if implemented) are hooks that allow the object to perform tasks relevant to the moment. These methods are (in the order of):

1. `initialize`-This method enables a class to initialize itself before it or its instances any other messages. Superclasses receive this message before subclasses. Classes that use the old `initialize` mechanism implement `initialize` to set their class version. Other possible uses are registering a class for service and initializing some global state that is used by all instances. However, it's better to do these kinds of tasks lazily (that is, the first time they're needed) in an instance method rather than `initialize`.

2. `init` (or other initializer)-You must implement `init` or some other initializer to initialize the state of the instance unless work done by the superclass's designated initializer is sufficient for your class. See "Object Creation" (page 77) for information on initializers, including designated initializers.

3. `initWithCoder`-If you expect objects of your class to be archived—for examples, your class—should adopt `NSCoding` protocol and implement its two methods, `initWithCoder` and `encodeCoder`. In these methods you must decode and encode, the instance variables of the object in a format suitable for archive. You can use the decode and encoding methods of `NSCoding` for this purpose or the key-value archiving facilities of `NSKeyedArchiver` and `NSKeyedUnarchiver`. When the object is unarchived without being explicitly, the initializer is invoked. After decoding the instance-values, you assign them to your attributes, retaining or copying them if necessary. For more on this, see *Archives and Serializations Programming*.

4. `awakeFromNib`-When an application loads a file, an `awakeFromNib` message is sent to each object loaded from the archive, but only if it can respond to the message, and only after all the objects in the archive have been loaded. When an object receives an `awakeFromNib` message, it is guaranteed to have all its outlet instance variables set. The object that owns the file (File's Owner) implements this to perform programmatic initializations that require outlet and target-connections to be set.

5. `encodeWith`-Implement this if your class should be archived. This method is invoked just before the destruction of the object. The design of `initCoder` however:

6. `dealloc` or `finalize`-In memory-managed programs, the `dealloc` method to release instance variables deallocate any other memory created by an instance of the class. The instance is destroyed soon after this method returns. In garbage-collected, you need to implement the `finalize` method instead. See "The deallocation and finalize Methods" (page 85) for further information.

An application's singleton object sends messages to an object—if the application object's delegate and implements the appropriate methods—at the beginning and end of the application's life. After the launch, the application object sends its delegate messages, depending on the runtime and platform:

- In AppKit, the application sends `applicationWillFinishLaunching:` and `applicationDidFinishLaunching:` to the delegate. The former is sent just before any double-clicked document is opened, the latter just afterward.
- In UIKit, the application sends `application:didFinishLaunchingWithOptions:` to the delegate.

In these methods the delegate can restore application state and specify global application logic that needs to happen just once in the application's runtime existence. Just before it terminates, the application object sends willTerminate: to its delegate, which can gracefully handle program termination by saving documents (and particularly in iOS) application state.
