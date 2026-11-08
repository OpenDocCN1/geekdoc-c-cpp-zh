# # Chapter 22
## Interface to C

# ### Chapter Telegram

+   - **C library with C interface**
+     Extension often provided by third parties.
+   - **extern "C"**
+     Mark a function so that it can be used by C++ programs.
+   - **void\* or void pointer**
+     Non-type-safe raw pointer type, to and from which all raw pointer types can be converted; often part of C interfaces.
+   - **Custom delete function or custom deleter**
+     Feature of `shared_ptr`, which can be useful for releasing C resources.

If you are writing a program that uses third-party libraries, then there is a good chance that these libraries come with a C interface. Fortunately, C++ is written in such a way that you can definitely include libraries for C as well. So your choice is not limited.

What is limited is your choice of language features. If you want to use a C library, you can only use C language elements. Here is a by no means exhaustive list of restrictions that you have to accept:

+   - You have no classes. Structures can only have certain elements; for example, constructors are omitted, and everything must be public. For simplicity, you should only have data elements.
+   - There are no references. You pass a value or raw pointer.
+   - Many things from the C++ standard library are taboo. You cannot use standard containers, strings, or streams, but the C++ language designers have thought about interaction possibilities.
+   - C functions do not throw exceptions. You usually deal with error codes as return values or parameters.
+   - There are no overloaded functions in C; each name has a fixed set of parameter types (this has partially changed with C11). operator functions do not exist either.
+   - You will rarely encounter `const` with parameters. When `const` is present, it is more for documentation purposes. You cannot be sure that the C function does not modify your parameter passed by pointer.