previous chapters. Pseudocode for the SetFine( ) method, which contains a nested i.f, is shown in Figure 5-12.

![](bbox=[0.22, 0.25, 0.66, 0.78])

# FIGURE 5-12 Pseudocode for the SetFine() method

The problem definition indicates that for every 5 miles over the speed limit the additional fine is $87.50. A whole number value representing the overage is needed. For example, if the speedLimit is 35 and the ticketedSpeed is 42, only one additional fee of $87.50 is added to the fine. If the ticketedSpeed is 45, two additional $87.50 fees are added. This value is determined by doing integer division. An assumption for the pseudocode is that all variables, except fine, are of type int. This forces the division to be integer division.

42 - 35 = 7 miles over the limit

7 / 5 = 1

Notice that the result is not 1.40, because integer division produces an integer result.

You should always desk check your design. It is especially important when selection statements are included as part of your solution. With the SpeedingTicket example, a