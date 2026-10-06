# 14.5 Inheritance 555

```
 // Class variable to reference a FinalExam object.
Declare FinalExam exam

// Prompt the user for the number of questions
// on the exam.
Display "Enter the number of questions on the exam."
Input questions

// Prompt the user for the number of questions
// missed by the student.
Display "Enter the number of questions that the ",
"student missed."

// Create a FinalExam object.
Set exam = FinalExam(questions, missed)

// Display the test results.
Display "Each question on the exam counts ",
exam.getPointsEach(), " points."
Display "The exam score is ", exam.getScore()
Display "The exam grade is ", exam.getGrade()
End Module
```

Program Output (with Input Shown in Bold)
nEnter the number of questions on the exam.
[20]
Enter the number of questions that the student missed.
[3]
Each question on the exam counts 5 points.
The exam score is 85
The exam grade is B

In 20, the following statement creates an instance of the FinalExam class and assigns its address to the exam variable:

Set exam = FinalExam(questions, missed)

When a FinalExam object is created in memory, it not only has the members declared in the FinalExam class, but it also has the non-private members declared in the GradedActivity class. In lines 25 and 26, shown here, that two public methods of the GradedActivity class, getScore and getGrade, are directly called with the exam object:

Display "The exam score is ", exam.getScore()
Display "The exam grade is ", exam.getGrade()

When a subclass extends a superclass, the public members of the subclass become public members of the subclass. In this program, the getScore and getGrade methods can be called with the exam object because they are public members of the object’s superclass.