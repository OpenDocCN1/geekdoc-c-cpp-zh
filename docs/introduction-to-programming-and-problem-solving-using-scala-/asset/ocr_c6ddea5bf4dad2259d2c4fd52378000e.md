# Introduction to Programming and Problem-Solving Using Scala

that is not numeric is put inside double quotes in a CSV file. We will ignore that for now and only deal with numbers.

We can read in this file and see the result in the REPL.

```
scala>fileToDataGrid("numbers.txt", *, *)
res8: Array(Array[Double]) = Array(Array(1.0, 0.0, 0.0),
Array(1.0, 1.0, 0.0), Array(0.0, 0.0, 1.0)
```

Everything here is pretty clean with the possible exception of the delimiter. In this file, it would have worked to use the delimiter ,. However, it is robust. If there were any extra spaces before or after the comma it would fail. It would also fail if a space was left after the comma. Using "* as the delimiter means that this code will work with a comma with zero or more spaces before or after it.

Even with this, the dataGrid leaves some things to be desired. We are not trying to make it with Strings so do not consider it a problem if this function crashes when there is a value in the file that is not a number. More problematic is that it does not deal well with blanks. In a CSV file there are two types of blanks that occur. One is when there are two commas with nothing between them and one is when there is a completely blank line. If these occurs in the file right now, our code will not respond. We could fix this in our current version by adding some logic, and as long as we are with skipping the blanks, it is easier to do this for loops and guards.

```
def dataGrid(lines:Iterator[String],delim:String):Array[Array[Double]] = {
  for (l <- lines; if !l.trim.isEmpty) yield {
    for (n <- l.split(delim); if !n.trim.isEmpty) yield n.trim.toDouble
  }
}.toArray
```

The guards make it easy to skip things that do not fit what we want. In this case, what we want is a String that is not empty. The trim method on a String gives back a new String with all leading and trailing space removed.

# 9.3.3 Reading from Other Things

One of the things about the scala.io.Source object is that it has more just than the fromFile method for us use in reading files. Indeed, there are quite few different methods that start with scala.io.Source. We will consider only one of them, and though you can certainly get to the API to look at others. You might find most interesting is the fromURL(s:String) method. URL stands for Uniform Resource Locator, and they are the things that you type into the address bar of a web browser. You call this method passing it a URL as a String, very much what you would put in the web browser.

This makes remarkably easy to have your program read information off the web. For example, executing the following line will give you the contents of your web page as a String.

```
Source.fromURL("http://cs.trinity.edu/mlewis/").mkString
```

You can do everything with this Source that you would do with a Source from a file. Like with the file, the Source is an Iterator you can only read through without calling