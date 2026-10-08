
## Inspecting Classes

```c
const char *name = [className UTF8String];
printf("%s\n\tivars:\n\n", name);
Class cls = NSStringFromString(className);
unsigned int ivarCount;
Ivar *ivars =
class_copyIvarList(cls, &ivarCount);
for (unsigned int i=0; i<ivarCount; i++) {
    printf("\t%s\n\n", ivar_getName(ivars[i]));
}
free(ivars);
unsigned int methodCount;
Method *methods =
class_copyMethodList(cls, &methodCount);
printf("%s\n\tMethods:\n\n", name);
for (unsigned int i=0; i<methodCount; i++) {
    printf("\t%s\n", sel_getName(method_getName(methods[i])));
}
```

From: class.m
Once you have a pointer to a class, either by enumerating all classes, sending a -class message to an object, or using NSStringFromString(), you can inspect it. The class structure contains a lot of information about Objective-C classes, all of which is available to the programmer.

With older runtimes, Class was a typedef for struct objc_class, which was defined in a header. On more modern systems, Class is an opaque type and you are expected to interact with it via a set of public functions. This makes it easier to evolve the ABI over time. The layout of the class structure can be changed just by modifying the compiler and runtime, without needing changes to any other code.

The Tree.m example prints the instance variables and methods for all of the classes in the system. There is a lot more metadata that you can access. For example, instance variables store their type and the offset from the start of the object.

This information is used in the implementation of KVC. When you set a value for a key, and KVC is permitted to directly access instance variables, then it will first find an instance variable with the matching name. It will then find the type and determine whether it needs to unbox the object. Finally, it will add the ivar pointer to the object and then perform the assignment at this address.

It does something similar with accessor methods. Methods store their name, their types, and their method pointer. The type information is important, because it allows other code to construct a call frame. By checking the types of an accessor method, the KVC code can cast the method pointer to the correct type and then call it, setting or getting a particular property.

With newer runtimes, there is metadata stored for declared properties as well. Almost anything that you set about a class can be inspected by calling runtime functions. The only thing that you can't do is retrieve the source code for individual methods.

## Creating New Classes

```objc
#include <objc/runtime.h>

id fakeDealloc(id self, SEL _cmd, ... ) {
    NSLog(\@"%@ sent a -dealloc message", self);
}
void makeIndestructible(id obj) {
    Class new =
        objc_allocateClassPair(obj->isa, "Fake", 0);
    class_addMethod(new, @selector(dealloc),
        (IMP)fakeDealloc, "v@");
    objc_registerClassPair(new);
    obj->isa = new;
}
```

From: newClass.m

Creating new classes at run time is rare, but it does provide a lot of opportunities for very dynamic behavior or optimization. We already looked at a bit of the Foundation framework that does this. The key-value observing mechanism creates new classes to intercept accessor method calls.

The most important thing about creating classes at run time is that it demonstrates one of the core principles of Objective-C; that nothing the compiler does is magic. You can generate in your own C code everything that the compiler generates from Objective-C code. Of course, the compiler will probably do a better job of optimizing the result, and the Objective-C version will be simpler. If this were not the case, there wouldn’t be much point in Objective-C. Creating a new class involves three steps. First you allocate the class pair, then you add methods, instance variables, and protocols, and finally you register the class pair with the runtime.

> **Note:** The term class pair can seem confusing. Every Objective-C class in your source code is compiled to two classes at run time. An object is an instance of the *class*, and the class is an instance of the *metaclass*. Instance methods are attached to the class and class methods are attached to the metaclass. When you send a message to the class, the metaclass is used to look up the corresponding method.

When you allocate the class pair, you must provide the superclass, the name of the new class, and the amount of space added on the end of the class structure. The name of the new class must be unique. The example code for this section will not work if you call the function twice. The simplest way of working around this is to keep a counter in a static variable, increment it atomically every time that you create a new class, and append it to the class name string.

The extra space on the end of the class can be very useful when you combine class creation with isa-swizzling. Changing the isa pointer of an existing class lets you add methods, but not instance variables. You can, however, create some space on the end of the class structure and store extra data there. Calling object_getIndexedIvars() with the class as the argument will give you the address of the start of this data.

You can use this functionality to implement other object models. I've used it, for example, to add prototype-based object orientation to Objective-C, allowing closures to be used as methods and added to a single object.

## Adding New Instance Variables

```objc
#include <objc/runtime.h>

@interface NSObject (Annotated)
-(NSString*)annotation;
-(void)setAnnotation:(NSString*)aString;
@end
static char key;

@implementation NSObject (Annotated)
-(NSString*)annotation
{
    return objc_getAssociatedObject(self, &key);
}
-(void)setAnnotation:(NSString*)aString
{
    objc_setAssociatedObject(self, &key, aString, OBJC_ASSOCIATION_RETAIN);
}
@end

int main(void) {
    [AutoreleasePool new];
    id obj = [NSDictionary new];
    [obj setAnnotation:@"A note"];
    NSLog("Annotation: %@", [obj annotation]);
    return 0;
}
```

Starting with OS X 10.6, the Objective-C runtime provides a mechanism that allows you to almost—add instance variables to existing classes. There are two functions, used for storing associative references. These are object pointers that are associated with the object, after its creation.

Adding new instance variables is not possible after an object has been created, because its memory layout is fixed by this point, but the best thing. The example at the start of this section shows a category on NSObject that demonstrates this capability. It allows you to associate a string value with any object, via a pair of methods.

There are two things to note about the functions for setting and getting associative references. The first is the key. This has to be a unique pointer value, not used by any other code to identify a different associative reference. The simplest way of doing this is to define some static variable in the file and use its address.

The other thing to note is the association policy. These policies mirror those available for declared properties. In this case, we're telling the runtime to retain the object now and to release it when the object is destroyed.

There are some cases where associative references are very useful, especially when debugging. If you use the retain policy, the associated object will be released when the object that it is associated with is deallocated, so you can use a block to log a message about the deallocation, for example, without having to modify the object you are deallocating. You can also use it to easily differentiate two objects, for example, by adding a note indicating where they were created via a category like the one in the example. Be aware, however, that associative references are quite expensive. If you make heavy use of them in production code, don’t be surprised if your code becomes very slow.
