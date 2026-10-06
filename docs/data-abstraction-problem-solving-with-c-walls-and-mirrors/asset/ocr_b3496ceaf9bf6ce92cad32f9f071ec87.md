# Using a Stack to Search a Flight Map

To implement the rule of not visiting a city more than once, you simply mark a city when it has been visited. When choosing the next city to visit, you restrict consideration to unmarked cities adjacent to the top of the stack. The algorithm becomes

Mark the visited cities

```
aStack = a empty stack
Clear marks on all cities
```

Next draft of the search algorithm

```
aStack.push(originCity) // Push origin city onto the top of stack
Mark the origin as visited
while (a sequence of flights from the origin to the destination has not been found) {
    // Invariant: The stack contains a directed path from the origin city at
    // the bottom of the stack to the top of the stack
    if (no flights exists from the city on the top of the stack to unvisited cities) {
        aStack.pop() // Backtrack
    } else {
        Select an unvisited destination city C for a flight on the top of the stack
        aStack.push(C)
        Mark C as visited
    }
}
```

Finally, you need to refine the condition in the while statement. That is, you need to refine the algorithm's final determination of whether a path exists from the origin to the destination. which states that the stack contains a directed path from the origin city to the city on the top of the stack, implies that the algorithm can reach an affirmative conclusion if the city at the top of the stack is the destination city. On the other hand, the algorithm can reach a negative conclusion only after it has exhausted all possibilities—that is, the algorithm has backtracked to the origin and there remain no unvisited cities to fly from the origin. At that point, the algorithm will pop the origin city from the stack and the stack will become empty.
With this refinement, the algorithm appears as follows:

```
// Searches for a sequence of flights from originCity to destinationCity
search(originCity: City, destinationCity: City): boolean
```

The final version of the search algorithm

```
aStack = new empty stack
Clear marks on all cities
aStack.push(originCity) // Push origin city onto the stack
Mark the origin as visited
while (aStack.isEmpty() and destinationCity is not at the top of the stack) {
    // Invariant: The stack contains a directed path from the origin city at
    // the bottom of the stack to the top of the stack
    if (no flights exists from the city on the top of the stack to unvisited cities) {
        aStack.pop() // Backtrack
    } else {
        Select an unvisited destination city C for a flight from the top of the stack
        aStack.push(C)
        Mark C as visited
    }
}
if (aStack.isEmpty()) {
    return false // No path exists
} else {
    return true // Path exists
}
```