# 7.5.1 The Option Type

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

# 7.5.2 Parametric Functions

Types like List, Array, and Option are not the only things that can have parameters. Functions can have parameters as well. This is something that we will revisit later on, but it can help you to read the API if you are introduced to the syntax. We would make a function parametric if we want it to work with multiple different types. The simplest example of a PARAMETRIC FUNCTION is the identity method shown here.

```
scala> def ident[A](a:A)=a
ident: [A](a: A)A
```

This method takes an argument of any type and returns the value passed in. While there are not many situations where you would want to do this, it demonstrates the syntax of parametric functions. You simply place a type parameter name in square brackets between the function name and the normal argument list. It also demonstrates the power of parametric functions, especially if we put it to use as we do here.

```
scala> ident(3)
```