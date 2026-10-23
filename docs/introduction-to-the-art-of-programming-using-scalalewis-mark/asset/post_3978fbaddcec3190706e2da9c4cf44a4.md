
Now we can demonstrate how this works by calling it on a file called numbers.txt that we have created. The file has the values for a 3x3 identity matrix with the values separated by commas as shown here.

```
1.0, 0.0, 0.0
0.0, 1.0, 0.0
0.0, 0.0, 1.0
```

The choice of format is particular because this is what you would get if you had Excel® write out a CSV format with only numbers. CSV stands for Comma Separated Values. It is more complex if we include non-numeric data. Anything that is not numeric is put inside of double quotes in a CSV file. We will ignore that for now and only deal with numbers.

We can read in this file and see the result in the REPL.

```
scala> fileToDataGrid("numbers.txt", ", *", "*")
res0: Array[Array[Double]] = Array(Array(1.0, 0.0, 0.0),
Array(0.0, 1.0, 0.0), Array(0.0, 0.0, 1.0))
```

Everything here should be pretty clear with the possible exception of the delimiter. For this file, it would have worked to use the delimiter ", ". However, that delimiter is not all that robust. If there were any extra spaces either before or after the comma it would fail. It would also fail if a space was left out after the comma.

Even with this delimiter, the dataGrid method leaves some things to be desired. We are not trying to make it deal with Strings so we do not consider it a problem if this function crashes when there is a string in the file that is not a number. More problematic is the fact that it also does not deal well with blanks. In a CSV file there are two types of blanks that can occur. One is when there are two commas with nothing between them and one is when there is a completely blank line. If either of these occurs in the file right now, our code will not respond well. We could fix this in our current version by adding some extra logic, but as long as we are good with just skipping the blanks, it is easier to do this with for loops and if guards.

```
def dataGrid(lines:Iterator[String],delim:String):Array[Array[Double]] = {
  (for(l <- lines; if(!l.trim.isEmpty)) yield {
    for(n <- l.split(delim); if(!n.trim.isEmpty)) yield n.trim.toDouble
  }).toArray
}
```

The if guards make it easy to skip things that do not fit what we want. In this case, what we want is a String that is not empty. The trim method on a String gives back a new String with all leading and trailing white space removed.

## 9.3.3 Reading from Other Things

One of the nice things about the scala.io.Source object is that it has more than just the fromFile method for us to use in reading files. Indeed, there are quite a few different methods that start with from in scala.io.Source. We will only consider one of them here, though you can certainly go to the API to look at others. The one you might find most interesting is the fromURL(s:String) method. URL stands for Uniform Resource Locator and they are the things that you type into the address bar of a web browser. You call this method passing it a URL as a String, very much like what you would put in the web browser.

This makes it remarkably easy to have your program read information off of the web.

For example, executing the following line will give you back the contents of my web page as a *String*.

```
Source.fromURL("http://www.cs.trinity.edu/~mlewis/").mkString
```

You can do everything with this *Source* that you would do with a *Source* from a file. Like with the file, the *Source* is an *Iterator* so you can only read through it once without calling *reset*. This also makes sense because if there is nothing slower on a modern computer than reading from a hard disk, it is reading information from the web.

## 9.3.4 Other Options (Java Based)

The advantage of using a *scala.io.Source* with *getLines* is that you get a Scala based *Iterator* that has all the methods you have gotten used to in working with the *List* and *Array* types. However, that does not mean that *Source* is always your best option. For many situations, you might find that the *java.util.Scanner* class is better.

The *java.util.Scanner* class has methods for reading specific types of data as well as for checking if there are specific types of data available. Here is a sampling of the methods that are available.

- *hasNext()*:*Boolean* - Check to see if there is another “word”.
- *hasNextDouble()*:*Boolean* - Check to see if there is a *Double* ready to read.
- *hasNextInt()*:*Boolean* - Check to see if there is an *Int* ready to read.
- *hasNextLine()*:*Boolean* - Check to see if there is a line of text ready to read.
- *next()*:*String* - Read the next “word”.
- *nextDouble()*:*Double* - Read the next *Double*.
- *nextInt()*:*Int* - Read the next *Int*.
- *nextLine()*:*String* - Read the next line of text.
- *useDelimiter(pattern: String)* - Change the pattern used for the delimiter.

This list should be fairly self-explanatory. The only thing one might wonder about is why “word” is in quotes. The reason for this is reflected in the last method listed. When you want to read a “word” with a *Scanner*, it will read up to the next delimiter, whatever that happens to be. By default it is any grouping of white space.

In order to use a *Scanner*, you have to make one. To do this you probably want to *import java.util.Scanner* and use the following expression.

```
new Scanner(file)
```

The *file* needs to be an expression that has the type *java.io.File*, which we will also make with a *new* expression and probably also want to *import*. Putting this together, you could put something like this into a program to read and print a bunch of *Ints*.

```
import java.util.Scanner
import java.io.File

val sc = new Scanner(new File("numbers.txt"))
while(sc.hasNextInt) {
println(sc.nextInt())
}
sc.close()
```

The choice of printing here comes from the fact that the Scanner does not nicely produce a Scala collection. You can get the values into a collection, but it will typically take a bit more effort. You should also remember to close your Scanners when you are done with them. If they link to a file, they are holding onto valuable resources.

## 9.4 Writing to File

Scala does not provide any functionality for writing to a file in its own libraries. That is something that is already well supported by Java and adding Scala libraries has not yet been seen as providing a significant benefit. There are many ways to set up a file to write to in Java. The easiest, and the one that we will use, is the java.io.PrintWriter. We can make a new PrintWriter with new and tell it the name of the file we want to write to as the only argument. So we can get a PrintWriter that we can use for doing output with this code.

```
import java.io.PrintWriter
val pw = new PrintWriter("output.txt")
```

Now we could call methods on pw that will cause things to be written to that file. You can use print and println methods to print to the file in much the same way that you have been using those functions in Scala to print to standard output.

Using this we could write the following code to print 100 random points with x and y values between 0 and 1.

```
for(i <- 1 to 100) {
  pw.println(math.random+" "+math.random)
}
pw.close()
```

The last line is critical because the PrintWriter is also using a file resource and buffering, just like the BufferedSource. However, it holds things in memory until there is enough to make it worth writing to the disk. If you do not close the file, the text in the buffer will not have been written out. If you are not done with the file, but you want to make sure that what you have written goes into the file, you can use the flush method.

```
pw.flush
```

When you call this, anything in the buffer will be written out. This way if the computer crashes, loses power, or something else goes wrong, that information will be out of the volatile memory.

### 9.4.1 Appending to File

Creating a PrintWriter in the way just described has the side effect that it will either create a new file or delete an existing one and write over it. If there is an existing file and you want to append to the end of it instead of overwriting it, there is one more step that
