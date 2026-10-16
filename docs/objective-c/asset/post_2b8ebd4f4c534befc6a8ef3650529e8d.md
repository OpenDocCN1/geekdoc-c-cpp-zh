
The real purpose of the initializer, aside from creating self, is to initialize any data members in the object. So, after you have verified that self is not nil, you can initialize your variables. Having initialized your variables, you then return self from your initializer method.

In some cases, it may make sense to provide multiple initializers for your class. For example, if there are different ways to create an object and different parameters need to be passed to the initializer in these different states. In these cases, you can create multiple, different initializers that take different parameters. To avoid duplication in your code, however, it makes sense to call other initializers from within your initializer. Doing this allows you to keep specific initialization in one place and only one place.

In addition to the concept of an initializer, there is also the concept of the designated initializer. Typically it takes the fewest number of parameters of all your initializers, and it is the final initializer that all your other initializers will call to set up the initial state of your object.

An example of this is shown in Listing 3.6.

## Listing 3.6
### An example showing different initializers is calling the designated initializer

```
-(id)init
{
    if((self = [super init]))
    {
        memberVariable = [[NSMutableArray alloc] init];
    }
    return self;
}

-(id)initWithArray:(NSMutableArray *)inArray
{
    if((self = [self init]))
    {
        memberVariable = [inArray retain];
    }
    return self;
}
```

The second kind of special method that you need to be familiar with is the dealloc method. The dealloc method is the opposite of the init method. It enables you to free up resources that were allocated in your init method or elsewhere in your object. You must be sure to call the superclass dealloc method before the method exits. Listing 3.7 shows an example of a dealloc method.

## Listing 3.7
### An example showing a dealloc method

```
-(void)dealloc
{
    [memberVariable release]; memberVariable = nil;
    [super dealloc];
}
```

## CAUTION

You should be sure not to call the super dealloc method before releasing your own variables. This can cause a crash.

I discuss initializer and dealloc methods in greater detail in Chapter 4. For now, it’s important that you simply be familiar with the methods because you will be using these methods in the upcoming example code.

## Writing class methods

In Objective-C, classes themselves also have many of the same capabilities as objects. For example, classes have the ability to have static methods declared upon them that can be called directly from the class itself. When using these kinds of methods, you don’t need to have instantiated an instance of the class that you’re working with. This can be convenient for methods that are used for creating instances of your class, such as factories and singletons. In fact, the Cocoa frameworks utilize class methods for many of the built-in classes for the purposes of creating instances of the class. In other languages, such as C++ or Java, class methods are often referred to as “static methods.” If you are familiar with these languages, you may be familiar with this terminology.

## NOTE

A factory method in Objective-C is a class method that is used as a convenience for constructing an object. It always returns an autoreleased object. Factory methods are covered more in Chapter 4.

## CROSS-REFERENCE

Singletons are covered in Chapter 17.

Declaring a class method is very similar to declaring an object method; the only difference is that instead of using a hyphen in front of the method declaration, instead you use a plus sign. Listing 3.8 shows an example of a class method declaration.

## Listing 3.8
### A class method declaration

```
@interface Foo : NSObject
{
    NSMutableArray *memberVariable;
    NSString *anotherMemberVariable;
}
@property (nonatomic, retain) NSMutableArray * memberVariable;
@property (nonatomic, retain) NSString * anotherMemberVariable;

-(id)init;
-(id)initWithArray:(NSMutableArray *)inArray;

// a class method
+(id)fooWithArray:(NSMutableArray *)inArray;

@end
```

The implementation of a class method is identical to the implementation of an object method. However, class methods do not have access to any of the object’s member variables. To understand why, remember that a class method is called directly off the class itself, not off an instance of that class. Therefore, there is no object that the data can be stored within in order to operate on that data. Listing 3.9 shows an example of a class method implementation.

## Listing 3.9
### A class method definition

```
@implementation Foo

+(id)fooWithArray:(NSMutableArray *)inArray
{
    return [[[self alloc] initWithArray:inArray] autorelease];
}

@end
```

