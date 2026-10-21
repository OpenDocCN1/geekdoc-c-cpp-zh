In Kotlin, you can define functions as extensions and invoke them as methods. Also, a Kotlin method declared infix can be invoked in infix notation. This example combines both features to define an infix extension max to integers:

```
infix fun Int.max(that: Int): Int = if (this > that) this else that
```

Given this definition, you can write expressions like x.max(y) or x max y on integers x and y. There is no support for these features in Java.

Neither language supports symbolic names, but several operators can be defined in Kotlin by implementing a corresponding method:

```
operator fun String.times(count: Int): String {
    val builder = StringBuilder(this.length * count)
    for (i in 1..count) builder.append(this)
    return builder.toString()
}
"A" * 3 // "AAA"
```

In this example, an operator * similar to Scala’s is added on strings by implementing an extension method times. Other operators have corresponding method names: “+” is plus, “++” is inc, “+=” is plusAssign, “..” is rangeTo, and so on.

A special method invoke plays the role of Scala’s apply:

```
operator fun String.invoke(i: Int): Char = this[i]
"foo"(2) // 'o'
```

Note that this[i] is actually compiled into a method call this.get(i). By defining your own get, you can set up a square bracket syntax on your own types, something that is not possible in Scala. There is no support for user-defined operators or for functions applied implicitly in Java.

In both Java and Kotlin, you can parameterize functions by types. For instance, the following function returns the first and last elements of a list as a short list: