```
bool Map::isPath(City originCity, City destinationCity)
{
   bool success;
   Stack aStack;
   unvisitAll(); // Clear marks on all cities
   // Push origin city onto aStack and mark it as visited
   aStack.push(originCity);
   markVisited(originCity);
   City topCity = aStack.peek();
   while (!aStack.isEmpty() && (topCity != destinationCity))
   {
      // The stack contains a directed path from the origin city
      // at the bottom of the stack to the city at the top of
      // the stack
      // Find an unvisited city adjacent to the city on the
      // top of the stack
      City nextCity = getNextCity(topCity, nextCity);
      if (nextCity == NO_CITY)
      {
         aStack.pop(); // No city found; backtrack
      }
      else
      { // Visit city
         aStack.push(nextCity);
         markVisited(nextCity);
      } // end if
      if (!aStack.isEmpty())
         topCity = aStack.peek();
   } // end while
   return !aStack.isEmpty();
} // end isPath
```

Programming Problem 11 at the end of this chapter provides implementation details that will enable you to complete the solution to the HPAir problem.

**Note: The STL class stack**

The Standard Template Library (STL) contains the container stack, which is a template class. However, some methods of this class have slightly different names than the ones we have used here. You can use the STL stack to implement the algorithms given in this chapter until we write our own implementations in the next chapter. Alternatively, you can use the class OurStack, as described in Programming Problem 1 at the end of this chapter. You can learn more about the STL in C++ Interlude 7.

**Question 8** Trace the method isPath with the map in Figure 6-10 for the following requests. Show the state of the stack after each step.

+   a. Fly from A to B.
+   b. Fly from A to D.
+   c. Fly from C to G.