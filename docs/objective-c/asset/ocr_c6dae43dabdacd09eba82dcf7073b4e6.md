# Listing 9.10

# A macro to print the value of a variable

```
#define LOGVAR(var) NSLog(@"%s: %@", #var, var);
```

The key here is to prefix the variable name itself with a # symbol. This invokes the stringification.

If you use this macro in an application as shown in Listing 9.11, you can see that it will first print the name of the variable, and then it will print the value of that variable.

# Listing 9.11

# Using a macro to print the value of a variable

```
#import <Foundation/Foundation.h>

#define LOGVAR(var) NSLog(@"%s: %@", #var, var);

int main (int argc, const char * argv[])
{
    NSAutoreleasePool * pool = [[NSAutoreleasePool alloc] init];

    NSString *someVar = @"This is the value.";

    LOGVAR(someVar);

    [pool drain];
    return 0;
}
```

The LOGVAR(someVar) line gets expanded to something like Listing 9.12.