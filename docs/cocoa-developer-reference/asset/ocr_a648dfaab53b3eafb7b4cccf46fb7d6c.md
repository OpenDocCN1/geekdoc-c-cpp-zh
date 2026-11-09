As an example, assume you have an object called `myObject`, an instance of `MyClass`, which has a property called `thisInt`. The following code will trigger a KVO update **as long as you run it inside another object**:

```
myObject.thisInt = 15;
```

The accessor method is triggered by an external property write. But if you include internal update code within myObject, the assignment doesn’t use an accessor, and so the assignment is invisible to KVO.

```
@implementation MyClass
...
thisInt += 10;
```

One solution is to force updates with explicit code:

```
[self willChangeValueForKey: @"thisInt"];
thisInt = thisInt + 10;
[self didChangeValueForKey: @"thisInt"];
```

This is ugly and is a lot of extra trouble when you want to add one number to another. Other solutions are possible, but the most elegant is to use `self` and dot syntax for critical assignments:

```
self.thisInt = thisInt+10;
```

Specifying `self` forces the assignment to use an accessor, which solves the problem in a simple and readable way. Use it for *critical* assignments only. To improve performance, don’t use it for intermediate steps in a calculation.

You must also check that accessors are used when working with bindings (described in Chapter 13). Bindings use KVO, and if you don’t set values with accessors, they don’t track updates correctly.

![](bbox=[0.119, 0.673, 0.188, 0.729])

**CAUTION**  
This solution works with dot syntax. If you don’t approve of dot syntax, you’ll have to use ugly, old-fashioned constructions like `[self setThisInt: [self thisInt] + 10];`.

# Using KVO

KVO can be immensely powerful. Your application can monitor events anywhere in your code and respond automatically to given values or application states. Setting a value in one place in the code can trigger a chain of dependent events automatically. Many Cocoa objects are KVO compliant; your application can watch for changes in Cocoa object properties and respond as needed. Some applications include the following: