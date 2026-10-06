
# 174 CHAPTER 5 Recursion as a Problem-Solving Technique

## Possible outcomes of the exhaustive search strategy

Consider the possible outcomes of applying the following strategy:

1. You eventually reach the destination city and conclude that it is possible to fly from the origin to the destination.
2. You reach a city C from which there are no departing flights.
3. You go around in circles. For example, from C you go to C2, then to C3, and from C3 you go back to C2. You might continue this tour of the three cities forever; that is, the algorithm might not terminate.

If you always obtained the first outcome, everyone would be happy. This corresponds to a base case of the recursive algorithm. If you ever reach the destination city, no additional problems of "from C to the destination" are generated, and the algorithm terminates. However, HPAIR does not fly between all pairs of cities, you certainly cannot expect that the algorithm will find a path from the origin to the destination city; if city P in Figure 5-4 is the origin city and city Q is the destination city, the algorithm could not possibly find a path from city P to city Q.

Even if there were flights from the origin to the destination, it would take a luck of the previous strategy to discover it—the algorithm would return "correct" flight at each step. Even if there is a way to get from city P to city Z in Figure 5-4, the algorithm might not find it and might reach result 2 or 3. That is, if city P chooses to go to city F instead of city Z, the algorithm has to go to city F where there are no flights out (outcome 2). On the other hand, the algorithm might choose to go to city Q from city W. From city W, W might choose to go to city S. It would then have to go to city T and back to W. W might once again choose to go to city S and continue in circles (outcome 3).

## Use backtracking to recover from a wrong choice

You need to make the algorithm more sophisticated, so that it always finds a path from the origin to the destination, and otherwise terminates with the conclusion that there is no such path. The earlier strategy fails when there are no departing flights. This certainly does not mean that there is no way to get from the origin to the destination; it implies only that there is no way to get from city C to the destination. It was a mistake to go to city C. After discovering such a mistake, the algorithm can retract its steps, or backtrack, to the city that was visited before. Once back at city C', the algorithm can select some city other than C. If this were the case, it would mean that there was a mistake to visit city C', and you would then need to backtrack again—this time to get to the city that was visited before C'.

For example, say that, in trying to get from city P to city Z in Figure 5-4, the algorithm first chooses from city P to R and then to city X. As there are no departing flights from X, the algorithm must backtrack to R, the city visited before X. Once back at R, the algorithm would then go to some city other than X. But you would discover this is not possible. The algorithm would then backtrack once more, this time to city P, which was visited before- R. From city P, the algorithm would then need to go to city W, which is in the right direction!

We can resolve these problems by refining our strategy. We mark visited cities and never fly to a

### A refinement of the recursive search algorithm

```cpp
// Discover whether a sequence of flights from originCity to destinationCity exists.
search(originCity: City, destinationCity: City): boolean
  if (originCity is destinationCity)
    Terminate- the destination is reached
  else
    for (each unvisited city C adjacent to originCity)
      search(C, destinationCity)
```

# FIGURE 5-5 A piece of a flight map

![](img/d0cb86b2f18b2db569968ad7c743510e_201_0.png)

Now consider what happens when the algorithm returns a city that has no unvisited city adjacent to it. For example, consider the piece of a flight map in Figure 5-5. When searchR returns city M—that is, when the originCity has the value M—the loop will not be entered, because no unvisited cities are adjacent to M. Hence, the searchR(City) algorithm returns. This return has the effect of backtracking to city L, from which the flight originated. In terms of the previous pseudocode, the return is made to the point from which the call searchR(destination) occurred. This point is within the loop, which iterates through the cities adjacent to L; that is, the originCity has the value L.

After backtracking from M to L, the loop will again execute. This loop chooses city K, resulting in the recursive search(K,destination). From this point, the algorithm will either reach the destination and terminate—or backtrack again to city L. If it backtracks to L, for there are no more unvisited cities adjacent to L, a return from searchR terminate. The effect is to backtrack to the city O. If the algorithm ever backtracks to the origin city and no remaining unvisited cities are adjacent to it, the algorithm will terminate, and you can conclude that no sequence of flights from the origin to the destination exists. Notice that the algorithm will always terminate in one way or another, because it will either reach the destination or run out of unvisited cities to try.

> **Note: Backtracking**
When searching for a sequence of flights between cities, you must take into account the possibility that the algorithm will make wrong choices. For example, the algorithm must be able to backtrack when it hits a dead end, and you must eliminate the possibility that the algorithm will cycle.

**Operations on the flight map.** Now consider the operations that the search algorithm must perform on the flight map. The algorithm marks cities as it visits them, determines whether a city has been visited, and determines which cities are adjacent to a given city. You can treat the flight map as an ADT that has at least these operations in addition to the search itself. Other possible operations include placing data into the flight map, inserting a city adjacent to another city, displaying the flight map, displaying a list of all cities, and displaying all cities that are adjacent to a given city, the ADT flight map could include the following operations, given here in UML notation.

# CHAPTER 5 Recursion as a Problem-Solving Technique

### ADT flight map operations

```cpp
// Reads flight information into the flight map.
+readFlightMap(cityFileName: string, flightFileName: string): void

// Displays flight information.
+displayFlightMap(): void

// Displays the names of all cities that HPA serves.
+displayAllCities(): void

// Displays all cities that are adjacent to a given city.
+displayAdjacentCities(aCity: City): void

// Marks a city as visited.
+markVisited(aCity: City): void

// Clears marks on all cities.
+unvisitAll(): void

// Sees whether a city was visited.
+isVisited(aCity: City): boolean

// Inserts a city to another city in a flight map.
+insertAdjacent(aCity: City, adjCity: City): void

// Returns the next unvisited city, if any, is adjacent to a given city.
// Returns null if no unvisited adjacent city is found.
+getNext(fromCity: City): City

// Tests whether a sequence of flights exists between two cities.
+isPath(originCity: City, destinationCity: City): boolean
```

The latter operation isPath uses the searchR algorithm to make its determination. method isPath uses the C++ definition. Note that NO_CITY is a City object that defines as a constant for getNext to return in case it does not find an unvisited city.

### C++ implementation of searchR

```cpp
// Tests whether a sequence of flights exists between two cities.
@pre originCity and destinationCity both exist in the flight map.
@post Cities visited during the search are marked as visited
in the flight map.
@param originCity The origin city.
@param destinationCity The destination city.
@return True if a sequence of flights exists from originCity
to destinationCity; otherwise returns false.
bool isPath(City originCity, City destinationCity)
{
    bool result, done;

    // Mark the current city as visited
    markVisited(originCity);

    // Base case: the destination is reached
    if (originCity == destinationCity)
        result = true;
    else // Try a flight to each unvisited city
        {
            done = false;
            City nextCity = getNextCity(originCity);
```
