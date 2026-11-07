# Addition Program Pseudocode

Let’s look at a pseudocode example that might help a programmer create the addition program of Fig. 2.4. The following pseudocode corresponds to the algorithm that inputs two integers from the user, adds them and displays their sum. We show the complete pseudocode listing here. We’ll show how to create pseudocode from a problem statement later in the chapter.

+   1. Prompt the user to enter the first integer
+   2. Input the first integer
+   3. 
+   4. Prompt the user to enter the second integer
+   5. Input the second integer
+   6. 
+   7. Add first integer and second integer, store result
+   8. Display result

The pseudocode statements are simply English statements that convey what task is to be performed in C++. Lines 1–2 correspond to the C++ statements in lines 12–13 of Fig. 2.4. Lines 4–5 correspond to the statements in lines 15–16, and lines 7–8 correspond to the statements in lines 18 and 20.

# Checkpoint

+   1. **(Fill-in)** The actions described by pseudocode might include ________, ________, ________ or ________.
+      **Answer:** input, output, assignments, calculations.
+   2. **(Fill-in)** ________ is an informal language that helps you develop algorithms without worrying about the strict details of C++ language syntax.
+      **Answer:** Pseudocode.

# 3.4 Control Structures

Typically, program statements execute one after the other in the order in which they’re written. This process is called sequential execution. Various C++ statements, which we’ll soon discuss, enable you to specify that the next statement to execute is not necessarily the next one in sequence. This is called transfer of control.

During the 1960s, it became clear that the indiscriminate use of transfers of control was the root of many problems experienced by software development groups. The blame was pointed at the goto statement (used in most programming languages of the time), which allows you to specify a transfer of control to one of a wide range of destinations in a program.

The research of Böhm and Jacopini¹ demonstrated that programs could be written without any goto statements. The challenge for the era’s programmers was shifting their styles to “goto-less programming.” The term structured programming became almost

1. C. Böhm and G. Jacopini, “Flow Diagrams, Turing Machines, and Languages with Only Two Formation Rules,” Communications of the ACM, vol. 9, No. 5, May 1966, pp. 336–371.