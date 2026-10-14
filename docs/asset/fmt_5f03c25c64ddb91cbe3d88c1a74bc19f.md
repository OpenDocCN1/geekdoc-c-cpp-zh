
In the following example, the variables `c` and `o` both refer to the same `Circle` object. The fact that the type of `c` is `Circle` and the type of `o` is `object` (the alias for `System.Object`) in effect provides two different views of the same item in memory.

```
Circle c;
c = new Circle(42);
object o;
o = c;
```

The following diagram illustrates how the variables `c` and `o` refer to the same item on the heap.

![](img/16f6e3fe08f01ddadb2741a92c392b0e_248_0.png)

## Boxing

As you have just seen, variables of type `object` can refer to any item of any reference type. However, variables of type `object` can also refer to a value type. For example, the following two statements initialize the variable `i` (of type `int`, a value type) to 42 and then initialize the variable `o` (of type `object`, a reference type) to `i`:

```
int i = 42;
object o = i;
```

The second statement requires a little explanation to appreciate what is actually happening. Remember that `i` is a value type and that it lives on the stack. If the reference inside `o` referred directly to `i`, the reference would refer to the stack. However, all references must refer to objects on the heap; creating references to items on the stack could seriously compromise the robustness of the runtime and create a potential security flaw, so it is not allowed. Therefore, the runtime allocates a piece of memory from the heap, copies the value of integer `i` to this piece of memory, and then refers the object `o` to this copy. This automatic copying of an item from the stack to the heap is called boxing. The following diagram shows the result:

![](img/16f6e3fe08f01ddadb2741a92c392b0e_249_0.png)

## Important

If you modify the original value of the variable `i`, the value on the heap referenced through `o` will not change. Likewise, if you modify the value on the heap, the original value of the variable will not change.

## Unboxing

Because a variable of type `object` can refer to a boxed copy of a value, it’s only reasonable to allow you to get at that boxed value through the variable. You might expect to be able to access the boxed `int` value that a variable `o` refers to by using a simple assignment statement such as this:

```
int i = o;
```

However, if you try this syntax, you’ll get a compile-time error. If you think about it, it’s pretty sensible that you can’t use the `int i = o;` syntax. After all, `o` could be referencing absolutely anything and not just an `int`. Consider what would happen in the following code if this statement were allowed:

```
Circle c = new Circle();
int i = 42;
object o;

o = c;  // o refers to a circle
i = o;  // what is stored in i?
```

To obtain the value of the boxed copy, you must use what is known as a cast. This is an operation that checks whether converting an item of one type to another is safe before actually making the copy. You prefix the `object` variable with the name of the type in parentheses, as in this example:

```
int i = 42;
object o = i; // boxes
i = (int)o;   // compiles okay
```

The effect of this cast is subtle. The compiler notices that you’ve specified the type `int` in the cast. Next, the compiler generates code to check what `o` actually refers to at run time. It could be absolutely anything. Just because your cast says `o` refers to an `int`, that doesn’t mean it actually does. If `o` really does refer to a boxed `int` and everything matches, the cast succeeds and the compiler-generated code extracts the value from the boxed `int` and copies it to `i`. (In this example, the boxed value is then stored in `i`.) This is called unboxing. The following diagram shows what is happening:

![](img/16f6e3fe08f01ddadb2741a92c392b0e_250_0.png)

On the other hand, if `o` does not refer to a boxed `int`, there is a type mismatch, causing the cast to fail. The compiler-generated code throws an `InvalidCastException` exception at run time. Here’s an example of an unboxing cast that fails:

```
Circle c = new Circle(42);
object o = c;    // doesn't box because Circle is a reference variable
int i = (int)o;   // compiles okay but throws an exception at run time
```

The following diagram illustrates this case:

```
Circle c = new Circle(42);
object o = c;
int i = (int)o;
```

`throw InvalidCastException`

You will use boxing and unboxing in later exercises. Keep in mind that boxing and unboxing are expensive operations because of the amount of checking required and the need to allocate additional heap memory. Boxing has its uses, but injudicious use can severely impair the performance of a program. You will see an alternative to boxing in Chapter 17, "Introducing generics."

## Casting data safely

By using a cast, you can specify that, in your opinion, the data referenced by an object has a specific type and that it is safe to reference the object by using that type. The key phrase here is "in your opinion." The C# compiler will not check that this is the case, but the runtime will. If the type of object in memory does not match the cast, the runtime will throw an `InvalidCastException`, as described in the preceding section. You should be prepared to catch this exception and handle it appropriately if it occurs.

However, catching an exception and attempting to recover in the event that the type of an object is not what you expected it to be is a rather cumbersome approach. C# provides two more very useful operators that can help you perform casting in a much more elegant manner: the `is` and `as` operators.

## The `is` operator

You can use the `is` operator to verify that the type of an object is what you expect it to be, like this:

```
WrappedInt wi = new WrappedInt();
…
object o = wi;
if (o is WrappedInt)
{
    WrappedInt temp = (WrappedInt)o; // This is safe; o is a WrappedInt
    …
}
```

The `is` operator takes two operands: a reference to an object on the left, and the name of a type on the right. If the type of the object referenced on the heap has the specified type, `is` evaluates to `true`; otherwise, `is` evaluates to `false`. The preceding code attempts to cast the reference to the object variable `o` only if it knows that the cast will succeed.

## The `as` operator

The `as` operator fulfills a similar role to `is` but in a slightly truncated manner. You use the `as` operator like this:

```
WrappedInt wi = new WrappedInt();
…
object o = wi;
WrappedInt temp = o as WrappedInt;
if (temp != null)
{
    …  // Cast was successful
}
```

Like the `is` operator, the `as` operator takes an object and a type as its operands. The runtime attempts to cast the object to the specified type. If the cast is successful, the result is returned and, in this example, is assigned to the `WrappedInt` variable `temp`. If the cast is unsuccessful, the `as` operator evaluates to the `null` value and assigns that to `temp` instead.

There is a little more to the `is` and `as` operators than is described here, and Chapter 12 discusses them in greater detail.

## Pointers and unsafe code

This section is purely for your information and is aimed at developers who are familiar with C or C++. If you are new to programming, feel free to skip this section.

If you have already written programs in languages such as C or C++, much of the discussion in this chapter concerning object references might be familiar in that both languages have a construct that provides similar functionality: a pointer.

A pointer is a variable that holds the address of, or a reference to, an 内存中的项（在堆上或堆栈上）。使用特殊的语法来标识变量为指针。例如，以下语句声明变量 `pi` 为指向整数的指针：

```
int *pi;
```

尽管变量 `pi` 被声明为指针，但它在初始化之前实际上并不指向任何地方。例如，要使用 `pi` 指向整数变量 `i`，可以使用以下语句以及取地址运算符（`&`），它返回变量的地址：

```
int *pi;
int i = 99;
...
pi = &i;
```

你可以通过指针变量 `pi` 访问和修改变量 `i` 中保存的值，如下所示：

```
*pi = 100;
```

此代码将变量 `i` 的值更新为 100，因为 `pi` 指向与变量 `i` 相同的内存位置。
