
# 9.3 Reading from Files

Now that you have seen **packages** and **import** statements it is time to actually use `scala.io.Source` to help us read information from sources other than standard input. There are other ways that we could read from files that use the Java libraries, some of which we will discuss in chapters 22 and 33, but for now we will use `Source` because it provides us with sufficient capabilities. Any code in this section will assume that you have done an **import** of `scala.io.Source` so that we can refer to it by the short name.

There is an object called `Source` that has methods we can call to get instances of type `Source` that we will use to read from things. The simplest way to read from a file is to use the `fromFile` method of the `Source` object.

```
scala> val fileSource=Source.fromFile("ch8.txt")
fileSource: scala.io.BufferedSource = non-empty iterator
```

As you can see from this output, the object we got back was specifically of the type `scala.io.BufferedSource`. The `BufferedSource` type will provide better performance for files which is why we were given that. It happens that reading from a hard disk is one of the slowest things you can do on a computer. A big part of the slowdown is the result of having to move to the right part of the disk. As a result, it is much faster to read a bunch of data at once, even if you do not need it all yet, than it is to read each little piece of data one byte at a time. The `BufferedSource` does exactly this. It reads in a relatively large amount of data into a buffer and then gives you that data as you request it. When the buffer is emptied, it will read again.

When you are done with the `Source` object, you should call `close` on it. In this case that would look like the following.

```scala
fileSource.close
```

There are many reasons you should remember to do this, but two really stand out. The first is that a program is only allowed to have a certain number of files open at a given time. If you fail to close files for an extended period of time, you can run out of available file descriptor and then you will try to open a file and have it fail. It also signals to Scala that you are done with the file so that it can clean up things like the memory that was used for the buffer.

> **FileNotFoundException and IOException**
> 
> File handling activities include a lot of operations where things can go wrong. In the case of `fromFile` you could have mistyped the file name or the file that is specified might not be one that you can read from. Either of these situations would result in a `java.io.FileNotFoundException`. When reading from files, you could also attempt to do something like read beyond the end of a file. This and other mislabels would result in a more general `java.io.IOException`. If we want to make your code deal with these situations gracefully, you will need to use the *try/catch* expression that was mentioned in chapter 6.
> 
> The full details of this construct are left for section 22.3. However, if this situation you might have code like the following.

```
def readStuffFromFile(fileName:String):SomeType = {
 try {
  val fileSource = Source.fromFile(fileName)
  // ...
  fileSource.close()
 } catch {
  case e:java.io.FileNotFoundException =>
   // An expression to build an empty SomeType
 }
}
```

## 9.3.1 Iterators

When the value of the BufferedSource is printed all it shows is “non-empty iterator”. This is because the BufferedSource, and the normal Source, are both of a more general type called an Iterator. An Iterator is much like the Array and List types that we saw previously. In fact, virtually all the methods that we could call on the Array and the List are available on an Iterator. The difference is that a basic Iterator can only be used once. The Array and the List are said to be iterable, which means that they can give us multiple Iterators to use to call those methods over and over again. In the case of an Iterator, once you call a method that runs through the whole thing, it is spent and you can not use it again.

```
scala> fileSource.mkString
res0: String = This is a sample text file that I have written to use
for chapter 9. There really is not all that much to this file. It is
simply supposed to be used to illustrate how we can read from files.

scala> fileSource.mkString
res1: String =

scala> fileSource
res2: scala.io.BufferedSource = empty iterator
```

The first call to mkString gives us back a string that has the contents of the file. The second call gives us back nothing. The reason for this is clear if we look at the value of fileSource. After reading through the file the first time, it has gone from a non-empty iterator to an empty iterator. There is nothing left for us to read. The Source type provides a method called reset that you do not get in most Iterators. The reset method gives you a new Source that is set back to the beginning for you to read again.

At a fundamental level, the Iterator type is based on two methods: hasNext and next. The hasNext method returns a Boolean and tells you whether or not there is something more in the Iterator. The next method will give you that next thing. You should be able to picture how these two methods can be used in either a while loop or with recursion to let you run through the entire contents of the Iterator.

The reason the BufferedSource is just an iterator is not hard to understand. Remember, reading files is extremely slow. You should do it once and get the information you want that time. Reading it over and over again would be inefficient. To help force you toward efficiency, you would have to explicitly reset the file or open it back up to iterate through it again.

With the List and Array types, you saw that they were parametric. We could make a List[Int] or a List[String]. This is also true of Iterators. The Source and BufferedSource types are specifically Iterator[Char]. This means that they operate naturally on individual characters. If you call functions like map or filter, or if you convert the Iterator to a List or an Array, the result will be a bunch of characters.

While technically all the data that you want is in the form of characters, it can be a bit difficult to operate with it in that format. For this reason, there is a method called getLines that will give you back a different Iterator. This new Iterator is of the type Iterator[String] and each element is a full line in the file without the newline character at the end.

## 9.3.2 String split Method

Even lines are not always all that useful because there might be multiple pieces of data on each line. There are many ways that you can split up a String into different pieces. For most purposes, the simplest of these is the split method. The split method takes a single argument that is a String, which should be the delimiter between the pieces you want split up. It will then return an Array[String] with everything that was separated by that delimiter. Here is a simple example.

```
scala> "This is a test.".split(" ")
res4: Array[java.lang.String] = Array(This, is, a, test.)
```

The String, “This is a test.”, is split up using a single space as the delimiter. The result has each word from the String as a separate element.

Technically, the argument to split is a REGULAR EXPRESSION. We will not go into the details of regular expressions until chapter 30. There are just a few things that are worth mentioning at this point. The regular expression can have more than one character. Also, the characters ‘+’ and ‘*’ have special meanings. The ‘+’ says that the character before it can occur one or more times while the ‘*’ says that it can occur zero or more times. This is worth mentioning at this point because it is not uncommon for inputs to potentially have multiple spaces between words. To handle this, you will often call split with " +" instead of just a space.

Now we want to put the split method into action with the ability to read the file line-by-line. What we want to do is create code that will read in numeric data from a file into a 2-D data structure. In this case, we will create a 2-D Array because the direct access capability is useful for most of the applications we would want to use this in. We will do this in two different ways. We will break this up into two functions. The first function will work with any Iterator[String] and give us back the Array[Array[Double]] that we want. The Iterator[String] is helpful because that is what getLines will give us and that is more flexible than forcing it to be a file. The second function will take a file name and return the Array[Array[Double]]. It will not do much itself other than use a Source to read the file and pass that Iterator to the first function. Both functions will also take a delimiter for split so that the person calling them can choose what we split on.

```
def dataGrid(lines:Iterator[String],delim:String):Array[Array[Double]] = {
  (lines.map(s => s.split(delim).map(_.toDouble))).toArray
}
```

```
def fileToDataGrid(fileName:String,delim:String):Array[Array[Double]] = {
  dataGrid(Source.fromFile(fileName).getLines,delim)
}
```
