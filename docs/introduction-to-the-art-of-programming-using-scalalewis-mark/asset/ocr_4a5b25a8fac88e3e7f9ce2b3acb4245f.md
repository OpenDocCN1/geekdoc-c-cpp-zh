> specified InputStream. Much of the code we will use with streams will be reading binary data instead of text data, but you should know that this option exists.

# 22.3 Exceptions

If you run one of the scripts and provide a name for the input file that is not valid you will get something that looks somewhat like the following.

```
java.io.FileNotFoundException: notthere.txt (No such file or directory)
    at java.io.FileInputStream.open(Native Method)
    at java.io.FileInputStream.<init>(FileInputStream.java:138)
    at java.io.FileInputStream.<init>(FileInputStream.java:97)
    at Main$$anon$1.<init>(ReadBytes.scala:3)
    at Main.main(ReadBytes.scala:1)
    at Main.main(ReadBytes.scala)
    ...
```

You have probably seen quite a few outputs like this in working with Scala. This is a stack trace and it was printed out because something bad happened that caused the program to throw an exception. To this point we have generally ignored exceptions and expected the user or the computer to behave in a way that would allow the program to run without errors. It is time to learn how to deal with these situations instead of ignoring them and hoping they will not occur.

Exceptions are meant to occur in exceptional circumstances, such as when there is an error. In the example above, you can see that it was a java.io.FileNotFoundException that occurred. This should make sense given that we tried to open a file that was not there. Real applications need to be able to deal with this. For example, if a user specified a file that did not exist, the program should tell the user that and perhaps ask for an alternate file. It should not crash. In order to prevent the crash, we need a construct that has the ability to execute some alternate code when an exception occurs. The construct for doing this is the try/catch.

To understand this construct, it helps to have some terminology. The act of raising an exception is described by the term "throw". You can use the throw keyword to indicate when an exception occurs in your own code. Here we demonstrate this in the REPL.

```
scala> throw new Exception("Testing")
java.lang.Exception: Testing
    at .<init>(<console>:8)
    at .<clinit>(<console>)
    at .<init>(<console>:11)
    at .<clinit>(<console>)
    ...
```

You can throw any subtype of the java.lang.Throwable class. The two immediate subtypes of this are java.lang.Error and java.lang.Exception. Typically an Error represents something that you will not be able to recover from. An Exception is something that you should consider dealing with. While this example throws an instance of Exception itself, that is not something you should do normally. Instead, you should throw a subtype