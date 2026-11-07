
## 3.2 Algorithms

Any computing problem can be solved by executing a series of actions in a specific order. An algorithm is a procedure for solving a problem in terms of

- 1. the actions to execute and
- 2. the order in which these actions execute

The following example demonstrates that correctly specifying the order in which the actions execute is essential.

Consider the “rise-and-shine algorithm,” one executive follows for getting out of bed and going to work: (1) Get out of bed; (2) take off pajamas; (3) take a shower; (4) get dressed; (5) eat breakfast; (6) carpool to work. This routine gets the executive to work well prepared to make critical decisions. Suppose that the same steps are performed in a slightly different order: (1) Get out of bed; (2) take off pajamas; (3) get dressed; (4) take a shower; (5) eat breakfast; (6) carpool to work. In this case, our executive shows up for work soaking wet. Specifying the order in which statements (actions) execute in a program is called program control. This chapter investigates program control using C++’s control statements.

### Checkpoint

- 1. *(Fill-in)* Specifying the order in which statements (actions) execute in a program is called ________.
  **Answer:** program control.
- 2. *(Fill-in)* A procedure for solving a problem in terms of the ________ to execute and the ________ in which these actions execute is called an algorithm.
  **Answer:** actions, order.

## 3.3 Pseudocode

Pseudocode is an informal language that helps you develop algorithms without worrying about the strict details of C++ language syntax. The pseudocode we present is particularly useful for developing algorithms that will be converted to structured portions of C++ programs. Pseudocode is similar to everyday English (or your preferred language)—it’s convenient and user-friendly, but it’s not an actual computer programming language. You’ll see an algorithm written in pseudocode momentarily.

Pseudocode does not execute on computers. Rather, it helps you “think out” a program before attempting to write it in a programming language like C++. This chapter provides several examples of using pseudocode to develop C++ programs.

The style of pseudocode we present consists purely of characters, so you can type pseudocode conveniently using any text-editor program. A carefully prepared pseudocode program can easily be converted to a corresponding C++ program.

Pseudocode typically describes only statements representing the actions that occur after you convert a program from pseudocode to C++ and run the program. Such actions might include input, output, assignments or calculations. In our pseudocode, we typically do not include variable declarations, but some programmers choose to list variables and mention their purposes.

### Addition Program Pseudocode

Let’s look at a pseudocode example that might help a programmer create the addition program of Fig. 2.4. The following pseudocode corresponds to the algorithm that inputs two integers from the user, adds them and displays their sum. We show the complete pseudocode listing here. We’ll show how to create pseudocode from a problem statement later in the chapter.

- 1. Prompt the user to enter the first integer
- 2. Input the first integer
- 3.
- 4. Prompt the user to enter the second integer
- 5. Input the second integer
- 6.
- 7. Add first integer and second integer, store result
- 8. Display result

The pseudocode statements are simply English statements that convey what task is to be performed in C++. Lines 1–2 correspond to the C++ statements in lines 12–13 of Fig. 2.4. Lines 4–5 correspond to the statements in lines 15–16, and lines 7–8 correspond to the statements in lines 18 and 20.

### Checkpoint

- 1. **(Fill-in)** The actions described by pseudocode might include ________, ________, ________ or ________.
  **Answer:** input, output, assignments, calculations.
- 2. **(Fill-in)** ________ is an informal language that helps you develop algorithms without worrying about the strict details of C++ language syntax.
  **Answer:** Pseudocode.

## 3.4 Control Structures

Typically, program statements execute one after the other in the order in which they’re written. This process is called sequential execution. Various C++ statements, which we’ll soon discuss, enable you to specify that the next statement to execute is not necessarily the next one in sequence. This is called transfer of control.

During the 1960s, it became clear that the indiscriminate use of transfers of control was the root of many problems experienced by software development groups. The blame was pointed at the goto statement (used in most programming languages of the time), which allows you to specify a transfer of control to one of a wide range of destinations in a program.

The research of Böhm and Jacopini¹ demonstrated that programs could be written without any goto statements. The challenge for the era’s programmers was shifting their styles to “goto-less programming.” The term structured programming became almost

- 1. C. Böhm and G. Jacopini, “Flow Diagrams, Turing Machines, and Languages with Only Two Formation Rules,” Communications of the ACM, vol. 9, No. 5, May 1966, pp. 366–371.

The solid circle at the top of the activity diagram represents the initial state—the beginning of the workflow before the program performs the modeled actions. The solid circle surrounded by a hollow circle at the bottom of the diagram represents the final state—that is, the end of the workflow after the program performs its actions.

The preceding sequence-structure activity diagram also includes rectangles with the upper-right corners folded over. These are UML notes (like C++ comments)—explanatory remarks describing the purpose of symbols in the diagram. A dotted line connects each note with the element it describes. This diagram’s UML notes show how the diagram relates to the C++ code for each action state. Activity diagrams usually do not show the C++ code.

### 3.4.2 Selection Statements

C++ has three types of selection statements. The if selection statement performs (selects) an action (or group of actions) if a condition is true or skips it if the condition is false. The if…else selection statement performs an action (or group of actions) if a condition is true and performs a different action (or group of actions) if the condition is false. The switch selection statement (Chapter 4) performs one of many different actions (or groups of actions), depending on the value of an expression.

The if statement is called a single-selection statement because it selects or ignores a single action (or group of actions). The if…else statement is called a double-selection statement because it selects between two different actions (or groups of actions). The switch statement is called a multiple-selection statement because it selects among many different actions (or groups of actions).

### 3.4.3 Iteration Statements

C++ provides four iteration statements—also called repetition statements or looping statements—for performing statements repeatedly while a loop-continuation condition remains true. The iteration statements are the while, do…while, for and range-based for. The while and for statements perform their action (or group of actions) zero or more times. If the loop-continuation condition is initially false, the action (or group of actions) does not execute. The do…while statement performs its action (or group of actions) one or more times. Chapter 4 presents the do…while and for statements. Chapter 6 presents the range-based for statement.

### Keywords

Each of the words if, else, switch, while, do and for is a C++ keyword. Keywords cannot be used as identifiers, such as variable names, and contain only lowercase letters (and sometimes underscores). The following table shows the complete list of C++ keywords:

| C++ keywords |  |  |  |  |
|---|---|---|---|---|
| alignas | alignof | and | and_eq | asm |
| auto | bitand | bitor | bool | break |
| case | catch | char | char16_t | char32_t |
| class | compl | const | const_cast | constexpr |
