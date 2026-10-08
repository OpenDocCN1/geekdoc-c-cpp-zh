# Managing Memory with Exceptions

Note: In Java, you can use exceptions as a local goto as a code path to the VM as being unusual, by throwing an exception and catching it in the same method. This is also possible in Objective-C, but it's incredibly inefficient. The @throw() statement will call the obj_exception_throw() function, which will call an unwind library function.

This will then read the DWARF data for the stack frame and call the Objective-C personality function. This function will then read more of the DWARF data, compare the class of the exception against the class of the catch block, and then set the instruction pointer to the address of the catch statement.

In Java, the VM will just translate this into an unconditional jump to the catch block. If you must use this pattern, then use a C goto statement in Objective-C. It's generally better to avoid it altogether, however, and find a solution that doesn't ignore the ideas of structured programming.

again afterward. This is one of the reasons why it's a bad idea to throw anything other than an NSArray object. Anyone who follows the suggestion in Apple's documentation for doing this will end up with code that only correctly handles NSArray objects and will prematurely destroy any other object type.