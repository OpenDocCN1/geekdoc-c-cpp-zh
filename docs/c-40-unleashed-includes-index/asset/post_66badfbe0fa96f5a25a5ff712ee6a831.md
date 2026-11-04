
Location property for a table and a kid in two different rooms, where location is relative to some corner of the room. The table is positioned at position (10,10), and the kid is reading his Tintin book also at position (10,10), so the same instance of the Point type could be used for both:

```
var p = new Point(10,10); // with Point a reference type
kid.Location = p;
table.Location = p;
```

Now, what happens if the person in the first room wants to move his table to position (20,20)? Different approaches can be taken, but the aliasing property of reference types can be disadvantageous. Because the same instance of Point is used for both Location properties, changes to this very instance will affect both objects’ locations:

```
p.X += 10;
p.Y += 10;
```

I’m guessing the kid won’t be happy to be moved by some invisible teleportation force, as illustrated in Figure 9.4.

![](img/a16f85e62ce9bdc527f4b09dbfe26092_496_0.png)

FIGURE 9.4 Point as a reference type.

Two things are really going on here. First, the fact Point is treated as a reference type makes aliasing possible. Second, we can assign to X and Y of the Point object—that is, the data is mutable. There are different ways to avoid the problem, but really the core problem lies in the fact we're using a reference type to denote something that has value characteristics. Is it really the case multiple things should be able to *refer* to the same point? Rather unlikely.

Using a value type for Point, things start to look quite different. Even though the same code will work, semantics are different. Upon assignment of the struct's value to the different Location properties, a copy is taken:

```
    var p = new Point(10,10); // With Point a value type
    kid.Location = p;
    table.Location = p;
```

The kid and table objects no longer refer to the same object: They simply don't *refer* to the point anymore; instead, they *store* a point *value*. The effect of changing the point's value on one of the objects is illustrated in Figure 9.5.

![](img/a16f85e62ce9bdc527f4b09dbfe26092_497_0.png)

FIGURE 9.5  Point as a value type.

## MUTABILITY, AN ORTHOGONAL CONCERN

The main consideration for choosing between value types versus reference types should be the desired semantics. If you naturally refer to some object, a reference type is appropriate so that multiple entities can refer to the same instance of it. On the other hand, value types represent things that are just that: values, as in quantities, coordinates, colors.

Although it typically doesn't make sense to mutate a value—and indeed, doing so is highly discouraged, as discussed later—neither the runtime nor the C# language prevents you from doing it. But quick, tell me what it would mean to you to change the number 1 or tweak the RGB representation of the color Red.

Reference types, more often than not, are written to be mutable in true imperative programming style, which gets reflected in object-oriented programming, as well (although it's not a fundamental pillar of OO). For example, calling a method for money transfer on an account will change its balance, and setting a person's age property will, uhm, change its age. However, it's perfectly doable to construct reference types that are immutable: Once created, you can't change their state anymore. The canonical example of an immutable reference type is System.String.

The de facto use of mutability in all sorts of circumstances is no longer an ideal practice in today's world of concurrent software. The more mutable state there is, the more synchronization is needed when objects are handed out and all sorts of components can start to mutate them. Therefore, the use of data structures that are immutable by default can be a huge advantage to aid in parallelizing software. When state is only readable, it's fine to hand out objects to different components; they can't spoil things. Simply stated, "shared mutable state = trouble."

At this point, neither the runtime nor most languages on top of it provide direct means to ensure or enforce immutability. That certainly may change in the future because the role of parallel computing is increasing. Traces of this influence can be found today in the new .NET 4.0 System.Threading namespace but also in the F# language where immutability is the default.

In summary, structs are value types and classes are reference types. Figure 9.6 highlights the role of structs and classes in the bigger picture of types. To declare such types, dedicated keywords are used, which unsurprisingly are called struct and class, respectively:

```csharp
struct Point
{
    // Members go here.
}

class Person
{
    // Members go here.
}
```

![](img/a16f85e62ce9bdc527f4b09dbfe26092_499_0.png)

FIGURE 9.6 Structs and classes.

## Heap Versus Stack

Lots of books start the discussion about reference types versus value types by pointing out their different memory-allocation characteristics. To say the least, this is a weird thing to do because this is truly an implementation detail. So the first decision factor when choosing between a reference type and a value type should concentrate on the intended semantics as opposed to potential benefits in terms of memory-allocation and -deallocation patterns.

We should pay some attention to the way things work on this level, too. Here's the deal:

- Value types (such as structs) are stack allocated.
- Reference types (such as classes) are heap allocated.

I'm actually omitting a slight detail for now (boxing), but this is the general picture. Pretty simple, isn't it? So, what's this heap and stack thing all about? We've already seen the use of the evaluation stack when looking at some intermediate language (IL) code generated by the C# compiler. The data stored for value type instances simply lives on that stack directly (that is, without referring to some other place in memory). For example, Int32 is a value type, so in the following method, variables a and b, as well as the return value, live directly on the stack:

```
static int Add(int a, int b)
{
    return a + b;
}
```

Recall that this code basically performs four operations on the IL level, to fetch the two arguments one by one (pushing them on the stack), add them, and return to the caller:

```
ldarg.0
ldarg.1
add
ret
```

Figure 9.7 shows how this method operates, assuming it has been called from some Main method that passed in arguments 3 and 5.

![](img/a16f85e62ce9bdc527f4b09dbfe26092_500_0.png)

FIGURE 9.7 Value types' values live on the stack.

Strictly speaking, the runtime doesn't require all stack structures to be interwoven. In fact, we're dealing with at least two conceptual stacks:

- The call stack, where arguments, locals, and return values are kept
- The evaluation stack, where the IL code operates on as some kind of scratchpad

What's of more importance here is to observe that the values themselves are allocated on the stack. This has a couple of interesting effects with regard to memory use: A value can't outlive its stack frame. (That is, when a method returns, all its local variables and argument values are automatically deallocated.) In the last transition in Figure 9.7, this is made very clear: When Add returned, the values 3 and 5 that lived in its stack frame got lost.

## THE KEY TO RECURSION

Stack-allocated arguments and return values are the key to enabling recursion where a method is permitted to call itself. In much more primitive languages, arguments to procedures were kept in statically known memory locations. As a result, only one call to a certain procedure could be in flight at the same time because there's only one place for its arguments. Making a second call would override the data in those argument slots, and similar problems exist for keeping track of the return value (and the return address, for the same reason).

Not only deallocating memory on the stack is trivial (simply by lowering the high-water mark for memory allocated on the stack), allocation is equally trivial. Just store the value on top of the stack and move the high-water mark up for subsequent allocations not to overwrite the newly allocated value. If the stack runs out of space for some reason (for example, too deep recursion), a StackOverflowException results.

The main advantage lies in the trivial deallocation, which has a performance benefit over deallocation of heap objects, as you will see. As a downside, extra care is needed when handing out references to objects on the stack. Luckily, this is something the C# language protects us against, putting very strict rules on passing stack-allocated objects “by reference.” We discuss this further in Chapter 10, “Methods,” but here’s the idea:

```
static void ChangeIt(ref int a)
{
    a = 42;
}

static void Main()
{
    int x = 24;
    ChangeIt(ref x);
    Console.WriteLine(x); // will print 42
}
```

Notice that the use of the ref keyword to indicate a parameter is passed by reference, both at the declaration site (the ChangeIt method definition on top) and the use site (the call to it from Main). The execution of the preceding code is depicted in Figure 9.8.
