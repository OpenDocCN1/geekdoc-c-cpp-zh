However, you used the @synthesize construct to implement them:

```
@synthesize productName, voltage;
```

Objective-C compiler trivia: When compiling for iOS or a 64-bit Mac OS X program, you don’t need to declare the instance variables. The @property/@synthesize calls are sufficient to make the space for the data.

Open up Appliances and comment out the instance variables in Appliance.h:

```
{
    // NSString *productName;
    // int voltage;
}
```

Rebuild and run the program.

In this book, we always declare the instance variables. It is a nice form of documentation and makes your code usable within 32-bit Mac OS X programs. Uncomment the instance variables.

# Property attributes

Now let’s take a closer look at the different attributes you can use to control how the accessors for a property will be created.

# Mutability

A property can be declared readwrite or readonly. The default is readwrite, which means that both a setter and a getter method are created. If you don’t want a setter method to be created, you mark the property as readonly:

```
@property (readonly) int voltage;
```

# Lifetime specifiers

A property can also be declared unsafe_unretained, strong, weak, or copy. This option determines how the setter handles its memory management.

unsafe_unretained is the default and the simplest: it just assigns the passed-in value to the property. Imagine this declaration and definition:

```
@property (unsafe_unretained) int averageScore;
// "@property int averageScore" would also work here
...
@synthesize averageScore;
```

This would result in a setter method that’s pretty much equivalent to:

```
- (void)setAverageScore:(int)d
{
    averageScore = d;
}
```

In Appliance, voltage is an unsafe, unretained property. You will always use unsafe_unretained for properties that hold non-objects.