# 2.10 Type Parameters

In many typed programming languages, functions can be parameterized by types. What this means is that a function not only uses typed arguments, but the types of these arguments (and the type of the return value) are themselves arguments of the function. This is known as parametric polymorphism, sometimes referred to as generics (Java) or templates (C++). Consider function first, which returns the first element of a pair:

```
// DON'T DO THIS!
def first(pair: (Any, Any)): Any = pair(0)
```

Argument pair has type (Any, Any), which represents pairs of any types—Any being the type of everything in Scala. The function can be applied to a pair of integers, as in first((1, 2)), or a pair of strings, as in first(("A", "B")). The problem with this definition of first is that its return type is Any. When you apply first to a pair of integers, the function returns a value of type Any. This value happens to be an integer, but the type information is lost:

```
first((1, 2))                         // has type Any
first((1, 2)) + 10                    // rejected by the compiler
first(("egg", "chicken"))           // has type Any
first(("egg", "chicken")).toUpperCase // rejected by the compiler
```

With explicit names, arguments can be reordered arbitrarily. All of the following calls are valid:

```
formatMessage(msg = "hello", user = "Joe")
formatMessage(user = "Joe", msg = "hello")
formatMessage(user = "Joe", withNewline = false, msg = "hello")
```

Even when they are not strictly necessary, you can sometimes rely on argument names to improve code readability:

```
formatMessage("Tweedledee", "Tweedledum") // which is user and which is message?
formatMessage(msg = "Tweedledee", user = "Tweedledum") // clearer

Writer("/var/log/app.log", true) // what is true?
Writer("/var/log/app.log", autoflush = true) // clearer
```