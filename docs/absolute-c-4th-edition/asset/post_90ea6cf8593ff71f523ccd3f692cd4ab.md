
For an easier version, assume that there is always exactly one blank symbol between any occurrence of `cin` and a following `<<`, and similarly assume that there is always exactly one blank space between each occurrence of `cout` and a following `>>`. For a harder version, allow for the possibility that there may be any number of blanks, even zero, between `cin` and `<<` and between `cout` and `>>`; in this harder case, the replacement corrected version has only one blank between `cin` and `cout` and the following operator. The program to be corrected is in one file and the corrected version is output to a second file. Your program should define a function that is called with the input and output-file streams as arguments. *(Hint: Even if you are doing the harder version, you will probably find it easier and quicker to first do the easier version and then modify your program so that it performs the harder task.)*

- 12. Write a program that allows the user to type in any one-line question and then answers that question. The program will not really pay any attention to the question, but will simply read the question line and discard all that it reads. It always gives one of the following answers:
  
  ```text
  I’m not sure but I think you will find the answer in Chapter #N.
  That’s a good question.
  If I were you, I would not worry about such things.
  That question has puzzled philosophers for centuries.
  I don’t know. I’m just a machine.
  I think it and the answer will come to you.
  I used to know the answer to that question, but I’ve forgotten it.
  The answer can be found in a secret place in the woods.
  ```

These answers are stored in a file (one answer per line), and your program simply reads the next answer from the file and writes it out as the answer to the question. After your program has read the entire file, it simply closes the file, reopens the file, and starts down the list of answers again.

Whenever your program outputs the first answer, it should replace the two symbols `#N` with a number between 1 and 20 (including the possibility of 1 and 20). In order to choose a number between 1 and 20, your program should initialize a variable to 20 and decrease the variable’s value by 1 each time it outputs a number so that the chapter numbers count backward from 20 to 1. When the variable reaches the value 0, your program should change its value back to 20. Give the number 20 the name `NUMBER_OF_CHAPTERS` with a global named constant declaration using the const modifier. *(Hint: Use the function new-line defined in this chapter.)*

- 13. This project is the same as Programming Project 12 except that in this project your program will use a more sophisticated method for choosing the answer to a question. When your program reads a question, it counts the number of characters in the question and stores the number in a variable named `count`. It then responds with answer number `count%ANSWERS`. The first answer in the file is answer number 0, the next is answer number 1, then 2, and so forth. `ANSWERS` is defined in a constant declaration, as shown below, so that it is equal to the number of answers in the answer file:

```cpp
const int ANSWERS = 8;
```

This way you can change the answer file so that it contains more or fewer answers and you need change only the constant declaration to make your program work correctly for a different number of possible answers. Assume that the answer listed first in the file will always be the following, even if the answer file is changed:

I’m not sure but I think you will find the answer in Chapter #N.

When replacing the two characters #N with a number, use the number `(count%NUMBER_OF_CHAPTERS + 1)`, where count is the variable discussed above, and NUMBER_OF_CHAPTERS is a global named constant defined to be equal to the number of chapters in this book.

- 14. This program numbers the lines found in a text file.

Write a program that reads text from a file and outputs each line preceded by a line number. Print the line number right-adjusted in a field of three spaces. Follow the line number with a colon, then one space, then the text of the line. You should get a character at a time, and write code to ignore leading blanks on each line. You may assume that the lines are short enough to fit within a line on the screen. Otherwise, allow default printer or screen output behavior if the line is too long (that is, wrap or truncate).

A somewhat harder version determines the number of spaces needed in the field for the line numbers by counting lines before processing the lines of the file. This version of the program should insert a new line after the last complete word that will fit within a 72-character line.

- 15. In this program you are to process text to create a KWIX table (Key Word In conteXt table). The idea is to produce a list of keywords (not programming language keywords, rather words that have important technical meaning in a discussion), then for each instance of each keyword, place the keyword, the line number of the context, and the keyword in its context in the table. There may be more than one context for a given keyword. The sequence of entries within a keyword is to be the order of occurrence in the text. For this problem, “context” is a user-selected number of words before the keyword, the keyword itself, and a user-selected number of words after the keyword.

