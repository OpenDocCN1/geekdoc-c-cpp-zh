
## CHAPTER 8

## More on the Repetition Structure

To understand why the loops in Figure 8-1 are not interchangeable, you will desk-check them twice. For the first desk-check, Robin is one step away from her bedroom door. In the pretest, the loop's condition checks Robin's current location. Robin is not directly in the door, so she is told to walk forward and the loop's condition is evaluated again. Robin is now positioned correctly in front of her door, so the loop ends and Robin continues to the second instruction in the algorithm. The posttest loop, on the other hand, instructs Robin to walk forward, which places her directly in front of her bedroom door. The loop's condition is evaluated next. The condition checks whether Robin is positioned correctly; so the loop ends and Robin continues to the second instruction in the algorithm. Notice that when Robin is one step away from the door, the pretest and posttest produce the same result: both place her in front of the door. For the second desk-check, Robin is standing directly in front of her bedroom door. The condition checks Robin's location. Robin is already positioned correctly, so the walk forward instruction is bypassed and the loop ends. The posttest loop before the condition is evaluated. If Robin walks forward she will bump into the door. Obviously, the loop in Algorithm 2 does not work correctly when Robin starts directly in front of her bedroom door. You can fix this problem by adding a selection structure. The modified algorithm is shown in Figure 8-2.

![](img/d64a28a68f49d61137bf2f3170ac40ad_286_0.png)

![](img/d64a28a68f49d61137bf2f3170ac40ad_286_1.png)

### Modified Algorithm 2 – posttest loop

1. if (you are not directly in front of the bedroom door)
   repeat
     walk forward
   repeat while (while you are not directly in front of the bedroom door)
end if
2. if (the bedroom door is closed)
   open the bedroom door
end if
3. walk forward

## Figure 8-2 Selection structure added to Algorithm 2 from Figure 8-1

The posttest loop in Figure 8-2 is identical to the posttest loop in Figure 8-1, except it is executed only when Robin is not directly in front of her bedroom door. To understand how the selection and repetition structures in Figure 8-2 work, you will desk-check that portion of the algorithm twice. For the first desk-check, Robin is one step away from her bedroom door. The algorithm in Figure 8-2 begins with a single-alternative selection choice which checks Robin's initial location. The condition evaluates to true because Robin is not directly in front of her bedroom door. Therefore, the selection's true path is processed. The first instruction in the selection (repeat) marks the beginning of a posttest loop. Next, the instruction in the loop bodies Robin to walk forward. The loop's condition is evaluated. At this point, Robin is positioned correctly; so the loop ends and so does this selection. Robin continues to the second instruction in the algorithm. For the second desk-check, Robin is directly in front of her bedroom door. Here, the condition in the selection structure checks Robin's initial location. In this case, Robin is already in front of her bedroom door, so the selection structure's condition evaluates to false. As a result, the selection structure ends without processing the posttest loop contained in its true path. Robin simply continues to the second instruction in the algorithm. Although the modified algorithm works correctly, most programmers prefer to use a posttest loop, rather than a pretest loop with a selection structure, because it is easier to understand. Posttest loops should be used only when these instructions must be processed at least once. Once you will find a posttest loop in programs that allow the user to select from a menu, such as a game program. This type of program uses the posttest loop to control the display of the menu, which must appear on the screen at once.

## Flowcharting a Posttest Loop

For many people, it's easier to understand the difference between a pretest loop and a posttest loop by viewing loops in flowchart form. Figure 8-3 shows the problem specification for the Miller Incorporated program from Chapter 7. It also shows two flowcharts in flowchart form. Algorithm 1, which you view in Figure 7-6 in Chapter 7, Algorithm 2 uses a pretest loop to get the amounts from the user; Algorithm 2 uses a posttest loop. Notice the diamond, which contains the loop's condition, at the top of a pretest loop; it appears at the bottom of a posttest loop.

### Problem specification
In each year, Miller pays a 5% bonus to each of his salespeople. The bonus is based on the amount of sales made by the salesperson during the previous year. The payroll clerk wants a program that calculates and displays the bonus amounts for as many salespeople as needed without having to run the program more than once. Because the sales amounts entered by the payroll clerk will be positive numbers, the payroll clerk will indicate he is finished by entering a sales amount of -1 (a negative number -1).

![](img/d64a28a68f49d61137bf2f3170ac40ad_287_0.png)

## CHAPTER 8 More on the Repetition Structure (continued)

![](img/d64a28a68f49d61137bf2f3170ac40ad_288_0.png)

Recall that the oval, rectangle, parallelogram, and diamond in a flowchart are called start/stop, processing, input/output, and decision symbols.

Figure 8-3 Miller Incorporated problem specification along with two algorithms shown in flowchart form

You can observe how a posttest loop operates in a program by desk-checking 2 in Figure 8-3. You will see using amounts of 10000 and 25000, followed by the sentinel value (-1). The first input/output symbol in the flowchart represents the priming read. In this case, the reading gets the first sales amount (10000) from the user. The instruction in the processing symbol is handled correctly and is the first instruction in the loop body. The instruction calculates the bonus by multiplying the sales amount by the bonus rate. Notice that the first sales amount is not compared to the sentinel value in a posttest loop. Figure 8-4 shows the first sales and bonus amounts recorded in the desk-check table.

| sales rate | bonus |
|---|---|
| .05 | 20000 | 500 |

Figure 8-4 First sales and bonus amounts recorded in the desk-check table

The first input/output symbol in the loop contains the instruction to display the bonus on the screen. In this case, the number 10000 will be displayed. The second input/output symbol in the loop body gets the next salesperson's sales (25000) from the user and represents the update read. Figure 8-5 shows the second sales amount recorded in the desk-check table.

| bonus rate | sales | bonus |
|---|---|---|
| .05 | 10000 | 500 |
| | 25000 | |

Figure 8-5 Second sales amount recorded in the desk-check table

The next symbol in the flowchart is the decision diamond. The diamond contains the posttest loop condition, which always marks the end of a posttest loop. The condition, which is phrased as a looping condition, compares the current sales amount with the sentinel value to determine whether the loop should be processed again (a true condition) or end (a false condition). Note that the first time the loop condition is evaluated. In this case, the condition evaluates to true (25000 is not equal to -1). When the condition evaluates to true, the computer processes the instructions in the loop body. Those instructions calculate and display the bonus for the second salesperson and then get another amount (in this case, the sentinel value) for the user. Figure 8-6 shows the current status of the desk-check table.

| bonus rate | sales | bonus |
|---|---|---|
| .05 | 10000 | 500 |
| | 25000 | 1250 |
| | -1 | sentinel value |

Figure 8-6 Current status of the desk-check table

Next, the condition is reevaluated whether the loop should be processed again (a true condition) or end (a false condition). In this case, the condition evaluates to false because the current sales amount is equal to the sentinel value. When the condition evaluates to true, the loop ends and continues again with the instruction immediately following the loop. In Algorithm 2's flowchart in 8-3, the loop is followed by the stop oval, which marks the end of the flowchart.

### Mini-Quiz 8-1

1. If the user enters the numbers 5, 8, 9, and -1, how many times will the condition in the following algorithm be evaluated?
   1. enter number
   2. repeat while (number is greater than or equal to 0)
      display number
      enter number
      end repeat
