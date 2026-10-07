# Figure 2-4 The life cycle of an object—simplified

| Message | Retain count | Comments |
| :--- | :--- | :--- |
| alloc (class method) | 1 | Object allocated; is a pointer set |
| init | 1 | Object initialized, can be used |
| doSomething | 1 | Message sent to object |
| retain | 2 | |
| release | 1 | Object is no longer needed |
| release | 0 | Instance variables released, allocated memory freed |
| dealloc (invoked) | | Object destroyed |

In course, in this scenario the creator of an object has no need to retain the object. It owns the object already, but if this creator were to pass the object to another object in a message, the situation changes. In Objective-C program, an object received from some other object is always assumed to be valid within the scope in it is obtained. The receiving object can send messages to the received object and can pass it to others. This assumption requires the sending object to behave appropriately and not prematurely free the object while a client object has a reference to it.

If the client wants to keep the received object around after it goes out of programmatic scope, it can retain it—. Retaining an object increments its retain count, thereby expressing an ownership interest in the object. The client object assumes a responsibility to retain the object at later time. If the creator of an object releases it, but a client has retained that same object, the object persists until the client releases it. Figure 2-5 illustrates this.

# Figure 2-5 Retaining a received object

| Creator | | Client |
| :--- | :--- | :--- |
| id anObj = [[MyClass alloc] 1 init]; | message | |
| [client doSomethingWith:anObj];
 //... | | (void)doSomethingWith:(id)anObj(
anivar = [anObj retain]:2
 //...
) |
| [anObj release]:1 | | (void)sometimeLater (
 if (anivar)
 [anivar release]:0
 ) |

74 Object Retention and Disposal
2010-12-13 | © 2010 Apple Inc. All Rights Reserved.