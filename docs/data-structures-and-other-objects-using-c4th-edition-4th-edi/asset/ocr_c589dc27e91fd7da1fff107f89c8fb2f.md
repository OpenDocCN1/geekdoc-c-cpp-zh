One final point about the value semantics: The programmer who uses the bag does not need to know whether the implementor has overridden the automatic value semantics. This programmer needs to know only that there is a valid value semantics. Therefore, the bag documentation indicates that there is a valid value semantics, but does not indicate whether the automatic value semantics was overridden.

# The Destructor

The final new factor for a class that uses dynamic memory is a special member function called the **destructor**. The primary purpose of the destructor is to return an object's dynamic memory to the heap when the object is no longer in use. The destructor has three unique features:

+   * The name of the destructor is always the tilde character (~) followed by the class name. In our example is the name of the destructor is ~bag.
+   * The destructor has no parameters and no return value. As with the constructor, you must not write `void` (or any other return type) at the front of the destructor's prototype. However, you must list the empty parameter list, as shown in this prototype: `~bag( )`;
+   * Programmers who use a class should not need to know about the destructor. This is because programs rarely activate the destructor explicitly. What good is a destructor that is never activated? The answer is that destructors are activated, but the activation is usually automatic whenever an object becomes inaccessible.

Several common situations cause automatic destructor activation:

+   1. Suppose a function has a local variable that is an object, like this:
+   ```
+   void example1( )
+   {
+       bag sample1;
+       ...
+   }
+   ```
+   When the function example1 returns, the destructor sample1.~bag( ) is automatically activated. The general situation: When a local variable is an object with a destructor, the destructor is automatically activated when the function returns.

destructors are automatically activated when an object becomes inaccessible

+   2. Suppose a function has a value parameter that is an object, like this:
+   ```
+   void example2(bag sample2)
+   // Does some calculation using a bag
+   ```
+   As with the previous example, when the function example2 returns, the destructor sample2.~bag( ) is automatically activated. On the other hand, if sample2 was a reference parameter, then the destructor would not be activated because a reference parameter is actually an object in the calling program, and that object is still accessible.