
Typically, you would only need to do this in cases where you did not specify the type of the protocol as part of the datatype for the variable in question. If you had specified the protocol is part of the datatype for the variable then the compiler would have flagged this variable for you if it did not implement the protocol required.

## NOTE

The -conformsToProtocol: method shown in Listing 7.6 only works with formal protocols. If you're using an informal protocol, use the NSObject method -respondsToSelector: as shown in Listing 7.7 instead.

Even when you are certain that a given object implements a given protocol, there is still the possibility that the object may not implement any of the optional methods of the protocol.

Remember, if an object does not implement an optional method and you call that method on that object, then your application will crash. Therefore, you need a way to determine if that object actually implements an optional method before you attempt to call it.

Fortunately, NSObject, which all objects inherit from, has a method which does exactly this. This method is -respondsToSelector: and it takes as a parameter a selector object.

Just like with the protocol object, a special directive can be used to convert a method signature into a selector object. That directive is the @selector() directive. Its use, along with the -respondsToSelector: method, is shown in Listing 7.7.

## Listing 7.7

## Testing to determine if an object implements an optional method

```
-(void)disconnected;
{
    if ([delegate respondsToSelector:@selector(networkConnectorDisconnected:)])
        [delegate networkConnectorDisconnected:self];

    // else implement some default behavior...
}
```

In this example, you first check to see if the object which implements the protocol in fact implements one of the optional methods using the call -respondsToSelector:. If it does, then it goes ahead and calls that method. If it does not, you can choose to either do nothing, or to implement some kind of default behavior instead.

## Avoiding Circular Protocol Dependencies

Protocols can refer to other protocols within their own declarations. For example, imagine a protocol which requires another protocol for use as a parameter to one of its methods, as shown in Listing 7.8.

## Listing 7.8

## A protocol requiring another protocol

```
@protocol Foo
- (void) someMethodRequiringBar: (id<Bar>) inBar;
@end
```

If the required protocol (Bar) also requires the original protocol (Foo), as shown in Listing 7.9, then a circular dependency is created between the two protocols. This generates a compiler error.

## Listing 7.9

## The Bar protocol, which requires the Foo protocol

```
@protocol Bar
- (void) someMethodRequiringFoo: (id<Foo>) inFoo;
@end
```

To resolve this problem, you can give a forward declaration of the required protocol which enables you to not include the file for the protocol that is required. For example, to prevent this circular dependency, you can add to the Bar.h interface file, the directive @protocol Foo; instead of importing the Foo.h file. This is shown in Listing 7.10.

## Listing 7.10

## A corrected version of the Bar protocol.

```
@protocol Foo;
@protocol Bar
- (void) someMethodRequiringFoo: (id<Foo>) inFoo;
@end
```

This occurrence is rare, but it’s important to know that you have this tool available to you if needed. By adding the @protocol Foo directive above the Bar protocol declaration, you are telling the compiler “Trust me, Foo is a protocol, and I’ll include it in my compilation, but I’m not importing the Foo.h here.”

## Exploring examples of protocol use

Protocols are used throughout Objective-C when working with application frameworks, such as Cocoa and Cocoa Touch. The biggest area of use is in delegation and datasource objects. Often, these are cases where the delegating object requires information at runtime that can’t be determined in a generic way, such as what columns to display in a given table view. Alternatively, they’re also used in cases where some process needs to happen in the background. You might call a method like -start, which returns immediately, and then receive a callback on a delegate protocol method telling you that the process has completed.

Just to give you an example of this in action, take a look at Listing 7.11. In this code, the application is creating an NSURLConnection, and firing it off. Later, as the data comes back from the URL request, it receives notice of that data via the protocol method -connection:didReceiveData:.

## Listing 7.11

## A class using an NSURLConnection and implementing the NSURLConnection delegate protocol methods

```
@implementation NetworkConnector
-(id)init
{
    if(self = [super init])
    {
        NSURL *url = [NSURL URLWithString:@"http://www.google.com"];
        NSURLRequest *req = [NSURLRequest requestWithURL:url];

        connection = [[NSURLConnection alloc] initWithRequest:req
            delegate:self startImmediately:YES];
    }
    return self;
}
// protocol methods
(void)connection:(NSURLConnection *)connection
    didReceiveData:(NSData *)inData
{
```

## Extending Existing Class Capabilities

No matter how well designed a class or framework is, inevitably, there will always be circumstances that you will encounter that the framework designer did not anticipate. Some developers go so far as to say that you should not plan for reusability in your code because at the end of the day, it is so difficult to achieve true universal reusability. I disagree with this notion, and I think that Objective-C provides some of the best tools for fostering reusability of any language available today.

In this chapter, I’m going to delve into some of the most powerful of those tools. While not completely unique to Objective-C, they are certainly examples of how the dynamism of Objective-C enables more flexibility and reuse than almost any other compiled language.

The technologies that I explain in this chapter center on the ability to extend the functionality of existing classes.

## Working with Third-Party Frameworks and Classes

If you’ve worked with any kind of programming frameworks at all in the past, you’ve probably run into a situation in which existing classes that are provided by the standard library of the language give you about 90 percent of the functionality that you’re looking for, but not the final 10 percent of the functionality that you really need. For example, you might have a string class, which doesn’t provide a regular expression search.

Because these frameworks are built by a third-party, usually you don’t have access to the source code of those frameworks. Because of this, changing the existing framework itself to add that additional 10 percent of functionality is not an option. Even in cases in which you do have access to the source code, it would be an extremely bad practice to have to distribute a modified, custom version of a standard library with your application.

![](img/aaee977487e7a3eefe7b1dd596e0f6fb_226_0.png)

Another option that you might consider, would be to inherit from the existing class, creating your own custom version of whatever class is that you need to change. By doing this, you could add whatever functionality you wanted to in your custom version of that class.

On the surface, this seems like it might be a good idea, and indeed, many new object oriented developers would jump on this opportunity as being the logical way to solve this problem. However, in practice, this actually leads to other problems. Specifically, other readers of your code may have difficulty grasping your intent. They might ask themselves why you created a custom string class. If you are only adding a few methods, creating a custom subclass is probably overkill.

The amount of confusion caused by your custom string class probably outweighs the benefit. Additionally, merging disparate subclasses from different code bases can be complicated and fraught with error. Imagine two different code bases with two slightly different subclasses of `NSString`. Imagine now that you want to use part of the functionality from the first code base and part of the functionality from the second code base. Aside from just the difficulty of merging the two `NSString` subclasses, if the two classes have different names then one or the other of the two code bases will have to be extensively edited in order to use the new, combined `NSString` class.

Metaphorically speaking, using subclasses in order to extend existing classes, in some cases, is akin to requiring that someone have a completely custom-built automobile delivered directly from the factory whenever the customer simply requires a different type of hubcaps.

I’m not trying to say that subclassing is inappropriate in all cases. In certain cases, subclassing is absolutely the right solution to a reusability problem. However, revisiting the object oriented development axiom that I mentioned in the last chapter, “favor composition over inheritance,” it’s easy to see that classes, when designed like automobiles, with reusable and replaceable parts, results in greater flexibility and greater customizability for anyone who has to reuse that class.

So, all that being said, let me introduce you to some parts of Objective-C that enable you to bolt on functionality from outside the classes without having access to source code and without subclassing.

## Working with Categories

The first technology that I want to talk about is called categories. Categories enable you to extend the functionality of existing classes by declaring and implementing methods on those classes, which then become usable throughout your application anywhere the original class is used.
