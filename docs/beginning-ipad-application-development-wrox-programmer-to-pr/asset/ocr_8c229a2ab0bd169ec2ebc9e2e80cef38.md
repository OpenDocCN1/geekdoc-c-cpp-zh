As an example, imagine that you want to test whether a string contains a valid email address. You can add an isEmail method to the NSString class so that you can call the isEmail method on any NSString instance, like this:

```
NSString *email = @"weimenglee@gmail.com";
if ([email isEmail]) {
    ...
}
```

To do so, you can simply create a new class file and code it as follows:

```
//---utils.h---
#import <Foundation/Foundation.h>

//---NSString is the class you are extending---
@interface NSString (stringUtils)

//---the method you are adding to the NSString class---
- (BOOL) isEmail;

@end
```

Basically, it looks the same as declaring a new class except that it does not inherit from any other class. The stringUtils is a name that identifies the category you are adding, and you can use any name you want.

Next, you need to implement the method(s) you are adding:

```
//---utils.m---
#import "Utils.h"

@implementation NSString (Utilities)

- (BOOL) isEmail {
    NSString *emailRegEx = @"(?... )";
    NSPredicate *regExPredicate = [NSPredicate predicateWithFormat:@"SELF MATCHES %@", emailRegEx];
    return [regExPredicate evaluateWithObject:self];
}

@end
```