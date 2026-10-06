
self A variable used inside a method to refer to the receiver of the message.

set An unordered collection of unique objects implemented under Foundation with the NSSet, NSMutableSet, and NSCountedSet classes.

setter method An accessor method that sets the value of an instance variable. See also getter method.

statement One or more expressions terminated by a semicolon.

statement block One or more statements enclosed in a set of curly blocks, and their scope is limited to that block.

static function A function declared with the static keyword that can be called only by other functions or methods defined in the same source file.

static typing Explicitly identifying the class to which an object belongs at compile time. See also dynamic typing.

static variable A variable whose scope is limited to the block or module in which it is defined. Static variables have default initial values of 0 and retain their values through method or function invocations.

structure An aggregate data type that can be assigned to other structures, of varying types. passed as arguments to functions and methods, and returned by them as well.

subclass Also known as a child class, a subclass inherits the methods and instance variables from its parent or superclass.

super A keyword used in a method to refer to the parent class of the receiver.

super class The parent class of a particular class. See also super.

synthesized method A setter or getter method that the compiler automatically creates for you. It was added to the Objective C 2.0 language.

UIKit A framework for developing applications for iOS devices. In addition to providing classes for working with usual UI elements such as windows, buttons, and labels, it defines classes for dealing with device-specific features such as the accelerometer and the touch interface. UIKit is part of Cocoa Touch.

Unicode character A standard for representing characters sets containing up to millions of characters. The NSString and NSMutableString classes work with strings containing Unicode characters.

union An aggregate data type, such as a structure containing members that share the storage area. Only one of those members can occupy the storage area at any point in time.

Xcode A compiling and debugging tool for program development with Mac OS X and iOS.

XML Extensible Markup Language. The default format for property lists generated on Mac OS X.

zone A designated area of memory for allocating data and objects. A program can work with multiple zones to more efficiently manage memory.

## Appendix B. Address Book Application Source Code

For your reference purposes, here are the complete interface and implementation files for the address book example you worked with throughout Part II. "The Foundation Framework." This includes the definitions for the AddressCard, and AddressBook classes. You should implement these classes on your system; then extend the class definitions to make them more practical and powerful. This is an excellent way for you to learn the language and become familiar with building programs, working with classes and objects, and working with the Foundation framework.

## AddressCard Interface File

```objc
#import <Foundation/Foundation.h>

@interface AddressCard : NSObject <NSCopying, NSCCoding>

@property (nonatomic, copy) NSString *name, *email;

-(void) setName:(NSString*) theName andEmail:(NSString*) theEmail;
-(void) assignName:(NSString *) theName andEmail:(NSString *) theEmail;
-(NSComparisonResult) compareNames:(id) element;

-(void) print;

@end
```

## AddressBook Interface File

```objc
#import <Foundation/Foundation.h>
#import "AddressCard.h"

@interface AddressBook: NSObject <NSCopying, NSCoding>

@property (nonatomic, copy) NSString *bookName;
@property (nonatomic, strong) NSMutableArray *book;

- (id) initWithName:(NSString *) name;
- (void) sort;
- (void) addCard:(AddressCard *) theCard;
- (void) sortCard;
- (void) removeCard:(AddressCard *) theCard;
- (int) entries;
- (void) list;
- (AddressCard *) lookup:(NSString *) theName;

@end
```

## AddressCard Implementation File

```objc
#import "AddressCard.h"

@implementation AddressCard

@synthesize name, email;

-(void) setName: (NSString *) theName andEmail:
(NSString *) theEmail
{
    self.name = theName;
    self.email = theEmail;
}

// Compare the two names from the specified address cards
-(NSComparisonResult) compareNames: (id) element
{
    return [name compare: [element]];
}

-(void) print
{
    NSLog("@===============================================");
    NSLog("@| (@| %-31s |", [name UTF8String]);
    NSLog("@| %-31s |", [email UTF8String]);
    NSLog("@|                               |");
    NSLog("@|                               |");
    NSLog("@|                               |");
    NSLog("@|               O               O               |");
    NSLog("@===============================================");
}

    return self;
}
@end
```

## AddressBook Implementation File

```objc
#import "AddressBook.h"

@implementation AddressBook

@synthesize book, bookName;

// set up the AddressBook's name and an empty book

-(id) initWithName:(NSString *) name {
    self = [super init];

    if (self) {
        bookName = [NSString stringWithWithString:name];
        book = [NSMutableArray array];
    }

    return self;
}

-(id) init {
    return [self initWithName:@""];
}

// Write our own setter to create a mutable copy

-(void) setBook:(NSArray *) theBook
{
    book = [theBook mutableCopy];
}

-(void) sort
{
    [book sortUsingSelector:@selector(compareNames)];
}

// Alternate sort using blocks
-(void) sort2
{
    [book sortUsingComparator:^(id obj1, id obj2) {
      return [[obj1 name] compare:[obj2 name]];
    }];
}

-(void) addCard:(AddressCard *) theCard
{
    [book addObject:theCard];
}

-(void) removeCard:(AddressCard *) theCard
{
    [book removeObjectIdenticalTo:theCard];
}

-(int) entries
{
    return [book count];
}

-(void) list
{
    NSLog("%======= Contents of: %@", bookName);

    for ( AddressCard *theCard in book ) {
        NSLog("%-32s %-32s", [theCard.name UTF8String], [theCard.email UTF8String]);
    }
    NSLog("=================================================");
}

-(id) initWithCoder:(NSCoder *) decoder
{
    bookName = [decoder decodeObject:@"AddressName"];
    book = [decoder decodeObject:@"AddressBook"];

    return self;
}

// Method for NSCopying protocol

-(id) copyWithZone:(NSZone *) zone
{
    id newBook = [[self class] allocWithZone:zone] init;

    [newBook setBookName:bookName];

    // The following will do a shallow copy of the address book
    [newBook setBook:book];

    return newBook;
}
@end
```

## Footnotes

## Chapter 13

- Technically speaking, its defined in the file NSObjRuntime.h, which is imported from inside the file Foundation.h
- Note the use of the strings "A string to be copied." and "So is this." in the program. These are not string objects, C-style character strings, as distinguished by the fact that an @ character does not precede the string. If a function expects an array of char as an argument, you may pass it an array of type char or a literal C-style character string, but not a character string object.

## Chapter 15

- Currently, unichar characters occupy 16 bits, but the Unicode standard provides for characters larger than that size. So in the future, unichar characters might be larger than 16 bits.
- Mac OS and iOS provide an entire Address Book framework offers extremely powerful capabilities for working with address books.
- You might also want an initWithName:andEmail: initialization method, but we don't show that here.
- A method called sortUsingFunction:context lets you use a function instead of a method to perform the comparison.
