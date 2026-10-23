a more complex method that we have not really dealt with before. However, it is ideal for what we are doing here as it effectively does what we wrote previously, but without the need for a for loop. The foldLeft method runs through the collection from left to right and applies a function to each element, compiling a result as it goes. The function is curried and the first argument list is a single value that tells what the compiled value should start off as. In this case, we are compiling a Map so we will start off with an empty one. The code we want to apply is very much like what was in the for loop previously. This is what it looks like when put together.

```
```text
def wordCount2(fileName:String):Map[String,Int] = {
  val source = io.Source.fromFile(fileName)
  val words = source.getLines.toSeq.flatMap(_.split(" "))
    .map(_.filter(_.isLetter).toLowercase)
  val counts = words.foldLeft(Map[String,Int]())((m,w) => {
    if(m.contains(w)) m + (w -> (m(w)+1))
    else m + (w -> 1))
  }
  source.close()
  counts
}
```
```

The function that is passed into foldLeft takes two arguments. The first is the compiled value so far and the second is the value that is being operated on. In this case the compiled value is a Map and we use the variable m to represent it. The value being passed in is the next word that we want to count and is represented by the name w as it was in the for loop previously.

The body of the function passed into foldLeft as the second argument list differs from what was inside the for loop previously in two ways. First, instead of referring to the mutable map counts, we use the argument name m. Second, we do not use +=. Instead we just use +. The += operator is not defined for the immutable map and what we are doing here is building a new immutable map that is passed forward to be used with the next word.

If you really want to push things a little harder you can get rid of the declaration of words all together. After all, the only thing it is used for is as the argument to foldLeft to build counts. Doing this and getting rid of some curly braces that are not technically needed produces the following code.

```
```text
def wordCount3(fileName:String):Map[String,Int] = {
  val source = io.Source.fromFile(fileName)
  val counts = source.getLines.toSeq.flatMap(_.split(" "))
    .map(_.filter(_.isLetter).toLowercase)
    .foldLeft(Map[String,Int]())((m,w) =>
      if(m.contains(w)) m + (w -> (m(w)+1))
      else m + (w -> 1))
  source.close()
  counts
}
```
```

This code is compact, but whether you really want to do things this way or not is debatable. The introduction of the variable words did add extra length to the code, but for most readers it probably also made things more understandable.

Having any version of wordCount implicitly gives us a set of the words as well. This is because the Map type has a method called keySet that returns a Set of all of the keys used in the Map. Because each key can only occur once, nothing is lost when you get the keys as a set. For efficiency reasons you would probably want to keep the uniqueWords