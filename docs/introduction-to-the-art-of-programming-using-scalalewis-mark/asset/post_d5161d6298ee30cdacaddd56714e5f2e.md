
List(6, 9, 1)
List(3, 9, 1)

- grouped(size:Int) Runs through the sequence, grouping items into groups of the specified size.

```
scala> lst.grouped(2).foreach(println)
List(7, 4)
List(6, 3)
List(9, 1)
```

```
scala> lst.grouped(3).foreach(println)
List(7, 4, 6)
List(3, 9, 1)
```

- inits - Provides an iterator going from the full sequence to an empty one, removing elements from the end.

```
scala> lst.inits.foreach(println)
List(7, 4, 6, 3, 9, 1)
List(7, 4, 6, 3, 9)
List(7, 4, 6, 3)
List(7, 4, 6)
List(7, 4)
List(7)
List()
```

- permutations - Lets you run through all the permutations of the sequence. Note that the example here only does permutations of the first three elements as there are 6! = 720 different ones for the full list.

```
scala> lst.take(3).permutations.foreach(println)
List(7, 4, 6)
List(7, 6, 4)
List(4, 7, 6)
List(4, 6, 7)
List(6, 7, 4)
List(6, 4, 7)
```

- sliding(size:Int) - Provides an iterator that gives the effect of sliding a window of a certain size across the sequence.

```
scala> lst.sliding(2).foreach(println)
List(7, 4)
List(4, 6)
List(6, 3)
List(3, 9)
List(9, 1)
```

```
scala> lst.sliding(3).foreach(println)
List(7, 4, 6)
List(4, 6, 3)
List(6, 3, 9)
List(3, 9, 1)
```

tails – Gives an iterator that runs through sublists starting with the full list and ending with an empty one removing one element from the left end each step.

```
scala> lst.tails.foreach(println)
List(7, 4, 6, 3, 9, 1)
List(4, 6, 3, 9, 1)
List(6, 3, 9, 1)
List(3, 9, 1)
List(9, 1)
List(1)
List()
```

If you want to do something more involved with the values given by the Iterator, you can convert it to a List or an Array with toList or toArray. However, if there are many elements, as is the case for lst.permutations you might want to filter it or do something else to narrow things down before doing that conversion.

These methods provide an easy way to do some more interesting work with data. For example, using sliding, you can quickly smooth noisy data by averaging a data series over a window. Using combinations or permutations, you could run through all possible options of some type and find the one that was the best in some way.

At some point you might have wondered where you would find out about all of these methods. Even with everything discussed in this section, our list is incomplete. The complete list of all the types available and methods for them can be found in the Applications Programmer Interface (API). You can find the Scala API at the main Scala website. This has a lot of elements that go beyond your current knowledge, but one of the main objectives of this book is that you will be able to look up information in the API when you have questions about how to do things in Scala.

## 7.5 A World of Types

We have only begun to scratch the surface when it comes to types in Scala. By the end of this book we will see that not only are there many, many types provided by the Scala language/libraries, we can define our own types and give them names. Still, it is worth being more explicit about what a type is and some of the details of types in Scala.

Let us begin with the question of what is a type. A type is a set of values and the associated operations that can be performed on those values. Consider the type Int. There are a set of different values that we can represent with an instance of Int. They are all the integer values between -2147483648 and 2147483647. There is also a set of operations that you can perform on an Int or on pairs of them such as addition and subtraction.

In this chapter we have begun to see that there is more to types in Scala than the basics like Int. The types List and Array are not complete on their own. They are parametric types. To be complete they have to have type parameters. So List[Int] is a complete type as is Array[String]. List and Array are far from the only parametric types. Many of the types in the Scala library are parametric. In the second half of this book we will make our own parametric types. For now it will be enough to talk about them in the existing library code and how they can be used with functions.

### 7.5.1 The Option Type

If you start digging through the API much you will find that the type Option comes up a fair bit. The idea of an Option type is that they should be used when you are not certain if you will have a value or not. An Option[A] can either be Some[A] or None. If it is Some it will have a value in it that can be retrieved with get. If there was no value then you get None and know that it does not have a value. An example of a method that does this is the find method on a sequence. You can call find on either a List or an Array and pass it a function that takes an element and returns a Boolean. The find method is supposed to return the first element for which the function returns true. That description sounds simple enough, but what if there is not one? What happens if find runs through the whole sequence and nothing makes the function return true? For that reason, the find method returns Option[A] where A is the type contained in the sequence. So if nothing works, it can return None.

