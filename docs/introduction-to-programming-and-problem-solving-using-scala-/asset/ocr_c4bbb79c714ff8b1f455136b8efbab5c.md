# 16.2.1 Methods and Members

Inside of the class you will write code exactly the way you anyplace else. There are small differences that will be discussed and the meaning and terminology changes a bit. When you write a variable declaration with val or var inside the body of a class, that is a member declaration. It is noted that data is stored in the objects that are created from class. When you use def to create a function, we call it a method because its scope in the class and the fact it is something that you will be able to call on objects created from this class. Any statements that you are not declarations of members (val or var) or methods (def) will be simply when you write a little script that includes a class declaration. For the class we will go back to the concept of grades in a class and write the class to represent a student. Here is a first draft of the class with some lines that use the class.

```
class Student(name:String, id:String) {
  var tests: List[Double]()
  var quizzes: List[Double]()
  var assignments: List[Double]()

  def testAverage = tests.sum/tests.size
  def quizAverage = quizzes.sum/quizzes.size
  def assignmentAverage = assignments.sum/assignments.size
  def courseAverage = testAverage*0.4 + quizAverage*0.1 + assignmentAverage*0.5
}
```

```
val john = new Student("John Doe", "0123456")
john.tests += 78
john.quizzes += 85
println(john.testAverage)
```

The class begins with a class declaration that looks like a case class and really is not too different from a def. After the keyword class is the type of, in this case Student. This is followed by a list of parameters to the class. In this case we have two Strings named name and id. The body of the class is denoted with curly braces and inside of the braces we have three member variable declarations for grades and four method declarations for taking averages.

After the class declaration are four lines of code. The first declares a variable john that is set to be a new Student with the name John Doe and a student number of 0123456. The second and third statements add two tests of 78 and 85 to this student. This is simple, it is not clear that we really want the grades to be anything. The last statement in the script provides the average for the grades by calling the testAverage method.

# 16.2.1.1 Parameters as Members

Everything in this example should feel straightforward. It really does not look much from things that we have done before. This would change if we try to make the print statement a bit more informative.

```
println(john.name+" has a "+john.testAverage+" test average.")
```

If you change the println to this and run the script you will get an error message that might not make sense to you.

```
ScalaCS1/Chapters/ObjectOrientation/Code/Student1.scala:16: error: value name is not a member of this.Student
```