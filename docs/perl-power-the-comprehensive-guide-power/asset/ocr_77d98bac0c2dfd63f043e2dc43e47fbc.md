| Term | Discussion |
|---|---|
| Parentheses | Use of parentheses can group operations. Parentheses deserve special notice because they provide a way to override the precedence of operators. You exert control over their associations. |
| `goto` | Perl provides a `goto` operator. When you use this operator, you guide the flow of the program using target labels. |
| Blocks | A block is a labeled sequence of statements defined by some type of name and usually enclosed in parentheses. |
| Subroutines | Subroutines are also known as functions or methods. A function can be viewed as a labeled block. The label of the block identifies the block, and when you “call” the block in the flow of a program, you in essence continue to sequentially execute the program. |

You can find programming examples and extended explanations of items in subsequent sections of this chapter and in Chapter 11.

# goto Problems

Programs that involve solely sequential operations tend to be rare, but it remains that sequence lies at the basis of all programs. Statements execute one after another. As is the case with those that employ selection and repetition control structures, a program that uses only sequential statements can still present programmers with problems relating to duration and order. The order of execution brings to light the widely accepted notion that use of the goto operator tends to create problems.

The goto operator redirects the flow of a program to a point in a program that a label designates. When you use the goto operator to redirect the flow of the program, the flow goes from the statement containing goto to the point designated by the label. Convention dictates that you should capitalize labels. To define a label, you type the name of the label followed by a colon. You can access labels in any order.

At one time, programmers posed no particularly strong objections to the use of goto operations. The reason for this was that programs tended to lack subroutines (functions or methods), were short and simple, and were characterized by fairly extended commentary. Over time, this situation has changed. Now programmers usually consider use of the goto operator unacceptable. Listing10_02 illustrates the use of the goto operator.

```
```perl
#Listing10_02
goto AUTHOR;

TITLE:
($Lines =<<TITLE);

              The Goal
```
```