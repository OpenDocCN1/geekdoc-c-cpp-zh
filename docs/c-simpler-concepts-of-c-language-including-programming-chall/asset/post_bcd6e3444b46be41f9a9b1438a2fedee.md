
## CODING GUIDELINES

Naming conventions represent one area in Computer Science where there are far too divergent views (program layout is the other principle area). The primary purpose of an object's name in a programming language is to describe the use and/or contents of that. A secondary consideration may be to describe the type of the object. Programmers use different mechanisms to handle these objectives. Unfortunately, there are far many 'conventions' in place; it would be asking much to expect any programmer to follow several different standards. Therefore, this standard will apply across all languages as much as possible.

The vast majority of programmers know only one language - English. Some programmers may not be familiar with a common non-English phrase that is not in their language (e.g., rendezvous). Since English is the common language of most programmers, all identifiers use easily recognizable English words and phrases.

## 15.4.4. Organizing control structures

Although the control structures in modern languages trace their roots back to Algol-60, there is a surprising number of subtle variations between the control structures found in common programming languages used today. This paper will describe a mechanism to unify the various control structures the programming languages we use in an attempt to make it possible for a Visual BASIC programmer to easily understand code written in Pascal or C++ as well as make it possible for C++ programmers to read BASIC and Pascal programs, etc.

Typical programming languages contain eight flow-of-control statements: two conditional statements (if..thenelse and case/switch), four loops (while, repeat.., until/do..while, for, and loop), a program unit invocation (i.e., procedure call), and a sequence. There are other less common control structures include processes/co routines, for loops (iterators), and generators, but this paper will focus only on the most common control mechanisms.

Control structures typically come in two forms: those that act on a single statement as an operand and those that act on a sequence of statements. For example, the if..then statement in Pascal operates on a single statement:

> if (expression) then Statement;

Of course it is possible to apply Pascal's statement to a list of statements, that involves creating a compound statement using a begin..end pair. There are two problems with this type of statement. First of all, it introduces the problem of where you are supposed to put the begin and end in a well-formatted program. This is a very controversial issue with large numbers of programmers in different camps. Some feel an if with a compound statement should look like this:

```
if (expression) then begin
{ Statement 1 }
{ Statement 2 }
{ Statement n }
end;
```

Others feel it should look like this:

```
if (expression) then
begin
[ Statement 1 ]
[ Statement 2 ]
.
.
[ Statement n ]
end;
```

C/C++ programmers are even worse, there are no less than four common ways of putting the opening and closing braces around a compound statement after an "if". The second problem with C/C++ and Pascal's "if" statements is the ambiguity involved. Consider the following Pascal code:

```
if (expression) then
if (expression) then
(* Statement *)
else (* Statement *);
```

The nested code should be clearly intended. For example, in the below code it is difficult to say which 'if' does the 'else' belongs to.

### Incorrect

```
if (expression) then
If (expression) then
...
def;
else
...
def;
```

### Correct

```
if (expression) then
If (expression) then
...
endif;
```

```
else
```

...

```
endif;```

Now there is no question that the else belongs to the first if above, not the second. Note that this form of “if” statement allows you to attach a list of statements(between if and else or if and endif) rather than a single or compound statement. Furthermore, it totally eliminates the religious argument where to put the braces or the begin.. end pair on the first. The complete set of modern programming language constructs includes:

- if.then..elseif..else..endif
- select.case..default..select(typical case/switch statement)
- while..endwhile
- repeat..until
- loop..endloop
- for..endfor
- break
- breakif
- continue

## Loops

There are three general categories of looping constructs available in common high-level-loops that test for termination at the beginning of the loop (e.g., while), loops that test for loop termination at the bottom of the loop (e.g., repeat..until), and those that test for loop termination in the middle of the loop (e.g., loop..endloop). It is possible to simulate any one of these loops using any of the others. This is particularly trivial with loop..endloop construct:

```
/ Test for loop termination at beginning of LOOP..ENDLOOP */
loop
breakif (x==y);
endloop;
```

```
/ Test for loop termination in the middle of LOOP..ENDLOOP */
loop
breakif (x==y);
endloop;
```

```
/* Test for loop termination at the end of LOOP.ENDLOOP */
loop
breakif (x==y);
endloop;
```

Given the flexibility of the loop..endloop control structure, you might question why one would even burden a compiler with the other loop statements. However, using the appropriate loop structure makes a program far more readable, therefore, you should never use one type of loop when the situation demands another.

## 15.4.5. Program layout

After naming conventions and where to put braces (or Begin...End), the other argument programmers engage in how to lay out a program, what are the indentations one should use in a well written program? Unfortunately, the layout is something that varies by language. The layout of an easy to read C/C++ program is considerably different than that of an assembly language, Prolog, or Bison/YACC program. Usually, this section will describe those conventions that generally apply to all programs. According to McConnell (Code Complete), research shows that there is a strong correlation between program indentation and comprehensibility. Miaria et al. ("Program Indentation and Comprehension") concluded that indentation in the two to four character range was optimal even many subjects felt that six-space indentation looked better. These results are probably due to the fact that the eye has to travel less distance.

The principle tool for creating good layout is whitespace (or the lack thereof). The following paragraphs summarize McConnell's finding on the subject:

- Grouping: Related statements should be grouped together. Statements that logically belong together contain no interleaving whitespace.
- Blank lines: Blank lines should separate declarations from the start of code, logically related statements from unrelated statements, and blocks of comments from blocks of code.
- Alignment: Align objects that belong together. Examples include type names in a declaration, assignment operators in a sequence of related statements, and columns of initialized data.
- Indentation: Indenting statements inside block statements improves readability; see the de-facto comments and rules earlier in this.

In theory, a line of source code can be arbitrarily long. In practice, there are several limitations on source code lines. Paramount is the amount of text that will fit on a terminal device and what can be printed on a typical sheet of paper. If this isn't enough to suggest an 80 character limit on source lines, McConnell suggests that longer lines are harder to read.

If a statement approaches the limit of 80 characters, it should be broken at a reasonable point and split across two lines. If the line is a control statement involving a particularly long logical expression, the expression should be broken up at a logical point (e.g., at the point of a low-precedence operator outside any parentheses) or the remainder of the expression placed underneath the first part of the expression. E.g.,

```
(
 x + y * z) < (ComputeProfits(1980,1990) / 1.0775 ) && &&
( ValueOfStock[This Year] >= ValueOfStock[LastYear] )
<< statements >>
endif;
```

Many statements (e.g., IF, WHILE, FOR, and function calls) contain a keyword followed by a parenthesis. If it is too long to fit on one line, putting the opening and closing parentheses in the same column as the first character of the start of the statement and indenting the remaining expression elements. The example above demonstrates this for the "IF" statement. The following examples demonstrate this technique for other statements:
