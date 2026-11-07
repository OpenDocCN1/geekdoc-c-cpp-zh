# 12.3 **Exception Safety Guarantees and noexcept**

Client-code programmers need to know what to expect when using your code. Is there a potential for exceptions? If so, what will the program’s state be if an exception occurs? When you design your code, consider what **exception safety guarantees** you’ll make.¹⁸,¹⁹

+   - **No guarantee**—If an exception occurs, the program may be in an invalid state and resources, like dynamically allocated memory, could be leaked.
+   - **Basic exception guarantee**—If an exception occurs, objects’ states remain valid but possibly modified, and no resources are leaked. Generally, code that can cause exceptions should provide at least a basic exception guarantee.
+   - **Strong exception guarantee**—If an exception occurs, objects’ states remain unmodified or, if objects were modified, they’re returned to their original states before the operation that caused the exception. We implemented the copy assignment operator in Chapter 11’s MyArray class with a strong exception guarantee via the copy-and-swap idiom. The operator first copies its argument, which could fail to allocate resources. In that case, the assignment fails without modifying the original object; otherwise, the assignment completes successfully.
+   - **No throw exception guarantee**—The operation does not throw exceptions. For example, in Chapter 11, the MyArray class’s move constructor, move assignment operator and friend function swap were declared noexcept. They work with existing resources rather than allocating new ones, so they cannot fail. Only functions that truly cannot fail should be declared noexcept. If an exception occurs in a noexcept function, the program terminates immediately.

# ✓ **Checkpoint**

+   1. *(True/False)* With no exception safety guarantee, if an exception occurs, the program may be in an invalid state and resources like dynamically allocated memory could leak.
+      **Answer:** True.
+   
+   2. *(True/False)* With a basic exception guarantee, if an exception occurs, objects’ states remain valid but possibly modified, and no resources leak.
+      **Answer:** True.
+   
+   3. *(True/False)* With a strong exception guarantee, if an exception occurs, objects’ states remain unmodified or return to their original states before the operation that caused the exception.
+      **Answer:** True.