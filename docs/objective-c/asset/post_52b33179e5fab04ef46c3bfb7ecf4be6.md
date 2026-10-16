
## Listing 3.25 (continued)

```
[johnAppleseed addReport::janeDoe];

joeBlow.salary = 50000;
janeDoe.salary = 75000;
johnAppleseed.salary = 100000;

NSMutableArray *allEmployees = [NSMutableArray array];
[allEmployees addObject:joeBlow];
[allEmployees addObject:janeDoe];
[allEmployees addObject:johnAppleseed];

for (Employee *employee in allEmployees)
{
    [employee giveRaise::10];
    NSLog(@"Employee %@ %@'s salary is: %.2f with a bonus of: %.2f", employee.firstName, employee.lastName, employee.salary, employee.bonus);
}

[johnAppleseed release];
[janeDoe release];
[joeBlow release];

[pool drain];
return 0;
}
```

Essentially, this code creates three employees, Joe Blow, Jane Doe, and John Appleseed. John Appleseed is the manager of Joe Blow and Jane Doe. Each of these employees is created and added to an array that contains all the employees. Finally, the application iterates over the array of employees and gives them all a bonus and a raise.

Summary In this chapter, I’ve introduced you to the very basics of object-oriented programming and how you declare classes and work with them in Objective-C. I’ve shown you how to create classes, how to work with inheritance, how to work with polymorphism, and how to encapsulate your data in your classes using properties. Throughout the rest of the book, you work with objects a great deal.

## 4 Understanding Objective-C Memory Management

One of the biggest challenges you may face as a new Objective-C developer when coming to the platform from other languages, such as Java, Ruby, and Python, is that Objective-C requires that you think about memory management. Many other modern languages have built-in memory management systems (garbage collection, for example) which enable the programmer to ignore most memory management concerns. Objective-C has a garbage collected runtime version, but it is relatively new to the language and unavailable when working on some of the platforms that Objective-C runs on, such as iPhone and iPad. As a result, while it would be nice to say that a new Objective-C developer has no need to be concerned about memory management, doing so would be a disservice to you as a new student of Objective-C. It is entirely likely that even if you are not writing Objective-C code for platforms other than MacOS X, you will still run into MacOS X code, which does not have garbage collection and requires you to manage your memory manually.

Fortunately, however, if you become familiar with the Objective-C memory management rules, even managing your memory by hand can be a reasonably simple affair. By the time you finish this chapter, you should have all of the knowledge of all of the tools that you will require to work with both memory managed code as well as non-memory managed code.

### Using Reference Counting

Before I begin reviewing the actual tools that you will use to manage your memory in Objective-C, I first want to introduce you to the mechanism that Objective-C uses under the hood to make manual memory management almost as easy as using a garbage-collected environment.

Every object that inherits from NSObject inherits certain memory management behaviors. Internal to these objects there exists a counter called the retain count. Using certain calls, this counter can be incremented or decremented. The Objective-C language runtime knows that when the retain count reaches zero, the object in question can be deallocated. When the object is deallocated, all of its memory resources are given back to the system to be reused.

The retain count can be incremented by using several standardized means. First and foremost, any time you create a new object using a method whose name contains the words alloc, or create, the object returned will have a retain count of one. Additionally, any time you acquire an object by using a method with a method name containing the word copy, that object will also have a retain count of one. You can manually increment the retain count by calling the method retain. Finally, you can decrement the retain count by calling the method release. Again, when the retain count reaches zero, the object, and its memory, are deallocated.

In the following listings, I go over a few scenarios to show how this works in practice. First, in Listing 4.1 I allocate an object using a standard alloc, and init.

### Listing 4.1
### A standard allocation of an object

```
Bar *foo = [[Bar alloc] init];
```

In this case, at the end of this method, the object foo has a retain count of one.

Now take a look at Listing 4.2

### Listing 4.2
### Retaining an object

```
Bar *foo = [[Bar alloc] init];
[foo retain];
```

In this case, in addition to allocating the object using an alloc call, I’m also incrementing the retain count by using the retain method. At the end of this code, the object has a retain count of two.

Now look at Listing 4.3

### Listing 4.3
### Allocating and releasing an object.

```
Bar *foo = [[Bar alloc] init];
[foo release];
[foo doSomething];
```

