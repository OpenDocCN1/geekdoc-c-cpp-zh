
# Chapter 15 Numbers, Strings, and Collections

A similar discussion applies to using numberWithUnsignedInt: versus numberWithUnsignedInteger:

You'll encounter NSNumber objects in programs throughout the remainder of this chapter. You may want to look at the documentation for the NSDNumber class before moving to the next section. That class is a subclass of NSNumber and provides methods for doing arithmetic with numbers at the object level.

# String Objects

You've encountered string objects in your programs before. Whenever you enclosed a sequence of character strings inside a pair of double quotes, as in

```
"Programming is fun"
```

you created a character string object in Objective-C. The Foundation framework supports a class named NSString for working with string objects. C-style strings consist of char characters, NSString objects consist of unichar characters. A unichar character is a multibyte character according to the Unicode standard. This enables you to work with character sets that contain literally millions of characters. Luckily, you don't have to worry about the internal representation of your strings since the NSString class automatically handles this for you. By using the methods from this class, you can more easily develop applications that are localized—that is, made to work in different languages around the world.

As you know, you create a constant string object in Objective-C by putting the @ in front of the string of double-quoted strings. The expression

```
"Programming is fun"
```

creates a constant character string object. In particular, it is a constant character string that belongs to the class NSConstantString. NSConstantString is a subclass of the string object class NSString.

# More on the NSLog Function

Program 15.2, which follows, how to define an NSString object and assign an initial value to it. It also shows how to use the formatters %@ to display an NSString object.

Program 15.2

```
#import <Foundation/Foundation.h>

int main (int argc, char *argv[]) {

[AutoreleasePool pool = [AutoreleasePool alloc] init];
```

> Currently, unichar characters occupy 16 bits, but the Unicode standard provides for characters larger than that size. So in the future, unichar characters might be larger than 16 bits. The bottom line is to never make an assumption about the size of a Unicode character.

```
NSString *str = @"Programming is fun";

NSLog("@%@", str);

[pool drain];
return 0;
}
```

# Program 15.2 Output

Programming is fun

In the line

```
NSString *str = @"Programming is fun";
```

the constant string object Programming is fun is assigned to the NSString variable str.
Its is then displayed using NSLog.
The NSLog format characters %@ can be used to display not just NSString objects,
other objects as well. For example, given the following

```
NSNumber *intNumber = [NSNumberWithInteger:100];
```

the NSLog call

```
NSLog("@%@", intNumber);
```

produces the following output:

100

# The description Method

You can also use the %@ format characters to display the entire contents of arrays, dictionaries, and sets. In fact, they can be used to display objects from your own classes as well, as long as you override the description method inherited by your class. If you don't override the method, NSLog simply displays the name of the class it belongs to and the address of the object in memory.That's the default implementation for the description method that is inherited from the NSObject object.

Following is an example of a description method that you could add to your Fraction class implementation section to have it format a Fraction object. This uses NSString's stringWith: method; a method that resembles NSLog but, unlike the function, the purpose of this method is to return the formatted string as the result, rather than writing it to the console:

```
-(NSString *) description
{
    return [NSString stringWithFormat:@"%i/%i", numerator, denominator];
}
```

# Chapter 15 Numbers, Strings, and Collections

# Note

Methods such as stringWithFormat allow a variable number of arguments to be provided (in the format string and the data to be formatted). Such arguments are provided to the method as a comma-separated list of values.

With this method defined in your Fraction class (statements and with Fraction objects f1 and f2 set appropriately), you could then write statements like the following in your program:

```
sum = [f1 add: f2];
```

```
NSLog("The sum of %@ and %@ is %@", f1, f2, sum);
```

to get a single line of output like this:

The sum of 1/2 and 1/4 is 3/4

Adding your own description method to your classes is a good debugging tool—allows you to display your objects in a meaningful way.

# Mutable Versus Immutable Objects

you create an object whose contents cannot be changed. This is referred to as an immutable object. The NSString class deals with immutable strings. Frequently, you'll want to deal with strings you can change. For example, you might want to delete some characters from a string or perform a search-and-replace operation on a string. These types of strings are handled by the NSMutableString class.

Program 15.3 shows basic ways to work with immutable character strings in your programs.

15.3

// Basic String Operations

```
#import <Foundation/Foundation.h>
```

```
int main (int argc, char *argv[]) {
    NSAutoreleasePool *pool = [NSAutoreleasePool alloc];
    NSString *str1 = @"This is string A";
    NSString *str2 = @"This is string B";
    NSString *res;
    NSComparisonResult compareResult;

// Count the number of characters
    NSLog("Length of str1: %lu", [str1 length]);

// Copy one string to another
    res = [NSString stringWithString:str1];
    NSLog("copy: %@", res);
}
```

```
// Copy one string to the end of another
str2 = [str1 stringByAppendingString: str2];
NSLog(["@Concatenation: %@", str2]);

// Test if 2 strings are equal
if ([str isEqualToString: res] == YES)
NSLog(["@str1 == res\]);
else
NSLog(["@str1 != res\]);

// Test if one string is <, or > than another
compareResult = [str1 compare: str2];

if (compareResult == NSOrderedAscending)
NSLog(["@str1 < str2\]);
else if (compareResult == NSOrderedSame)
NSLog(["@str1 == str2\]);
else // must be NSOrderedDescending
NSLog(["@str1 > str2\]);

// Convert a string to uppercase
res = [str1 uppercaseString];
NSLog(["@Uppercase conversion: %@", [res UTF8String]]]);

// Convert a string to lowercase
res = [str1 lowercaseString];
NSLog(["@Lowercase conversion: %@", res]);

NSLog(["@Original string: %@", str1]);

[pool drain];
return 0;
```

# Program 15.3 Output

Length of str1: 16
Copy: This is string A
Concatenation: This is string AThis is string B
str1 = res
str1 < str2
Uppercase conversion: THIS IS STRING A
Lowercase conversion: this is string a
Original string: This is string A

Program 15.3 declares three immutable NSString objects: str1, str2, and res.
The first two are initialized to constant character string objects. The declaration

NSComparisonResult compareResult to hold the result of the string comparison that will be performed later in the program.

# Chapter 15 Numbers, Strings, and Collections

You can use the length method to count the number of characters in a string. It returns an unsigned integer value of type NSUInteger.The output verifies that the string @"This is string A

contains 16 characters. The statement

```
res = [NSString stringWithString:str];
```

shows how to create a new string with the contents of another. The resulting NSString object is assigned to res and is displayed to verify the results. An actual copy of the string contents is made here, not just another reference to the same string in memory.That str and str2 refer to two different objects, which is different from simply performing a simple assignment like this:

```
res = str;
```

As we have previously discussed, this statement would simply create another reference to the same object in memory.

The stringByAppendingString: method can join two string characters. So the expression

```
[str stringByAppendingString:str2];
```

creates a new string object that contains the characters str1 followed by str2, returning the result. The original string objects, str1 and str2, are not affected by this operation (they can't be because both are immutable strings).

The isEqual: method is used in the program to test whether two character strings are equal—that, if they contain the same characters. You can use the compare: method if you need to determine the ordering of two character strings—for example, if you wanted to sort an array of them. Similar to the method you used for comparing NSNumber objects, the result of comparison is NSOrderedAscending if the first string is lexicographically less than the second, NSSame if the two strings are equal, and NSOrderedDescending if the first string is lexicographically greater than the second.
