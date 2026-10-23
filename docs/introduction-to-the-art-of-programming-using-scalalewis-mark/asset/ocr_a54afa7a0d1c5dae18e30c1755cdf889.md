way we would write them on paper and get back an answer. Real programming involves tying together multiple lines of instructions to solve larger problems. In order to do this, we need to have a way to give names to the work we have done and refer back to them.

There are three keywords in Scala that give names to values. We will see the first two here: val and var. To begin with, let us look at the full syntax of val and var in two samples. Then we can pull them apart, talk about what they do, see how they are different, and discuss what parts of them are optional.

```
```
scala> val age:Int=5
age: Int = 5
```
```

```
```
scala> var average:Int=(2+3+4+5)/4
average: Int = 3
```
```

Syntactically the only difference between these two is that one says val and the other says var. That is followed by a name with a colon and a type after it. The rules for names in Scala are that they need to start with a letter or an underscore followed by zero or more letters, numbers, and underscores. Scala is also case sensitive. So the names AGE, age, Age, and agE are all different. In general it is considered very poor style to use names that differ only in capitalization. Scala borrows a standard naming convention from Java called camel case. The names of values begin with a lower case letter and the first letter of subsequent words are capitalized. For example, theClassAverage is a name that follows this convention. Type names use the same convention except that the first letter is capitalized. This is called camel case because the capital letters look like humps.

The types in both of these examples are followed by an equals sign and an expression. Unlike many other programming languages, this is not optional in Scala. In Scala, when you declare a val or var, you must give it an initial value at that point.³

While the initial value is not optional, the type generally is. This too is unlike most programming languages. As we have already seen, Scala is able to figure out the types of things for us in many situations. If we leave off the colon and the type, Scala will simply use whatever type it determines is appropriate for the expression in the initial value. Most of the time, the type that it gives us will be exactly what we want. Using this we could instead have the following shorter forms of these declarations.

```
```
scala> val age=5
age: Int = 5
```
```

```
```
scala> var average=(2+3+4+5)/4
average: Int = 3
```
```

The reason for using a val or var declaration is that they give a name to the value that we can refer back to later. For example, we could now type in age+10 and Scala would give us 15. The names serve two purposes. They prevent us from typing in expressions over and over again. They also help give meaning to what we are doing. You should try to pick names that help you or other readers figure out what is going on with a piece of code.

So far we have discussed all the similarities between val and var and you might be wondering in what way they are different. The declarations themselves are basically identical. The difference is not in the syntax, but in the meaning, or semantics. A val declaration gives a name to a reference to a value. That reference can not be changed. It will refer to

> 3 There are very good reasons for requiring initialization of variables. Even in languages that do not require it, a programmer can make his/her life a lot easier by initializing all variables at creation. The declaration and initialization should ideally happen at the point where you have a real value to put into the variable. This prevents many errors and as a result, can save you a lot of time in your programming.