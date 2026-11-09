Example 2

```
`manager.decSalary = manager.decSalary * 1.05`
```

multiplies the contents of the manager.decSalary member by 1.05, and then assigns the result to the member

Example 3

```
`lblSalary.Text = manager.decSalary.ToString("C2")`
```

formats the value contained in the manager.decSalary member and then displays the result in the lblSalary control

Figure 22-4: Examples of using a member of a structure variable (continued from previous page)

The advantages of using structures will become more apparent as you code the applications in the next two sections.

Before continuing, it may be helpful to view the Ch22-Structures video.

# WILLOW POOLS APPLICATION

The sales manager at Willow Pools wants an application that determines the amount of water required to fill a rectangular pool. To perform this task, the application will need to calculate the volume of the pool. You calculate the volume by first multiplying the pool's length by its width, and then multiplying the result by the pool's depth. Assuming the length, width, and depth are measured in feet, this gives you the volume in cubic feet. To determine the number of gallons of water, you multiply the number of cubic feet by 7.48, because there are 7.48 gallons in one cubic foot. Figure 22-5 shows a sample run of the Willow Pools application, and Figure 22-6 shows one way of coding the application without using a structure. (Only the CalcVolume function and btnCalc control's Click event procedure are shown in the figure.) Notice that the btnCalc control's Click event procedure passes three variables *by value* to the CalcVolume function. The function determines whether the three values it receives are greater than zero. If they are, the function uses the values to calculate the volume of the pool; otherwise, it assigns the number 0 as the pool's volume. The function returns the volume as a Decimal number to the Click event procedure, which assigns the value to the decPoolVolume variable.