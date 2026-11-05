# Constants

The cost of each five miles over the speed limit is a set amount that everyone pays. It is defined as a constant value in the Ticket class. Setting it as a constant allows quick modification to the memory location when the minimum charges change. The identifier and preset constant value are

```
COST_PER_5_OVER = 87.50
```

# Design a Solution

The desired output is to display the fine amount. Figure 5-9 shows a prototype for what the final output should be. The xxx.xx is placed in the prototype to represent the location in which the calculated value should appear. For many applications, it is also useful to display the values used in calculations.

![](bbox=[0.24, 0.51, 0.58, 0.78])

Figure 5-9 Prototype for the SpeedingTicket example

As you read in earlier chapters, the object-oriented approach focuses attention on the design of the object. A Ticket object has both data and behavior characteristics that can be identified. Given the characteristics of student classification, speed limit, and ticketed speed, the Ticket object's major action or behavior is to set the fine amount. Class diagrams are used to help design and document these characteristics. Figure 5-10 shows the class diagrams for the SpeedingTicket example.