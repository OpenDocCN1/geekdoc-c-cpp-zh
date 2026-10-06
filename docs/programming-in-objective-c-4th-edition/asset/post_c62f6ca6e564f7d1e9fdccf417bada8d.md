
```objc
-(NSString *) substringToIndex:i
-(NSComparator *) caseInsensitiveCompare:nsstring
-(NSComparator *) compare:nsstring
-(BOOL) hasPrefix:nsstring
-(BOOL) hasSuffix:nsstring
-(BOOL) isEqualToString:nsstring
-(NSString *) capitalizedString
-(NSString *) lowercaseString
-(NSString *) uppercaseString
-(const char *) UTF8String
-(double) doubleValue
-(float) floatValue
-(NSInteger) integerValue
-(int) intValue
```

Returns a substring from the start of the string up to the character at index i
Compares two strings, ignoring case
Compares two strings
Tests whether a string begins with nsstring
Tests whether a string ends with nsstring
Tests whether two strings are equal
Returns a string with the first letter of every word capitalized (and the remaining letters in each converted to lower case)
Returns a string converted to lower case
Returns a string converted to upper case
Returns a string converted to a UTF-8 C-style string
Returns a double precision point representation of the string
Returns a floating point representation of the string
Returns an NSInteger representation of the string
Returns the integer representation of the string

In Tables 15.2 and 15.3, url is an NSURL object, path is an NSString object specifying the path to a file, nsstring is an NSString object, i is an NSInteger value representing a valid character number in a string, enc is an NSStringEncoding object that specifies the character encoding, err is an NSError object that describes an error if one occurs, size and opts are NSIntegers, and range is an NSRange structure indicating a valid range of characters within a string.

The methods in Table 15.3 either create or modify NSMutableString objects.

## Table 15.3. Common NSMutableString Methods

| Method | Description |
| --- | --- |
| +(id) stringWithCapacity: size | Creates a string initially containing size characters. |
| -(id) initWithCapacity: size | Initializes a string with an initial capacity of size characters. |
| -(void) setString: nsstring | Sets a string to nsstring. |
| -(void) appendString: nsstring | Appends nsstring to the end of the receiver. |
| -(void) deleteCharactersInRange: range | Deletes characters in a specified range. |
| -(void) insertStringAtIndex: i | Inserts nsstring into the receiver starting at index i. |
| -(void) replaceCharactersInRange: range: nsstring | Replaces characters in a specified range with nsstring. |

NSString objects are used extensively throughout the remainder of this text. If you need to parse strings into tokens, you can take a look at Foundation’s NSCanner class.

## Array Objects

A Foundation array is an ordered collection of objects. Most often, elements in an array are of one particular type, but that’s not required. Just as mutable and immutable strings, there are mutable and immutable arrays. Immutable arrays are handled by the NSArray class, whereas mutable ones are handled by NSMutableArray. The latter is a subclass of the former, which means it inherits its methods.

Program 15.6 sets up an array to store the months of the year and then prints them.

## Program 15.6

```objc
#import <Foundation/Foundation.h>

int main (int argc, char * argv[])
{
    int i;
    @autoreleasepool {
        // Create an array to contain the month names
        NSArray *monthNames = [NSArray arrayWithObjects:
            "@January", "@February", "@March",
            "@April", "@May", "@June", "@July", "@August",
            "@September", "@October", "@November", "@December",
            nil];

        // Now list all the elements in the array
        NSLog("@@Month Name: =====");

        for (i = 0; i < 12; i++) {
            NSLog("@%2i %@", i + 1, [monthNames objectAtIndex: i]);
        }
    }
    return 0;
}
```

## Program 15.6. Output

| Month Name | |
|---|---|
| 1 | January |
| 2 | February |
| 3 | March |
| 4 | April |
| 5 | May |
| 6 | June |
| 7 | July |
| 8 | August |
| 9 | September |
| 10 | October |
| 11 | November |
| 12 | December |

You can use the class `arrayWithObjects:` to create an array with a list of objects as its elements. In such a case, the objects are listed in order and are separated by commas. This is a special syntax used by methods that can take a variable number of arguments. To mark the end of the list, `nil` must be specified as the last value in the list—it isn't actually stored inside the array.

In `Program 15.6` `monthNames` is set to the 12 string values specified by the arguments to `arrayWithObjects:`.

Elements are identified in an array by their index numbers. Similar to `NSString` objects, indexing begins with zero. So an array containing 12 elements has valid index numbers 0–11. To retrieve an element of an array using its index number, you use the `objectAtIndex:` method.

The program simply executes a `for` loop to extract each element from the array using the `objectAtIndex:` method. Each retrieved element is displayed with `NSLog`.

## Program 15.7

```objc
#import <Foundation/Foundation.h>

int main (int argc, char * argv[])
{
    int i;
    @autoreleasepool {
        NSMutableArray *numbers = [NSMutableArray array];
        NSNumber *myNumber;

        // Create an array and add number objects
        for (i = 0; i < 10; i++) {
            myNumber = [NSNumber numberCreated:i];
            [numbers addObject:myNumber];
        }

        // Sequence through the array and display each element
        for (i = 0; i < numbers.count; i++) {
            NSLog("%@", [numbers objectAtIndex:i]);
        }

        // Display the entire array at once
        NSLog("==== a single");
        NSLog("%%@", numbers);
    }
    return 0;
}
```

## Program 15.7. Output

| Month Name | |
|---|---|
| 1 | 0 |
| 2 | 1 |
| 3 | 2 |
| 4 | 3 |
| 5 | 4 |
| 6 | 5 |
| 7 | 6 |
| 8 | 7 |
| 9 | 8 |
| 10 | 9 |
| ==== a single | [0, 1, 2, 3, 4, 5, 6, 7, 8, 9] |

## Note

How does NSLog know how to display the objects stored in the array? For each element in the array, NSLog will use the description method from the class the element belongs to. If it's the default method inherited from NSObject, you'll just get the object's class and address, as previously noted. In this case, however, you get a meaningful display—indicating there is a customized description method that has been implemented in the Number class.
