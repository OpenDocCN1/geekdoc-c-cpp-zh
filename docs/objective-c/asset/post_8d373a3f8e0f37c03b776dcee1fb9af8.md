
Objective-C differs from other languages in its implementation of these particular patterns. My goal here is not a full catalog of patterns, but instead a sampling of patterns that are particularly illustrative, and which will help you approach other design pattern books more comfortably as an Objective-C programmer.

## Describing Design Patterns in Objective-C

Most design pattern books follow a specific format in the description of their patterns. Typically, these books begin by stating a particular type of problem. They then follow the problem statement with a description of the solution, including code for the solution, and then finally a discussion about the solution. For the purposes of the design patterns I am going to discuss here I intend to follow this pattern.

## Using Singletons

### Problem

You need to ensure that there is one and only one instance of a particular class in your application and provide a global point of access to it. This may be due to design constraints or for the purposes of controlling access to a finite resource.

### Solution

The solution to this problem is called a singleton. A singleton is a class that ensures that you cannot create more than one instance of it. Normally, this is accomplished by creating a single instance of that class the first time the constructor for your class is called. Subsequent calls to the constructor check for the existence of the global instance, and if it exists, returns a reference to the global instance rather than creating a new one.

Implementing a singleton in Objective-C consists of several steps. First, you have to create the global instance. The global instance is typically stored in a global variable. One important aspect of this global instance is that you should be sure to set the instance to nil. You will later be checking whether this variable is set to nil when your initializer is called. Listing 17.1 shows a typical declaration of a global singleton instance. Typically, this declaration is put into the implementation file for the class that you are turning into a singleton.

### Listing 17.1

#### The global instance definition

```
static MyClass *instance = nil;
```

After you have created the place to store your global instance, you need to provide global access to that instance through a factory method which checks for the existence of the instance, and if it does not exist creates it. This is shown in Listing 17.2.

### Listing 17.2

#### The singleton factory method

```
+(MyClass *)sharedInstance;
{
    @synchronized(self)
    {
        if(!instance)
            [[self alloc] init];
    }
    return instance;
}
```

This method is declared as a class method so that it can be accessed from the class itself. When it's called, it first checks to see if the instance variable has been initialized. If it has not, then it initializes the instance variable. Finally, it returns the global instance.

The place where the actual initialization of the global instance variable occurs is in the +allocWithZone: method, which is ultimately what's called when you call the last method +alloc. This method is shown in Listing 17.3.

### Listing 17.3

#### Initializing the global instance

```
+(id)allocWithZone:(NSZone *)inZone;
{
    @synchronized(self)
    {
        if(!instance)
        {
            instance = [super allocWithZone:inZone];
```

```
return instance;
}
}
return nil;
}
```

Using this method rather than the factory method to verify and initialize the global instance ensures that even if someone attempts to create an instance of your singleton using the standard +alloc and -init methods, they will still receive the global instance and not a new copy.

You should implement some methods in order to ensure the safety of the global instance. For example, you should also implement the method -copyWithZone:. This method is called when your object receives a call to the method -copy. Normally, this is expected to make a copy of your object as well as all of its attributes. By overriding this method, you can instead simply return yourself, or in other words, since it would only ever be called on the global instance, you are in fact simply returning a pointer to the global instance. Listing 17.4 shows how you would implement this method.

### Listing 17.4

#### Implementing -copyWithZone:

```
-(id)copyWithZone:(NSZone *)inZone;
{
    return self;
}
```

In a non-garbage collected, retain count memory model, you should also override the appropriate methods to prevent your global instance from being released. Therefore, you need to override the methods -retain, -retainCount, -release, and -autorelease. Each of these should be overridden with the intent to prevent your object from being retained, or released. You will only ever have one instance of this object, and it should only ever have a retain count of one

Listing 17.5 also shows all four of these methods as they should be implemented on a singleton.

### Listing 17.5

#### Implementing memory management methods

```
- (id)retain;
{
    return self;
}

- (unsigned)retainCount;
{
    return NSUIntegerMax;
}

- (void)release;
{
    // empty
}

- (id)autorelease;
{
    return self;
}
```

Essentially, each of these methods is being overridden to do simply nothing. Once you’ve implemented your singleton, to use it, you simply use the global factory method. The first time you access it, the global instance will be initialized. All subsequent calls to the factory method will return that original instance. Because you’ve overridden all of the memory management methods, any attempt to retain or release that object will simply do nothing.

### NOTE

The methods described here for implementing a singleton in Objective-C are what I would call the “safe” methods. In other words, if you are distributing your code to third parties who might misuse your singleton, the techniques shown here are the safest. In the discussion section on this design pattern, I will also show you a shortcut “unsafe” version, which you can also use at your discretion.

### Discussion

Foundation, Cocoa, Cocoa Touch, and many other frameworks that are used in conjunction with Objective-C make extensive use of singletons. Most often, these are used in cases where the object in question is encapsulating access to a resource for which there can only ever be one instance of it. For example, the NSNotificationCenter has a singleton at its heart. Similarly, in Cocoa Touch the UIApplication, for which there is only ever one application that you might be running in, also has a singleton.

Singletons are one of the most powerful and most commonly used design patterns. They are often used in places where developers might be tempted to use a global variable. The advantages of the singleton over a global variable are that the singleton allows you better control over exactly when the global instance is created, and also insures that there can only ever be one global instance. Without Singletons, it might be possible for some part of your application to reinitialize the global instance. Singletons prevent that.

The technique that I showed you previously for creating a singleton is considered to be the “safe” technique. If you are a developer of a library for third-party consumption, or if you are working on a team where you cannot be certain that users of your API will understand that your object is a singleton and that it does not need to be released or retained and so on, I recommend using this technique for your singletons.

However, if you are a solo developer developing your code for yourself, and you feel confident in the fact that you know better than to release your Singleton prematurely, then a simpler version of the singleton pattern is shown in Listing 17.6.

### Listing 17.6

#### The cheaters version of a singleton

```
static MyClass *instance = nil;

+(id)sharedInstance;
{
    if(!instance)
    {
        instance = [MyClass new];
    }
    return instance;
}
```

This is really all you need to do to implement an unsafe singleton. All the other methods that I described are really there to prevent you from hurting yourself with your own code. Some things that are notably absent here are things such as, overriding the memory management methods, thread safety, and so on. The key here is that you have to know as a user of this singleton that it is, in fact, a singleton and must not be released or retained. Additionally, you need to be sure that when you are initializing your global instance that you are doing it before you launch any external threads. Although reading the contents of the instance variable from multiple threads at once is safe, it would not be safe to write to it. Therefore, you need to make sure that your first access to the shared instance method is done prior to the creation of any threads that might need to access the global instance.
