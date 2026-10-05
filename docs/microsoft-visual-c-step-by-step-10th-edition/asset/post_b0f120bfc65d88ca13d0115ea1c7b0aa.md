
[content]

- When you create an object (an instance of a class) by using the `new` keyword, the memory required to build the object is acquired from the heap. You've seen that the same object can be referenced from several places using reference variables. When the last reference to an object disappears, the memory used by the object becomes available again (although it might not be reclaimed immediately). Objects created on the heap therefore have some indeterminate lifespan; an object is created using the `new` keyword, but it disappears sometime after the last reference to the object is removed. Chapter 14 includes a more detailed discussion of how heap memory is reclaimed.

> Note
> All value types are created on the stack. By default, reference types (objects) are created on the heap, although the reference itself is on the stack. (There are some exceptions to this rule, which you'll learn in later chapters.) Nullable objects are actually reference types, and are created on the heap.

The names `stack` and `heap` come from the way in which the runtime manages the memory:

- Stack memory is organized like boxes stacked neatly on top of one another. When a method is called, each parameter is placed in the top of the stack. Each local variable is likewise assigned a box, which is placed on top of boxes already on the stack. When a method finishes, think of it as being like a box being removed from the stack.
- Heap memory is a large pile of boxes strewn around a room rather than stacked neatly on top of one another. Each box has a label indicating whether it is in use. When a new object is created, the runtime searches for an empty box and allocates it to the object. The reference to the object is stored in a local variable on the stack. The runtime keeps track of the number of references to each box. (Remember: two variables can refer to the same object.) When the last reference disappears, the runtime marks the box as not in use; at some point in the future, it empties the box and makes it available.

# Using the stack and the heap

Now let's examine what happens when a method named Method is called:

```c
void Method(int param)
{
    Circle c;
    c = new Circle(param);
    ...
}
```

Suppose the argument passed into param is the value 42. When the method is called, a block of memory (just enough for an int) is allocated from the stack and initialized with the value 42. As execution moves inside the method, another block of memory big enough to hold a reference (a memory address) is also allocated from the stack, but left uninitialized. This is for the Circle variable, c. Next, another piece of memory big enough for a Circle object is allocated from the heap. This is what the new keyword does. The Circle constructor runs to convert this raw heap memory to a Circle object. A reference to this object is stored in the variable c. The following illustration shows this process:

![](img/4f6c1423ece9eeb79a4a4e5db8b1746d_346_0.png)

At this point, you should note two things:

- Although the object is stored on the heap, the reference to the object (the variable c) is stored on the stack.
- Heap memory is not infinite. If heap memory is exhausted, the `new` operator will throw an `OutOfMemoryException` exception, and the object will not be created.

> Note
> The `Circle` constructor could also throw an exception. If it does, the memory allocated to the `Circle` object will be reclaimed, and the value returned by the constructor will be `null`.

When the method ends, the parameters and local variables go out of scope. The memory acquired for `c` and `param` is automatically released back to the stack. The runtime notes that the `Circle` object is no longer referenced and at some point in the future will for its memory to be reclaimed by the heap. (See Chapter 14.)

# System.Object class

One of the most important reference types in .NET is the `Object` class in the `System` namespace. To fully appreciate the significance of the `System.Object` class, you must understand inheritance, which is described in Chapter 12, “Working with inheritance.” For now, simply accept that all classes are specialized types of `System.Object` and that you can use `System.Object` to create a variable that can refer to any type. `System.Object` is such an important class that C# provides the `object` keyword as an alias for `System.Object`. In your code, you can use `object`, or you can write `System.Object`. They mean the same thing.

> Tip
> The `object` keyword rather than `System.Object`. It’s more direct, and it’s consistent with other keywords that are synonyms for classes, such as `string` for `System.String` and others that are covered in Chapter 9.

In the following example, the variables c and o both refer to the same Circle object. The fact that the type of c is Circle and the type of o is object (the alias for System.Object) in effect provides two different views of the same item in memory.

```csharp
Circle c;
c = new Circle(42);
object o;
o = c;
```

The following diagram illustrates how the variables c and o refer to the same item on the heap:

![](img/4f6c1423ece9eeb79a4a4e5db8b1746d_348_0.png)

# Boxing

As you have just seen, variables of type object can refer to any item of any reference type. However, variables of type object can also refer to a value type. For example, the two statements initialize the variable i (of type int, a value type) to 42 and then initialize the variable o (of type object, a reference type) to i:

```csharp
i = 42;
object o = i;
```

The second statement requires a little explanation to appreciate what's actually happening. Remember that i is a value type and that it lives on the stack. If the reference inside o referred directly to i, the reference would refer to the stack. However, references should refer to objects on the heap.

Creating uncontrolled references to items on the stack could seriously compromise the robustness of the runtime and potentially create a security flaw, so it is not allowed. Therefore, the runtime allocates a piece of memory from the heap, copies the value of integer i to this piece of memory, and then refers the object o to this copy. This automatic copying of an item from the stack to the heap is called boxing. The following diagram shows the:

![](img/4f6c1423ece9eeb79a4a4e5db8b1746d_349_0.png)

> Important
> If you modify the original value of i, the boxed value referenced through o will not change.

# Unboxing

Because a variable of type object can refer to anything, it's only reasonable that you can get the boxed value through the variable. You might expect to be able to access the int value by using a simple assignment statement such as:

```csharp
int i = o;
```

However, if you try this syntax, you'll get a compile-time error. After all, o could be referencing anything and not just int. Consider what would happen in the following code if this statement were allowed:

```csharp
Circle c = new Circle();
int i = 42;
object o;
o = c; // refers to a circle
i = o; // what is stored in i?
```

To obtain the value of the boxed copy, you must use what is known as a cast. This is an operation that checks whether converting an item of one type to another is safe before actually making the copy. You prefix the object variable with the name of the type in parentheses, as in this example:

```csharp
int i = 42;
object o = i; // boxes
i = (int)o; // compiles okay
```

The value of this cast is subtle. The compiler notices that you've specified the type int in the case. Next, the compiler generates code to check what o refers to at runtime. It could be absolutely anything. Just because your cast says o refers to an int, doesn't mean it actually does. If o really refer to a boxed int and everything matches, the cast succeeds, and the compiler-generated code extracts the value from the boxed int and copies it to i. (In this example, the boxed value is then stored in i.) This is called unboxing. The following diagram shows what's happening:

On the other hand, if o does not refer to a boxed int, there is a type mismatch, causing the cast to fail. The compiler-generated code throws an InvalidCastException exception at runtime. Here's an example of unboxing cast that fails:
[/content]
