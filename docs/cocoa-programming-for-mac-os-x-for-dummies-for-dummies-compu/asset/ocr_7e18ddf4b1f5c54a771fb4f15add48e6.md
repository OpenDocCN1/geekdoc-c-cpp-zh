Then when you want to display the name, you ask the Driver instance for it with the firstName method:

```
- (NSString *)firstName;
```

The @end marks the end of the Driver class declaration.

# Implementing the class

Click the Driver.m file to reveal its code. To this file, add the following code:

```
@implementation
-(int)go:(BOOL)distance {
  if (distance)
    return 10;
  else
    return 5;
}

-(NSString *)firstName {
  return firstName;
}

-(void)setName:(NSString *)name {
  [name retain];
  [firstName release];
  firstName = name;
}

-(void)dealloc {
  [firstName release];
  [super dealloc];
}

@end
```

Here's how the code works:

+   - This code begins by importing the Driver.h interface, where the declaration of your Driver class resides.
- The code then defines the methods for that class. All methods appear within the @implementation and @end lines.
- As you know from the header file, this class has three methods. The go method returns a value of 5 or 10 based on the distance parameter.