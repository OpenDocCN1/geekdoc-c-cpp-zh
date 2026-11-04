query, such as a filter's predicate function or a projection's mapping function. For local query execution, it makes perfect sense to compile those lambda expressions to pieces of IL code that can run on the local machine. But when the query is supposed to run remotely, say on a relational database engine, it needs to be translated into a target query language, say SQL.

LINQ providers that target external data stores therefore need a way to cross-compile the user's intended query expression—that was written using LINQ—into whatever query language they're targeting, such as SQL, XPath, and so on. Various approaches can be taken to solve this:

+   - Do not support extensibility for LINQ; instead, bake knowledge of various query languages into the C# compiler and let it do the translation. Clearly this is unacceptable from a maintenance point of view and clashes with the main goal of LINQ (that is, to provide unification of all sorts of query languages, including the ones we don't know of yet).
+   - Have LINQ providers decompile the intermediate language (IL) code that was emitted by the C# compiler and go from there to the target query language. Not only would this be far too complicated to be widely accepted by query provider writers, but it also would prevent the compiler from changing its IL emission (for example, to add more optimization, given that query providers would expect specific patterns).
+   - Instead of turning lambda expressions directly into IL code, translate them into some kind of intermediate representation with an object model that can be consumed by query providers. This sounds much more promising, and this is where expression trees come in.

So what are those expression trees? In essence, they are a way to represent code as data that can be inspected at runtime. Consider the following lambda expression:

```
(int a, int b) => a + b;
```

Two possible translations exist. The first one is to turn it into IL code that's readily available for local execution, using delegates:

```
Func<int, int, int> add = (a, b) => a + b;
int three = add(1, 2);
```

The alternative is to assign the lambda expression to an expression tree, in which case the compiler emits the code as data:

```
Expression<Func<int, int, int>> add = (a, b) => a + b;
// the code represented by add can be inspected at runtime
```

A graphical representation of the expression tree used in our previous example is shown in Figure 2.3.