The table has an alphabetized column of keywords followed by a line number(s) where the keyword occurs, followed by a column of all contexts within which the keyword occurs. See the example below. For a choice of text consult your instructor.

*Hints:* To get your list of keywords, you should choose and type in several paragraphs from the text, then omit from your paragraph “boring” words such as forms of the verb “to be”; pronouns such as I, me, he, she, her, you, us, them, who, which, etc.; Finally, sort the keyword list and remove duplicates. The better job you do at this, the more useful output you will get.

*Example:* A paragraph and its KWIX Listing:

There are at least two complications when reading and writing with random access via an fstream: (1) You normally work in bytes using

the type `char` or arrays of `char` and need to handle conversions on your own, and (2) You typically need to position a pointer (indicating where the read or write begins) before each read or write.

KWIX Listing:

| Keyword | Line Number | Keyword in Context |
|---|---|---:|
| access | 2 | with random *access* via |
| arrays | 3 | *char* or *arrays* of |
| bytes | 2 | work in *bytes* using |
| char | 3 | the type *char* or |
| char | 3 | array of *char* and |
| conversions | 3 | handle type *conversions* on |

The table is longer than these sample entries.

![](img/9505fd46e120aa9c1406715936ff6251_539_0.png)

## 13 CHAPTER Recursion

### 13.1 RECURSIVE void FUNCTIONS 549

- Example: Vertical Numbers 549
- Tracing a Recursive Call 552
- A Closer Look at Recursion 555
- Pitfall: Infinite Recursion 556
- Stacks for Recursion 558
- Pitfall: Stack Overflow 559
- Recursion versus Iteration 559

### 13.2 RECURSIVE FUNCTIONS THAT RETURN A VALUE 561

- General Form for a Recursive Function That Returns a Value 561
- Example: Another Powers Function 561

### 13.3 THINKING RECURSIVELY 566

- Recursive Design Techniques 566
- Binary Search 568

- CHAPTER SUMMARY 576
- ANSWERS TO SELF-TEST EXERCISES 576
- PROGRAMMING PROJECTS 581

![](img/9505fd46e120aa9c1406715936ff6251_540_0.png)

## Recursion

After a lecture on cosmology and the structure of the solar system, William James was accosted by a little old lady.
"Your theory that the sun is the center of the solar system, and the earth is a ball which rotates around it has a very convincing ring to it, Mr. James, but it's wrong. I've got a better theory," said the little old lady.
"And what is that, madam?" inquired James politely.
"That we live on a crust of earth which is on the back of a giant turtle."
Not wishing to demolish this absurd little theory by bringing to bear the masses of scientific evidence he had at his command, James decided to gently dissuade his opponent by making her see some of the inadequacies of her position.
"If your theory is correct, madam," he asked, "what does this turtle stand on?"
"You're a very clever man, Mr. James, and that's a very good question" replied the little old lady, "but I have an answer to it. And it is this: the first turtle stands on the back of a second, far larger, turtle, who stands directly under him."
"But what does this second turtle stand on?" persisted James patiently.
To this the little old lady crowed triumphantly. "It's no use, Mr. James—it's turtles all the way down."

> J. R. Ross, Constraints on Variables in Syntax

## INTRODUCTION

A function definition that includes a call to itself is said to be recursive. Like most modern programming languages, C++ allows functions to be recursive. If used with a little care, recursion can be a useful programming technique. This chapter introduces the basic techniques needed for defining successful recursive functions. There is nothing in this chapter that is truly unique to C++. If you are already familiar with recursion you can safely skip this chapter.
This chapter only uses material from Chapters 1 to 5. Sections 13.1 and 13.2 do not use any material from Chapter 5, so you can cover recursion any time after Chapter 4. If you have not read Chapter 11, you may find it helpful to review the section of Chapter 1 on namespaces.
