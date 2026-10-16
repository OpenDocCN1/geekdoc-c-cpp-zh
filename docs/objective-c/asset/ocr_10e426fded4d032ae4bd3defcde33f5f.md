# Listing 9.3 (continued)

```
[[NSUserDefaults standardUserDefaults] setObject:someValue forKey:THE_KEY];

// do stuff...

NSString *theValue = [[NSUserDefaults standardUserDefaults] stringForKey:THE_KEY];

[pool drain];
return 0;
}
```

As you can see, at the top of this new source listing we are defining a macro called THE_KEY. This macro is being defined to be @ "MY_IMPORTANT_DATA" . Everywhere in the subsequent code where the words THE_KEY are located will be replaced with the string @ "MY_IMPORTANT_DATA" when the program is compiled. This will happen transparently as part of the compilation process but the end result is that this code, when compiled, will actually wind up being exactly the same as the listing that we saw previously. The only difference is that when you are writing the source code you can take advantage of Xcode’s built-in code completion, and the compiler will detect if you have any instances of THE_KEY that were typed incorrectly. For example, if you accidentally wrote THE_KEY instead of THE_KEY, the compiler can check for that condition and issue an error.

Listing 9.4 shows another example where the program is taking different actions depending on whether the given macro value (DEBUGGING) is defined.

# Listing 9.4

# Optional compilation based on a macro

```
#import <Foundation/Foundation.h>

#define DEBUGGING 1

int main (int argc, const char * argv[])
{
    NSAutoreleasePool * pool = [[NSAutoreleasePool alloc] init];
#ifde f DEBUGGING
```