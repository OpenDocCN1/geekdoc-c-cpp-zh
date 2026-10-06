worry about the internal representation of the characters in your strings because the NSString class automatically handles this for you.1 By using the methods from this class, you can more easily develop applications that can be localized—that is, made to work in different languages around the world.

As you know, you create a constant character string object in Objective-C by putting the @ character in front of the string of double-quoted characters. So the expression

```
@@"Programming is fun"
```

creates a constant character string object. In particular, it is a constant character string that belongs to the class NSString.NSConstantString is a subclass of the string object class NSString.

# More on the NSLog Function

Program 15.2, which follows, shows how to define NSString object and assign an initial value to it. It also shows how to use the format characters %@ to display NSString object.

# Program 15.2

```
#import <Foundation/Foundation.h>

int main (int argc, char * argv[])
{
    autoreleasepool {
        NSString *str = @"Programming is fun";

        NSLog (@"%@", str);
    }
```