+   1. They are exactly the same task. The only difference is that they use different data to do the computation. The only things that change between subtask 2 and subtask 3 are the size of the pizza and its price.
+   2. The result of subtask 2 and the result of subtask 3 are each a single value: the price per square inch of the pizza.

Whenever a subtask takes some values, such as some numbers, and returns a single value, it is natural to implement the subtask as a function. Whenever two or more such subtasks perform the same computation, they can be implemented as the same function called with different arguments each time it is used. We therefore decide to use a function called unitPrice to compute the price per square inch of a pizza. The function declaration and explanatory comment for this function will be as follows:

```
double unitPrice(int diameter, double price);
//Returns the price per square inch of a pizza. The formal
//parameter named diameter is the diameter of the pizza in
//inches. The formal parameter named price is the price of
//the pizza.
```

# Algorithm Design

Subtask 1 is straightforward. The program will simply ask for the input values and store them in four variables, which we will call diameterSmall, diameterLarge, priceSmall, and priceLarge.

Subtask 4 is routine. To determine which pizza is the best buy, we just compare the cost per square inch of the two pizzas using the less-than operator. Subtask 5 is a routine output of the results.

Subtasks 2 and 3 are implemented as calls to the function unitPrice. Next, we design the algorithm for this function. The hard part of the algorithm is determining the area of the pizza. Once we know the area, we can easily determine the price per square inch using division, as follows:

price/area

where area is a variable that holds the area of the pizza. This expression will be the value returned by the function unitPrice. But we still need to formulate a method for computing the area of the pizza.

A pizza is basically a circle (made up of bread, cheese, sauce, and so forth). The area of a circle (and hence of a pizza) is πr², where r is the radius of the circle and π is the number called "pi," which is approximately equal to 3.14159. The radius is one half of the diameter.

The algorithm for the function unitPrice can be outlined as follows:

# Algorithm Outline for the Function unitPrice

+   1. Compute the radius of the pizza.
+   2. Compute the area of the pizza using the formula πr².
+   3. Return the value of the expression (price/area).

When to define a function

Subtask 1

Subtasks 4 and 5

Subtasks 2 and 3