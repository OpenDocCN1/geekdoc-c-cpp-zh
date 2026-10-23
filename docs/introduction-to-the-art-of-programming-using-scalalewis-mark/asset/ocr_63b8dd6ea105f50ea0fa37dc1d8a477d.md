```
else (s.quizzes.sum-s.quizzes.min)/(s.quizzes.length-1)
println(s.quizzes.mkString("Quizzes:",", "," = "+quizAve))
val testAve=if(s.tests.isEmpty) 0.0
else s.tests.sum/s.tests.length
println(s.tests.mkString("Tests:",", "," = "+testAve))
println("Average = "+(0.5*assnAve+0.3*testAve+0.2*quizAve))
}
}
```

This function uses the code from the earlier class average function and inserts some print statements. The only thing in here that might seem odd is the use of a mkString method that takes three arguments instead of just one. With this longer version, the first string goes before all the elements and the third one goes after all the elements. The argument in the middle is the delimiter as it has been in previous usage.

```
def loadSection(fileName:String):(String,Section) = {
val src=Source.fromFile(fileName)
val lines=src.getLines
val section=Section(Array.fill(lines.next().toInt)(Student(
lines.next(),
lines.next().split(" ").filter(_.length>0).map(_.toDouble).toList,
lines.next().split(" ").filter(_.length>0).map(_.toDouble).toList,
lines.next().split(" ").filter(_.length>0).map(_.toDouble).toList
)))
src.close
(fileName,section)
}
```

This function includes three lines for handling the file. The meat of the function is in the declaration of the section variable, which calls lines.next() anytime that it needs a new line from the input file. The first time is to read how many students are in the section for building the Array. Each student pulls in four lines for the name and three different grade types. The lines of grades are split, filtered, and them mapped to Doubles before they are converted to a List. The filter is required for the situation where you have not entered any grades of a particular type.

You might wonder why the return type of this function includes the fileName that was passed in. Technically this is not required, but it makes this function integrate much more nicely at the bottom of the script.

```
val (fileName,section)=if(args.length<1) createSection
else loadSection(args(0))
mainMenu(section)
saveSection(fileName,section)
```

Having createSection and loadSection return the same information greatly simplifies this part of the code as they can be called together in a simple if expression.

That is everything. You now have a full little application that could be used to store a grade book for some course. Try putting this code in and playing with it a while.