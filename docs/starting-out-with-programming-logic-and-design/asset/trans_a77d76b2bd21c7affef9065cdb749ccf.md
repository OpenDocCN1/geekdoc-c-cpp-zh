

## 14.5 继承 555

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

程序输出（输入部分已加粗）
nEnter the number of questions on the exam.
**20**
Enter the number of questions that the student missed.
**3**
Each question on the exam counts 5 points.
The exam score is 85
The exam grade is B

在第 20 中，以下语句创建了 FinalExam 类的实例，并将其地址赋值给 exam 变量：

Set exam = FinalExam(questions, missed)

当在内存中创建一个 FinalExam 对象时，它不仅拥有 FinalExam 类中声明的成员，还拥有 GradedActivity 类中声明的非私有成员。在所示的第 25 行和第 26 行中，直接通过 exam 对象调用了 GradedActivity 类的两个公共方法 getScore 和 getGrade：

Display "The exam score is ", exam.getScore()
Display "The exam grade is ", exam.getGrade()

当子类扩展父类时，子类的公共成员将成为该子类的公共成员。在程序程序中，可以可以通过 exam 对象调用 getScore 和 getGrade 方法，因为它们是该对象父类的公共成员。

## UML 图中的继承

你通过用一根末端带有空心箭头的线连接两个类，在 UML 图中展示继承。箭头指向父类。图 14-20 是一幅显示 GradedActivity 类和 FinalExam 类之间关系的 UML 图。

图 14-20 显示继承关系的 UML 图

| GradedActivity | FinalExam |
| :--- | :--- |
| - score : Real | - numQuestions : Integer |
| + setScore(s: Real) | - pointsEach : Real |
| + getScore() : Real | - numMissed : Integer |
| + getGrade() : String | + FinalExam(questions : Integer, missed : Integer) |
| | + getPointsEach() : Real |
| | + getNumMissed() : Integer |

## 继承不可反向运行

在继承关系中，子类从父类继承成员，反之亦然。这意味着父类无法调用子类的方法。例如，如果我们创建一个 GradedActivity 对象，它无法调用 getPointsEach 和 getNumMissed 方法，因为它们是 FinalExam 类的成员。

## 检查点

- 14.21 在本节中，我们讨论了子类和父类。哪一个是通用类，哪一个是专门化类？
- 14.22 说两个对象之间存在“是”（is a）关系意味着什么？
- 14.23 子类从其父类继承了什么？
- 14.24 查看以下伪代码；哪一行是类定义的第一行？父类的名称是什么？子类的名称是什么？

```
Class Canary Extends Bird
```

## 多态

**概念：** 多态允许你在不同的类（通过继承关系相关的类）中创建同名的方法，并让你能够根据用于调用的对象类型来调用正确的方法。

“多态”一术指的是对象采取多种形式的能力。这是面向对象编程的一个强大特性。在本节中，我们将查看多态的两个要素：

1. 在父类中定义一个方法，然后在子类中定义一个相同的方法。当子类具有与父类相同的方法名时，通常认为子类方法*重写*了父类方法。
2. 声明一个父类类型的变量，然后使用它来引用子类或类型的对象。

描述多态的最佳方法是进行演示，因此让我们看一个简单的示例。列表 14-10 显示了名为 Animal 的类的伪代码。

## 列表 14-10

```
1 Class Animal
2   //showSpecies 方法
3 Public Module showSpecies()
4     Display "I'm a regular animal."
5 End Module
6 
7   //makeSound 方法
8 Public Module makeSound()
9     Display "Grrr"
10 End Module
11 End Class
```

该类有两个方法：*showSpecies* 和 *makeSound*。这里有一个创建类实例并调用这些方法的伪代码示例：

```
Declare Animal myAnimal
Set myAnimal = New Animal()
Call myAnimal.showSpecies()
Call myAnimal.makeSound()
```

如果这是实际代码，它将显示如下：

I'm a regular animal.
Grrr

接下来，查看列表 14-10（注意：后续页面转向了 Dog 和 Cat 的示例）。

（注：提供的 581-583 页 OCR 包含了 Dog 和 Cat 类的重复描述。）

