member function draw, but each shape’s implementation is quite different. In a program that draws many different shapes, it would be convenient to treat them all generally as base-class Shape objects. Using a base-class Shape pointer to invoke function draw, we could draw any shape. At runtime, the program would dynamically determine which derived-class draw function to use based on the type of the object to which the base-class Shape pointer points. This is runtime polymorphic behavior. **With virtual functions, the type of the object pointed to (or referenced)—not the type of the pointer (or reference)—determines which member function to invoke.**

# 10.7.2 Declaring virtual Functions

To enable this runtime polymorphic behavior, declare the base-class member function draw as `virtual`, then override it in each derived class to draw the appropriate shape. An **overridden function in a derived class must have the _same signature_ as the base-class function it overrides.** To declare a virtual function, precede its prototype with the keyword `virtual`. For example,

```
virtual void draw() const;
```

would appear in base class Shape to indicate that draw is a virtual function that takes no arguments and returns nothing. This function is declared const because a draw function should not modify the Shape object on which it’s invoked. Virtual functions do not have to be const and can receive arguments and return values as appropriate. **Once a function is declared virtual, it’s virtual in all classes derived directly or indirectly from that base class.** If a derived class does not override a virtual function from its base class, the derived class inherits its base class’s virtual function implementation.

# ✓  Checkpoint

+   1. **(True/False)** An overridden function in a derived class must have the same signature as the base-class function it overrides.
+   
+      **Answer:** True.
+   
+   2. **(True/False)** Once a function is declared virtual, it must explicitly be declared virtual in all classes derived directly or indirectly from that base class.
+   
+      **Answer:** False. Actually, once a function is declared virtual, it’s virtual in all classes derived directly or indirectly from that base class.
+   
+   3. **(Discussion)** Assume that class Shape contains the following function prototype:
+   
+      ```cpp
+      virtual void draw() const;
+      ```
+   
+      If class Square inherits from Shape but does not override draw, would class Square have a draw member function? Explain why or why not.
+   
+      **Answer:** Yes, class Square would have a draw member function because it would inherit its base class Shape’s virtual function implementation.