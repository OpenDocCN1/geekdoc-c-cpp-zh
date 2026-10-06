
# Introduction to Programming and Problem-Solving Using Scala

saveSection(fileName, section)

This comes after the definition of both the case classes and the different functions. If you run the script with this in, you will be prompted for the information on the Section after you enter it that script stops. You can then look at the file that you told to save and make sure it looks like you would expect.

We will hold the loadSection function until the end and go into the main functionality with mainMenu and printMenu. You can write them in the following way.

```scala
def printMenu:Unit = {
    printf("Select an option:")
    "1. Add Test Grade
    2. Add Assignment Grade
    3. Add Quiz Grade
    4. PrintAverages
    5. Save and Quit"
}
```

```scala
def mainMenu(section:Section):Unit = {
    var option = 0
    do {
        printMenu
        option = readInt()
        option match {
            case 1 => addTest(section)
            case 2 => addAssignment(section)
            case 3 => addQuiz(section)
            case 4 => printAverages(section)
            case 5 => println("Goodbye!")
            case _ => println("Invalid option. try again.")
        }
    } while (option!=5)
```

You cannot test this code yet because mainMenu calls four other functions that have not been written yet. Once we have written them, we can put a call to mainMenu at the end of the script before the call to saveSection.

The three different functions will all look pretty much the same. We will only show the addTest function and let you figure out how function will work. It is worth noting that the Student is immutable. All the fields in the case class vals cannot be changed. The String and the three different List[Int] values are all immutable once a Student is created, it is set forever. However, the Section type stores the Students in an Array. This means we can change Student objects referred to. We can use the copy capabilities of the case class to make new instances that are almost the same for small variations. Using this, the addTest function could be written in the following way.

```scala
def addTest(section:Section):Unit = {
    for (i <- 0 until section.students.length) {
        println("Enter the grade for "+section.students(i).name+"")
        section.students(i) = section.students(i).
        copy(tests=readInt()::section.students(i).tests)
    }
}
```

# Case Classes

This code works just fine, but it is a bit verbose because we have to type section.students(i) so many times. We have to have the index because we need to be able to do the assignment to element of the Array. The section.students(i) before the equal sign in the assignment is hard to rid of because we have to mutate that value in the design of this code. The code could be shortened with appropriate use of imports, but there is another, more interesting solution.

```scala
def addTest(section:Section):Unit = {
    for ((s
```

This version uses zipWith and a pattern on the tuple to give us both a short name for the student, s, and an index into the array. Both of them are equally correct so one that makes more sense to you and duplicate it for assignments and quizzes.

The next function in the menu is printAverages and the course average. It could be helpful to just print students and the partial averages well. What is done in this version.

```scala
def printAverages(section:Section):Unit = {
    for (s <- section.students) {
        println(s.name)
        val assnave = if (s.assignments.isEmpty) 0.0
        else s.assignments.sum/s.assignments.length
        println(s.mkString("Assignments: ", ", ", "+assnave"))
        val quizave = if (s.quizzes.isEmpty) 0.0
        else s.quizzes.sum/s.quizzes.min/s.quizzes.length-1
        println(s.mkString("Quizzes: ", ", ", "="+quizave"))
        val testave = if (s.tests.isEmpty) 0.0
        else s.tests.sum/s.tests.length
        println(s.mkString("Tests: ", ", ", "="+testave))
        println("Average: "+0.5*assnave+0.3*testave+0.2*quizave)
    }
}
```

This function uses the code from the clearer classAverage and inserts some print statements. The only thing in here that might seem odd the use of a mkString instead of just. With this version, the first string goes before all the elements and the third one goes after all the elements. The argument in the middle is the delimiter as it has in previous usage.

```scala
def loadSection(fileName:String):(String,Section) = {
    val src = Source.FromFile(fileName)
    val lines = src.getLines
    val section = Section(Array(lines.next().toInt)(Student(
        lines.next().split(" ")).filter(_.length>0).map(_.toDouble).toList,
        lines.next().split(" ")).filter(_.length>0).map(_.toDouble).toList,
        lines.next().split(" ")).filter(_.length>0).map(_.toDouble).toList
    )))
    src.close
    (fileName,section)
}
```

# Introduction to Programming and Problem-Solving Using Scala

This function includes three lines for handling the file. The most important part of the function is in the declaration of the section variable which calls lines.next() anytime it needs a new line. The first time is to read how many students are in the section by reading the Array. Each student pulls in four lines for name and three different grade types. The lines are split, and then mapped to Doubles. The filter is required for the situation where you entered any grades. Technically this is not required, but it makes this function much nicely at the bottom of the script.

```scala
# Listing 1.1: Grade.scala

import java.io.Stdin
import java.io.Source
import java.io.PrintWriter

case class Student(name:String, assignments:List[Double], tests:List[Double], quizzes:List[Double])

case class Section(students:Array[Student])

def average(s:Student):Double = {
  val assave = if (s.assignments.isEmpty) 0.0
  else s.assignments.sum/s.assignments.length
  val quizave = if (s.quizzes.isEmpty) 0.0
  else (s.quizzes.sum-s.quizzes.min)/(s.quizzes.length-1)
  val testave = if (s.tests.isEmpty) 0.0
  else s.tests.sum/s.tests.length
  0.5*assave +0.3*testave +0.2*quizave
}

def createSection:(String

def saveSection(fileName:String, section:Section):Unit = {
  val pw = new PrintWriter(fileName)
  pw.println(section.students.length)
  for (s <- section.students) {
    pw.println(s.name)
    pw.println(s.assignments.mkString("Assignments: ", ", "))
    pw.println(s.tests.mkString("Tests: ", ", "))
    pw.println(s.quizzes.mkString("Quizzes: ", ", "))
  }
  pw.close
}

def loadSection(fileName:String):(String,Section) = {
  var src = Source.fromFile(fileName)
  val lines = src.getLines
  val section = Section(Array.fill(lines.next().toInt)(Student(
    lines.next().split(" ")).filter(_.length>0).map(_.toDouble).toList,
    lines.next().split(" ")).filter(_.length>0).map(_.toDouble).toList,
    lines.next().split(" ")).filter(_.length>0).map(_.toDouble).toList
  )))
  src.close
  (fileName,section)
}

def addTest(section:Section):Unit = {
  for (i <- 0 until section.students.length) {
    println("Enter the grade for "+section.students(i).name+"")
    section.students(i) = section.students(i).copy(tests=readInt()::section.students(i).tests)
  }
}

def addAssignment(section:Section):Unit = {
  for (i <- 0 until section.students.length) {
    println("Enter the grade for "+section.students(i).name+"")
    section.students(i) = section.students(i).copy(assignments=readInt()::section.students(i).assignments)
  }
}

def addQuiz(section:Section):Unit = {
  for (i <- 0 until section.students.length) {
    println("Enter the grade for "+section.students(i).name+"")
    section.students(i) = section.students(i).copy(quizzes=readInt()::section.students(i).quizzes)
  }
}

def printAverages(section:Section):Unit = {
  for (s <- section.students) {
    println(s.name)
    val assAve = if (s.assignments.isEmpty) 0.0
    else s.assignments.sum/s.assignments.length
    println(s.assignments.mkString("Assignments: ", ", ") = ""+assAve)
    val quizAve = if (s.quizzes.length<2) 0.0
    else (s.quizzes.sum-s.quizzes.min)/(s.quizzes.length-1)
    // Note: The OCR text was incomplete here, following logic from previous pages
  }
}

val (fileName, section) = if (args.length<1) createSection(args(0)) else loadSection(args(0))
mainMenu(section)
saveSection(fileName, section)
```
