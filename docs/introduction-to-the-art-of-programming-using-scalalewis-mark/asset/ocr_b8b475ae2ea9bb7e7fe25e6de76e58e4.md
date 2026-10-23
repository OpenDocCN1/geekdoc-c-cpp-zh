objects¹ which extend the first class. The use of case types makes it easier to take full advantage of the pattern matching.

# B.5 Covariant, Contravariant, and Invariant Types

Chapter 25 brought up the concept of covariant types in relation to immutable linked lists. This deals with how Scala treats type parameters when it comes to determining subtype relationships for the main type. Imagine you have the following declarations.

```
class Stuff[A](val a:A)
class MoreStuff[A](a:A, val b:A) extends Stuff[A](a)
```

You can see from this that MoreStuff is a subtype of Stuff. However, this ignores the fact that Stuff and MoreStuff are not well-defined types on their own. In reality, you have to provide a type parameter to have a well defined type. In this case we can say that MoreStuff[String] is a subtype of Stuff[String]. The question is, is MoreStuff[String] and subtype of Stuff[AnyRef]? You might be tempted to say that it is, but as written, it is not. If you try to pass an instance of MoreStuff[String] into a function/method that accepts Stuff[AnyRef], Scala will complain. If you put the types above into the REPL, you can quickly test that with the following.

```
scala> def hasNull(s:Stuff[AnyRef]) = s.a==null
hasNull: (s: Stuff[AnyRef])Boolean
```

```
scala> val s = new Stuff("Hi")
s: Stuff[String] = Stuff@c8d310f
```

```
scala> hasNull(s)
<console>:11: error: type mismatch;
 found : Stuff[String]
 required: Stuff[AnyRef]
Note: String <: AnyRef, but class Stuff is invariant in type A.
You may wish to define A as +A instead. (SLS 4.5)
        hasNull(s)
                 ^
```

```
scala> val ms = new MoreStuff("hi","mom")
ms: MoreStuff[String] = MoreStuff@035e20aca
```

```
scala> hasNull(ms)
<console>:12: error: type mismatch;
 found : MoreStuff[String]
 required: Stuff[AnyRef]
Note: String <: AnyRef, but class Stuff is invariant in type A.
You may wish to define A as +A instead. (SLS 4.5)
        hasNull(ms)
                 ^
```