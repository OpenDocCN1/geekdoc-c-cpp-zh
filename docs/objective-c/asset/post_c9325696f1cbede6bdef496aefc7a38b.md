
## Listing 6.3
(continued)

```
else if([[column name] isEqualToString:@"lastName"])
    [column setValue:[self lastName]];
else if([[column name] isEqualToString:@"age"])
    [column setValue:[self lastName]];
else if([[column name] isEqualToString:@"birthDate"])
    [column setValue:[self lastName]];
...
}
[row save];
}
```

This code is going to get hairy pretty quickly. Now take a look at the same code using the key value coding method. Listing 6.4 shows the updated code.

## Listing 6.4
### Serialize method using KVC

```
-(BOOL)serializeToTable:(Table *)inTable
{
    Row *row = [inTable addRow];
    for(Column *column in row)
    {
        [column setValue:[self valueForKey:[column name]]];
    }
    [row save];
}
```

As you can see, the new version isn’t just smaller in terms of lines of code, but it’s also more resilient and flexible. As you add new columns to the table, you need only additionally add attributes to this object to store the values for those fields. This serialize method automatically extracts those values from the attributes and stores them for us without any changes to this method whatsoever. Again, the serialize method isn’t something that you’re going to use everywhere in your code. I want to stress that. Using KVC accessors instead of normal accessors is

usually more code than you need. But in these kinds of conditions it enables you to write code that is more dynamic and also enables you to reduce the number of places in your code where you have to represent the information about the attributes of your objects. When you can query an object about its attributes, you don’t have to commit that information to as many places in code. That’s always a good thing — the most bug-free code is code that isn’t written.

## Working with key paths

In order to use key value coding, you must first figure out which key paths you can construct and what you can access with those key paths.

You can think of working with KVC accessors like using a dictionary. The keys to the dictionary are strings. The strings themselves are the names of the attributes on the object on which you are operating. Because of this requirement, a certain number of rules have to be followed in terms of your key and thus attribute naming. First, your keys must use ASCII encoding. This means that you cannot have keys that use unusual characters that would not normally be usable in an attribute name. Secondly, your keys must begin with a lowercase letter. Underscores are also allowed for this first letter, but no numbers, and no uppercase. Finally, your key cannot contain any whitespace.

Thankfully, because the attribute that you’re accessing has to be a valid symbol name anyway, most of these rules are rules that you are probably already following in the first place.

Listing 6.5 shows some examples of valid key paths and invalid key paths.

## Listing 6.5
### Valid and invalid key paths.

// valid
[foo valueForKeyPath:@"someMember"];
[foo valueForKeyPath:@"someMember.someAttributeOnMember"];
[foo valueForKeyPath:@"someOtherMember"];

// invalid
[foo valueForKeyPath:@"4fun"];
[foo valueForKeyPath:@"kermit the frog"];
[foo valueForKeyPath:@"SomethingWickedThisWayComes"];
[foo valueForKeyPath:@"THISWONTWORK"];
[foo valueForKeyPath:@"thisAlsoWon'tWork"];

As I discuss earlier, you can traverse relationships between objects and access attributes on sub objects by using a key path. A key path is the key in which the relationships between different objects are spanned by using dots, as in the example above @"someMember.someAttributeOnMember". The key path accesses the someMember attribute on the foo object, finds the someAttributeOnMember attribute on whatever class someMember is, and it returns the value stored there. A variety of syntactical sugar has been provided in the specification of these key paths. In addition to being able to traverse these relationships, you can even access functions that operate on collections of objects, such as their count, and so on. For example, Listing 6.6 shows some of the built-in functions that you can use as part of these key paths.

## Listing 6.6
### Using functions inside key paths.

```
[anArrayOfProducts valueForKeyPath:@"@avg.price"];
[anArrayOfProducts valueForKeyPath:@"@sum.cost"];
[store valueForKeyPath:@"products.@count"];
```

Functions operate only on arrays and sets of objects. In the example, the first two lines are accessing product objects. Those products have attributes, such as price and cost. The functions given take the values specified for the attributes on each object in the array and then perform the specified function on those values. In other words, the first item iterates over each of the items in the array of products, collects the price from each of those products, and then averages them.

The syntax for using these functions consists of prefixing the name of the function with the @ sign, then the name of the function, a "." and then the attribute on which to operate. The one exception to the requirement for the attribute on which to operate is the "@count" function, which simply returns the count of items in the collection.

Table 6.1 shows a list of these functions.

| Function | Purpose |
|---|---|
| @avg | Returns the average of all elements of the array or set. |
| @count | Returns the count of elements in the array or set. |
| @max | Returns the max value of all of the elements in the array or set. |
| @min | Returns the minimum value of all of the elements in the array or set. |
| @sum | Returns a sum of all of the values of all of the elements in the array or set. |
| @unionOfArrays/@distinctUnionOfArrays | Given a collection of arrays returns an array containing all of the arrays in the collection. In the case of the distinct version, it returns only unique arrays. |
| @unionOfSets/@distinctUnionOfSets | Given a collection of sets returns a set containing all of the sets together. In the case of the distinct version, it returns only unique sets. |
| @unionOfObjects/@distinctUnionOfObjects | Given a collection of sets or arrays, returns all of the elements of all of the collections as a single array. The distinct version returns only unique elements. |

## Writing KVC compliant accessors

The Objective-C runtime accomplishes all of this magic partially through capabilities of the underlying frameworks and partially thanks to coding style conventions. Although the Objective-C runtime does the heavy lifting as far as the functionality of KVC, it relies upon you, the developer, to write accessors for your properties that follow specific conventions so that it can retrieve and set values by using KVC.

The KVC standard for setters and getters is to use setters that follow a pattern of set<Value>: and getters that follow the pattern of simply <value>. In both of these cases, the <value> part of the pattern should be replaced with the name of the property that you are accessing. This property should be a member variable whose name is specified using camel case.

> NOTE
> The term camel case refers to a standard for variable naming in which the words in a variable are packed together into one long string. In this string, the first letter of each word, with the exception of the first word, is capitalized. For example, to write a variable name called "some variable name," you would write it as someVariableName. Notice, when looking at the variable name, that the capital letters in the inner part of the variable name resemble the hump on a camel. This is where it derives its name.

So, given a class definition as shown in Listing 6.7, you might write accessors as shown in Listing 6.7.

## Listing 6.7
### Class definition with member variables.

```
@interface MyClass : NSObject
{
    float x;
    float y;
    NSString *something;
}
```

## Listing 6.7 (continued)

```
}
-(void)setX:(float)inX;
-(void)setY:(float)inY;
-(void)setSomething:(NSString *)inSomething;
-(float)x;
-(float)y;
-(NSString *)something;
@end
```

KVC compliant accessors.

```
@implementation MyClass
-(void)setX:(float)inX;
{
    x = inX;
}

-(void)setY:(float)inY;
{
    y = inY;
}

-(void)setSomething:(NSString *)inSomething;
{
    NSString *oldValue = something;
    something = [inSomething retain];
    [oldValue release];
}

-(float)x;
{
    return x;
}

-(float)y;
{
    return y;
}

-(NSString *)something;
{
    return something;
}

@end
```
