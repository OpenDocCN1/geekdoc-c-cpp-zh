
In fact, you can verify that it has found the correct maximum value in this particular example, e.g., just by visually inspecting the example input and output.

We will briefly discuss automatic testing later in the book.

There seems to be a bit of confusion regarding software testing in the community. Some people ask whether all software need to be tested.

The software testing can be classified in many different ways, including unit testing vs integration or system testing, black-box testing vs white-box testing, and manual testing vs automatic testing, etc.

The question is not *whether*. The answer to this question is always *yes*. All software *must* be tested. In some way. To some degree.

The real question is *how* and *how much*. Some developers religiously follow the TDD (test driven development), in which they write automatic test programs first *before* they even start working on the main software. Some developers insist on the "100% code coverage", which means that every branch of the code execution flows (e.g., *if* vs *else*) needs to be tested.

The author, personally, does not believe in any of these extremes. In many cases, what is "reasonable" dictates what kind of testing, and to what degree, needs to be done. Sometimes "good enough" is good enough.

### 11.2.2. Grammar

Generics is a very important part of the C# programming language.

It is not just an "advanced topic" which the beginning programmers can ignore "until later". You may not need to create your own generic classes or generic methods (in the beginning), but it is nonetheless essential to understand the basic concepts of generics.

This is similar to the use of *delegates*. You may not have a need to define your own delegates "until later", but you will still need to understand what they are and how to use them. Note that we introduced the delegates rather early in this book.

The main program calls the generic `TryFindMax()` method with an "integer list" (`List<int>`).

.NET defines a number of "collection types". It supports a *list*, which is a dynamically sized list data structure, and a *dictionary*, which is a key value mapping data structure, among other types.

One thing to note is that there are two different kinds for each collection type and their related types such as interfaces, etc.

One kind is a "non-generic" kind. It stores any object, value or reference, as a base type `object`. Since all types in C# inherits from `object` (`System.Object` in .NET), we can store any objects in a non-generic collection instance. These are there primarily for historical reasons, however.

If you use non-generic collections (e.g., from the `System.Collections` namespace), you may end up losing most, if not all, of the benefits of using the strongly typed languages like C#. We will not use any non-generic collections in this book.

The other kind is *generic* collections. The generic collection types can support a broad range of specific types as their elements, like `int` or `string`, not just the broadest possible type object.

The catch is that when you instantiate a generic collection type, you need to specify a specific type. That is, although a generic type or generic method, in general, can support a range of types, e.g., more than one types, for its "associated type(s)", one can only use the generic type/method by fixing its associated type(s) to a specific type(s) (allowed by the generic definitions).

The variables of an instantiated/specialized generic type are no longer "generic". They only work with that specific type.

The sample code uses a generic list `System.Collections.Generic.List<T>`, which is sort of a dynamic array, whose size can change at run time unlike the builtin array type.

The T in the angular brackets (<...>) is known as the "type parameter". It is just a placeholder (for the associated type), and it is customary to use the letter T (T for "Type"), if there is only one type parameter, although that is not required.

As stated, we define a generic type (and, a generic collection) "generically" (that is, over a range of different types), but we can only use it for a particular fixed associated type (i.e., its element type).

In the example, we use the `int` type:

```
var list = new List<int>();
```

This statement declares a variable `list` of type `List<int>`. An instance of the `List<int>` type can contain elements of type `int`, but nothing else. Note the relationship between the collection type `List<int>` and its associated element type `int`.

If you are new to C# and haven't used any generics before, then the syntax using the angular brackets might seem strange at first.

**i**
But, `List<int>` is conceptually no different from, for example, `ListOfInts`. Unlike the arbitrary names `ListOflnts` or `List_Of_Integers`, etc., however, the compiler can do a lot for `List<int>`. For one thing, you cannot store objects of any types other than `int` into `List<int>` (because that is the contract imposed by the generics).

A list (generic or non-generic) can be initialized using the list initializer syntax (or, more broadly, the "collection initializer" syntax). In the example, we use a pair of curly braces to specify a set of initial integer values, just like the way we do with the array initializations.

The type of list declared this way (using var) is `List<int>?`, that is a nullable list of `ints`. This fact does not concern us for this particular example. One could have explicitly declared the variable as the type `List<int>`.

Furthermore, note that it is often customary to use an interface type (which is considered "broader") than an implementation type (which is considered "narrower"). In the case of the generic class `List<T>`, it "implements" a generic interface `IList<T>`. Therefore, `List<int>` implements `IList<int>`.

We could have declared list as follows, since we do not use any implementation details specific to the `List<int>` implementation.

```
IList<int> list = new List<int>(){
    17, 9, 21, 33, 22,
};
```

Or, we could have just declared it as `List<int>`. In this small example, there is little difference.

If we declare a variable with a specific implementation type, then we can use the shorthand new( ) syntax on the right hand side because the type of the right hand side expression is fixed by the explicit declaration of type List<int>.

```
List<int> list = new( ) {
   17, 9, 21, 33, 22,
};
```

![](img/25af69ec45b3c0b589a8dccd0c2a88be_182_0.png)

We will go over the basic concepts of the "object oriented programming" (OOP) later in the book, in particular, in the first few lessons of the next part. For now, if anything does not make sense to you, then you can just ignore them and move on.

As a general comment, you will get most out of this book by reading through the book from beginning to end (or, as far as you can go) rather than trying to understand every detail.

The main program then calls the TryFindMax( ) static method of the Finder class with this test integer list.

The TryFindMax( ) method is defined using generics. Although we only use it for List<int> in this particular case, there can be benefits for working on a slightly more general, or broader, problem. In any case, this is for illustration.

Let's look at the method declaration:

```
bool TryFindMax<T>(IList<T> list, out T? max) where T : IComparable<T> {
}
```

We discussed the internal access modifier, which makes this method accessible by anyone in the same assembly, and the static modifier, which makes it behave like a function, not an object member method.

### 11.2. Code Reading - TryFindMax Function

The method returns a bool value, and its name has a type parameter appended at the end. This indicates that TryFindMax<T>() is a generic method. The associated type parameter, T by convention, can be used, once declared this way, in the method parameter list as well as in the body of the method.

In general, T can be any type. In certain method definitions, or type definitions, however, using an arbitrary type may not make sense. In this particular example, the method is supposed to return the biggest value among the elements in a given list.

If a particular type T has no concept of "biggest", or "bigger" more generally, then this method will not make sense for such a type. This is where the where clause comes in. It is called the "type constraint".

We are declaring that we are defining the TryFindMax<T> method only for the types that implements the interface IComparable<T> from the System namespace, not for any type. (Note that we are using using System in virtually every source file when we use anything from the System namespace.)

That is, one cannot use our TryFindMax<T> method with an associated type that does not implement System.IComparable<T>.

System.Int32 (or, int), as well as all other numeric types in C#, happens to implement System.IComparable<System.Int32> (or, the corresponding IComparable<T> specializations). That is, the values of the int type are "comparable". (We will discuss the interfaces in more detail later in the book.)

Why is this important? This is because the implementation uses the fact that an object of that type has a method CompareTo(T) (as defined in IComparable<T>). This is a "codification" of the condition, as stated, that the values of the type need to be "comparable". Otherwise, the "max" cannot be defined.

Let's first take a look at an example which does not use generics. Let's keep using int for simplicity.
