# Type Basics and Argument Passing 175

Imagine we wanted to square the value that we found, but only if we found it. Then map would be a good fit.2

```
scala lst.find(_ < 4).map(_ => i*)
res4: Option[Int] = Some(9)
```

```
scala lst.find(_ < 1).map(_ => i)
res5: Option[Int] = None
```

As you can see, the challenge with map, or flatMap, is that you get back another object of type Option. You can go through many maps, flatMaps, and even filters with an Option, but at some point you will likely need to use one of the other approaches to unwrap it.

If you actually want to do something in the case you have a None then you need to turn to basic conditionals. The more idiomatic way to do this in Scala is using match. This example takes the result of find and tells us what it found or tells us that nothing was found.

```
scala lst.find(_ < 4) match {
  case Some(i) => "Found "+i
  case None => "Nothing found"
}
6: String = Found 3
```

Note that this is using the pattern matching capabilities of the match expression to get the value of the Option.
The Option type also has an isEmpty that is true for None and false for Some as well as a get method that will return the value in a Some or crash if None. This allows you to use an if as. This is the least idiomatic method of dealing with an Option and is generally frowned upon. Code using that does the same thing as the match above look like this.

```
scala val result = lst.find(_ < 4)
res: Option[Int] = Some(3)
scala if(result.isEmpty) "Nothing found" else "Found "+result.get
res7: String = Found 3
```

Note that the result of the call to find needs to be given a name. This is because pattern matching, it is used twice in the code, and calling it twice would be inefficient.

# 7.3 Parametric Functions

Types like List, Array, and Option are not the only things that can have parameters. Functions can have parameters as well. This is something that is not used much in this book as it is more important in later courses, but it can help you to read the API if you are introduced to the syntax. We would make a parametric function if we want to work with

> 2 You would use flatMap instead of map if the function you were applying was going to result in an Option. You likely do not want an Option[Option[A]] for whatever A you are using, so flatMap flattens it to only a single Option.