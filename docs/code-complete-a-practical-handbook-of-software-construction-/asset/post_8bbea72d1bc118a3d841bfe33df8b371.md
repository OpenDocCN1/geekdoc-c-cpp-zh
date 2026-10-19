
“Writing a comment makes you think harder about what your code is doing,” Ismene said, returning from the lunchroom. “If it’s hard to comment, either it’s bad code or you don’t understand it well enough. Either way, you need to spend more time on the code, so the time you spent commenting wasn’t wasted because it pointed you to required work.”

“All right,” Socrates said. “I can’t think of any more questions, and I think Ismene got the best of you guys today. We’ll encourage commenting, but we won’t be naive about it. We’ll have code reviews so that everyone will get a good sense of the kind of comments that actually help. If you have trouble understanding someone else’s code, let them know how they can improve it.”

## 32.4 Keys to Effective Comments

> As long as there are ill-defined goals, bizarre bugs, and unrealistic schedules, there will be Real Programmers willing to jump in and Solve The Problem, saving the documentation for later. Long live Fortran! —Ed Post

What does the following routine do?

```
Java Mystery Routine Number One
// write out the sums 1..n for all n from 1 to num
current = 1;
previous = 0;
sum = 1;
for ( int i = 0; i < num; i++ ) {
    System.out.println( "Sum = " + sum );
    sum = current + previous;
    previous = current;
    current = sum;
}
```

Your best guess?

This routine computes the first num Fibonacci numbers. Its coding style is a little better than the style of the routine at the beginning of the chapter, but the comment is wrong, and if you blindly trust the comment, you head down the primrose path in the wrong direction.

What about this one?

```
Java Mystery Routine Number Two
// set product to "base"
product = base;

// loop from 2 to "num"
for ( int i = 2; i <= num; i++ ) {
    // multiply "base" by "product"
    product = product * base;
}
System.out.println( "Product = " + product );
```

This routine raises an integer base to the integer power num. The comments in this routine are accurate, but they add nothing to the code. They are merely a more verbose version of the code itself.

Here’s one last routine:

```
Java Mystery Routine Number Three
// compute the square root of Num using the Newton-Raphson approximation
r = num / 2;
while ( abs( r - (num/r) ) > TOLERANCE ) {
    r = 0.5 * ( r + (num/r) );
}
System.out.println( "r = " + r );
```

This routine computes the square root of num. The code isn’t great, but the comment is accurate.

Which routine was easiest for you to figure out correctly? None of the routines is particularly well written—the variable names are especially poor. In a nutshell, however, these routines illustrate the strengths and weaknesses of internal comments. Routine One has an incorrect comment. Routine Two’s commenting merely repeats the code and is therefore useless. Only Routine Three’s commenting earns its rent. Poor comments are worse than no comments. Routines One and Two would be better with no comments than with the poor comments they have.

The following subsections describe keys to writing effective comments.

### Kinds of Comments

Comments can be classified into six categories:

#### Repeat of the Code

A repetitious comment restates what the code does in different words. It merely gives the reader of the code more to read without providing additional information.

#### Explanation of the Code

Explanatory comments are typically used to explain complicated, tricky, or sensitive pieces of code. In such situations they are useful, but usually that’s only because the code is confusing. If the code is so complicated that it needs to be explained, it’s nearly always better to improve the code than it is to add comments. Make the code itself clearer, and then use summary or intent comments.

Here’s a particularly difficult style to maintain:

![](img/649c8eee28c38ca1e062691e45dc9883_826_0.png)

### Microsoft Visual Basic Example of a Commenting Style That’s Hard to Maintain

```
`set up Color enumerated type
+----------------------------+
---
set up Vegetable enumerated type
+----------------------------+
---`
```

It’s hard to know what value the plus sign at the beginning and end of each dashed line adds to the comment, but it’s easy to guess that every time a comment changes, the underline has to be adjusted so that the ending plus sign is in precisely the right place. And what do you do when a comment spills over into two lines? How do you align the plus signs? Take words out of the comment so that it takes up only one line? Make both lines the same length? The problems with this approach multiply when you try to apply it consistently.

A common guideline for Java and C++ that arises from a similar motivation is to use // syntax for single-line comments and /* ... */ syntax for longer comments, as shown here:

### Java Example of Using Different Comment Syntaxes for Different Purposes

```
// This is a short comment
---
/* This is a much longer comment. Four score and seven years ago our fathers brought forth on this continent a new nation, conceived in liberty and dedicated to the proposition that all men are created equal. Now we are engaged in a great civil war, testing whether that nation or any nation so conceived and so dedicated can long endure. We are met on a great battlefield of that war. We have come to dedicate a portion of that field as a final resting-place for those who here gave their lives that that nation might live. It is altogether fitting and proper that we should do this.
*/
```

The first comment is easy to maintain as long as it’s kept short. For longer comments, the task of creating long columns of double slashes, manually breaking lines of text between rows, and similar activities is not very rewarding, and so the /* ... */ syntax is more appropriate for multiline comments.

![](img/649c8eee28c38ca1e062691e45dc9883_826_1.png)

The point is that you should pay attention to how you spend your time. If you spend a lot of time entering and deleting dashes to make plus signs line up, you’re not programming, you’re wasting time. Find a more efficient style. In the case of the underlines with plus signs, you could choose to have just the comments without any underlining. If you need to use underlines for emphasis, find some way other than

### Optimum Number of Comments

![](img/649c8eee28c38ca1e062691e45dc9883_828_0.png)

Capers Jones points out that studies at IBM found that a commenting density of one comment roughly every 10 statements was the density at which clarity seemed to peak. Fewer comments made the code hard to understand. More comments also reduced code understandability (Jones 2000).

This kind of research can be abused, and projects sometimes adopt a standard such as “programs must have one comment at least every five lines.” This standard addresses the symptom of programmers’ not writing clear code, but it doesn’t address the cause.

If you use the Pseudocode Programming Process effectively, you’ll probably end up with a comment for every few lines of code. The number of comments, however, will be a side effect of the process itself. Rather than focusing on the number of comments, focus on whether each comment is efficient. If the comments describe why the code was written and meet the other criteria established in this chapter, you’ll have enough comments.

## 32.5 Commenting Techniques

Commenting is amenable to several different techniques depending on the level to which the comments apply: program, file, routine, paragraph, or individual line.

### Commenting Individual Lines

In good code, the need to comment individual lines of code is rare. Here are two possible reasons a line of code would need a comment:

- The single line is complicated enough to need an explanation.
- The single line once had an error, and you want a record of the error.

Here are some guidelines for commenting a line of code:

#### Avoid self-indulgent comments

Many years ago, I heard the story of a maintenance programmer who was called out of bed to fix a malfunctioning program. The program’s author had left the company and couldn’t be reached. The maintenance programmer hadn’t worked on the program before, and after examining the documentation carefully, he found only one comment. It looked like this:

```
MOV AX, 723h   ; R. I. P. L. V. B.
```

After working with the program through the night and puzzling over the comment, the programmer made a successful patch and went home to bed. Months later, he met the program’s author at a conference and found out that the comment stood for “Rest in peace, Ludwig van Beethoven.” Beethoven died in 1827 (decimal), which is 723 (hexadecimal). The fact that 723h was needed in that spot had nothing to do with the comment. Aaarrrghhhh!
