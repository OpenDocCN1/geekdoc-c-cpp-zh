# FIGURE 5-4 Flight map for HPAir

![](bbox=[0.335, 0.141, 0.495, 0.32])

**Representing the flight data.** The flight map in Figure 5-4 represents the routes that HPAir flies. An arrow from city $C_i$ to city $C_j$ indicates a flight from $C_i$ to $C_j$. In this case, $C_i$ is adjacent to $C_j$ and the path from $C_i$ to $C_j$ is called a **directed path**. Notice that if $C_j$ is adjacent to $C_i$, it does not follow that $C_i$ is adjacent to $C_j$. For example, in Figure 5-4, there is a flight from $R$ to $X$, but not from city $X$ to $R$. As you will see in Chapter 20, the flight map in Figure 5-4 is called a **directed graph.**

**The nature of the search.** When processing a customer's request to fly from some origin to some destination, you must determine from the flight map whether there is a route from the origin to the destination. By examining the flight map in Figure 5-4, you can see that a customer could fly from city $P$ to city $Z$ by flying to city $W$, then to city $Y$, and finally to city $Z$; that is, there is a directed path from $P$ to $Z$: $P ightarrow W ightarrow Y ightarrow Z$. Thus, you must develop an algorithm that searches the flight map for a directed path from the origin to the destination. Such a path might involve either a single flight or a sequence of flights. The solution developed here performs an **exhaustive search**. That is, beginning at the origin, the solution will try every possible sequence of flights until it finds one to the destination or determines that no such sequence exists.

First consider how you might perform the search by hand. One approach is to start at the origin city $C_i$ and select an arbitrary flight that departs from the origin city. This flight will lead to a new city $C_j$. If $C_j$ happens to be the destination, you are done; otherwise, you must attempt to go from $C_j$ to the destination. To do this, you select a path out of $C_j$. This flight will lead to city $C_k$. If $C_k$ is the destination, otherwise, you must attempt to get from $C_k$ to the destination, and so on.

**A recursive strategy.** To fly from the origin city to the destination city by flying from the origin city $C$ to a city $C$ and then flying from $C$ to the destination has a distinct recursive flavor. We can re-state this strategy as follows: 

+   To fly from the origin to the destination:
  Select a city $C$ adjacent to the origin
  Fly from the origin to city $C$
    if ($C$ is the destination city)
      Terminate—the destination is reached
    else
      Fly from city $C$ to the destination

> $C_i$ is adjacent to $C_j$ if there is a directed path from $C_i$ to $C_j$.