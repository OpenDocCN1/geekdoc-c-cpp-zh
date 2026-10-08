
method or an instance variable, you will get the type encoding. This is very useful. In the framework, I use this information to iterate over the encodings of instance variables and automatically serialize them.

## Using Blocks

```
int (^getCounter(void))(void)
{
    __block int counter;
    int(^block)(void) = ^void() { counter++; };
    return Block_copy(block);
}
int main(void)
{
    [NSAutleasePool new];
    int(^block)(void) = getCounter();
    NSAssert(block == 2, @"Block counted incorrectly");
    int(^block2)(void) = getCounter();
    NSAssert(block2 == 2, @"Block didn't start from 0");
    return 0;
}
```
*From: block.m*

With 1.6, Apple introduced blocks as a C language extension, most often used in conjunction with Objective-C. Blocks are closures, sometimes called lambdas. The name comes from Smalltalk, where closures encapsulate variables. The syntax for creating blocks is quite ugly. It is based on the C syntax for function pointers, but with a caret replacing the asterisk. Blocks can be used almost exactly like function pointers. You can call them just like functions, but you can't cast them to function pointers because they have a different calling convention. In the example, the getCounter() function returns a new block that implements a counter. Every time you call this, it returns a value one greater than the last time you called it. This works because the counter variable in the scope where block was created is declared with the __block specifier. Any variables on the stack that blocks reference will be copied to the heap and reference counted. When you call Block_copy(), the block itself is copied to the heap if it's on the stack, or has its reference count incremented if it not. Block_copy() is actually a macro that wraps the function and casts the return type from void* to the type of argument.

## CHAPTER 2: An Objective-C Primer

In the latest version of the Foundation framework, you will find a lot of methods that take blocks as arguments. You can, for example, iterate over an array with a block as an argument. Blocks don’t add any expressiveness to the C language. A block is just a function pointer and a data pointer hidden inside a single structure, with some extra logic in the compiler to insert the data pointer as hidden argument to the function when it is called. This doesn’t mean that blocks are not useful. After all, the same is true of Objective-C; it doesn’t let you do anything that you can’t do in C, it just adds some syntactic sugar that makes things easier. Like Objective-C objects, blocks have an isa pointer and can be sent messages. They are instances of the NSBlock abstract class, which implements the NSCopying protocol. Most of the object-like behavior of blocks is undocumented. You can store them in Objective-C collections, but don’t depend on their ability to understand any specific messages. With the latest versions of Clang, blocks also support introspection, exposing their types as Objective-C types. We’ll look at blocks in more detail in Chapter 15.

## Memory Management

If you come from a C or C++ background, you're probably used to tracking ownership of objects and manually allocating and destroying them. If you're coming from a language such as Java, you're probably accustomed to having the garbage collector take care of all of this for you.

Objective-C does not, at the language level, provide anything for allocating or deallocating objects. This is left up to C code. You commonly allocate objects by sending their class +alloc message. This then calls something like malloc() to allocate the space for the object. Sending a dealloc message to the instance will clean up its variables and delete it. The Foundation framework adds reference counting to this simple manual memory management. This makes life much easier, once you understand how it works. Newer compilers provide some assistance for you, eliminating the need to write the reference counting code yourself.

## Retaining and Releasing

```
NSArray *anArray = [NSArray array];
anArray = [[NSArray alloc] init];
[anArray release];
```
*From: retainRelease.m*

Every object that inherits from NSObject has a reference count associated with it. When this reference count reaches 0, it is destroyed. An object created with +alloc or any of the related methods, such as +new or +allocWithZone:, begins life with a reference count of one.

To control the reference count of an object, you send it -retain and -release messages. As their names would imply, you should use these messages when you want to retain a reference to an object, or when you want to release an existing reference. The -retain message increments the object’s reference count, and the -release message decrements it.

You can also send a -retainCount message to an object to determine its current reference count. It's tempting to use this for optimization and invoke some special cases when you are sure there is only one reference to an object. This is a very bad idea.

## Retaining and Releasing

Pointers in Objective-C are divided into two categories: owning references and non-owning references. An owning reference is one that contributes towards the reference count. When you call a method like +new or -retain, you get an owning reference. This means that an object may be referenced in two places, even though its reference count is only one. Temporary variables are typically non-owning. Automatic reference counting and garbage collection, which we’ll look at later in this chapter, both introduce special kinds of non-owning references.

## Assigning to Instance Variables

```
(void)setStringValue:(NSString*)aString {
    id tmp = [aString retain];
    [string release];
    string = tmp;
}
```
*From: ivar.m*

There are a few things that you have to be careful about when using reference counting in this way. Consider the following simple set method:

```
(void)setStringValue:(NSString*)aString {
    [string release];
    string = [aString retain];
}
```
*From: ivar.m*

This looks sensible. You release the reference to the old value, then retain the new value and assign it. Most of the time, this will work, but in a few cases it won't, and that can be confusing to debug What happens if the value of aString and string are the same? In this case, you are sending the same object arelease message then a retain message. If some other code holds references to this object, it will still work, but if not then the first message will cause the object to be destroyed and the second will be sent to a dangling pointer.

A more correct implementation of this method would retain the new object first, as shown at the start of this section. Note that you should assign the result of the -retain message because some objects will return another object when you retain them. This is very rare, but it does happen on occasion.

Finally, this method is not thread-safe. If you want a thread-safe set method, you need to retain the new value, perform an atomic exchange operation on the result and instance variable, and then release the old value. In general, however, it is almost impossible to reason about code that supports this kind of fine-grained concurrency, and the amount of cache churn it causes will offset any performance gains from parallelism, so it's a terrible idea. If you really need it, it's better to use declared properties to synthesize the accessor than try to write it yourself.
