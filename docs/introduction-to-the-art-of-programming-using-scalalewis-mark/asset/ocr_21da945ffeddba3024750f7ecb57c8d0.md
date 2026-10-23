will continue to grow through the rest of the book and you want to be certain you understand what is going on with it.

# Scala Applications Revisited

If you have ever selected to option in Eclipse to make a Scala application, you have inevitably noticed that it does not create an object with a main method. Instead, it makes an object that extends a type called App. The App type provides a main method so your code simply goes into the body of the object. You can use the variable args to get hold of any command-line arguments. Here is a sample that does that.

```
object MyApp extends App {
  println(args mkString (" "))
}
```

Now that you know about inheritance, you can choose to use this method of making applications if you prefer.

# 19.4 Parametric Polymorphism

The inclusion polymorphism we get from inheritance and subtyping is not the only form of universal polymorphism. There is a second type called parametric polymorphism. This type of polymorphism was briefly discussed in section 7.5.2. It is also something that we have been using extensively since chapter 7. You use it every time you deal with a List or an Array. This is what we get when we write code that has type parameters.

You have become familiar with using parentheses to pass values to methods when you call them or classes when you construct a new object. In the same way, you can use square brackets to pass type parameters. Consider these two declarations.

```
scala> val lst1 = Array(1,2,3)
lst1: Array[Int] = Array(1, 2, 3)
```

```
scala> val lst2 = Array[Any](1,2,3)
lst2: Array[Any] = Array(1, 2, 3)
```

They both declare arrays that store the values 1, 2, and 3. Those values are all Ints so if we let Scala infer a type, as in the first case, we get Array[Int]. In the second case we explicitly pass in a parameter type of Any and we get back that type. The syntax here is to pass any type arguments in square brackets before the parentheses with the value arguments. You might feel like there is not any difference between these two lists, but the type parameter changes what you can do with them.

```
scala> lst1.sum
res0: Int = 6
```

```
scala> lst2.sum
<console>:9: error: could not find implicit value for parameter num: Numeric[Any]
```