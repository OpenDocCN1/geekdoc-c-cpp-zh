As of Objective C 2.0, a form of memory management known as garbage collection became available. With garbage collection, the system automatically determines which objects own other objects, automatically freeing up (or garbage-collecting) objects that are no longer referenced as space is needed during the program’s execution.

The iOS runtime environment doesn’t support garbage collection, so you don't have the option to use it when developing programs for that platform. That is, you can only use it when developing Mac OS X applications.

If you decide to use garbage collection, you must turn it on when building programs with Xcode. You can do this through your project’s Build Settings menu. Under the Apple LLVM compiler 3.0 Language settings, there is a setting called Objective-C Garbage Collection. Changing that from its default value of Unsupported to Required specifies that your program will be built with automatic garbage collection enabled (see Figure 17.1).

# Figure 17.1. Enabling garbage collection