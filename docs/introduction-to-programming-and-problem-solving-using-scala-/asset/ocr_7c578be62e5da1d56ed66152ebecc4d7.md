# 4.4 Problem Decomposition

As we said, programming is about problem solving. One of the major aspects of problem solving is breaking hard problems into smaller pieces. There are a number of reasons to do this. The most obvious reason is that big problems are hard to solve. If you can break a big problem into smaller pieces, it is often easier to solve the pieces and then build an answer to the full problem from the answers to the pieces. This can be repeated on each sub-problem until you reach a level where the pieces are simple to solve.

A second advantage to breaking problems is that the solutions to the pieces might be useful in themselves. This allows you to potentially reuse pieces of code. The ability to reuse existing code is critical in programming. There are many different ways that you can break up a problem. A good way to tell it if one is better than another is if one gives you functions that are more likely to be able to reuse.

A third advantage of decomposing a problem is that the resulting code is easier to read and modify. If the top level functions give you a better idea of what is going on in the low level functions. In addition, if you decide at some point that you need to modify something is done, it is easier to determine where the change needs to be and how to make it the problem has been broken down in a logical way.

A fourth advantage is that they are easy to debug. When you mess something up in your code it is a lot easier to find and fix bugs in small pieces of code than in large pieces of code. Functions let you make small pieces of code operate independently, so you can verify each function works on its own, independent of others.

We looked at two problems and how they could be programmed as a set of instructions that can put inside of a function. The question now how we could break these things up? If you go back to the original designs, the descriptions of how to solve the problem was done piece by piece in a way that worked well for breaking them apart.

Let us begin with the grading program. There are four basic parts to this problem. We find the average of the tests, the assignments, and the quizzes. Once we have those, we combine them using the proper properties. Each could be broken out into a separate function. If we write this into a file it might look like the following.

Listing 4.2: CourseAverageParts.scala

```
def testAve(test1:Double,test2:Double):Double = (test1+test2)/2
def assnAve(assn1:Double,assn2:Double,assn3:Double):Double = (assn1+assn2+assn3)/3
def quizAve(quiz1:Double,quiz2:Double,quiz3:Double,quiz4:Double):Double = {
  minQuiz = quiz1 min2 min3 min4
  (quiz1+quiz2+quiz3+quiz4-minQuiz)/3
}
def fullAve(test:Double,assn:Double,quiz:Double):Double = test*0.4+assn*0.4+quiz*0.2
```

The "bug" has a long history in engineering, going back at least Thomas Edison. It was pulled into the field of electronic computers when an actual moth found in a relay in the Mark II in 1947. The name implies that these accidentally crashed into software without any action from programmers. In reality, you create the bugs in your software when you do things that are incorrect.