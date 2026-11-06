**error** (i.e., the result of an arithmetic operation is smaller than the smallest number that can be stored in a given numeric type).

![](bbox=[0.118, 0.194, 0.19, 0.248])

# Error-Prevention Tip 17.8

*Using inheritance with exceptions enables an exception handler to* `catch` *related errors with concise notation. One approach is to* `catch` *each type of reference to a derived-class exception object individually, but a more concise approach is to* `catch` *pointers or references to base-class exception objects instead. Also, catching pointers or references to derived-class exception objects individually is error prone, especially if you forget to test explicitly for one or more of the derived-class reference types.*

![](bbox=[0.12, 0.63, 0.19, 0.688])

# Common Programming Error 17.6

*Placing a* `catch` *handler that catches a base-class object before a* `catch` *that catches an object of a class derived from that base class is a logic error. The base-class* `catch` *catches all objects of classes*