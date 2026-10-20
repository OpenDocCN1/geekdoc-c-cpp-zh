# 6.1.1 Required States of Moved-From Objects

The requirements for moved-from objects in the C++ standard library are nothing special. That is, for any function, the requirements it formulates for the passed types and objects also apply to any moved-from objects passed or used internally.

Basically, you always have to be able to destroy a moved-from object. In addition, in many functions, you have to be able to assign a new value to a moved-from object.

Consider, for example, how we swap the values of two objects a and b (which might be part of a sorting operation). Swapping is usually implemented as follows (see Figure 6.1):

+   - Move a to a new temporary object tmp (so that a becomes a moved-from object).
+   - Move-assign b to the moved-from object a (so that b becomes a moved-from object).
+   - Move-assign tmp to the moved-from object b (so that tmp becomes a moved-from object).
+   - Destroy the moved-from object tmp.

![](bbox=[0.175, 0.365, 0.8, 0.6])

Figure 6.1. Moved-from objects in swap functions

Note that we might also have self-swapping by passing the same object to both parameters. In that case, we might even assign an object with a moved-from state to itself. This all should work (provided a moved-from object still can have any value).

So, for moved-from objects we have the same basic requirements that usually apply to all objects:

+   - We have to be able to destroy moved-from objects.
+   - We have to be able to assign a new value to moved-from objects.
+   - We should be able to copy, move, or assign moved-from objects to other objects.

Moved-from objects should also be able to deal with additional requirements particular operations have. For example, to sort objects we have to support calling operator< or the sorting criterion for all objects. This also applies to moved-from objects. You might argue that in your sorting algorithm you should know which object was moved so that you can avoid comparing it, but the C++ standard library does not require that. This, by the way, also means that you can pass moved-from objects to sort them. As long as they support all required operations, everything is fine.