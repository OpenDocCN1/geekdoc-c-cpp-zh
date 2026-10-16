
## NOTE

Be sure to remove the candidates array from your interface, if you are working off the project from the previous example.

## Listing 5.18

## Implementation file for the GCD version of PrimeFinder

```
#import "PrimeFinder.h"

@implementation PrimeFinder
@synthesize startedDate;
@synthesize endedDate;
@synthesize primes;
@dynamic elapsedTime;

-(void)dealloc
{
    [self setPrimes:nil];
    [self setStartedDate:nil];
    [self setEndedDate:nil];
    [super dealloc];
}

-(id)initWithMaxNumber:(NSUInteger)inMaxNumber
{
    if(self = [super init])
    {
        maxNumber = inMaxNumber;
    }
    return self;
}

-(void)start
{
    [self setStartedDate:[NSDate date]];

    NSMutableArray *result = [NSMutableArray array];

    dispatch_queue_t globalQueue = dispatch_get_global_queue(0, 0);
    dispatch_group_t group = dispatch_group_create();
    for(NSUInteger number = 2; number <= maxNumber; ++number)
{
dispatch_block_t isPrime = ^
{
for(NSUInteger n = 2; n < number; ++n)
if((number % n) == 0)
return;
@synchronized(result)
{
[result addObject:[NSNumber numberWithInteger:number]];
};
dispatch_group_async(group, globalQueue, isPrime);
}
dispatch_group_wait(group, DISPATCH_TIME_FOREVER);
[self setEndedDate:[NSDate date]];
[self setPrimes:result];
}
-(NSTimeInterval)elapsedTime
{
return [endedDate timeIntervalSinceDate:startedDate];
}
@end
```

In this code, the block in question is being specified to be of type dispatch_block_t, which is a special typedef provided by the Grand Central Dispatch functions for use in defining blocks to be passed to the GCD queues. The important thing to understand is that these are normal blocks just like you’ve been working with previously. The actual definition of the dispatch_block_t is shown in Listing 5.19 for your reference.

The definition of dispatch_block_t

```
typedef void (^dispatch_block_t)(void);
```

If you run this version of the program, you should see a substantial improvement in performance. On my computer, it shaves about 45 to 50 percent off the runtime involved in calculating the prime numbers. Your mileage will vary, of course.

## Summary

In this chapter, I introduced you to a powerful new tool in the Objective-C toolbox. Code blocks are incredibly useful in that they give you the ability to encapsulate small anonymous chunks of code and pass those chunks of code around as if they were objects. This gives you the ability to create generic methods that can be retooled with different functionality by simply passing new types of blocks to them as arguments. Additionally, blocks make working with Grand Central Dispatch incredibly simple because they provide you with the ability to express chunks of functionality and then send that functionality into a queue to be executed.

## Using Key Value Coding and Key Value Observing

The Objective-C runtime provides you with a variety of advanced tools for not just interacting with the operating system frameworks, but also for interacting with the attributes of your code. One tool available to you is the concept I cover in this chapter called Key Value Coding. Key Value Coding, or KVC as it is often referred to in Objective-C circles.

## Accessing Object Properties Using Key Value Coding

Key value coding gives you the ability to access attributes of your classes using a set of standardized accessor methods in addition to your normal setter and getters. You can use these accessor methods to get and set properties of your classes by specifying string identifiers that represent the names of the attributes you want to access. In addition to enabling you to access these attributes using these string identifiers, you can also access object relationships and sub objects by using a standardized syntax.

To give you an example of what I'm talking about, take a look at Listing 6.1

```
Some example classes.

@interface Bar : NSObject
{
    NSArray *array;
    NSString *stringOnBar;
}
```

## Listing 6.1

![](img/aaee977487e7a3eefe7b1dd596e0f6fb_182_0.png)

## Listing 6.1 (continued)

```
@property (retain, nonatomic) NSArray * array;
@property (retain, nonatomic) NSString * stringOnBar;
@end

@interface Foo : NSObject
{
    Bar *bar;
    NSString *stringOnFoo;
}
@property (retain, nonatomic) Bar * bar;
@property (retain, nonatomic) NSString * stringOnFoo;
@end
```

Given the two classes shown, as you can see, we have a class called Foo. This class has a string attribute, as well as another attribute defining a relationship between Foo and the class Bar. This relationship is defined by virtue of the bar property on Foo.

I've already shown you how by defining properties for the attributes of a given class, Objective-C gives you setters and getters for each of those properties. In addition to those standard setters and getters, it also provides you a set of Key Value Coding accessors as well.

The most commonly used of these key value coding accessors are the ones that enable you to access the attributes of a given class directly. These are the calls -valueForKey:, which allows you to read an attribute by specifying a parameter representing the name of the attribute you wish to access as a string, set -setValueForKey:, which allows you to set the value of a given attribute, also by specifying the name of the attribute as a string.

When working with more complicated relationships, where you want to access an attribute of an attribute, you can specify a more complex key path using dot notation. So, for example, if you have an object with an attribute of type Bar called bar, which additionally has an attribute called stringOnBar, you can use the method -valueForKeyPath:, specifying the dot notation path to the attribute, "bar.stringOnBar". Additionally, there's the -setValue:forKeyPath: method as well.

Again, looking at code may be the easiest way to describe what I'm talking about. The Objective-C runtime automatically generates for you code that enables you to read and write to the attributes of those classes by using the calls that I just talked about, as shown in Listing 6.2

## Listing 6.2

## Accessing the attributes of our classes using KVC accessors

```
Foo *foo = [[Foo alloc] init];
[foo setValue:@"blah blah" forKey:@"stringOnFoo"];
NSString *string = [foo valueForKey:@"stringOnFoo"];
[foo setValue:@"The quick brown fox." forKeyPath:@"bar.stringOnBar"];
NSString *string2 = [foo valueForKeyPath:@"bar.stringOnBar"];
```

So, as you can see, literally speaking, you can specify the name of the attribute that you want to access using a string, and you can read its value or you can write its value. You can even, as shown in the case where you are accessing the attributes of the Bar class, traverse a relationship between two objects and access the attributes of child objects of the primary object that you are accessing.

This may seem a bit confusing at first, and you may wonder why you need to know this. For most of your day-to-day coding, using Key Value Coding methods to set and access your properties probably will wind up being more typing, and more error-prone than simply accessing the setters and getters on your class directly. However, a small number of edge cases where being able to access these attributes dynamically, using values that can change at runtime rather than at compile time, can be incredibly powerful.

Listing 6.3 shows an example of a class that needs to serialize a pen object into a database table. In the first example shown, the serialization routine iterates over each of the fields of the table. As it iterates it needs a complex if statement to determine what accessor to call on the object that it is attempting to serialize so it can get the value to be serialized into the given field.

## Listing 6.3

## Serializing a table without KVC.

```
-(BOOL)serializeToTable:(Table *)inTable
{
    Row *row = [inTable addRow];
    for(Column *column in row)
    {
        if([[column name] isEqualToString:@"firstName"])
            [column setValue:[self firstName]];
```
