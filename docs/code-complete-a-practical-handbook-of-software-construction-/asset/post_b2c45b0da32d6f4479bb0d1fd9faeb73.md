
Use the labeled break structure if your language supports it. Java supports use of labeled breaks to prevent the kind of problem experienced with the New York City telephone outage. A labeled break can be used to exit a for loop, an if statement, or any block of code enclosed in braces (Arnold, Gosling, and Holmes 2000).

Here’s a possible solution to the New York City telephone code problem, with the programming language changed from C++ to Java to show the labeled break:

**Java Example of a Better Use of a Labeled break Statement Within a do-switch-if Block**

```java
do {
    ...
    switch
        CALL_CENTER_DOWN:
        if () {
            ...
            break CALL_CENTER_DOWN;
            ...
        }
        ...
} while ( ... );
```

> The target of the labeled break is unambiguous.

Use break and continue only with caution. Use of break eliminates the possibility of treating a loop as a black box. Limiting yourself to only one statement to control a loop’s exit condition is a powerful way to simplify your loops. Using a break forces the person reading your code to look inside the loop for an understanding of the loop control. That makes the loop more difficult to understand.

Use break only after you have considered the alternatives. You don’t know with certainty whether continue and break are virtuous or evil constructs. Some computer scientists argue that they are a legitimate technique in structured programming; some argue that they aren’t. Because you don’t know in general whether continue and break are right or wrong, use them, but only with a fear that you might be wrong. It really is a simple proposition: if you can’t defend a break or a continue, don’t use it.

## Checking Endpoints

A single loop usually has three cases of interest: the first case, an arbitrarily selected middle case, and the last case. When you create a loop, mentally run through the first, middle, and last cases to make sure that the loop doesn’t have any off-by-one errors. If you have any special cases that are different from the first or last case, check those too. If the loop contains complex computations, get out your calculator and manually check the calculations.

Designers of Ada decided to make for loop indexes invalid outside their loops; trying to use one outside its for loop generates an error at compile time.

C++ and Java implement the same idea to some extent—they allow loop indexes to be declared within a loop, but they don’t require it. In the example on page 378, the recordCount variable could be declared inside the for statement, which would limit its scope to the for loop, like this:

**C++ Example of Declaring a Loop-Index Variable Within a for loop**

```cpp
for ( int recordCount = 0; recordCount < MAX_RECORDS; recordCount++ ) {
    // looping code that uses recordCount
}
```

In principle, this technique should allow creation of code that redeclares recordCount in multiple loops without any risk of misusing the two different recordCounts. That usage would give rise to code that looks like this:

**C++ Example of Declaring Loop-Indexes Within for loops and Reusing Them Safely—Maybe!**

```cpp
for ( int recordCount = 0; recordCount < MAX_RECORDS; recordCount++ ) {
    // looping code that uses recordCount
}
// intervening code
for ( int recordCount = 0; recordCount < MAX_RECORDS; recordCount++ ) {
    // additional looping code that uses a different recordCount
}
```

This technique is helpful for documenting the purpose of the recordCount variable; however, don’t rely on your compiler to enforce recordCount’s scope. Section 6.3.3.1 of The C++ Programming Language (Stroustrup 1997) says that recordCount should have a scope limited to its loop. When I checked this functionality with three different C++ compilers, however, I got three different results:

- The first compiler flagged recordCount in the second for loop for multiple variable declarations and generated an error.
- The second compiler accepted recordCount in the second for loop but allowed it to be used outside the first for loop.
- The third compiler allowed both usages of recordCount and did not allow either one to be used outside the for loop in which it was declared.

As is often the case with more esoteric language features, compiler implementations can vary.

## How Long Should a Loop Be?

Loop length can be measured in lines of code or depth of nesting. Here are some guidelines:

**Make your loops short enough to view all at once** If you usually look at loops on your monitor and your monitor displays 50 lines, that puts a 50-line restriction on you. Experts have suggested a loop-length limit of one page. When you begin to appreciate the principle of writing simple code, however, you'll rarely write loops longer than 15 or 20 lines.

Cross-Reference For details on simplifying nesting, see Section 19.4, "Taming Dangerously Deep Nesting."

**Limit nesting to three levels** Studies have shown that the ability of programmers to comprehend a loop deteriorates significantly beyond three levels of nesting (Yourdon 1986a). If you're going beyond that number of levels, make the loop shorter (conceptually) by breaking part of it into a routine or simplifying the control structure.

**Move loop innards of long loops into routines** If the loop is well designed, the code on the inside of a loop can often be moved into one or more routines that are called from within the loop.

**Make long loops especially clear** Length adds complexity. If you write a short loop, you can use riskier control structures such as *break* and *continue*, multiple exits, complicated termination conditions, and so on. If you write a longer loop and feel any concern for your reader, you'll give the loop a single exit and make the exit condition unmistakably clear.

## 16.3 Creating Loops Easily—From the Inside Out

If you sometimes have trouble coding a complex loop—which most programmers do—you can use a simple technique to get it right the first time. Here's the general process. Start with one case. Code that case with literals. Then indent it, put a loop around it, and replace the literals with loop indexes or computed expressions. Put another loop around that, if necessary, and replace more literals. Continue the process as long as you have to. When you finish, add all the necessary initializations. Since you start at the simple case and work outward to generalize it, you might think of this as coding from the inside out.

Cross-Reference Coding a loop from the inside out is similar to the process described in Chapter 9, "The Pseudocode Programming Process."

Suppose you're writing a program for an insurance company. It has life-insurance rates that vary according to a person's age and sex. Your job is to write a routine that computes the total life-insurance premium for a group. You need a loop that takes the rate for each person in a list and adds it to a total. Here's how you'd do it.

First, in comments, write the steps the body of the loop needs to perform. It’s easier to write down what needs to be done when you’re not thinking about details of syntax, loop indexes, array indexes, and so on.

**Step 1: Creating a Loop from the Inside Out (Pseudocode Example)**

```text
-- get rate from table
-- add rate to total
```

Second, convert the comments in the body of the loop to code, as much as you can without actually writing the whole loop. In this case, get the rate for one person and add it to the overall total. Use concrete, specific data rather than abstractions.

> *table* doesn’t have any indexes yet.

**Step 2: Creating a Loop from the Inside Out (Pseudocode Example)**

```text
rate = table[ ]
totalRate = totalRate + rate
```

The example assumes that *table* is an array that holds the rate data. You don’t have to worry about the array indexes at first. *rate* is the variable that holds the rate data selected from the rate table. Likewise, *totalRate* is a variable that holds the total of the rates.

Next, put in indexes for the *table* array:

**Step 3: Creating a Loop from the Inside Out (Pseudocode Example)**

```text
rate = table[ census.Age ][ census.Gender ]
totalRate = totalRate + rate
```

The array is accessed by age and sex, so *census.Age* and *census.Gender* are used to index the array. The example assumes that *census* is a structure that holds information about people in the group to be rated.

The next step is to build a loop around the existing statements. Since the loop is supposed to compute the rates for each person in a group, the loop should be indexed by person.

**Step 4: Creating a Loop from the Inside Out (Pseudocode Example)**

```text
For person = firstPerson to lastPerson
    rate = table[ census.Age, census.Gender ]
    totalRate = totalRate + rate
End For
```

All you have to do here is put the *for* loop around the existing code and then indent the existing code and put it inside a *begin-end* pair. Finally, check to make sure that the variables that depend on the *person* loop index have been generalized. In this case, the *census* variable varies with *person*, so it should be generalized appropriately.
