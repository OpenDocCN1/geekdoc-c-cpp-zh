When we speak mutable versus immutable string objects, we talk about changing the actual characters within the string. Either a mutable or an immutable string object can always be set to a completely different string object during execution of the program. This was stressed in the discussion of Program 15.3. So, for example, consider the following:

```
str1 = @"This is a string"
...
str1 = [str1 substringFromIndex: 5];
```

In this case, str1 is first set to a constant character string object. Later in the program, it is set to a substring. In such a case, str1 could be declared as either a mutable or an immutable string object. Be sure you understand this point.

Program 15.5 shows some ways to work with mutable strings in your programs.

# Program 15.5

```
// Basic String Operations - Mutable Strings

#import <Foundation/Foundation.h>

int main (int argc, char * argv[]) {
    @autoreleasepool {
        NSString *strl = @"This is string A"
        NSString *search, *replace;
        NSMutableString *mstr;
        NSRange substr;

    // Create mutable string from nonmutable
```