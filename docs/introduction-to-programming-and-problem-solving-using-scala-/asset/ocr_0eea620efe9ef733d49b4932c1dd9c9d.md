# Type Basics and Argument Passing

Near the bottom on the right side of the figure is a type called Null. This is a subtype of all the AnyRef types. One implication of this is that any AnyRef type, or any function/method with a result that is a subtype of AnyRef can have a value of null. This exists in Scala to maintain backward compatibility with Java. However, as a general rule you should try to avoid using Null in your programs as they are very prone to crash.

At the very bottom of the diagram is a type called Nothing which is a subtype of all other types in Scala. There is no value of Nothing which exists to make the type system complete and handle situations when functions do not result in anything. We are not going to do anything in this block that requires you to use the Nothing explicitly, but there are times it might appear anyway, and understanding what it will help you figure out what is going on. Consider the following examples that make an empty List and an empty Array.

```
scala> List()
res8: List[Nothing] = List()
scala> Array()
res9: Array[Nothing] = Array()
```

Note that the type was inferred by Scala. Do not freak out when you see it. Instead replace something in your code that is probably not giving Scala enough information about types to figure out something else.

# 7.5 Variable Length Argument Lists

Have you wondered how we are construct Lists and Arrays with calls like this?

```
val lst = List(7,4,6,3,9,1)
val lst2 = List(1,2,3)
```

What exactly is going on? It turns out that List in this usage is one of singleton objects mentioned in section 7.1, and you have put code in it that allows it to be called like a function. More importantly for us now, we are able to pass a variable number of arguments in this call. In the first case we have seen, it would just as well with any other number. The functions we have written cannot do this. So far we had an argument with a specific number of values in it. How can we make it our function let us pass in a variable number of arguments? In Scala, this is not hard to do. This will allow the caller to pass zero or more of the type to create a VARIABLE LENGTH ARGUMENT LIST.·4

A convenient place to do this would be an average function like we might use for calculating a grade. Such method might look something like this:

```
def average(nums:Double):Double = ???
```

> ·These are referred to by the shorter name, varags.