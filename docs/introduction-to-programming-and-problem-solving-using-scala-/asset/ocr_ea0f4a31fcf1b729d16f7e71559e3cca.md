# Introduction to Programming and Problem-Solving Using Scala

scala package and then all the contents of the object scala.Predef. You can see the full structure of packages for Scala by looking at the API.

# 9.3 Reading from Files

Now is time to actually use scala.io.Source to help us read information from sources other than standard input. There are other ways that we could read files from a hard disk using the Java libraries, but for now we will use Source because it provides us with sufficient capabilities and ties in with the Scala collections that we have already discussed. Any code in this section will assume that you have done an import of scala.io.Source so that we can refer to it as just Source.

There is an object Source that has methods we can call to get instances of type Source that we will use to read from. The simplest way to read a file is to use the fromFile of the Source object.

```
scala val fileSource = Source.FromFile("sampleFile.txt")
fileSource: scala.io.BufferedSource = non-empty iterator
```

As you can see from this output, the object we got was specific of the type scala.io.BufferedSource. The BufferedSource type will provide better performance for files which is why we were given that. It happens that reading from a hard disk is one of the slowest things you can do on a computer. A big part of the slowdown is because of having to move the right part of the disk. As a result, it is much faster to read a bunch of data at once, even if you do not need it all, then it is to read each piece of data one byte at a time. The BufferedSource does exactly this. It reads in a relatively large amount of data into a buffer and then gives you that data as you request it. When buffer is empty, it will read again.

When you are done with the Source object, you should call close on it. In this case that would look like the following.

```
fileSource.close
```

There are many things you should remember to this, but two really stand out. The first is that a program is only allowed to have a certain number of files open at a given time. If you fail to close files for an extended period of time, you can run out of available file descriptors and then when you try to open another one it will fail. It also signals to Scala that you are done with the file so that it can clean up things like the memory that was used for the buffer.

# FileNotFoundException and IOException

File handling activities involve a lot of operations where things can go wrong. In the case of fromFile you could have mistyped the file name or the file that is specified might be one that you cannot read. From these situations would result in a java.io.FileNotFoundException. When reading from files, you could also attempt to do something like reading beyond the end of a file. And other mishaps would result in a more general java.io.IOException. If we want to make your code deal with these