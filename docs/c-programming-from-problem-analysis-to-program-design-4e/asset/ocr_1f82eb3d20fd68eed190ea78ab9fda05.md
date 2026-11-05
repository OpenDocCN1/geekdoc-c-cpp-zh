Because the expression evaluates to false, the line following the if statement is skipped or bypassed. The executable statement after the Console.WriteLine() would be the next one performed after the expression is evaluated.

# PROGRAMMING EXAMPLE: SpeedingTicket

This programming example demonstrates an application that calculates fines for traffic tickets issued on campus. A nested if...else selection statement is used in the design. Figure 5-8 shows the problem definition.

> Consider the situation of issuing parking tickets on campus and determining the fines associated with the ticket.
> 
> All students are charged an initial $75.00 when ticketed. Additional charges are based on how much over the speed limit the ticket reads. There is a 35 MPH per hour (MPH) speed limit on most streets on campus. Two roads are posted with a speed limit at 15 MPH. Fines are expensive on campus. After the initial $75 fee, an extra $7.50 is charged for every 5 MPH students are clocked over the speed limit.
> 
> The traffic office feels seniors have been around for a while and should know better than to speed on campus. They add even more fees to their fine. At the same time, they try to cut freshmen a little slack. Seniors are charged an extra $50 when they get caught speeding, unless they are traveling more than 20 MPH over the speed limit. Then they are charged an extra $200.
> 
> If freshmen are exceeding the speed limit by less than 20 MPH, they get a $50 deduction off their fines. But, freshmen, sophomores, and juniors traveling 20 MPH or more are fined an additional $100.

FIGURE 5-8 Problem specification for SpeedingTicket example

# ANALYZE THE PROBLEM

You should review the problem specification in Figure 5-8 and make sure you understand the problem definition. The purpose of the application is to calculate a fine based on the reported speed, speed limit, and classification of a student.