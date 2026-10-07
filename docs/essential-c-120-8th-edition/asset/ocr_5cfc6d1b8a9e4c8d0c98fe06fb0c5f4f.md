# 8 Interfaces

Polymorphism is available in C# not only via inheritance (as discussed in Chapter 7) but also via interfaces. Unlike abstract classes, interfaces could not include any implementation—until C# 8.0. (But even in C# 8.0, it is questionable whether we should use this capability except for “versioning” the interfaces.) Like abstract classes, however, interfaces define a set of members that callers can rely on being implemented.

![](bbox=[0.16, 0.439, 0.868, 0.646])

By implementing an interface, a type defines its capabilities. The interface implementation relationship is a “can do” relationship. The type can do what the interface requires an implementing type to do. The interface defines the contract between the types that implement the interface and the code that uses the interface.