In this case, after calling the method release, the object has a retain count of zero, and would therefore be deallocated. The following line, because it's attempting to access a deallocated object, would result in a crash.

Obviously, that code is an error. Listing 4.4 shows another example of an error, in this case, a memory leak.

### Listing 4.4
### A memory leak

```
Bar *foo = [[Bar alloc] init];
[foo retain];
[foo release];
```

In this code, I've allocated an object, then retained that object, and then released it, but only once. If this were a member variable, and I was eventually sending it the second release to deallocate the object for good, that would be fine. In this case, however, we're only dealing with the code in this particular stack, and this would in fact be a memory leak.

Listing 4.5 shows another example of an error that can occur, can you tell what it is?

### Listing 4.5
### Failure to retain an object

```
@interface Foo : NSObject
{
    memberVariable
}

@end

@implementation Foo

-(void)someMethod;
{
    memberVariable = [someOtherObject getFoo];
}

@end
```

In this case, the code in question should be retaining the object that it received through the call that didn’t have alloc, copy, or create in the method name. When the program exits this method, the object in question will be deallocated by the program’s runtime releasing it. This will result in a crash the next time that object is accessed. Because the variable being used here is a member variable, it should be retained.

### NOTE

Technically, the object will be deallocated at the end of the next run loop iteration assuming nothing else has retained it before then, but for the purposes of following the memory management rules, you can assume, if it goes out of scope and you haven’t retained it, it’s been deallocated.

### Learning the memory management rules

Keeping track of retain counts may seem complicated, but memorizing them can make working with Objective-C much easier.

- Any object you create using a method call containing the word alloc, copy, or create, is an object, and thus memory, that you own. You are responsible for sending a release to that same object at some point in the future to free that resource. Anything that looks like [[Foo alloc] init...] is something you need to release. Anything that looks like [Foo copy] you need to release. And anything that looks like CreateFoo() returns something you need to release.

An object you acquire which is not received by calling a method with one of the aforementioned words in it, you don’t own. These objects can be used as much as you want within the current execution stack, but after you leave your current stack you cannot expect that they will remain available for your use.

When you receive an object from some other method call, you’re going to get back an object that has been “autoreleased.” I discuss autoreleasing later in this chapter, but the important point is that an autoreleased object will be released the next time your application exits its run loop. This release will likely happen as soon as you leave your current method. Don’t expect that object to live beyond the current method, for example, if you’re assigning it to a member variable, then you need to retain it.

When you increment the retain count on an object, either by allocating it, copying it, or retaining it, you are taking ownership of that object, and staking a claim on it. You are stating that you require access to this object for some indefinite period of time, and when you are finished with it, you will give up ownership of that object, and allow it to be destroyed.

### CAUTION

Although you are becoming the owner of an object by retaining it, ownership does not imply exclusivity. Others may own the object, as well. You are not the only person who could be accessing the object and changing its values.

### Using autorelease

I’ve already mentioned autorelease. The autorelease concept is central to Objective-C memory management. It enables Objective-C to solve a critical problem that has faced other languages, such as C++ and C: defining a standard “handoff” mechanism for objects returned from other methods and how the memory associated with them is managed.

For example, if you think about a C++ method or function that returns an object, who is the owner of that object? Is it the method that was called? Or is it the calling method? How do you handle the transfer of that memory from one owner to another without somehow having it all spill out onto the floor somewhere in between? C++ and C have handled that through a variety of means. For the most part, it’s been up to the individual developer to create and document whatever standard they want to follow. The end result is that when learning a new library, you also need to learn whatever memory management system it’s using as well. Some libraries might prefer smart pointers, while others might prefer known contracts, for example.

When Objective-C was faced with this problem, the developers of Objective-C created the concept of "autorelease". Autorelease is a method that you call on an object just like release. However, instead of immediately decrementing the retain count on the object, you can think of autorelease as a promise from the runtime that it will decrement the retain count the next time the application’s run loop exits. Typically, this happens when your current method exits. When the retain count is decremented in this manner, the object will be released just like normal.

## In This Chapter

- Introducing memory management
- Using reference counting
- Building objects that manage memory
- Using garbage collection
- Converting existing code to garbage collection
- Knowing what memory management model to use
