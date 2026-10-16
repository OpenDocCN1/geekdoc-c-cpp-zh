After you have created the place to store your global instance, you need to provide global access to that instance through a factory method which checks for the existence of the instance, and if it does not exist creates it. This is shown in Listing 17.2.

# Listing 17.2

# The singleton factory method

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

# Listing 17.3

# Initializing the global instance

```
+(id)allocWithZone:(NSZone *)inZone;
{
    @synchronized(self)
    {
        if(!instance)
        {
            instance = [super allocWithZone:inZone];
```