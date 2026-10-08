# Flowcharting a Posttest Loop

structure checks Robin's initial location. In this case, Robin is already in front of her bedroom door, so the selection structure's condition evaluates to false. As a result, the selection structure ends without processing the posttest loop contained in its true path. Robin simply continues to the second instruction in the algorithm. Although the modified algorithm works correctly, most programmers prefer to use a posttest loop, rather than a pretest loop with a selection structure, because it is easier to understand. Posttest loops should be used only when these instructions must be processed at least once. Once you will find a posttest loop in programs that allow the user to select from a menu, such as a game program. This type of program uses the posttest loop to control the display of the menu, which must appear on the screen at once.

# Flowcharting a Posttest Loop

For many people, it's easier to understand the difference between a pretest loop and a posttest loop by viewing loops in flowchart form. Figure 8-3 shows the problem specification for the Miller Incorporated program from Chapter 7. It also shows two flowcharts in flowchart form. Algorithm 1, which you view in Figure 7-6 in Chapter 7, Algorithm 2 uses a pretest loop to get the amounts from the user; Algorithm 2 uses a posttest loop. Notice the diamond, which contains the loop's condition, at the top of a pretest loop; it appears at the bottom of a posttest loop.

### Problem specification
In each year, Miller pays a 5% bonus to each of his salespeople. The bonus is based on the amount of sales made by the salesperson during the previous year. The payroll clerk wants a program that calculates and displays the bonus amounts for as many salespeople as needed without having to run the program more than once. Because the sales amounts entered by the payroll clerk will be positive numbers, the payroll clerk will indicate he is finished by entering a sales amount of -1 (a negative number 1).

![](bbox=[0.118, 0.655, 0.783, 0.903])