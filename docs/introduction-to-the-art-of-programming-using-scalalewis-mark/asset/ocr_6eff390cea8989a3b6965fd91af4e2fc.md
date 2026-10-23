needs to be added. Instead of simply telling the `PrintWriter` what file name to use, we tell it a `java.io.FileWriter` to use. When we create a `FileWriter` we can tell it the file name and also give it a Boolean value that tells it whether or not to append. If the Boolean value is true, the contents of the existing file will be left in place and anything else written will go to the end of the file. If it is false it will behave like what we had before. So if you wanted to append to the output.txt file you could do the following.

```
import java.io.{FileWriter,PrintWriter}
val pw = new PrintWriter(new FileWriter("output.txt",true))
```

# printf and format

If you have an application where you have to be picky about the formatting of output there are some additional functions/methods that you should be aware of. These are the `printf` function for printing to a screen or file and the `format` method on String. These two methods provide you with a way of encoding how you either want something printed or how you want a string to look. They use a style of formatting that is the default way of doing things in the C programming language.

A full description of formatting is beyond the scope of this book and can be found in the Java API under `java.util.Formatter`. You can find the Java API through a web search or going to the `java.oracle.com` web site. As of this writing, Java 7 is the current version. You would want to look at the Java SE 7 version of the API or whatever newer version might be available. A brief introduction is presented here.

Let us start by creating a few variables and printing them using `println` the way we are accustomed to doing.

```
scala> val g = 6.67e-11
g: Double = 6.67E-11

scala> val name = "Mark"
name: java.lang.String = Mark

scala> val classSize = 20
classSize: Int = 20

scala> println(g+" "+name+" "+classSize)
6.67E-11 Mark 20
```

This approach requires using + a lot for String concatenation. It also gives us very little control over how the different values are printed. Both complaints can be addressed using `printf`.

The `printf` function uses variable arguments length parameters. The first argument is a format String. This is followed by arguments for that format. The format String can include format specifiers. These start with a percent sign and end with a character that specifies a type of conversion. Between these there can be some additional information that describe how the conversion should be applied. Some of the more common conversion types are:

+   - d – decimal formatting for an integer,
+   - e – scientific notation for a floating point value,