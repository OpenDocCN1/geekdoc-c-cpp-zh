a constructor.) By convention, constructors in JavaScript begin with a capital letter to distinguish them from nonconstructor functions. For example, this code instantiates a generic object and stores a reference to it in object:

```
var object = new Object();
```

Reference types do not store the object directly into the variable to which it is assigned, so the object variable in this example doesn’t actually contain the object instance. Instead, it holds a pointer (or reference) to the location in memory where the object exists. This is the primary difference between objects and primitive values, as the primitive is stored directly in the variable.

When you assign an object to a variable, you’re actually assigning a pointer. That means if you assign one variable to another, each variable gets a copy of the pointer, and both still reference the same object in memory. For example:

```
var object1 = new Object();
var object2 = object1;
```

This code first creates an object (with new) and stores a reference in object1. Next, object2 is assigned the value of object1. There is still only the one instance of the object that was created on the first line, but both variables now point to that object, as illustrated in Figure 1-3.

![](bbox=[0.24, 0.56, 0.82, 0.73])

Figure 1-3: Two variables pointing to one object

# Dereferencing Objects

JavaScript is a garbage-collected language, so you don’t really need to worry about memory allocations when you use reference types. However, it’s best to dereference objects that you no longer need so that the garbage collector can free up that memory. The best way to do this is to set the object variable to null.