Let us run through two examples to see how this works using our list of integers we have been using throughout this chapter.

```
scala> lst.find(_<4)
res20: Option[Int] = Some(3)
```

```
scala> lst.find(_<1)
res21: Option[Int] = None
```

The list does contain elements that are less than 4. The first of these is 3 so we get back Some(3). However, it does not contain anything less than 1 so that call returns None. You might wonder how you can use this type of return value. The answer is to use match. This little example takes the result of a find and tells us what it found or else tells us that nothing was found.

```
scala> lst.find(_<4) match {
| case Some(i) => "Found "+i
| case None => "Nothing found"
| }
res22: java.lang.String = Found 3
```

### 7.5.2 Parametric Functions

Types like List, Array, and Option are not the only things that can have parameters. Functions can have parameters as well. This is something that we will revisit later on, but it can help you to read the API if you are introduced to the syntax. We would make a function parametric if we want it to work with multiple different types. The simplest example of a PARAMETRIC FUNCTION is the identity method shown here.

```
scala> def ident[A](a:A)=a
ident: [A](a: A)A
```

This method takes an argument of any type and returns the value passed in. While there are not many situations where you would want to do this, it demonstrates the syntax of parametric functions. You simply place a type parameter name in square brackets between the function name and the normal argument list. It also demonstrates the power of parametric functions, especially if we put it to use as we do here.

```
scala> ident(3)
```

function f. So there are three types involved here, the type passed into g, the type returned by g then passed into f, and the type returned by f. Thanks to parametric types, we can write such a function in one line of Scala.

```
def compose[A,B,C] (f: (B)=>A, g: (C)=>B) : (C)=>A = (x)=>f(g(x))
```

### 7.5.3 Subtyping

So far we have talked about types as if they are completely independent and unrelated. We have written functions that might works with an Int or a String or a Tuple. By adding parameters we were able to make functions that could work with any type, but this still did not imply any relationship between the types. In reality, Scala, like most object-oriented languages, supports SUBTYPING. A type B is a SUBTYPE of type A if any place where we would want to use an object of type A, we can use an object of type B instead.

We will go into a lot more detail about subtyping when we talk about inheritance in chapter 19, but for now you should be aware of the term because there will be times when it will come up. Some of the general subtype relationships in Scala are shown in figure 7.1. At the top of the figure there is an ultimate supertype called Any. Every object in Scala is an instance of Any. Since all values in Scala are objects, everything is an instance of Any, either directly or indirectly. The types like Int and Double that we learned about back in chapter 3 are on the left-hand side of figure 7.1, a type called AnyVal which is a subtype of Any. On the right-hand side there is another type called AnyRef that has a bunch of unspecified types below it. All the other types we have or will talk about fall somewhere under AnyRef. At the bottom of the diagram is a type called Nothing which is a subtype of all other types in Scala. There is no value of type Nothing, The type exists to make the type system complete and to handle situations when functions do not return.

We will not be making significant explicit use of parametric functions and subtyping until significantly later in the book in chapter 19. However, these concepts will come up in implicit ways before then so you should be aware of their existence.

## 7.6 Variable Length Argument Lists

Have you wondered about constructing Lists and Arrays with calls like this?

```
val lst=List(7,4,6,3,9,1)
```

There are some details that we will not go into, but one aspect of this type of call is something that we now know enough to talk about. We are able to pass a variable number of arguments in this call. In this case we have passed six arguments, but it would work just as well with any other number. The functions we have written can not do this. Every function we have written so far has had an argument list with a specific number of values in it. So how can we make it so our function will let us pass in a variable number of arguments? In fact, it is not hard to do. Simply add an asterisk after the last type of the last argument in the parameter list. This will allow the caller to pass zero or more of that type.

A convenient place to do this would be an average function like we might use for calculating a grade. Such a method might look something like this.

```
def average(nums:Double*):Double =
```
