# 20

# Heat Flow via Time Stepping

> As the present now
> Will later be past
> The order is
> Rapidly fadin'
> 
> And the first one now
> Will later be last
> For the times they are a-changin'
> 
> Bob Dylan

This chapter examines the heat equation and develops the leapfrog method for solving it on a space–time lattice. We also develop an improved Crank–Nicolson method that determines the solution over all of space in a single step. Time stepping is simple, yet important, and we will see it again when we attack various wave equations.

# 20.1

# Heat Flow via Time-Stepping (Leapfrog)

Problem You are given an aluminum bar of length L = 1 m and width w aligned along the x-axis (Figure 20.1). It is insulated along its length but not at its ends. Initially the bar is at a uniform temperature of 100 °C, and then both ends are placed in contact with ice water at 0 °C. Heat flows out of the noninsulated ends only. Your problem is to determine how the temperature will vary as we move along the length of the bar at later times.

![](bbox=[0.12, 0.69, 0.45, 0.76])

Figure 20.1 A metallic bar insulated along its length with its ends in contact with ice. The bar is displayed in dark gray and the insulation is of lighter gray.