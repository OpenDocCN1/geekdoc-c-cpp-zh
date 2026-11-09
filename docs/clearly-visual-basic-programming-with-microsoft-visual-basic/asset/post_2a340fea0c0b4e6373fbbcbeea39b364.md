
Figure 13-4 shows a modified version of the previous problem specification; in this version, Rob is 10 steps away from the door. How could you rewrite the original algorithm to reflect this minor change? One way is by adding nine more *walk forward* instructions to the original algorithm; however, that would be quite cumbersome to write. Imagine if Rob were 500 steps from the door! A better way to modify the original algorithm is by adding a repetition structure to it, as shown in the modified algorithm in Figure 13-4. The repetition structure, which begins with the *repeat 10 times:* line and ends with the *end repeat* line, directs Rob to walk forward 10 times.

```
Rob is standing in his hallway facing his bedroom door. The door, which may or may not be closed, is 10 steps away from Rob. Rob wants to go inside his bedroom.

1. repeat 10 times:
       walk forward
   end repeat
2. if the door is closed, do this:
       open the door
   end if
3. walk forward
```

**Figure 13-4: Fourth problem using Rob**

Figure 13-5 shows a modified version of the previous problem specification. In this version, the number of steps between Rob and the door is unknown. He might be 10 steps away or 500 steps away; or, Rob might already be directly in front of the door. How will this affect the algorithm shown in Figure 13-4? The repetition structure in the algorithm will need to be changed because the number of steps between Rob and the door is no longer known. Rather than telling Rob to repeat the *walk forward* instruction 10 times, the repetition structure will need to tell him to repeat the instruction until he is directly in front of the door. Once Rob is positioned correctly, he still will need to follow the second and third instructions in the algorithm. The modified algorithm is included in Figure 13-5. The repetition structure begins with the *repeat until you are directly in front of the door:* line, and it ends with the *end repeat* line.

Rob is standing in his hallway facing his bedroom door. The door, which may or may not be closed, is an unknown number of steps away from Rob. Rob wants to go inside his bedroom.

```
1. repeat until you are directly in front of the door:
    walk forward
end repeat
2. if the door is closed, do this:
    open the door
end if
3. walk forward
```

**Figure 13-5: Fifth problem using Rob**

The repetition structure in Figure 13-5's algorithm ends when Rob is standing directly in front of his bedroom door. If Rob is 10 steps away from the door, the repetition structure directs him to walk forward 10 times before determining whether the door is closed. Similarly, if Rob is 500 steps away from the door, the repetition structure directs him to walk forward 500 times. If Rob is directly in front of the door, the *walk forward* instruction in the repetition structure is bypassed.

## MINI-QUIZ 1

- 1. Rob is sitting in a chair in his living room. Next to the chair is a table. On top of the table is Rob's cell phone. Your task is to direct Rob to pick up his cell phone. Does the solution to this problem require a repetition structure? If so, what needs to be repeated?
- 2. Rob is sitting in a chair in his living room. At the other end of the room is a table. On top of the table is Rob's cell phone. Your task is to direct Rob to pick up his cell phone, but only when the phone rings. Does the solution to this problem require a repetition structure? If so, what needs to be repeated?
- 3. Rob wants to write down, on a piece of paper, the name of each book in his personal library. The loop in the solution can begin with *repeat for* ____________.

## THE DO...LOOP STATEMENT

Before solving real-world problems that require a repetition structure, you will learn about the Do...Loop statement, which is one of three statements used to code a repetition structure in Visual Basic. (The other two statements, For...Next and For Each...Next, are covered in subsequent chapters.) You can use the Do...Loop statement to code both a pretest loop and a posttest loop. As mentioned earlier, this chapter covers pretest loops. Figure 13-6 shows the syntax of the Do...Loop statement when used to code a pretest loop. The statement begins with the Do clause and ends with the Loop clause. Between both clauses, you enter the instructions you want the computer to repeat. The {While | Until} portion of the syntax indicates that you can select only one of the keywords appearing within the braces—either While or Until. You do not type the braces or the pipe symbol (|) when entering the Do...Loop statement. You follow the While or Until keyword with a *condition*, which can contain variables, constants, properties, methods, or operators. Like the *condition* in the If...Then...Else statement, the *condition* in the Do...Loop statement must evaluate to a Boolean value—either True or False. The *condition* determines whether the computer processes the loop instructions. The keyword While indicates that the loop instructions should be processed *while* the condition is true. The keyword Until, on the other hand, indicates that the loop instructions should be processed *until* the condition becomes true. Also included in Figure 13-6 are two examples of pretest loops. Both examples produce the same result, which is to display the numbers 1, 2, and 3 in message boxes.

**DO...LOOP STATEMENT**

*Syntax for coding a pretest loop*

**Do {While | Until}** *condition*

*instructions to be processed either while the condition is true or until the condition becomes true*

**Loop**

Example 1

```vb
intNumber = 1
Do While intNumber <= 3
    MessageBox.Show(intNumber.ToString)
    intNumber = intNumber + 1
Loop
```

Example 2

```vb
intNumber = 1
Do Until intNumber > 3
    MessageBox.Show(intNumber.ToString)
    intNumber = intNumber + 1
Loop
```

**Figure 13-6: Syntax and examples of the Do...Loop statement for a pretest loop**

Both examples in Figure 13-6 begin by assigning the number 1 to an Integer variable named intNumber. The intNumber variable is called a **counter variable**, because it is used to count something. Repetition structures use counter variables to count such things as the number of employees paid in a week or the number of positive numbers entered by the user. The repetition structures in Figure 13-6 use the intNumber counter variable to keep track of the number of times the loop instructions are processed. Counter variables are always numeric variables and are typically assigned a beginning value of either 0 or 1, depending on the value required by the application. The assignment is done outside the loop, because it needs to be performed only once. Counter variables also must be updated. **Updating**, also called **incrementing**, means adding a number to the value stored in the counter variable. The number can be positive or negative, integer or non-integer. A counter variable is always incremented by a constant value, usually the number 1. You update the counter variable within the loop, because the updating task must be performed each time the loop instructions are processed. In both examples in Figure 13-6, the counter variable is updated by the intNumber = intNumber + 1 statement within the loop.

The Do clause in Example 1 in Figure 13-6 tells the computer to repeat the loop instructions *while* the value in the intNumber variable is less than or equal to 3. The Do clause in Example 2, on the other hand, tells the computer to repeat the loop instructions *until* the value in the intNumber variable is greater than 3. As mentioned earlier, both examples produce the same result; both simply represent two different ways of saying the same thing. Figure 13-7 describes the way the computer processes the code shown in Example 1. Notice that the loop ends when the counter variable, intNumber, contains the number 4.
