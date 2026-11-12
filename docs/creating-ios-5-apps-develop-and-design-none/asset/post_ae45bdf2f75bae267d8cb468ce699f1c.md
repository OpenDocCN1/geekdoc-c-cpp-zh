
## SINGLETONS

In its most basic concept, a singleton is a class that will only ever have a single object instantiated from it. Whenever you request a new object of that class, you gain a pointer back to the original.

Singletons are typically used to represent objects where only a single version exists. The UIApplication class is a good example. Each application has one and only one application object. Furthermore, you can access that application anywhere through the `[UIApplication sharedApplication]` method.

Of course, singletons are a constant source of Internet debates. Some argue that they are the spawn of all that is evil and that they should be avoided like the plague. If you use singletons, the terrorists win. Or, somewhat more rationally, a singleton is nothing more than an over-engineered global variable with good PR.

There is some truth to these complaints. When developers first encounter the singleton pattern, they often overdo it. Too many singletons can make your code very hard to follow. Singletons are also deceptively hard to write correctly (and there are different ideas about what “correctly” means). However, they can be incredibly useful when used appropriately. Most importantly, Cocoa Touch uses a number of singleton classes—so you should at least understand the basics, even if you never write your own.

The following is a typical, relatively safe implementation. In the class’s header file, declare a class method to access your shared instance:

```objectivec
+ (SampleSingleton*)sharedSampleSingleton;
```

Then open the implementation file and add an extension to your class. This extension will declare a private designated initializer.

```objectivec
@interface SampleSingleton()
- (id)initSharedInstance;
@end
```

Remember, we can call any method on any object—declaring the initializer as private only communicates our intent. Developers should only call methods that are declared in the header file—in this case, the developers should only access the shared object through the sharedSampleSingleton method.

Finally, in the `@implementation` block, implement the following methods:

```objectivec
+ (SampleSingleton*)sharedSampleSingleton {
    static SampleSingleton* sharedSingleton;
    static dispatch_once_t onceToken;
    dispatch_once(&onceToken, ^{
        sharedSingleton = [[SampleSingleton alloc]
                            initSharedInstance];
    });
    return sharedSingleton;
}

// Private Designated Initializer.
- (id)initSharedInstance {
    self = [super init];
    if (self) {
        // Do initialization here.
    }
    return self;
}

// Override the superclass's designated initializer to prevent
// its use.
// Calling this method will throw an exception.
- (id)init {
    [self doesNotRecognizeSelector:_cmd];
    return nil;
}
```

This code uses lazy initialization to create our shared instance (we don't actually allocate the instance until `sharedSampleSingleton` is called). Within `sharedSampleSingleton`, we use a `dispatch_once` block to protect our shared instance. The `dispatch_once` block is a thread-safe way to ensure that a block of code is only executed once during an application's lifetime.

**NOTE:** Before ARC, many singleton implementations would override a number of additional methods: `allocWithZone:`, `copyWithZone:`, `mutableCopyWithZone:`, and `release` were all common candidates. Locking these down helped prevent developers from accidentally creating additional copies of the singleton. However, these methods either cannot be overridden when compiling under ARC or are simply unnecessary. Apple currently recommends using a simpler singleton and relying on convention and communication to prevent duplicates.

We also override the superclass's designated initializer, causing it to throw an exception if called. Hiding our designated initializer, and disabling the superclass's designated initializer, prevents developers from accidentally creating copies (e.g., by calling `[[SampleSingleton alloc] init]`).

Note that `copy` and `mutableCopy` are also disabled by default. Since we did not implement `copyWithZone:` or `mutableCopyWithZone:`, these methods will automatically throw exceptions.

This implementation doesn't deal with the tricky issue of loading or saving your singleton from disk. How you implement the archiving code depends a lot on what loading and saving the singleton means in your application. Do you load the singleton once from disk when it is first created? Or does loading the singleton simply change the value stored in the singleton? For example, your application may have a `GameState` singleton. You will only ever have the one `GameState` object—but the state values may change as the user loads and saves games.

For an even more advanced twist, some of Cocoa Touch's singletons let you specify the singleton's class in the application's `info.plist` file. This allows you to create a subclass of the singleton class yet still ensure the proper version is loaded at runtime. If you need this sort of support, modify your code as shown here:

```objectivec
+ (SampleSingleton*)sharedSampleSingleton {
    static SampleSingleton* sharedSingleton;
    static dispatch_once_t onceToken;
    dispatch_once(&onceToken, ^{
        NSBundle* main = [NSBundle mainBundle];
        NSDictionary* info = [main infoDictionary];
        NSString* className =
            [info objectForKey:@"SampleSingleton"];
        Class singletonClass = NSClassFromString(className);
        if (!singletonClass) {
            singletonClass = self;
        }
        sharedSingleton =
            [[singletonClass alloc] initSharedInstance];
    });
    return sharedSingleton;
}
```

This code accesses the `info.plist` file and looks for a key named `SampleSingleton`. If it finds one, it interprets the corresponding value as a class name and attempts to look up the corresponding class object. If that succeeds, it uses that class to create the singleton object. Otherwise, it just uses the default singleton class.

## BLOCKS

Blocks are, hands down, my favorite addition to Objective-C 2.0. They are only available for iOS 4.0 or later. However, unless you are targeting really old devices, blocks can greatly simplify many algorithms.

For example, the UIView class has a number of methods for animating views using blocks. These methods provide a much more concise, much more elegant solution than the older animation API.

Blocks are somewhat similar to methods and functions in that they are a way of bundling up a number of expressions for later execution. Blocks, however, can be stored as variables and passed as arguments. We can create block variables as shown:

```objectivec
returnType (^blockName)(argumentTypes);
```

For example, let’s declare a block variable named sum that returns an integer and takes two integer arguments:

```objectivec
int (^sum)(int, int);
```

You can define a literal block starting with the caret (^) and then declaring the arguments in parentheses and the actual code in curly brackets.

```objectivec
sum = ^(int a, int b){return a + b;};
```

Once a block variable is assigned, you can call it just like any other function.

```objectivec
NSLog(@"The sum of %d and %d is %d", 5, 6, sum(5, 6));
```

It’s important to note that blocks can capture any data that is in scope when the block is defined. For example, in this sample, addToOffset will take a single argument and add the offset variable to it.

```objectivec
int offset = 5;
int (^addToOffset)(int) = ^(int value){return offset + value;};
```

> **NOTE:** When a block captures a local variable stored on the stack, it treats this variable as a `const` value. You can read the value but not modify it. If you need to mutate a local variable, you must declare it using the `__block` storage type modifier. Generally, this only applies to local C types and structs. You can already mutate objects, instance variables, and anything else allocated on the heap.

![](img/fe9fea534a8e7868f811f7cd33da015f_124_0.png)

Usually, however, we don’t create or call block variables. Instead, we pass literal blocks to methods and functions as arguments. For example, NSArray has a method, `enumerateObjectsUsingBlock:`, that takes a single block. This method will iterate through all the objects in the array. For each object, it calls the block, passing in the object, the object’s index, and a reference to a stop value.
