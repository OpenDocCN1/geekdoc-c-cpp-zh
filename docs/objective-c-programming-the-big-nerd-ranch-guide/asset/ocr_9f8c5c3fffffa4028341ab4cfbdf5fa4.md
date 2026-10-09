```
#import <Foundation/Foundation.h>
int main (int argc, const char * argv[])
{
    @autoreleasepool {
        NSLog(@"\u03c0 is %f", M_PI);
        NSLog(@"%d is larger", MAX(10, 12));
    }
    return 0;
}
```

MAX is not a function; it is a #define. The most basic C version of MAX is:
#define MAX(A, B)    ((A) > (B) ? (A) : (B))

So, by the time the compiler saw the line you just added, it looked like this:
NSLog(@"%d is larger", ((10) > (12) ? (10) : (12)));

When you use #define to do function-like stuff instead of simply substituting a value, you are creating a macro.

# Global variables

Instead of using #define, Objective-C programmers commonly use global variables to hold constant values.

Let's add to your program to explain. First, there is a class named NSLocale that stores information about different geographical locations. You can get an instance of the user's current locale and then ask it questions. For instance, if you wanted to know what the currency is in the user's locale, you could ask for it like this:

```
#import <Foundation/Foundation.h>
int main (int argc, const char * argv[])
{
    @autoreleasepool {
        NSLog(@"\u03c0 is %f", M_PI);
        NSLog(@"%d is larger", MAX(10, 12));

        NSLocale *here = [NSLocale currentLocale];
        NSString *currency = [here objectForKey:@"currency"];
        NSLog(@"Money is %@", currency);
    }
    return 0;
}
```

Build and run it. Depending on where you are, you should see something like

Money is USD

If, however, you mistype the key as @"Kuruncy", you won't get anything back. To prevent this problem, the Foundation framework defines a global variable called NSLocaleCurrencyCode. It isn't easier to type, but if you do mistype it, the compiler will complain. Also, code completion in Xcode works