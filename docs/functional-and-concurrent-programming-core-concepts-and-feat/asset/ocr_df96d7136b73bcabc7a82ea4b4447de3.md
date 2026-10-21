# # Chapter 15 Types (and Related Concepts)

Sometimes, the type being inferred cannot even be expressed in the programming language:

```
```java
var task = new Runnable() {
public int result;
public void run() {
result = 42;
}
};
task.run();
int r = task.result; // 42
```
```

Variable task is defined using var, without an explicit type. The type inferred by the Java compiler is not Runnable—for which task.result on the last line would be rejected—but a form of Runnable that also defines a public field result. This type cannot be expressed within the Java language.6

When a compiler makes a decision that does not suit your needs, you can sometimes specify a desired type explicitly, as long as you choose a type that contains the value. For instance, this code cannot be compiled:

```
```scala
var books = List.empty
books ::= book1 // rejected by the compiler
```
```

The intent is for books to start as an empty list, to which books can then be added. However, the compiler infers type List[Nothing] for variable books and refuses to reassign it with a list of books. Instead, you can express your intent with an explicit type declaration:

```
```scala
var books: List[Book] = List.empty
books ::= book1 // adds book1 to the list
```
```

The variants var books = List.empty[Book] (an explicit type parameter to function empty) and var books = List.empty : List[Book] (a type ascription on value List.empty) would also work. Similarly,

```
```scala
var solution = None
if solutionIsFound then solution = Some(value) // rejected by the compiler
```
```

> It can be expressed in Scala as Runnable { def result: Int }.