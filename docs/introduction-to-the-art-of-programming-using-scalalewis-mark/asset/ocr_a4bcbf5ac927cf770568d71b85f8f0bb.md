```
import java.io._

class Student(val name:String, val grades:Array[Int]) extends Serializable

object Main {
	d	ef main(args:Array[String]) {
		args(0) match {
			case "-r" =>
				val ois = new ObjectInputStream(new BufferedInputStream(new
						FileInputStream(args(1))))
				ois.readObject() match {
					case s:Student => println(s.name+" "+s.grades.mkString(",", ","))
					case _ => println("Unidentified type.")
				}
				ois.close()
			case "-w" =>
				val oos = new ObjectOutputStream(new BufferedOutputStream(new
						FileOutputStream(args(1))))
				val s = new Student(args(2), args.drop(3).map(_.toInt))
				oos.writeObject(s)
				oos.close()
			case _ =>
				println("Usage: -r filename | -w filename name g1 g2 ...")
		}
	}
}
```

Put this in a file and compile it with scalac. From the command-line you can invoke this first step using this command.<sup>4</sup>

```
scala Main -w obj.bin John 98 78 88 93 100 83
```

After running this there will be a file called “obj.bin”. You can look at it with cat or xxd. You will see that this is clearly a binary file, but there are some parts that are human readable strings. One of these is the name itself, but there are others that gives type names like Student and java/lang/String. These have to be in the file because when you *deserialize* the file it has to know what types of objects to create. You can verify that this process works with the following command.

```
scala Main -r obj.bin
```

This will read back in the file you just created and print the Student object that was read.

One critical aspect to note about the code for the -r option is that it includes a match. If you leave out the match and assign the result of ois.readObject() to a variable, the variable will have type AnyRef. That is because readObject has a return type of AnyRef. You will not be able to get name or grades from an AnyRef because that type does not have those. The match allows you to check the type of the object that was read in and do the print statement we want if it is a Student or print an error message if it is not.<sup>5</sup>

When an object is serialized, some indication of its type is written out, followed by a

> 4You can do this in Eclipse as well. You need to open the Run settings and change the arguments. Using command-line arguments is easier in the terminal. If you want to test this in Eclipse you might consider changing from using args to standard input and output.

> 5This same type of operation can be done with isInstanceOf[A] and asInstanceOf[A] methods. However, the use of these methods is strongly frowned upon in Scala. Using a match is the appropriate Scala style for determining the type of an object and getting a reference to that object of the proper type.