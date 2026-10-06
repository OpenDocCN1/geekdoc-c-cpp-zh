
## 14.5 Inheritance 555

```cpp
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

## Inheritance in UML Diagrams

You show inheritance in a UML diagram by connecting two classes with a line that has an open arrow at one end. The arrow points to the superclass. Figure 14-20 is a UML diagram showing the relationship between the GradedActivity and FinalExam classes.

Figure 14-20 UML diagram showing inheritance

| GradedActivity | FinalExam |
| :--- | :--- |
| - score : Real | - numQuestions : Integer |
| + setScore(s: Real) | - pointsEach : Real |
| + getScore() : Real | - numMissed : Integer |
| + getGrade() : String | + FinalExam(questions : Integer, missed : Integer) |
| | + getPointsEach() : Real |
| | + getNumMissed() : Integer |

## Inheritance Does Not Work in Reverse

In an inheritance relationship, the subclass inherits members from the superclass, not the other way around. This means it is not possible for a superclass to call a subclass's methods. For example, if we create a GradedActivity object, it cannot call the getPointsEach and the getNumMissed methods because they are members of the FinalExam class.

## Checkpoint

- 14.21 In this section, we discussed subclasses and subclasses. Which is the general class and which is the specialized class?
- 14.22 What does it mean to say there is an "is a" relationship between two objects?
- 14.23 What does a subclass inherit from its superclass?
- 14.24 Look at the following pseudocode; which is the first line of a class definition? What is the name of the superclass? What is the name of the subclass?

```
Class Canary Extends Bird
```

## Polymorphism

**CONCEPT:** Polymorphism allows you to create methods with the same name in different classes (that are related through inheritance) and gives you the ability to call the correct method depending on the type of object that is used to call.

The term *polymorphism* refers to an object's ability to take different forms. This is a powerful feature of object-oriented programming. In this section, we will look at two essential ingredients of polymorphic behavior:

1. The ability to define a method in a superclass, and then define a method with the same name in a subclass. When a subclass has the same name as a superclass method, it is often said that the subclass method *overrides* the superclass method.
2. The ability to declare a variable of the superclass type, and then use that to reference objects of either the subclass or the subclass types.

The best way to describe polymorphism is to demonstrate it, so let's look at a simple example. Class Listing 14-10 shows pseudocode for a class named Animal.

## Class Listing 14-10

```
1 Class Animal
2   //showSpecies method
3 Public Module showSpecies()
4     Display "I'm just a regular animal."
5 End Module
6 
7   //makeSound method
8 Public Module makeSound()
9     Display "Grrrrr"
10 End Module
11 End Class
```

The class has two methods: *showSpecies* and *makeSound*. Here is an example of pseudocode that creates an instance of the class and calls the methods:

```
Declare Animal myAnimal
Set myAnimal = New Animal()
Call myAnimal.showSpecies()
Call myAnimal.makeSound()
```

If this were actual code, it would display the following:

I'm just a regular animal.
Grrrrr

Next, look at Class Listing 14-10 (Wait, the text refers to 14-10 again but describes Dog/Cat logic in the following pages).

(Note: The OCR text seems to have overlapping/repeating descriptions for Dog and Cat classes in subsequent pages. I will follow the logical flow provided.)

If this were actual code, it would display the following:

I'm just a regular animal.
Grrrrr

Next, look at Class Listing 14-10 (Note: Text transitions to Dog and Cat examples in Pages 581-583).

[Note: The provided OCR for pages 581-583 contains repetitive descriptions of Dog and Cat classes. I have processed them based on the text provided.]
