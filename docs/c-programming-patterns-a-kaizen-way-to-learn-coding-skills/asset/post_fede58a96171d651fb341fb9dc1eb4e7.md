
## Kaizen Principles: To Improve Programming Logic

The Kaizen principle is a Japanese philosophy that refers to the set of activities that promote **continuous improvement**. **Improvement is not an activity which is meant to be done once or few times and then leave it. A continuous improvement is a process which consists of simple steps that leads to improvements in various areas.**

## Small improvements everyday

It focuses on incremental improvements as compared to finding exact solutions to the problems. Any improvement is better than ZERO improvement and 100% postponement. So make small simple targets and achieve it by putting efforts. Even 1% improvement is valuable and therefore small gains combined together in longer run yields big results. Basically don’t break the learning pattern and it’s better to learn something rather than postponing it 100%. This activity also help to break the habit of procrastination, if somebody who really find it hard to get rid of.

## Measurement and feedback

The implementer of this principle has to be mentally prepared to find their own mistakes in logical expression and overall programming logic. Each mistake is treated as a lesson in the path of overall improvement. So total focus is on incremental improvements rather than on complete solutions to programming problems. The learning of process of programming logic should be based on pictorial based exercises rather than mathematical based problems. When a learner practice programming logic based on pictorial based exercises, the feedback on applied logic can be known easily and clearly. Not only limited to this, it will create lot of curiosity and interest to learn programming. Moreover, it also helps to eliminate one of the commonest issue of;

> “how to keep focus while learning programming?”.

## Let go of assumptions

The usual and common way to learn programming is just by randomly experimenting it based on assumptions. This takes much more time to learn programming logic as it required hell lot of practice. Learning programming by assumptions is a switch off to many of them. Since it doesn’t reflect any standard way of learning. Most of us can’t able to make a good assumptions and in every subject area is highly impossible and there is no standard formula for assumptions that can work with anybody. If an approach for learning sparks visualisation and thought process, then it will be easy for anybody to learn it.

## Speak with data, manage by facts

The programmer should devise a solution based on the data and facts. The most important protocol which makes programming logic that works correctly is to understand the intelligence involved in the flow of data.

The trick to get this intelligence is to express flow of data in one or more logical expressions using our version of observation table known as logic trace table. The logical expression is made up of one or more variables and operators. Finally, programming logic is made up of one or more logical expressions. We can easily learn this art of making logical expressions using data and through appropriate practice mentioned in the **section-programming patterns.**

## Implementing Kaizen model for logic building skills

- Start a topic and learn till you reach a point where you are ready to analyse a solved example. Concentrate on that example till you get a feel that you have understood everything about the program.
- Then try to implement that solved example without referring it. Make a strong will that once you start implementing already studied program, you are not going to refer it back that particular solved program. You can refer theoretical explanation but not program. There are lot of chances that you may get many error syntactically or logically as well. In that situation, you can refer theoretical explanation about the concept but do not allow yourself to see the solution. Try your best to resolve issues by yourself referring theoretical explanation.
- Please maintain an excel or spreadsheet file to note down the errors you encountered in a program. When you yourself able to resolve the errors, please note down the reasons also why you have adopted that approach. Also, what you thought previously and afterwards you faced that particular logical error.
- Every new day when you want to start your learning, please have a quick look to your error file that you were maintaining every time, you implement the solved program when encountered any error(s). Referring back to those errors while learning every new day will help to do better next time and it will also helps you to quickly revise the concept. We should maintain this practice to avoid common logical errors so those errors should not become part of our habit. So it is good to correct those loopholes in the beginning itself, since breaking a habit consumes sufficient efforts. What we practice, that will become our habit whether good or bad. Here, we are trying to **convert failures into lessons**. It is more rewarding when we get improved from mistakes as early as possible so that we can invest more time learning other important subjects in our life.
- If two times you are able to solve all the solved examples from the book back to back without referring to the solutions, then you will be in a better position to write program effectively.
- Hints are there for unsolved problems in the explanations of solved exercises. If you are unable to solve unsolved problem, just try 2-3 attempts and move forward to complete the book. Come back again and try to attempt the remaining ones.
- Two times back to back, if you are able to solve all the solved exercise without referring to the solutions and also unsolved problems, then logic wise you will be in a very comfortable position. You will get the courage to build programming logic for more difficult level and can be able to deal other heavier subjects of programming like data-structures and design of algorithms with confidence.

## Repeat the above **kaizen(continuous improvement) model**
to produce solutions, _single attempts_ for all programs with
**<u>0 defect</u>**.

> > The GREAT aim of education is not knowledge but action.
> >
> > — Herbert Spencer

## Basic Format of C Program

The general format/template for our program will be something like as follows.

```
SampleFile.c
#include <stdio.h>

int main() {
    // Your program logic goes here
    return 0;
}
```

## How we can write our programming logic using C file?

In order to check the correctness of our programming logic we are required to do two things:

- 1) From SampleFile.c file create your program file, give program's name.
- 2) Place all your programming code in between code block of main method.

```
int main() {
    // Your program logic goes here
    return 0;
}
```

Code Block starts with open curly bracket { . It ends with closing curly bracket }.

If suppose we want write a program and our name of program is Welcome, then the name of the program will be given by the Welcome.c program file. For now just ignore return 0, int main(), #include <stdio.h> and other theoretical stuff. Just reuse this SampleFile.c file whenever you want to write a new program.

The following Welcome.c program outputs the text Welcome to C Programming.

```
Welcome.c
/*
 * This is my first program.
 * Program to print welcome message.
 */
#include <stdio.h>
int main() {
    //program logic goes here
    printf("Welcome to C Programming.");
    return 0;
}
```

## Output

Welcome to C Programming.

The multi-line comments are given by /* multi-line...*/
The single line comment is given by // single-line...

Comments are for our understanding/documentation purpose and not a part of our programming code. The C compiler ignores it.

**How to execute a C program in order to verify programming logic?**

Please refer the following title at end of this book.

**Appendix-A: Installation of IDE and project set-up**

It shows step-by-step procedure to create a **C** project using eclipse IDE and further shows how to create and **execute** a C program with screen-shots. Eclipse IDE is for free and widely used in software industry also.

Alternatively, you can use one of the online editor shown as follows.

https://www.tutorialspoint.com/compile_c_online.php

Click the **Execute** button to run the program. By default, **Source File** tab will be opened to write the program. A separate Result window is shown, to display the output of the program.

![](img/67765455776ddeb6395161cd553ecd87_21_0.png)

## **Console Output**

Let's try to use C programming language's inbuilt method **printf** to output result in different ways. We can use these methods to generate 2-dimensional output to verify our understanding of logic.

| | |
|---|---|
| `printf("\ntext");` | **Moves the cursor to the next line & prints the text to the console.** |
| `printf("text");` | **Print text to the console.** |
| `printf("\n");` | **Moves the cursor to the next line.** |

| Following programming statement(s) means the same. It outputs the given **text** and **moves to the next line** in the console outputting window. |||
|---|---|---|
| `printf("text");`<br>`printf("\n");` | `printf("text\n");` | `printf("text");printf("\n");` |
