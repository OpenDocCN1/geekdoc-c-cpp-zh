or as __unsafe_untained. The former is safer, because it ensures there is no chance of a dangling pointer: When the delegate is destroyed, the instance variable will be set to nil.

There are two disadvantages of using a weak pointer. The first is portability. Weak pointers work on iOS 5, Mac OS X 10.7, and with GNUstep, but they don't work on older versions of iOS or Mac OS X. The other disadvantage is performance. Every access to a weak pointer goes via a helper function. This checks that the object was not in the process of deallocation and retains it if it is still valid, or returns nil if it is not.

In contrast, unsafe unretained pointers are just plain pointers. They are cheap to access and work on any deployment target. Their disadvantage is that you are responsible for ensuring that you don't try to access them after the pointee has been deallocated.

A good compromise is to use weak pointers when debugging and unsafe unretained pointers for deployment. Add debug assert statements checking that the pointer is not nil before you send it any messages, and you'll end up with a helpful error, rather than a crash, if you have bugs.