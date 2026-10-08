# Sending Messages by Name 341

passed in as a hidden argument.
You have to remember to call either objc_msgSend_sret() or objc_msgSend_fret(). This is quite messy, because it means that you have to be aware of the calling conventions on your target platform.
With the GNU runtimes, this is much simpler. There is no objc_msgSend() function. Instead, you call objc_msg_lookup() and then call the returned function pointer, after casting it to the correct types.

The easiest way of doing this that is portable between runtimes is to use the -methodForSelector: method on NSObject. This returns a pointer to the method, which the function used to implement you you can then call. This takes two hidden arguments; the receiver and the selector.

This is almost enough to call a method by name. The missing part is some mechanism for turning strings into selectors. The NSSelectorFromString() function does exactly this. It takes an NSString as an argument and returns a selector. You can then pass this to -methodForSelector:, and as the second argument to the returned function.