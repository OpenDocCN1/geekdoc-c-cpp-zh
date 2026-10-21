
In this instance, Python is the fussier language, refusing to append a number to a string. So, it is not necessarily the case that a language is always stronger, or always weaker. Furthermore, what’s acceptable varies not only from language to language, but also over time. As of today, the variant

```
price + ": " + book.title
```

is rejected by Python, triggers a deprecation warning in Scala, and is perfectly fine in Java. Before concluding that Python is more strongly typed than Scala—itself more strongly typed than Java—consider a different scenario:

```
if book.pagecount:
    print(book.title)
```

In this program, the number of pages in a book—ostensibly an integer—is being used as a Boolean value in a test. This works in Python, but would trigger a type error in both Scala and Java.

You might argue that using numbers in tests is convenient—pagecount in the preceding test stands for pagecount != 0—but being loose with the Boolean type can also be dangerous. Consider first this Java program:

```
Set<Book> books = ... // a set of books

if (books.add(book))
    added += 1;
```

Method add returns true if an element is actually added (that is, if it was not already in the set). As a result, this code correctly counts added books. However, don’t write the same thing in Python:

```
books = ... # a set of books

# DON'T DO THIS!
if books.add(book):
    added += 1
```

The add method in Python is “void”: It returns None,¹ and None evaluates to false in a Boolean test. Python’s type checking does not catch the mistake—the program can be executed, but variable added is not incremented.

> ¹This is Python’s None, not the None of options in Scala. Python’s None is closer to Scala’s unit.

## 15.1 Typing Strategies

To further muddy the discussion, languages can also define backdoors to their own type system, inviting weakness where the language is strong. The Python function

```
```python
def print_title(book):
    print(book.title)
```
```

displays book titles but can also be called on an integer, in which case it will fail from not finding a suitable title attribute (as described earlier). To better handle the mistake, the function can be rewritten to test the type of its argument explicitly:

```
```python
def print_title(book):
    if isinstance(book, Book):
        print(book.title)
    else:
        raise TypeError("not a book")
```
```

This added code is not needed in Scala, since the compiler can be trusted to check that the argument has the desired type. However, you can still write an equivalent to the Python function:

```
```scala
// DON'T DO THIS!
def printTitle(item: Any) =
    if item.isInstanceOf[Book] then
        val book = item.asInstanceOf[Book]
        println(book.title)
    else throw IllegalArgumentException("not a book")
```
```

Type checking by the compiler is bypassed, and replaced with a form of dynamic checking at runtime, thus weakening the overall type safety of the language.

Methods like isInstanceOf/asInstanceOf constitute a backdoor to the type system. They are sometimes necessary, but should not be abused. Some languages have no such loopholes. For example, the runtime type checking and casting used in function printTitle is not possible in—more static? more strongly typed?—languages like SML.

Although compilers can sometimes use type information to improve performance, the main motivation for types is to help programmers catch—and fix—mistakes. From a developer's standpoint, a useful type system is one that contributes to this goal, whether it does so by being “strong” or by being “static.”

Three characteristics of types often matter more to you as a programmer than the static/dynamic or strong/weak opposition. First, typing utility is determined by how

safe types are—that is, how effective they are at catching mistakes before these mistakes trigger runtime bugs. Second, convenience is contingent on how flexible a type system is: A flexible type system does not get in the way of the developer’s design. And third is simplicity: Some type systems are easier to understand, while others are more complex.

Of safety, flexibility, and simplicity, a programming language typically favors two at the expense of the third. How languages handle type variance, discussed in Section 15.8, is a perfect example. A language could make all data structures covariant; it would be simple and flexible, but unsafe. Or it can have them all be invariant, which is simple and safe, but lacks flexibility. Or it can define mechanisms for users to specify variance through annotations, which is safe and flexible, but more complex. In the case of variance, older languages (Java, C++) have favored simplicity and rigidity, but more modern languages (C#, Scala, Kotlin) have improved flexibility at the cost of increased complexity. The remainder of this chapter discusses several concepts that contribute to type safety, flexibility, and complexity.

## 15.2 Types as Sets

One simple way you can look at types is to think of them as sets of values.² The type String, for instance, is the set of all string values, and the type Int, the set of all (32-bit) integers. In terms of sets, "foo" ∈ String and 42 ∈ Int.³ If a program declares variable x to have type S, then x ∈ S should be true at all times during the execution of the program; otherwise, the type system is unsound. Similarly, if a function f specifies that its argument is of type T, a call f(x) is only valid if x ∈ T. Most importantly, if type S is a subtype of T, then S ⊆ T. Subtypes are discussed in Section 15.6.

As sets, types can be combined using standard set union and set intersection. Type S | T is the union of types S and T—in other words, the set of values that belong to S or to T. Type S & T is the intersection of types S and T. As an example, type Book & Serializable contains those book objects that can be serialized.

Some types are very small sets. For instance, Scala defines a type 42 that contains only the integer 42, and a type "foo" that contains only the string "foo". Type Unit also has a single element, value unit—denoted as "()"—and type Null contains only null. Type Boolean contains just two values, and so does type 0 | 1. This function flips 0 into 1 and 1 into 0, and can be invoked on only these two values:

```
def flip(x: 0 | 1): 0 | 1 = if x == 0 then 1 else 0
Scala
```

Smaller types are more precise and convey more information. The List(1,2,3) value is in type List[Int], but also in types Seq[Int], List[Any], and Any. Type List[Int] is the most informative: Seq[Int] includes non-list sequences, List[Any] includes lists of non-integer values, and Any includes objects that are not lists at all.

²Some languages, including Scala, also define kinds as sets of types. For instance, List is a kind that contains the types List[String] and List[Int], among others. This chapter does not cover kinds.

³"x ∈ S" denotes the fact that value x is an element of set S. "S ⊆ T" means that S is a subset of T: All the elements of S are also in T.

## 15.3 Types as Services

In Scala, every variable x defines a small type x.type that contains only x—the singleton {x} in terms of sets. For instance, the function

```
```scala
def doSomethingWithBook(book: Book): book.type = ...
```
```

does something with a book before returning it. Using Book as the return type would allow the function to return a different book, possibly a copy of the input. The very specific type book.type guarantees that the function returns the same book object used as input.

This approach is often used in “builder” classes to chain method calls. For instance, you can define a buffer with an append method:

```
```scala
class Buffer[A]:
  def append(value: A): Buffer[A] = ...
...
// used as:
val buffer = Buffer[String]()
buffer.append("foo").append("bar");
```
```

The intent is for method append to add an element to the buffer and to return the buffer itself so further operations can be applied. However, the Buffer[A] return type allows an implementation to return a different buffer. You can use a more specific type to make it clear that the buffer itself if being returned:

```
```scala
class Buffer[A]:
  def append(value: A): this.type = ...
...
```
```

Finally, some languages define a type Nothing that contains no value—the empty set. In Scala, for instance, the empty list, Nil, has type List[Nothing]. A function that specifies Nothing as its return type, such as Nil.head, cannot possibly return a value, since type Nothing is empty. All it can do is keep running forever or throw an exception. Because the empty set is a subset of every set, Nothing is a subtype of every type.

## 15.3 Types as Services

Another way you can look at types is to focus on how typed values can be used. In this view, a type is a collection of operations, or services, that you can utilize. A book is an object with a title, an author, and a page count. You can create a Book type to
