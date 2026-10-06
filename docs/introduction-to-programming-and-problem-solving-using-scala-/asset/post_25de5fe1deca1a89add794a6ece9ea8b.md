
# Text Files

which has the type Array[String]. We can get the values of this Array the same way we would any other Array. You can refer to args(0) to get the first argument after the file name, args(1) to get the second, and so on. A simple example to illustrate the use of arguments would be a script that converts two arguments to Doubles and adds them.

```scala
println(args(0).toDouble+args(1).toDouble())
```

If we put this into a file called add.scala we would call it with the following command on the command line.

```
scala add.scala 88 12
```

This would print 100.0 as the sum. The decimal point appears because the Strings are converted to Doubles as the sum is a Double and it returns a Double.

# 9.5.2 Mapping a File

To start off, we will write a script that uses two command line arguments for the input file name and the output file. The main functionality is in a function that will read a file and write a modified file using a function that is passed as a parameter to map from the character to the one.

To make it so that the formatting is reasonable, the transform function will only be for characters that are in the alphabet, whether they are uppercase or lowercase. This will leave white space punctuation intact. Such a function could be written in the following way.

```scala
def mapFile(inputFile:String,outFile:String,trans:Char) => Char):Unit = {
  val pw = new PrintWriter(outFile)
  val in = Source.fromFile(inputFile)
  for (c <- in) {
    pw.print(if (c.isLetter) trans(c) else c)
  }
  in.close
  pw.close
}
```

Make sure you do the two close at the end to clean up things before the function exits. But pw and in are local variables so once the program leaves this function you will not have any way to manually close them.

This function could be invoked with a simple identity function to make a copy of the file.

```scala
mapFile(args(0),args(1),c => c)
```

The function c=>c simply returns whatever is passed into it. If you put this in a file that imports for Source and PrintWriter, you can call it from the command line specifying two file names, one that exists and one that does not, and the contents of the file that exists will be copied to the new file name.

# 9.5.3 Character Offset

A simple way to make it much harder for anyone to read what is in your file is to take the characters and offset them by a specified amount in the alphabet. We will write a script that uses three line arguments: one for the input file name, one for the output file name, and let for the offset amount. The simplest code for doing this might look like the following.

```scala
val offset = args(2).toInt
mapFile(args(0),args(1),c=>(c+offset)).toChar
```

Here we convert the third argument to an Int and add it to whatever character we are crypting. This is to be turned back into a Char with toChar because doing arithmetic the Char implicitly results in an Int. 

This is simple and works well for both encoding and decoding. To decode a message, simply use an offset that is the additive inverse of what you used originally. The only thing lacking is that letters can be shifted out of the alphabet making them a bit odd when the text is printed. This problem can be resolved by having the characters wrap around the end of the alphabet. If the offset would move the letter beyond 'z', it wrapped back to 'a'. We also need to handle the case where the offset is wrapped before 'a'. The easy way to do this is with a modulo operator. The following code will work for any offset larger than -26.

```scala
val offset = args(2).toInt
mapFile(args(0),args(1),c=>{
  if (c.isLower)
    ('a'+(c-'a'+offset+26)%26).toChar
  else
    ('A'+(c-'A'+offset+26)).toChar
}
```

This code is a bit complex because it has to differentiate between lowercase and uppercase letters so it knows what to subtract from to get a value that can take the modulo of.

This code also does something that might look a bit odd to you. The first function liter now includes curly braces. Remember that the curly braces just make a code block which is an expression whose value is the value of the last expression in the code block. This block has only one statement, an if expression, putting it in a block helps to set it off and makes it easier to read.

# 9.5.4 Alphabet Flip

A different way to alter the letters is to flip the alphabet around. So a 'z' will become 'a', a 'y' will become 'b', and so on. This encoding does not need an extra argument for something like the offset. It also has an interesting side effect that the transformation is its own inverse. The code to do this might look like the following.

```scala
mapFile(args(0),args(1),c=>{
  if (c.isLower)
    ('a'+(25-(c-'a'))).toChar
  else
    ('A'+(25-(c-'A'))).toChar
}
```

This has the same basic structure of the normal offset version. It does not need an offset, and it uses an adjustment of 25 minus the characters position in the alphabet.

# 9.5.5 Key Word

Both of the methods described above are reasonably easy to cracking someone has some idea about what you are doing. For the offset method they just need to know what offset you used, and they can figure out if they get to look at a decent sample of encoded text. For the alphabet flipping all they need to know is what you are doing, and they can decrypt any message you send.

To make things little harder, you can use a key string to provide a variable offset. The encoding starts with the first letter in the key string and offsets the character by the number of positions that character is 'a'. It uses the second letter in the key string to offset the character in the message. This repeats until the end of the key string is reached as which point it wraps around and starts characters at the beginning. Code does what is shown here.

```scala
val key = args(2)
val factor = args(3).toInt
var keyIndex = 0
mapFile(args(0),c=>
  val offset = factor+(key(keyIndex)-'a')
  keyIndex = (keyIndex+1)%key.length
  if (c.isLower)
    ('a'+(c-'a'+offset+26)%26).toChar
  else
    ('A'+(c-'A'+offset+26)).toChar
)
```

This method needs both offset and factor. The key is used to create the new offset. The key wraps around the beginning. The code does what is shown here for the key.

# 9.5.6 Putting Together

To make this more useful, all approaches can be put into a single script. The script uses```scala
import scala.io.Source
import java.io.PrintWriter
```
(rest of the text follows)
