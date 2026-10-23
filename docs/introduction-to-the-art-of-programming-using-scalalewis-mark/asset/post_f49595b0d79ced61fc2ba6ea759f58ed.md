
Read for understanding, not just so you can say you have gotten through a chapter. Gaining understanding of early material is especially important in this topic because the material in any given chapter is typically highly dependent on the chapters before it. If you fail to understand one chapter, you are not likely to understand the ones that follow it either. As such, effort spent on the early chapters will pay off later on. Fortunately, there are resources that accompany this book that can help with this.

Students coming into this course who have a background in programming should consider taking a "fast path" to chapters 6 and 7. You do not want to skip them completely as there are aspects of Scala that will likely differ from what you have done before. One way to approach this is the go to the end of any given chapter and try to do the exercises. Refer back to the chapter as needed to complete them. Once you can do the exercises and a project or two, you should feel comfortable moving on.

## Book Website

The author has posted a number of different supplements to this book at www.programmingusingscala.net that can help you work through the material. Some of the material is code or prose that could not be put into the book due to length restrictions. The most useful things on the website are things that can not be represented in static text.

Many different sections have videos on the web that work through the material. Programming is a very non-linear process. This book typically shows completed pieces of code that do what we want. It is hard to demonstrate the process of building that code in the format of a book. The videos show construction of code from the ground up and include descriptions of the programmers thoughts as it is being done. This type of "live coding" is invaluable in learning to program as it lets you into the mind of a more experienced programmer where you can see the thought processes associated with the development of the code.

The website also includes solutions of some exercises for you to reference along with sample implementations of certain projects. Some of the projects, especially in the second half of the book, can be challenging to describe in text. To give you a better idea of what is expected, the author has implemented sample solutions that you can run to see what they do. The site also includes some additional exercises and links to data files and remote sites that make the exercises more relevant.

The second half of the book also includes large projects. For these, there are UML diagrams of the author's sample solution to help students see possible ways of breaking their problem down.

## To the Instructor

If you are reading this, it likely means that you are already aware of many of the features of Scala that make it a great programming language.² The flexibility of Scala means that things can be covered in many different ways. The approach taken in this book might be summarized as semi-functional/semi-imperative with objects later. It is worth describing exactly what is meant by that.

This book takes advantage of the aspects of Scala that support programming in the

²If you are currently unconvinced of the benefits of Scala for teaching CS1 and CS2, there is a complete discussion at www.programmingusingscala.net.

small. It is expected that students will operate mainly in the Read, Evaluate, Print Loop (REPL) and in a scripting environment through at least the first 10 chapters and possibly through the first 15. The benefit of this is that you can focus on logic instead of extra keywords and scoping rules. Students are easily overwhelmed early on and this approach helps to flatten the learning curve a bit.

Scala is purely object-oriented, so students will be using objects and calling methods on objects very early on. However, the construction of classes to build their own objects is postponed until later. Fitting with this approach, programs are written as scripts, not as applications, in the early part of the book. So the object keyword and things like def main(args: Array[String]) : Unit are postponed until students are ready to write programs that are big enough that they need the organization provided by doing proper object-orientation (OO) across multiple files.

The approach is described as semi-functional because there is significant use of higher order functions and function literals and immutable style is often preferred. However, this is not enforced in a zealous way and mutable state is introduced early on. Students are shown mutable and immutable approaches to a number of problems and the benefits and pitfalls of each approach are discussed.

While the ideal way to go through this book is in a linear fashion, particularly if you want to use the end-of-chapter projects as assignments, strict linearity is not required and you can choose to move some topics around so that concepts like class declarations are covered earlier. Though it would be a bit more challenging, it would be possible to use this book in a more purely functional manner by simply having students avoid var declarations (See chapter 3), assignments into mutable collections like arrays, and the use of while loops.

## Using this Book

This book is intended to cover CS1 and CS2. It is divided into two parts with Part I covering introductory programming concepts and Part II covering object-orientation, abstraction, and data structures. While the break between Part I and Part II falls close to where the semester break between CS1 and CS2 will fall, the two don’t have to be the same. Indeed, in my own use of this book I typically cover the first two chapters of Part II during the first semester for a variety of pedagogical reasons.

When looking at the chapters in Part I, you might feel that chapters 11 and 12 are outliers in certain ways. They definitely break from the straight algorithmic, problem-solving nature of the other chapters. This break was placed at this point in the book at the request of students who often find visual interfaces more compelling than text-based ones. Thanks to the syntax of Scala, it is possible to build GUIs without explicitly declaring classes or using keywords associated with it, such as extends. The same is true of graphics with components that draw themselves with the exception that the override keyword appears on the paint method. It is possible to skip these, but not advised as graphics play a role in many of the examples later in the book.

If you have a desire to cover full OO concepts earlier, chapters 16 and 17 can be moved to closely follow chapter 10. There are also a number of chapters through the book that contain material that can be skipped completely. For example, chapter 14 covers XML. Scala makes this fairly easy to do and it fits in well with the projects that are given to have students work on stored data in a formatted manner. However, if you don’t want to spend time on that topic it can be skipped with little impact on later content other than projects and occasional usage in later chapters.

To help you decide what you can and can’t skip, figure 1 shows rough dependencies for different chapters in the book. Arrows point from one chapter to later ones that have direct

dependencies. There will be occasional references to material that is not in the line of the dependency arrows, but the material should still be understandable.

## Preface

![](img/157fcf510c119278e4b1267c62717fa8_34_0.png)

**FIGURE 1:** This figure shows the dependencies between different chapters in the book so that you can plan what you want to cover or allow you to intelligently choose alternate paths through the book. Arrows point toward later chapters that use material from an earlier chapter. Chapters from Part I of the book go down the left and those from Part II go up the right.

The course website, www.programminginscal.net, includes a number of different types of material that can be helpful for instructors. There are solutions to certain exercises so you should check there before using exercises for grading purposes. Additional exercises with recent links and data sets are also available on the web.

There are executable JAR files for some of the projects to help students, and instructors, understand what is being asked for from the student. In the second half of the book, the projects get bigger and the website shows UML diagrams of the author’s solutions. Code for projects is never given so they are safe for graded material.

In addition, there are videos posted for many sections of the text. These are generally “live coding” sessions. Instructors should feel free to use these as pre-lectures or to use with an inverted-lecture format for certain class meetings.
