
statement transforms the compound statement into what is known as a _conditional_ block. Conditional blocks usually create compound statements; at the same time, you often introduce compound statements using control statements.

## Control Statements

Control statements provide the entryways to conditional statements or blocks of statements. As Figure 10.1 illustrates, a control statement consists of a word that designates the type of control you want to apply to a given block of statements. Figure 10.1 illustrates an `if` control statement. Logical expressions characterize control statements. The logical expression usually appears between parentheses that follow a keyword that identifies the control statement. A logical operator characterizes the logical expression that appears between the parentheses.

Following the control designation and its accompanying logical expression, you usually encounter the opening brace of the two braces that establish the scope of a controlled block of statements. Whether the block of statements enters the flow of your program depends on the behavior of the control statement.

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_249_0.png)

## Program Flow

Program flow consists of the path of logic your program follows when you execute it. The path of logic can vary from program execution to program execution due to the logical decisions you embed in your program. Control statements embody logical decisions, but both using and not using control statements serve to guide the flow of your program. Given this situation, three patterns of activity characterize the flow of most programs:

- **Sequence.** The statements a program contains execute one after another. It might be said that statements execute as the program presents them, but if you use `goto` operators to call functions, you can create a program in which the order of the statements in the text no longer corresponds to the sequence of their execution.

- **Selection.** You can embed decisions in a program that determines whether given blocks of the program are to be entered. The flow of the program depends on the outcomes of the decisions. Selection can involve single decisions or multiple decisions.

- **Repetition.** A program can execute such that certain blocks of its statements execute over and over again, according to a set number of repetitions that a counter controls or according to given conditions. If a condition is true, a block of your program repeatedly executes. If the condition becomes no longer true, then the repeated executions cease.

## Flow and Sequence

Programs flow sequentially when one statement after another executes until you reach the end of the program. Usually, the statements in a program that employ only sequential logic execute in the order in which you see them in the text of the program. You can alter this situation if you use labels and “go to” instructions, but even then it remains that your program executes according to a sequential logic. No decisions occur. Rather, you set a path, and the program follows it. Figure 10.2 illustrates the actions of a program that executes according to sequential logic.

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_250_0.png)

**Figure 10.2**
When a program executes sequentially, it moves invariably from one statement to another from beginning to end.

Table 10.1 provides discussion of a few of the terms related to sequential statements. The sequential flow of a program can include subroutines (also known as functions or methods). Chapter 12 covers the use of functions. The use of functions also relates to modules (see Chapter 13).

### Table 10.1 Discussion of Sequential Terms

| Term | Discussion |
|---|---|
| The semicolon (;) | You employ the semicolon to create a statement. A sequence consists of a set of statements. |
| Operator precedence | Operators possess precedence. In Chapter 5, Table 5.1 provides a summary of the operators Perl provides. The table also indicates their precedence. |
| Parentheses | Use of parentheses can group operations. Parentheses deserve special notice because they provide a way to override the precedence of operators. You exert control over their associations. |
| `goto` | Perl provides a `goto` operator. When you use this operator, you guide the flow of the program using target labels. |
| Blocks | A block is a labeled sequence of statements defined by some type of name and usually enclosed in braces. |
| Subroutines | Subroutines are also known as functions or methods. A function can be viewed as a labeled block. The label of the block identifies the block, and when you “call” the block in the flow of a program, you in essence continue to sequentially execute the program. |

You can find programming examples and extended explanations of items in subsequent sections of this chapter and in Chapter 11.

## goto Problems

Programs that involve solely sequential operations tend to be rare, but it remains that sequence lies at the basis of all programs. Statements execute one after another. As is the case with those that employ selection and repetition control structures, a program that uses only sequential statements can still present programmers with problems relating to duration and order. The order of execution brings to light the widely accepted notion that use of the goto operator tends to create problems.

The goto operator redirects the flow of a program to a point in a program that a label designates. When you use the goto operator to redirect the flow of the program, the flow goes from the statement containing goto to the point designated by the label. Convention dictates that you should capitalize labels. To define a label, you type the name of the label followed by a colon. You can access labels in any order.

At one time, programmers posed no particularly strong objections to the use of goto operations. The reason for this was that programs tended to lack subroutines (functions or methods), were short and simple, and were characterized by fairly extended commentary. Over time, this situation has changed. Now programmers usually consider use of the goto operator unacceptable. Listing10_02 illustrates the use of the goto operator.

```perl
#Listing10_02
goto AUTHOR;

TITLE:
($Lines =<<TITLE);

              The Goal

NOTE1:
($Lines=<<NOTE1);
[Vocabulary "Pelf": Wealth or riches dishonestly acquired.
NOTE1
print "\n".$Lines;
goto STANZA2;

END:
```

Listing10_02 uses seven labels. The flow the program maintains remains sequential, but the labels dictate the order of the flow. To understand the program, you must trace it from beginning to end following the labels and the statements that incorporate goto operators. Figure 10.3 illustrates the output of Listing10_02. The order of the information the program presents appears simple when displayed: author, title, stanza, note, stanza, source. Each time you use the goto operator, the program jumps to the designated label.

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_253_0.png)

**Figure 10.3**
Sequential execution can be altered using `goto` operators.

## Functional Ordering

Sequential organization of a program extends to the use of functions. A function creates a means of reordering statements in a program because it creates blocks of flow associated with the name of the function. A function provides both a block of flow and a set of parentheses that allow you to introduce specified values (arguments) into the functional block. Listing10_03 demonstrates the use of the `join()` function in this context. Variables defined earlier in the program are organized into output through the `join()` function. The sequence of their definition has little to do with the order in which you access them when you join and display them.

```perl
#Listing10_03

$SetA =

"\nHatch this world, without me wrought,"
```
