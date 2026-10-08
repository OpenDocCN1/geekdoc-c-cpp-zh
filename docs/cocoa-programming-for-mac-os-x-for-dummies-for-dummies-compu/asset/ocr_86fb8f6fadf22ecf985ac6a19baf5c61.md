you've freed an object in memory that you still need. Your code will crash when you try to access this freed object.

As you saw in the previous section, an object is allocated with the alloc method. The alloc method increases the reference count by one, so it needs a corresponding release.

```
SomeClass *object = [[SomeClass alloc] init];
do stuff with someObject here...
[someObject release];
```

So far, this is pretty simple because the allocation and release of the object are all within the same block of code. Where things get a little mind-bending is in the case of instance variables. Although it's legal to access instance variables by name in your methods, it's far wiser to access them only via

![](bbox=[0.115, 0.403, 0.198, 0.463])

Because of memory management issues, things can get ugly quickly if you don't use accessor methods to access instance variables. If you don't use accessor methods, there's a very real possibility that your application will leak memory or it will crash when you try to release an object that's already released.

For example, suppose that you have a class that has an NSString instance variable name. Declare two methods for accessing the instance variable. A getter (name) and a setter (setName:

```
@interface MyClass : NSObject {
NSString *name;
- (NSString *)name;
-(void)setName:(NSString *)aName;
@end
```

Then, in your implementation file, define the methods like this:

```
@implementation MyClass
-(NSString *)name {
  return name;
}
-(void)setName:(NSString *)aName {
 [name retain];
 [aName release];
 name = aName;
}
@end
```