The most common use of class methods is in the use of factories, like this method. Many classes in Cocoa and Cocoa Touch have factory methods defined on classes to make creation of objects easier. For example, the NSArray class includes the factory method [NSArray array] which returns a properly constructed NSArray object. (I discuss some special memory management rules in Chapter 4.) When creating class methods, you can use the self object to refer to the class itself, as in this case.

## Declaring objects

I’ve now shown you how to declare classes, including their data, their methods, and so on, but all of this would be useless if you couldn’t declare instances of your classes and use them. So now, let’s take a look at how you declare an instance of your class in your code.

Listing 3.10 shows an example of code where I’ve taken the class that we created in the previous section and now I want to use that class in my code to do something useful.

## Listing 3.10
### Creating an instance of your class

```
{ // plain old initializer Foo *object; object = [[Foo alloc] init]; [object doSomethingWithParameter:arg]; // all on one line Foo *object = [[Foo alloc] initWithArray:[NSMutableArray array]]; [object doSomethingWithParameter:arg]; // using a class method factory Foo *object = [Foo fooWithArray:[NSMutableArray array]]; [object doSomethingWithParameter:arg]; }
```

As you can see, declaring an instance of your class is very straightforward. First, you use your class name, filed by the pointer operator (*). Then you place the name of the variable that will hold the instance of your class, in this case “object”. You can, if you choose, initialize the object variable immediately, on the same line, as its declaration. To do this, you simply use the equal operator to assign the initialized value to your object variable. In the example code above, I’ve shown it both ways, first not initializing the variable, and then initializing the variable all on one line. I’m introducing an important new syntax in this code. You’ve seen it before in other sections of this book, and now I’m going to explain exactly what it’s all about. The syntax I’m referring to here is the use of the square bracket operators ([]).

## Introducing Objective-C

In Objective-C, methods are called on classes and objects by surrounding them in square brackets. You put the opening square bracket at the beginning of the object or class that the method relates to, and then you place the closing square bracket at the end of the method invocation. Thus, looking at the code above, you can see that in the initialization of our object variable, we actually have two method calls in both of the initialization code snippets. The first one is a call to alloc. This method is actually being called on the class. The second method call is for the method init. This method is actually being called on the object that is returned from the alloc call. It's important to recognize when looking at this code that the alloc call is in fact returning an object and that the init method is being called on that object. This is not uncommon whatsoever in Objective-C code to see nested calls like this where calls are made on objects returned from prior method calls.

Initializing an Objective-C object is actually a two-step process. The first step is used to allocate the memory that will be used to store the data and the methods that make up the object. This is what the alloc call is for. This is why the init and method can be called on the object that is returned from alloc. I cover this in more detail in the chapter on memory management, but it is important to note that any object that you allocate, using an alloc method, like shown here, must also be released. To release an object, you simply call the method release on the object. Release is a method that is defined on NSObject.

### Making calls on objects

After you have declared and created an instance of your class, you will, likely, want to make calls on that instance. You can call any of the methods that you have declared in your class as object methods, using the square bracket syntax I showed you in the previous section. However, only methods that are declared in the interface file of your class definition should be called from modules other than the class itself. Although it is technically possible to call methods that are not declared in the interface file, the compiler will issue a warning when you compile your code. Additionally, the compiler will be unable to determine the types of arguments and return values that the method requires, and thus it may not be able to catch errors that it would normally be able to catch.

In some cases, you may want to create methods in your class which are only for internal use to your class. Meaning, you don't want to expose their functionality to outside classes. In other languages such as C++ or Java, you might think of these methods as "private" methods. Objective-C has no syntax for declaring private methods, but if you do not expose the method in your interface file, then it is considered bad form by other classes to call those methods. Part of this is for the reasons that I mentioned in the previous paragraph, and part of it is because of social norms. You don't have to expose methods that you use strictly in your class to users of your class. You can declare methods in your implementation file alone, and they will be available for use in your implementation file. The only important thing to keep in mind when doing so is that the compiler still needs to know about your method signature before you use it. Therefore, methods that you use only in your implementation file, that you don't want to expose externally, should be placed above any methods that reference those methods. Listing 3.11 shows an example of what I mean.
